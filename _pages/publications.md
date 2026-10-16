---
layout: page
permalink: /publications/
title: Publications
description: Conference versions are folded into their journal versions. Citations and the newest preprints are on <a href="https://scholar.google.com/citations?user=OquWQpEAAAAJ&hl=en">Google Scholar</a>.
nav: true
nav_order: 1
# Topic filters. Each name must match a value used in the `topics` field of _bibliography/papers.bib.
topic_filters:
  - Human feedback
  - Reinforcement learning
  - Social choice
  - Game theory
  - Fairness and causality
  - Other ML
---

<!-- _pages/publications.md -->

<div class="dm-pub-tools">
  {% include bib_search.liquid %}
  <nav class="dm-topic-filters" aria-label="Filter by topic">
    <a class="dm-chip" href="#" data-topic="">All</a>
    {% for t in page.topic_filters %}
      <a class="dm-chip" href="#{{ t | uri_escape }}" data-topic="{{ t | downcase }}">{{ t }}</a>
    {% endfor %}
  </nav>
</div>

<div class="publications">

{% bibliography %}

</div>

<script>
  // Marks the active topic filter. Filtering itself is done by al-folio's bibsearch,
  // which reads the URL hash (#Reinforcement%20learning) into the search box.
  (function () {
    function mark() {
      var current = decodeURIComponent(window.location.hash.slice(1)).toLowerCase();
      document.querySelectorAll(".dm-chip").forEach(function (chip) {
        chip.setAttribute("aria-current", chip.getAttribute("data-topic") === current ? "true" : "false");
      });
    }
    window.addEventListener("hashchange", mark);
    document.addEventListener("DOMContentLoaded", mark);
  })();
</script>
