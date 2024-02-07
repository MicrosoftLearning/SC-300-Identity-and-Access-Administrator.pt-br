---
title: Instruções online hospedadas
permalink: index.html
layout: home
---

# Diretório de conteúdo

Os arquivos de laboratório necessários podem ser [baixados aqui](https://github.com/MicrosoftLearning/SC-300-Identity-and-Access-Administrator/archive/master.zip)

Hiperlinks para cada um dos exercícios de laboratório e demonstrações estão listados abaixo.

## Laboratórios

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions/Labs'" %}
| Módulo | Laboratório |
| --- | --- | 
{% for activity in labs  %}| {{ activity.lab.module }} | [{{ activity.lab.title }}{% if activity.lab.type %} — {{ activity.lab.type }}{% endif %}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
