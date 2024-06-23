---
title: Multiobjective optimization in machine learning
summary: Multiobjective optimization in machine learning
tags:
  - Multi-Objective Learning
  - Machine Learning
  - Multi-objective Optimization
date: '2014-05-01'

# Optional external URL for project (replaces project detail page).
external_link: ''

image:
  caption: Overview of the multiobjective learning framework.
  focal_point: Smart

url_code: ''
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

Machine learning problems commonly have to deal with implicit or explicit conflicting objectives, thus leading to trade-offs. One of the most traditional is the model complexity vs. error rate on training trade-off. However, more complex is the model, more capable to adapt to data, thus reducing error; and vice-versa. But there are many other conflicting goals such as: error rate on each class; error rate vs. interpretability; error rate vs. fairness metrics. 

Previous research investigated the impact of optimization methods in machine learning, finding interesting impacts of multi-objective optimization in model selection, ensemble diversity, and knowledge sharing for classification problems, and esulted in applications in biology, medicine, logistics, and power transmissions; and also have theoretical contributions to machine learning, operations research, and multi-objective optimization. 

This project has three main goals: 1) Create a software framework to ease modeling and running conflicting objectives in machine learning; 2) Investigate theoretical consequences of modeling machine learning problems as multi-objective ones; 3) Creation of models to be employed in a wide sprectrum of applications. As a result, we expect to create a helpful framework that would machine learning experts to model tasks with conflicting objectives.
