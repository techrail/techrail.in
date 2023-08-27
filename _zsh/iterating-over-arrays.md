---
published: false
layout: single
title: "Iterating over arrays in ZSH"
excerpt: "No Operating System is great enough unless you install the awesome apps built for it."
date: 2023-02-01
toc: true
toc_label: "On this page"
toc_icon: "terminal"
author_profile: false
permalink: "/zsh/interating-over-array/"
sidebar:
  nav: "zsh"
---

```zsh
#!/usr/bin/zsh
databases=('MySQL' 'PostgreSQL' 'MongoDB' 'Redis' 'Fauna' 'Cockroach DB')
for db in "${databases[@]}" ;do
        echo "Database: $db"
done
```