---
layout: default
img: Francis-Galton
img_link: http://en.wikipedia.org/wiki/Francis_Galton
caption: Fracis Galton wrote about the wisdom of crowds in his Nature article Vox Populi 
title: Syllabus
active_tab: syllabus
---

Subject to change as the term progresses.

<table class="table table-striped"> 
  <tbody>
    <tr>
      <th>Date</th>
      <th>Topic</th>
      <th>Readings</th>
    </tr>
    {% for lecture in site.data.syllabus %}
    <tr>
      <td>{{ lecture.date | date: "%b %d" }}</td>
      <td>
	{% if lecture.profile %}
	Company Profile:  
        {% endif %}
        {% if lecture.slides %}<a href="{{ lecture.slides }}">{{ lecture.title }}</a>
        {% else %}{{ lecture.title }}{% endif %}

	{% if lecture.speaker %}
        {% if lecture.speaker_url %} by <a href="{{ lecture.speaker_url }}">{{ lecture.speaker }}</a>
        {% else %} by {{ lecture.speaker }}{% endif %}
	{% endif %}

	{% if lecture.highlights %}
	  <ul>
	   {% for highlight in lecture.highlights %}	
	   <span class="text-muted"><li>
	   {{ highlight }}
	   </li></span>
          {% endfor %}
        {% endif %}
      </td>
      <td>
        {% if lecture.reading %}
          <ul class="fa-ul">
          {% for reading in lecture.reading %}
            <li>
            {% if reading.optional %}<i class="fa-li fa fa-star"> </i>
            {% else %}<i class="fa-li fa"> </i> {% endif %}
            {% if reading.url %}
            <a href="{{ reading.url }}">{{ reading.title }}</a>
            {% else %}
            {{ reading.title }} 
            {% endif %}
	    {% if reading.author %}
            by {{ reading.author }}
            {% endif %}
            </li>
          {% endfor %}
          </ul>
        {% endif %}
      </td>
    </tr>
    {% endfor %}
  </tbody>
</table>

