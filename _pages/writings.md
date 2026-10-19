---
layout: page
permalink: /writings/
title: Writings
description: Research statement, talk slides and other writing.
nav: true
nav_order: 6
---

{%- comment -%}
  Documents come from _data/writings.yml. On wide screens a PDF opens in the viewer
  beside the list; on phones (and without JavaScript) each link opens the file directly.
  Direct link to a document: /writings/#<id>, e.g. /writings/#research-statement
{%- endcomment -%}

{%- assign first_title = nil -%}
{%- assign first_href = nil -%}
{%- for cat in site.data.writings -%}
  {%- for item in cat.items -%}
    {%- assign ext = item.url | split: '?' | first | split: '#' | first | downcase | slice: -4, 4 -%}
    {%- if ext == '.pdf' and first_href == nil -%}
      {%- assign first_title = item.title -%}
      {%- if item.url contains '://' -%}{%- assign first_href = item.url -%}{%- else -%}{%- assign first_href = item.url | relative_url -%}{%- endif -%}
    {%- endif -%}
  {%- endfor -%}
{%- endfor -%}

<div class="dm-writings">
  <nav class="dm-writings-list" aria-label="Documents">
    {% for cat in site.data.writings %}
      {% if cat.items and cat.items.size > 0 %}
        <h2>{{ cat.category }}</h2>
        <ul>
          {% for item in cat.items %}
            {%- assign item_id = item.id | default: item.title | slugify -%}
            {%- assign ext = item.url | split: '?' | first | split: '#' | first | downcase | slice: -4, 4 -%}
            {%- if item.url contains '://' -%}{%- assign href = item.url -%}{%- else -%}{%- assign href = item.url | relative_url -%}{%- endif -%}
            <li>
              {% if ext == '.pdf' %}
                <a class="dm-doc-link" id="doc-{{ item_id }}" href="{{ href }}" data-pdf="{{ href }}" data-id="{{ item_id }}" data-title="{{ item.title | escape }}" aria-current="{% if href == first_href %}true{% else %}false{% endif %}">
                  <span class="dm-doc-title">{{ item.title }}</span>
                  {% if item.note %}<span class="dm-doc-note">{{ item.note }}</span>{% endif %}
                </a>
              {% else %}
                <a class="dm-doc-link" id="doc-{{ item_id }}" href="{{ href }}" target="_blank" rel="noopener">
                  <span class="dm-doc-title">{{ item.title }} <span aria-hidden="true">↗</span></span>
                  {% if item.note %}<span class="dm-doc-note">{{ item.note }}</span>{% endif %}
                </a>
              {% endif %}
            </li>
          {% endfor %}
        </ul>
      {% endif %}
    {% endfor %}
  </nav>

  {% if first_href %}
    <section class="dm-viewer" aria-live="polite" aria-label="Document viewer">
      <div class="dm-viewer-head">
        <h2 class="dm-viewer-title">{{ first_title }}</h2>
        <a class="dm-viewer-open" href="{{ first_href }}" target="_blank" rel="noopener">Open PDF in a new tab</a>
      </div>
      <iframe class="dm-viewer-frame" src="{{ first_href }}" title="{{ first_title | escape }}"></iframe>
    </section>
  {% endif %}
</div>

<script>
  (function () {
    var viewer = document.querySelector(".dm-viewer");
    if (!viewer) return;
    var frame = viewer.querySelector(".dm-viewer-frame");
    var heading = viewer.querySelector(".dm-viewer-title");
    var open = viewer.querySelector(".dm-viewer-open");
    var links = Array.prototype.slice.call(document.querySelectorAll(".dm-doc-link[data-pdf]"));
    var narrow = window.matchMedia("(max-width: 767.98px)");

    function show(link, updateHash) {
      links.forEach(function (l) {
        l.setAttribute("aria-current", l === link ? "true" : "false");
      });
      if (frame.getAttribute("src") !== link.dataset.pdf) frame.setAttribute("src", link.dataset.pdf);
      frame.title = link.dataset.title;
      heading.textContent = link.dataset.title;
      open.href = link.dataset.pdf;
      if (updateHash && history.replaceState) history.replaceState(null, "", "#" + link.dataset.id);
    }

    links.forEach(function (link) {
      link.addEventListener("click", function (event) {
        // Phones and modified clicks (new tab, etc.) open the PDF normally.
        if (narrow.matches || event.metaKey || event.ctrlKey || event.shiftKey || event.button !== 0) return;
        event.preventDefault();
        show(link, true);
      });
    });

    var wanted = decodeURIComponent(window.location.hash.slice(1));
    if (wanted) {
      var match = links.filter(function (l) {
        return l.dataset.id === wanted;
      })[0];
      if (match) show(match, false);
    }
  })();
</script>
