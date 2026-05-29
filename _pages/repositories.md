---
layout: page
permalink: /repositories/
title: REPOSITORIES
description: This page dynamically pulls my open-source contributions, machine learning pipelines, and software engineering projects directly from GitHub.
nav: true
nav_order: 4
---

Click on any repository card to view the source code, documentation, and commit history.

{% if site.data.repositories.github_users %}
<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
  {% for user in site.data.repositories.github_users %}
    {% include repository/repo_user.liquid username=user %}
  {% endfor %}
</div>
{% endif %}

{% if site.data.repositories.github_repos %}
<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
  {% for repo in site.data.repositories.github_repos %}
    {% include repository/repo.liquid repository=repo %}
  {% endfor %}
</div>
{% endif %}
