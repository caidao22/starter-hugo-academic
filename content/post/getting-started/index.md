---
title: Installing PETSc and Torchdiffeq on Theta
subtitle: Detailed step-by-step instructions on how to install PETSc and torchdiffeq on Argonne's supercomputer Theta.

# Summary for listings and search engines
summary: Detailed step-by-step instructions on how to install PETSc and torchdiffeq on Argonne's supercomputer Theta.

# Link this post with a project
projects: []

# Date published
date: "2021-08-27T00:00:00Z"

# Date updated
lastmod: "2021-08-27T00:00:00Z"

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'Image credit: [**ANL**]()'
  focal_point: ""
  placement: 1
  preview_only: false

authors:
- admin

tags:
- PETSc
- PyTorch

categories:
- Tutorial

---

## 📚 Table of Contents
1. [👉Prerequistie](#prerequisite)
2. [🦄Install PETSc](#install-petsc)
3. [✨Install torchdiffeq](#install-torchdiffeq)

## 👉 Prerequisite on ThetaGPU <a name="prerequisite"></a>

1. Request an interactive node

Once you login to Theta, do the following
```
ssh thetagpusn1
qsub -n 1 -t <NODE_TIME_IN_MINUTES> -A <ALLOCATION_NAME> -I
```

2. Enable python environment:
```
source /lus/theta-fs0/software/thetagpu/conda/2021-06-28/mconda3/setup.sh
```
Python is not avaible on thetagpusn nodes and GPU nodes. This will setup a conda environment with a recent "from scratch" build of the PyTorch repository on the master branch. The location is subject to change.

3. Set up internet connection:
```
export http_proxy=http://proxy.tmi.alcf.anl.gov:3128
export https_proxy=http://proxy.tmi.alcf.anl.gov:3128
```
Alternatively, you can add `--attrs=pubnet` when requesting nodes with `qsub `.

Now you can install python packages with `pip install`, e.g.
```
pip install Cython matplotlib scipy
```
💬More info can be found [here](https://www.alcf.anl.gov/support-center/theta-gpu-nodes/running-pytorch-conda)

4. Lunch jobs on Theta：
```
aprun -n 64 -N 64 ./<your_program> <program_arguments>
```
You need to use `aprun` to execute your program on Theta.
- `-n` specifies the total number of MPI ranks
- `-N` specifies the ranks per node
- Add `-q` if you want to silence the output such as `Application 22305720 resources: utime ~10s, stime ~3s, Rss ~18776, inblocks ~0, outblocks ~8`


## 🦄 Installation of PETSc <a name="install-petsc"></a>

- **GPU build**
```
git clone https://gitlab.com/petsc/petsc.git
cd petsc
./configure --download-revolve --with-shared-libraries COPTFLAGS=-O3 CXXOPTFLAGS=-O3 FOPTFLAGS=-O3 PETSC_ARCH=arch-theta-gpu-opt --with-cuda-gencodearch=80 --with-cuda=1 --with-cudac=nvcc --with-petsc4py --download-fblaslapack
```
Follow the printed instructions at the end of configure to do a `make`. If you enabled `petsc4py` (`--with-petsc4py`), add `<path_to_petsc>/petsc/arch-theta-cuda-opt/lib` to PYTHONPATH.
For example, the following can be run directly or added into your .bash_profile script.
```
export PYTHONPATH=<path_to_petsc>/petsc/arch-theta-cuda-opt/lib:PYTHONPATH
```

- **KNL build**
```
git clone https://gitlab.com/petsc/petsc.git
cd petsc
./configure --LIBS=-lstdc++ --known-64-bit-blas-indices=0 --known-bits-per-byte=8 --known-has-attribute-aligned=1 --known-level1-dcache-assoc=8 --known-level1-dcache-linesize=64 --known-level1-dcache-size=32768 --known-memcmp-ok=1 --known-mklspblas-supports-zero-based=0 --known-mpi-c-double-complex=1 --known-mpi-int64_t=1 --known-mpi-long-double=1 --known-mpi-shared-libraries=1 --known-sdot-returns-double=0 --known-sizeof-MPI_Comm=4 --known-sizeof-MPI_Fint=4 --known-sizeof-char=1 --known-sizeof-double=8 --known-sizeof-float=4 --known-sizeof-int=4 --known-sizeof-long-long=8 --known-sizeof-long=8 --known-sizeof-short=2 --known-sizeof-size_t=8 --known-sizeof-void-p=8 --known-snrm2-returns-double=0 --with-cc=cc --with-clib-autodetect=0 --with-cxx=CC --with-cxxlib-autodetect=0 --with-batch --with-debugging=0 --with-fc=0 --with-hdf5=0 --with-make-np --with-memalign=64 --with-shared-libraries COPTFLAGS=-O3 CXXOPTFLAGS=-O3 FOPTFLAGS=-O3 PETSC_ARCH=arch-theta-knl-opt
```
💡**Tips**
- Do not change any option before `--with-batch`
- For debug version, use `--with-debugging` and remove the OPTFLAGS
- `PETSC_ARCH` is just a folder name of your choice, used to discriminate different builds

## ✨ Installation of torchdiffeq <a name="install-torchdiffeq"></a>
```
git clone https://github.com/rtqichen/torchdiffeq.git
cd torchdiffeq
pip install --user -e .
```

