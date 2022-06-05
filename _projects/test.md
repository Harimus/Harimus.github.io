---
layout: default 
title: template project 
tags: "first project"

---

#  How to 
Just write your projects here. Keep in mind that it does not pick a layout by default,
so you have to specify it. This is possible by adding 
```yaml
collections:
  projects:
    outputs: true
```
in the `_config.yaml` file

You can see the page attributes below:

{{ page | inspect }}

