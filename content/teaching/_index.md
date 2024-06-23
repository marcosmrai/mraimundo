---
# Leave the homepage title empty to use the site title
title: 
date: 2024-06-20
type: landing

sections:
  - block: collection
    content:
      title: Lastest Courses
      text: ""
      count: 3
      filters:
        folders:
          - teaching
    design:
      view: compact
      columns: '1'
      
  - block: markdown
    content:
      title:
      subtitle: ''
    design:
      columns: '1'
      background:
        image: 
          filename: ic_grad.jpeg
          filters:
            brightness: 1
          parallax: false
          size: auto
          text_color_light: true
      spacing:
        padding: ['25%', '0', '25%', '0']
---
