---
layout: page
permalink: /publications/
title: publications
description: List of publications in reverse chronological order. See up-to-date citation information on [<a href="https://scholar.google.com/citations?user=qKGTyVMAAAAJ">Google Scholar</a>].
years: [2020,2019,2018,2016,2015,2014,2013]
nav: true
---

<div class="publications">

{% for y in page.years %}
  <h2 class="year">{{y}}</h2>
  {% bibliography -f papers -q @*[year={{y}}]* %}
{% endfor %}

</div>
