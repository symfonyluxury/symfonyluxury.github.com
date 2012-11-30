---
layout: page
title: luxury
tagline: 快乐码农
---
{% include JB/setup %}

<div class="row">
  <div class="span8">
    <ul class="posts unstyled">
      {% for post in site.posts %}
        <li>
          <h3>
            <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>
            <small class="pull-right">
              - {{ post.date | date: "%B %e, %Y" }}
            </small>
          </h3><br>
          <em>
            {{ post.description }}
          </em><br><br>
              <ul class="tag_box inline unstyled post-ul">
                <li>
                  <i class="icon-user"> </i> by <a href="/aboutMe.html">{{ site.author.name }}</a>
                  | <i class="icon-list"> </i> 分类：{{ post.category }}
                  | <i class="icon-tags"> </i> 标签：
                </li>
                {% assign tags_list = post.tags %}  
                {% include JB/tags_list %}
              </ul>
        </li>
        {% if forloop.last != true %}<hr>{% endif %}
      {% endfor %}
    </ul>
  </div>
</div>



