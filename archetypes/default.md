---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
draft: true
---

<h2>目次</h2>
{{ .TableOfContents }}