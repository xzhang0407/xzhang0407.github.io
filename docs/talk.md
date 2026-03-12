---
layout: default
title: Talks
nav_order: 3
---

# Talks
{: .no_toc }

<!-- {% assign sorted_talk = site.data.publications | where:"type",type | sort: 'year' %}
{% for talk in sorted_talk %}
{% assign talk = talk_hash[1] %}
<ul class="list-group list-group-flush">
  <li class="list-group-item">
    <p> {{ talk.title }} </p>
    <a href="{{ talk.citation_url }}">
    </a>
    {% for author in talk.authors %}
    	{{ author.name }},
    {% endfor %}
  </li>
</ul>
{% endfor %} -->

<div class="row">
  <div class="col-sm-12 mb-3 mt-3">
    <input type="text" id="myFilter" class="form-control" onkeyup="myFunction()" placeholder="&#xF002; &nbsp; Search for title, meeting" style="font-family:Arial, FontAwesome">
  </div>
</div>
<div class="row" id="myItems">
  <div class="col-sm-12 mb-3">
    {% assign sorted_talk = site.data.talk | sort: 'id' | reverse %}
    {% for talks in sorted_talk %}
    {% assign talks = talk_hash[1] %}
    <div class="card border-light">
      <div class="card-body">
        <h3 class="card-title">{{ talks.title }}</h3>
        {% for talk in talks.talks %}
        <h5 class="card-subtitle mb text-muted pb-1"> 
          {{ talk.type }} {% if talk.meeting %} at {% endif %} <b>{{ talk.meeting }}</b> {{ talk.time }}{% if talk.place %}, {% endif %}{{ talk.place }}
        </h5>
        <h5 class="card-text">
          {% if talk.pdf_link %}
          [<a href="/assets/others/{{ talk.pdf_link }}">
            Slides
          </a>]
          {% endif %}
          {% if talk.pdf_weblink %}
          [<a href="{{ talk.pdf_weblink }}">
            Slides
          </a>]
          {% endif %}
          {% if talk.notes_link %}
          [<a href="{{ talk.notes_link }}">
            Notes
          </a>]
          {% endif %}
          {% if talk.record_link %}
          [<a href="{{ talk.record_link }}">
            Recording
          </a>]
          {% endif %}
          {% if talk.url %}
          [<a href="{{ talk.url }}">
            Website
          </a>]
          {% endif %}
        </h5>
        {% endfor %}
      </div>
    </div>  
    {% endfor %}   
  </div>    
</div>


<script>
  function myFunction() {
    var input, filter, cards, cardContainer, h5, title, i;
    input = document.getElementById("myFilter");
    filter = input.value.toUpperCase();
    cardContainer = document.getElementById("myItems");
    cards = cardContainer.getElementsByClassName("card");
    for (i = 0; i < cards.length; i++) {
        title = cards[i].querySelector(".card-body h3.card-title");
        authors = cards[i].querySelector(".card-body h5.card-subtitle");
        if (title.innerText.toUpperCase().indexOf(filter) > -1 | authors.innerText.toUpperCase().indexOf(filter) > -1) {
            cards[i].style.display = "";
        } else {
            cards[i].style.display = "none";
        }
    }
}
</script>
