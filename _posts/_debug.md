---
title: "Debug Info"
permalink: /debug/
---

# Date Debugging

- **Jekyll build time:** {{ site.time }}
- **Jekyll timezone:** {{ site.timezone }}
- **Post dates:**
{% for post in site.posts %}
  - {{ post.date | date: "%Y-%m-%d %H:%M:%S %z" }} - {{ post.title }}
{% endfor %}