---
# Leave the homepage title empty to use the site title
title: ""
date: 2022-10-24
type: landing

design:
  # Default section spacing
  spacing: "6rem"

sections:
  - block: resume-biography-3
    content:
      username: admin
      text: |
        Cassidy Artz is a nationally experienced SAT/ACT Tutor and College Admissions Advisor who has helped hundreds of students achieve their academic goals since 2010. With a background in psychology from Northwestern University and a Master of Public Health from Emory University, Cassidy combines educational expertise with deep empathy and a personalized approach to learning. She specializes in working with students of all learning styles—including those with ADHD, test anxiety, and learning differences—and is known for her calm presence, strategic insights, and outstanding results.
        <br>
      button:
        text: Download CV
        url: uploads/resume.pdf
    design:
      css_class: dark
      background:
        color: black
        image:
          filename: stacked-peaks.svg
          filters:
            brightness: 1.0
          size: cover
          position: center
          parallax: false
  - block: markdown
    content:
      title: '📚 My Teaching Philosophy'
      subtitle: ''
      text: |-
        Cassidy believes that confidence is just as important as content.
        With her background in psychology and behavioral health, she understands how mindset, motivation, and executive function affect performance. She meets each student where they are—whether that means calming nerves before test day or turning around a history of academic frustration.
    design:
      columns: '1'
  - block: collection
    content:
      title: What Cassidy Offers
      filters:
        folders:
          - services
    design:
      view: article-grid
      fill_image: false
      columns: 2
---
