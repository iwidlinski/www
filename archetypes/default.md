---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
menu:
  sidebar:
    name: "{{ replace .Name "-" " " | title }}"
    identifier: "{{ .Name }}"
    parent: AWS-2025
    weight: 10
tags: ["aws", "certification"]
categories: ["aws"]
draft: true
---

