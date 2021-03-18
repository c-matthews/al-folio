---
layout: page
title: projects
permalink: /projects/
description: A collection of some of the projects that I've worked on.
nav: true
---

<div class="projects grid">

  {% assign sorted_projects = site.projects | sort: "importance" %}
  {% for project in sorted_projects %}
  <div class="grid-item">
    {% if project.redirect %}
    <a href="{{ project.redirect }}" target="_blank">
    {% else %}
    <a href="{{ project.url | relative_url }}">
    {% endif %}
      <div class="card hoverable">
        {% if project.img %}
        <img src="{{ project.img | relative_url }}" alt="project thumbnail">
        {% endif %}
        <div class="card-body">
          <h4 class="card-title" style="color:black;">{{ project.title }}</h4>
          <p class="card-text">{{ project.description }}</p>
          <div class="row ml-1 mr-1 p-0">
            {% if project.github %}
            <div class="github-icon">
              <div class="icon" data-toggle="tooltip" title="Code Repository">
                <a href="{{ project.github }}" style="margin-left:10px;" target="_blank"><i class="fab fa-github gh-icon"></i></a>
              </div>
            </div>
            {% endif %}
            {% if project.repo %}
            <div class="github-icon">
              <div class="icon" data-toggle="tooltip" title="Code Repository">
                <a href="{{ project.repo }}" style="margin-left:10px;" target="_blank"><i class="fas fa-cloud-download-alt"></i></a>
              </div>
            </div>
            {% endif %}
            {% if project.pdf %}
            <div class="github-icon">
              <div class="icon" data-toggle="tooltip" title="Article Link">
                <a href="{{ project.pdf }}" style="margin-left:10px;" target="_blank"> <i class="far fa-file-pdf"></i></a>
              </div>
            </div>
            {% endif %}
          </div>
        </div>
      </div>
    </a>
  </div>
{% endfor %}

</div>
