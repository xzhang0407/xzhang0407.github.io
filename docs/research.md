---
layout: default
title: Research
nav_order: 2
---

<span id="top"></span>

# Publications
{: .no_toc }

<!-- {% assign sorted_publications = site.data.publications | where:"type",type | sort: 'year' %}
{% for paper in sorted_publications %}
{% assign paper = paper_hash[1] %}
<ul class="list-group list-group-flush">
  <li class="list-group-item">
    <p> {{ paper.title }} </p>
    <a href="{{ paper.citation_url }}">
    </a>
    {% for author in paper.authors %}
    	{{ author.name }},
    {% endfor %}
  </li>
</ul>
{% endfor %} -->

<div class="row">
  <div class="col-sm-12 mb-3 mt-3">
    {% assign types = "Under review, Working paper" | split: ", " %}
      {% for type in types %}
        <button type="button" class="btn btn-link btn-sm" onclick="document.getElementById('{{ type | join: '_' }}').scrollIntoView();"> {{ type }}s </button>
    {% endfor %}
    <div class="input-group">
      <input type="text" id="myFilter" class="form-control" onkeyup="myFunction()" placeholder="&#xF002; &nbsp; Search for title, author, journal" style="font-family:Arial, FontAwesome">
      <div class="input-group-append">
        <button class="btn btn-outline-secondary dropdown-toggle" type="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">All Topics</button>
        <div class="dropdown-menu">
          <a class="dropdown-item" href="#" onclick="categorySelector('All')">All Topics</a>
          <div role="separator" class="dropdown-divider"></div>
          {% assign categories = "Digital Data" | split: ", " %} 
          {% for category in categories %}
            <a class="dropdown-item" href="#{{category | replace: ' ', '-'}}" onclick="categorySelector('{{ category }}')">{{ category }}</a>  
          {% endfor %}
        </div>
      </div>
    </div>
  </div>
</div>

<div class="row" id="myItems">
  {% assign types = "Under review, Working paper" | split: ", " %}
  {% assign counter = 0 %}
  {% for type in types %}
  <div class="col-sm-12 mb-3">
    <span id="{{ type | join: '_' }}"></span>
    <h2 style="display:inline;"> {{ type }}s </h2>
    <h5 style="text-align:right;float:right;"><a href="#top">[ Top ]</a></h5> 
    {% assign sorted_publications_year = site.data.publications | where:"work_type",type | sort: 'year' | reverse | group_by: 'year' %}
    {% for paper_year in sorted_publications_year %}
    {% assign papers = paper_year.items | sort: 'order' %}
    {% for paper in papers %}
    {% assign counter = counter | plus: 1 %}
    <div class="card border-light">
      <div class="card-body">
        <h3 class="card-title">{{ counter }}. {{ paper.title }}</h3>
        <h5 class="card-subtitle mb-2 text-muted pb-1"> 
          {% for author in paper.authors %}
            {% if forloop.index < paper.authors.size %} 
              {% if author.name == 'Junhui Cai' %}
                <b>{{ author.name }}</b>,
              {% else %} {{ author.name }},
              {% endif %}
            {% else %} 
              {% if author.name == 'Junhui Cai' %}
                <b>{{ author.name }}</b>
              {% else %} {{ author.name }}
              {% endif %}
            {% endif %}
          {% endfor %}
          ({{ paper.year }})
        </h5>
        <h5 class="card-text"> 
          {{ paper.source }}
        </h5>
        <h5 class="card-text"> 
          <b>{{ paper.award }}</b>
        </h5>
        <h5 class="card-subtitle mb-2 pb-1" id="category" style="display: none;"> 
          Categories: 
          {% for topic in paper.topic %}
            {% if forloop.index < paper.topic.size %} 
              {{ topic.topic }},
            {% else %} 
              {{ topic.topic }}
            {% endif %}
          {% endfor %}
        </h5>
        <h5 class="card-text"> 
          <!-- [<a data-toggle="collapse" data-target="#collapseDescription{{ paper.id }}" aria-expanded="false" aria-controls="collapseDescription{{ paper.id }}" href="">
            Description
          </a>] -->
          {% if paper.abstract %}
          [<a data-toggle="collapse" data-target="#collapseAbstract{{ paper.id }}" aria-expanded="false" aria-controls="collapseAbstract{{ paper.id }}" href="">
            Abstract
          </a>]
          {% endif %}
          {% if paper.citation_url %}
            [<a href="{{ paper.citation_url }}">
              Paper
            </a>]
          {% endif %}
          {% if paper.cites_url %}
            [<a href="{{ paper.cites_url }}" target="_blank">
              arXiv
            </a>]
          {% endif %}
          {% if paper.journal_url %}
            [<a href="{{ paper.journal_url }}" target="_blank">
              Published version
            </a>]
          {% endif %}
          {% if paper.code_url %}
            [<a href="{{ paper.code_url }}" target="_blank">
              Code
            </a>]
          {% endif %}
          {% if paper.ssrn_url %}
            [<a href="{{ paper.ssrn_url }}" target="_blank">
              SSRN
            </a>]
          {% endif %}
          {% if paper.article %}
            [<a href="{{ paper.article.url }}" target="_blank">
              {{ paper.article.name }}
            </a>]
          {% endif %}
        </h5>
        <div class="collapse" id="collapseAbstract{{ paper.id }}">
          <div class="container" style="text-align:justify">
            <!-- <hr/> -->
            <p style="font-size:15px">
            {{ paper.abstract }}
            </p>
          </div>
        </div>
        <!-- <div class="collapse" id="collapseDescription{{ paper.id }}">
          <div class="container">
            <hr/>
            {{ paper.description }}
          </div>
        </div> -->
      </div>
    </div>  
    {% endfor %}
    {% endfor %}
  </div>
  {% endfor %}
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
        type = cards[i].querySelector(".card-body h5.card-text");
        category = cards[i].querySelector("[id='category']");
        if (title.innerText.toUpperCase().indexOf(filter) > -1 | authors.innerText.toUpperCase().indexOf(filter) > -1 | type.innerText.toUpperCase().indexOf(filter) > -1 | category.innerText.toUpperCase().indexOf(filter) > -1 ) {
            cards[i].style.display = "";
        } else {
            cards[i].style.display = "none";
        }
    }
  }

  function categorySelector(topic) {
    var cardContainer, cards;
    cardContainer = document.getElementById("myItems");
    cards = cardContainer.getElementsByClassName("card");
    for (i = 0; i < cards.length; i++) {
        category = cards[i].querySelector("[id='category']");
        if ( category.innerText.indexOf(topic) > -1 | topic == "All") {
            cards[i].style.display = "";
        } else {
            cards[i].style.display = "none";
        }
    }
  }

  $(".dropdown-menu a").click(function(){
    $(this).parents(".input-group-append").find('.btn').html($(this).text());
    $(this).parents(".input-group-append").find('.btn').val($(this).data('value'));
  });

  document.addEventListener("DOMContentLoaded", function(event) {
    var categoryFromUrl = window.location.hash.substring(1);
    if (categoryFromUrl) {
        var categoryName = categoryFromUrl.replace('-', ' ');
        categorySelector(categoryName);
      }
  });

</script>
