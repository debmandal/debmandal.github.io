---
layout: page
permalink: /publications/
title: Publications
description: Publications by Debmalya Mandal. Preprints first, then papers by year; filter by topic or search.
nav: true
nav_order: 1
# Topic filters. Each name must match a value used in the `topics` field of _bibliography/papers.bib.
# (Links are lower-cased because al-folio's search only matches lower-case terms.)
# Keep `description` plain text: it also goes into the page's search-engine tags, where HTML breaks.
topic_filters:
  - Human feedback
  - Reinforcement learning
  - Robustness
  - Social choice
  - Game theory
  - Fairness and causality
---

<!-- _pages/publications.md -->

<p class="dm-page-intro">Conference versions are folded into their journal versions. Citations and the newest preprints are on <a href="https://scholar.google.com/citations?user=OquWQpEAAAAJ&amp;hl=en">Google Scholar</a>.</p>

<div class="dm-pub-tools">
  {% include bib_search.liquid %}
  <nav class="dm-topic-filters" aria-label="Filter by topic">
    <a class="dm-chip" href="#" data-topic="">All</a>
    {% for t in page.topic_filters %}
      <a class="dm-chip" href="#{{ t | downcase | uri_escape }}" data-topic="{{ t | downcase }}">{{ t }}</a>
    {% endfor %}
  </nav>
</div>

<!--p class="dm-venue-key" aria-label="Venue colours">
  <span class="dm-venue-swatch dm-venue-conf">Conference</span>
  <span class="dm-venue-swatch dm-venue-journal">Journal</span>
  <span class="dm-venue-swatch dm-venue-preprint">Preprint</span>
</p>
-->

<div class="publications">

<h2 class="bibliography">Preprints</h2>
{% bibliography --group_by none --query @misc %}

{% bibliography --query !@misc %}

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
