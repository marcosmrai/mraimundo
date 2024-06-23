---
# Leave the homepage title empty to use the site title
title: 
date: 2024-06-20
type: landing

sections:
  - block: about.biography
    id: about
    content:
      title: |
        Marcos M. Raimundo
      username: admin
      
      image:
        filename: marcos.jpg
      text: |

        
        Marcos M. Raimundo is an Assistant Professor at University of Campinas (UNICAMP), in the Institute of Computing (IC). He is also a faculty member of the REasoning for COmplex Data laboratory (Recod.ai). His research interests includes Machine Learning, Multi-objective Optimization, Ethical AI, Mathematical Programming.
  
  - block: collection
    content:
      title: Teaching
      subtitle:
      text:
      count: 5
      filters:
        author: ''
        category: ''
        exclude_featured: false
        publication_type: ''
        tag: ''
      offset: 0
      order: desc
      page_type: teaching
    design:
      view: card
      columns: '1'

  - block: collection
    content:
      title: Projects
      subtitle:
      text:
      count: 5
      filters:
        author: ''
        category: ''
        exclude_featured: false
        publication_type: ''
        tag: ''
      offset: 0
      order: desc
      page_type: project
    design:
      view: card
      columns: '2'

  - block: collection
    content:
      title: Latest Publications
      text: ""
      count: 5
      filters:
        folders:
          - publication
    design:
      view: citation
      columns: '1'
      
  - block: markdown
    content:
      title:
      subtitle: ''
      text: |
              {{% cta cta_link="./people/" cta_text="Meet the team →" %}}
    design:
      columns: '1'
      background:
        image: 
          filename: ./ic_pos.jpeg
          filters:
            brightness: 1
          parallax: false
          size: auto
          text_color_light: true
      spacing:
        padding: ['30%', '0', '30%', '0']
---
