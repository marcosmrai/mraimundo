---
title: Algorithms for Multi-objective Optimization
summary: 
tags:
  - Multi-objective Optimization
  - Mathematical Programming
date: '2013-05-01'

# Optional external URL for project (replaces project detail page).
external_link: ''

image:
  caption: MONISE's automatically obtained Pareto frontier.
  focal_point: Smart

url_code: 'https://github.com/marcosmrai/moopt'
url_pdf: ''
url_slides: ''
url_video: ''

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: example
---

Many practical applications are better modeled as optimization problem, characterized by the existence of multiple conflicting objectives. A classical and usual example is the compromise between maximizing consumer satisfaction and minimizing service cost. Indeed, dealing with conflicting objectives is omnipresent in our lives, and a significant portion of these multi-objective problems admits a proper mathematical formulation, so that we may resort to computational resources to obtain Pareto-optimal solutions, also called non-inferior solutions. 

Without any assumption from the decision maker, all non-inferior solutions are equally relevant, so what we want to research in this project are algorithms capable of find a good representative set of non inferior solutions - those methods are called a posteriori multiobjective methods. This optimization framework can be applied to logistic problems, economics and [machine learning](../mol/).
