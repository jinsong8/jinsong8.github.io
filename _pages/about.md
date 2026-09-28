---
layout: homepage
permalink: /
title: "Song Jin (金松)"
description: "Song Jin is a Ph.D. student at Renmin University of China, focusing on post-training for foundation models, with an emphasis on multimodal understanding and generation."
last_updated: "September 2026"
redirect_from:
  - /about/
  - /about.html
---

<!-- ───────── ABOUT ───────── -->
<section id="about" class="about">
  <div class="about-text">
    <h1 id="about-me">Song Jin <span class="zh" lang="zh">金松</span></h1>
    <p class="role">PhD Student · Renmin University of China</p>
    <p>
      I am a Ph.D. student at the Gaoling School of Artificial Intelligence,
      Renmin University of China (RUC), advised by
      Prof. <a href="https://scholar.google.com/citations?user=eLw6g-UAAAAJ">Rui Yan</a>
      and Prof. <a href="https://scholar.google.com/citations?user=vVhmzbAAAAAJ">Yong Liu</a>.
    </p>
    <p id="research">My research focuses on <strong>post-training for foundation models</strong>, with an emphasis on <strong>multimodal understanding and generation</strong>.</p>
    <p id="contact"><strong>I welcome research collaborations and discussions.</strong> Feel free to reach out at <span>{{ site.author.email_display }}</span>.</p>
    <ul class="social" aria-label="Links">
      <li><a href="#contact" title="Contact email">{% include homepage-icon.html name="envelope" %}<span>Email</span></a></li>
      <li><a href="{{ site.author.googlescholar }}" title="Google Scholar">{% include homepage-icon.html name="graduation-cap" %}<span>Scholar</span></a></li>
      <li><a href="https://github.com/{{ site.author.github }}" title="GitHub">{% include homepage-icon.html name="github" %}<span>GitHub</span></a></li>
    </ul>
  </div>
  <div class="about-photo">
    <img src="{{ site.author.avatar | relative_url }}" alt="Portrait of Song Jin" width="200" height="200">
  </div>
</section>

<!-- ───────── NEWS ───────── -->
<section id="news" class="section">
  <h2 id="-news">News</h2>
  <ul class="news-list">
    {% for item in site.data.homepage.news %}
    <li{% if forloop.index > 12 %} class="news-extra"{% endif %}><time datetime="{{ item.datetime }}">{{ item.date }}</time><p>{{ item.text }}</p></li>
    {% endfor %}
  </ul>
  <button class="news-toggle" id="news-toggle" aria-expanded="false"{% if site.data.homepage.news.size <= 12 %} hidden{% endif %}>Show earlier news</button>
</section>

<!-- ───────── PUBLICATIONS ───────── -->
<section id="publications" class="section">
  <h2 id="-publications">Selected Publications</h2>
  <ul class="pubs">
    {% for paper in site.data.homepage.publications %}
    <li class="pub">
      <a class="pub-figure" href="{{ paper.image | relative_url }}" data-lightbox>
        <img src="{{ paper.image | relative_url }}" alt="{{ paper.name }} overview figure" loading="lazy" decoding="async">
      </a>
      <div class="pub-body">
        <p class="pub-title">{{ paper.title }}</p>
        <p class="pub-authors">{{ paper.authors | escape | replace: 'Song Jin', '<strong>Song Jin</strong>' }}</p>
        <p class="pub-links">
          {% if paper.code %}<a href="{{ paper.code }}" aria-label="Source code for {{ paper.name }}">Code</a> / {% endif %}<a href="{{ paper.paper }}" aria-label="Read {{ paper.name }} on arXiv">Paper</a>
        </p>
        <p class="pub-venue"><span class="venue">{{ paper.venue }}</span>{% if paper.first_author %} · <span class="equal">First author</span>{% endif %}</p>
      </div>
    </li>
    {% endfor %}
  </ul>
</section>

<!-- ───────── EDUCATION ───────── -->
<section id="education" class="section">
  <h2 id="-educations">Education</h2>
  <ul class="timeline">
    {% for item in site.data.homepage.education %}
    <li><time>{{ item.dates }}</time><span>{{ item.degree }}, <strong>{{ item.institution }}</strong><br>{{ item.detail }}</span></li>
    {% endfor %}
  </ul>
</section>

<!-- ───────── EXPERIENCE ───────── -->
<section id="experience" class="section">
  <h2 id="-internships">Experience</h2>
  <ul class="timeline">
    {% for item in site.data.homepage.experience %}
    <li><time>{{ item.dates }}</time><span>Research Intern, <strong>{% if item.team %}{{ item.team }}, {% endif %}{{ item.company }}</strong>, {{ item.location }}{% if item.detail %}<br>{{ item.detail }}{% endif %}</span></li>
    {% endfor %}
  </ul>
</section>

<!-- ───────── AWARDS ───────── -->
<section id="awards" class="section">
  <h2 id="-honors-and-awards">Awards &amp; Honors</h2>
  <ul class="timeline">
    {% for item in site.data.homepage.awards %}
    <li><time datetime="{{ item.datetime }}">{{ item.date }}</time><span>{{ item.text }}</span></li>
    {% endfor %}
  </ul>
</section>

<!-- ───────── ACADEMIC SERVICES ───────── -->
<section id="academic-services" class="section">
  <h2>Academic Services</h2>
  {% for item in site.data.homepage.academic_services %}
  <p><strong>{{ item.role }}:</strong> {{ item.venues | join: ', ' }}.</p>
  {% endfor %}
</section>
