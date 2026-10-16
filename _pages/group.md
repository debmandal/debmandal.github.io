---
layout: page
permalink: /group/
title: Group
description: PhD students and collaborators at the University of Warwick.
nav: true
nav_order: 2
---

## PhD students

{% include dm_group_list.liquid people=site.data.group.phd %}

{% if site.data.group.alumni.size > 0 %}

## Alumni, interns and visitors

{% include dm_group_list.liquid people=site.data.group.alumni %}

{% endif %}

## Joining the group

<!-- Edit this paragraph: say whether you are recruiting, which funding routes apply and what to send. -->

I am happy to hear from prospective PhD students interested in reinforcement learning, learning from human feedback, social choice or multi-agent systems. Please email me with your CV and a short note on the problems you would like to work on.
