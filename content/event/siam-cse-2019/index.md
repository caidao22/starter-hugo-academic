---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Stable time integration for coupled ocean-atmosphere models"
event: SIAM Conference on Computational Science and Engineering (CSE19)
event_url: https://www.siam.org/conferences/cm/conference/cse19
location: Spokane, Washington, D.C.
address:
  street:
  city:
  region:
  postcode:
  country:
summary:
abstract: Fully coupled ocean-atmosphere models are needed to represent and understand the complicated interactions, becoming increasingly important in climate change assessment in recent years. Numerical stability issues may arise because of cost-effective time integration. In particular, the contributing factors include using large time stepsize, lack of accurate interface flux, and singe-iteration coupling. We investigate the stability of the coupled ocean-atmosphere models for a variety of interface conditions such as DIrichlet-Neumman condition and bulk condition which is unique to climate modelling. We will also discuss the use of Schwarz-in-time iterative schemes that can add implicitness to the interface points for better stability. The efficiency can be achieved by using modified interface conditions that lead to faster convergence and by exploiting task-level parallelism.

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2019-03-01
#date_end: 2019-12-17T13:35:58-06:00
all_day: true

# Schedule page publish date (NOT talk date).
publishDate: 2019-12-17T13:35:58-06:00

authors: []
tags: [time integration, coupled]

# Is this a featured talk? (true/false)
featured: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Custom links (optional).
#   Uncomment and edit lines below to show custom links.
# links:
# - name: Follow
#   url: https://twitter.com
#   icon_pack: fab
#   icon: twitter

# Optional filename of your slides within your talk's folder or a URL.
url_slides:

url_code:
url_pdf:
url_video:

# Markdown Slides (optional).
#   Associate this talk with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---
