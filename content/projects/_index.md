---
# Leave the homepage title empty to use the site title
title: 
date: 2024-06-20
type: landing

sections:
  - block: collection
    content:
      title: Projects
      text: ""
      filters:
        folders:
          - projects
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
          filename: ic_proj.png
          filters:
            brightness: 1
          parallax: false
          size: full
          text_color_light: true
      spacing:
        padding: ['20%', '0', '20%', '0']
---
