---
layout: page
title: Schedule
description: ""
---

{% assign current_module = 0 %}
{% assign skip_classes = 0 %}
{% assign prev_date = 0 %}

{% for item in site.data.lectures %}
{% if item.date %}
{% assign lecture = item %}
{% assign event_type = "upcoming" %}
{% assign today_date = "now" | date: "%s" | divided_by: 86400 %}
{% assign lecture_date = lecture.date | date: "%s" | divided_by: 86400 %}
{% if today_date > lecture_date %}
    {% assign event_type = "past" %}
{% elsif today_date <= lecture_date and today_date > prev_date %}
    {% assign event_type = "warning" %}
{% endif %}
{% assign prev_date = lecture_date %}

<tr class="{{ event_type }}">
    <th scope="row">{{ lecture.date }}</th>
    {% if lecture.title contains 'No class' or lecture.title contains 'cancelled' or lecture.title contains 'Quiz' or forloop.last %}
    {% assign skip_classes = skip_classes | plus: 1 %}
    <td colspan="4" align="center">{{ lecture.title }}</td>
    {% else %}
    <td>
        <!-- Lecture #{{ forloop.index | minus: current_module | minus: skip_classes }} -->
        <!-- {% if lecture.lecturer %}({{ lecture.lecturer }}){% endif %}: -->
        <!-- <br /> -->
        {{ lecture.title }}
        <br />
        [
            {% if lecture.slides %}
              <a href="{{ site.base }}{{ lecture.slides }}" target="_blank">slides</a>
            {% else %}
              slides
            {% endif %}
            {% if lecture.slides2 %}
              | <a href="{{ lecture.slides2 }}" target="_blank">slides 2</a>
            {% endif %}
            {% if lecture.annotated %}
              (<a href="{{ lecture.annotated }}" target="_blank">annotated</a>)
            {% endif %}
            {% if lecture.video %}
            | <a href="{{ lecture.video }}" target="_blank">video</a>
            {% else %}
            <!-- | video -->
            {% endif %}
            {% if lecture.notes %}
            | <a href="{{ lecture.notes }}" target="_blank">notes</a>
            {% endif %}
        ]
    </td>
    <td>
        {% if lecture.readings %}
        <ul>
        {% for reading in lecture.readings %}
            <li>{{ reading }}</li>
        {% endfor %}
        </ul>
        {% endif %}
    </td>
    <td>
        <p>{{ lecture.logistics }}</p>
    </td>
    {% endif %}
</tr>
{% else %}
{% assign current_module = current_module | plus: 1 %}
{% assign module = item %}
<tr class="info">
    <td colspan="5" align="center"><strong>{{ module.title }}</strong></td>
</tr>
{% endif %}
{% endfor %}

<!-- - When: Tuesday and Thursdays from 10:40 to noon
- Where: the Zoom Link available in [Canvas](https://canvas.cmu.edu/courses/22090) or [Piazza](https://piazza.com/cmu/spring2021/15884/home)

The schedule is tentative and subject to change.
We will have guest lectures and may accomodate the schedule accordingly.
 -->
<!--
| Date     | Plan                                                         |
|----------|--------------------------------------------------------------|
| Feb 2nd  | (week1) Course Introduction                                  |
| Feb 4th  | (week1) Machine Learning Framework Components                |
| Feb 9th  | (week2) Paper Discussions -- Machine Learning Frameworks     |
| Feb 11th | (week2) Automatic Differentiation                            |
| Feb 16th | (week3) Paper Discussions -- Automatic Differentiation       |
| Feb 18th | (week3) Graph-level Optimizations                            |
| Feb 23th | (week4) Break day, no class                                  |
| Feb 25th | (week4) Paper Discussion -- Graph-level Optimizations        |
| Mar 2nd  | (week5) Parallelism                                          |
| Mar 4th  | (week5) Paper Discussions -- Parallelism                     |
| Mar 9th  | (week6) Distributed Training                                 |
| Mar 11th | (week6) Paper Discussions -- Distributed Training            |
| Mar 16th | (week7) Hardware Backend Specialization and Optimizations    |
| Mar 18th | (week7) Paper Discussions -- Hardware Backend Specialization |
| Mar 23th | (week8) Machine Learning for Systems                         |
| Mar 25th | (week8) Paper Discussions -- Machine Learning for Systems    |
| Mar 30th | (week9) Machine Learning Compilation                         |
| Apr 1st  | (week9) Paper Discussions -- Machine Learning Compilation    |
| Apr 6th  | (week10) Automating ML Compilation                           |
| Apr 8th  | (week10) Paper Discussions -- Automating ML Compilation      |
| Apr 13th | (week11) TinyML                                              |
| Apr 15th | (week11) Paper Discussions -- TinyML                         |
| Apr 20th | (week12) TBD                                                 |
| Apr 22th | (week12)                                                     |
| Apr 27th | (week13) TBD                                                 |
| Apr 29th | (week13)                                                     |
| Mar 4th  | (week14) Project hacking week                                |
| Mar 6th  | (week14)                                                     |
| Mar 11th | (week15) Final project presentation                          |
|          |                                                              |
 -->
