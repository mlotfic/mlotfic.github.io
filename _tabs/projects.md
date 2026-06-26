---
layout: page
title: Projects
icon: fas fa-project-diagram
order: 5
permalink: /projects/
---

{% assign posts = site.posts | where: "type", "project" %}

<h1>Engineering Dashboard</h1>

{% assign domains = posts | map: "domain" | uniq | sort %}

{% for domain in domains %}
  <h2>{{ domain | upcase }}</h2>

  {% assign domain_posts = posts | where: "domain", domain %}
  {% assign projects = domain_posts | map: "project" | uniq | sort %}

  {% for project in projects %}
    {% assign items = domain_posts | where: "project", project | sort: "date" | reverse %}
    {% assign latest = items.first %}

    <div style="border:1px solid #ddd; padding:1rem; margin-bottom:1rem; border-radius:8px;">
      
      <h3>{{ project }}</h3>

      {% assign color = "gray" %}
      {% if latest.stage == "production" %}
        {% assign color = "green" %}
      {% elsif latest.stage == "prototype" %}
        {% assign color = "orange" %}
      {% endif %}

      <p>Status: <strong style="color: {{ color }}">{{ latest.stage }}</strong></p>

      {% if latest.metrics %}
        <ul>
          {% for m in latest.metrics %}
            <li><strong>{{ m[0] }}:</strong> {{ m[1] }}</li>
          {% endfor %}
        </ul>
      {% else %}
        <p>No metrics</p>
      {% endif %}

      {% if latest.metrics.documents and latest.metrics.errors %}
        {% assign success = latest.metrics.documents | minus: latest.metrics.errors %}
        {% assign rate = success | times: 100.0 | divided_by: latest.metrics.documents %}
        <p>Success Rate: {{ rate | round: 2 }}%</p>
      {% endif %}

      <details>
        <summary>Trend (last {{ items.size }} runs)</summary>

        <table>
          <tr>
            <th>Date</th>
            <th>Accuracy</th>
            <th>Latency</th>
          </tr>

          {% for post in items limit:5 %}
            <tr>
              <td>{{ post.date | date: "%Y-%m-%d" }}</td>
              <td>{{ post.metrics.accuracy }}</td>
              <td>{{ post.metrics.latency_ms }}</td>
            </tr>
          {% endfor %}
        </table>
      </details>

      <p>
        Latest Run:
        <a href="{{ latest.url }}">{{ latest.title }}</a>
      </p>

    </div>
  {% endfor %}
{% endfor %}