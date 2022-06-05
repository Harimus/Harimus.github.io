---
layout: default 
title: template project 
tags: "first project"
excerpt_separator: <!--excerpt-->

---
Here is the exceprt paragraph

Here's the second paragraph that should be excluded but is here because separator

<!--excerpt-->

#  How to 
Just write your projects here. Keep in mind that it does not pick a layout by default,
so you have to specify it. This is possible by adding 
```yaml
collections:
  projects:
    outputs: true
```

## Adding maths
$$ \frac{x^2}{y_2} $$


in the `_config.yaml` file

You can see the page attributes below:

{{ page | inspect }}

