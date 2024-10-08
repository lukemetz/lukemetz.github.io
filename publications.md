---
title: Publications
layout: page
---
## Publications

This list is a bit out of date. See my [Google Scholar](https://scholar.google.com/citations?user=k_u5ULgAAAAJ&hl=en) for a more recent work.


{% for pub in site.publications_list %}
{% if pub.year_split == true %}
  <p class="year"><b>{{pub.year}}</b></p>
{% else %}
  <div class="publication">
    <p class="title"><b>{{pub.title}}</b></p>
    <p class="people">
      {% for author in pub.people %}
        {% if author == "Luke Metz" %} <b> {% endif %}
        {% if author == "Luke Metz*" %} <b> {% endif %}
        {{author}}{% if forloop.last == false %},{% endif %}
        {% if author == "Luke Metz*" %} </b> {% endif %}
        {% if author == "Luke Metz" %}</b>{% endif %}
      {% endfor %}
    </p>
    <p class="location">{{pub.location}}</p>
    <p class="link"> <a href="{{pub.arxiv}}">pdf</a> </p>
  </div>
{% endif %}
{% endfor %}
