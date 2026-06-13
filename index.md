---
layout: default
title: About
nav_order: 1
description: "Homepage"
permalink: /
---

<div class="container">
	<div class="row">
		<div class="d-none d-md-block col-sm-3">
			<img src="{{'/assets/images/xinyuan-zhang.jpg'| prepend:site.baseurl}}" alt="Photo of Xinyuan Zhang" style="max-width:100%; border-radius:4px;">
		</div>
		<div class="col">
			<p class="text-justify">
				I'm Xinyuan Zhang, a PhD candidate in Analytics at the <a href="https://mendoza.nd.edu/research-faculty/academic-departments/information-technology-analytics-operations/">IT, Analytics, and Operations Department (ITAO)</a> at the Mendoza College of Business, University of Notre Dame. I am advised by <a href="https://ahmedabbasi.com">Ahmed Abbasi</a> and Jeff Cai. I am expected to graduate in May 2027.
			</p>
			<p class="text-justify">
				My research interests include computational design science, digital trace, healthcare, machine learning, tensor decomposition, and multimodal AI.
			</p>
		</div>
	</div>
</div>

<br>

## Contact

- Email: [xzhang38@nd.edu](mailto:xzhang38@nd.edu)
- Google Scholar: [scholar.google.com/citations?user=-pMwboQAAAAJ](https://scholar.google.com/citations?user=-pMwboQAAAAJ&hl=en)
- GitHub: [github.com/xzhang0407](https://github.com/xzhang0407)
- Address: Mendoza College of Business, Notre Dame, IN 46556

<br>

## Co-authors
<div>
	<div class="panel panel-default">
	  <div class="panel-body" id="coauthors">
	  </div>
	</div>
</div>

<script>
  function lastNameSort(a,b) {
    return a.split(" ").pop()[0] > b.split(" ").pop()[0] ? 1 : -1;
  };

  var pubs = {{ site.data.publications | jsonify }}, 
      coauthors = {{ site.data.coauthors | jsonify }};
  var authors = [];
  for (var pub, i = 0; pub = pubs[i++];) {
    var author_arr = pub.authors;
    for (var author, j = 0; author = author_arr[j++];) {
      if (author.name != "Xinyuan Zhang") {
        authors.push(author.name);
      }
    }
  }
  sorted_authors = authors.sort(lastNameSort);
  var author_obj = {};
  for(var author, i = 0; author = sorted_authors[i++];) {
  	if(author in author_obj) {
  		author_obj[author]++;
  	} else {
  		author_obj[author] = 1;
  	}
  }
  var author_arr = Object
    .keys(author_obj)
    .map(k => ({ "name": k, "count": author_obj[k] }));
  var merged = author_arr
    .map(x => Object.assign(x, coauthors.find(y => y.name == x.name )));

  var parsed = "<p class='text-justify'>";
  for(var item, i = 0; item = merged[i++];) {
    parsed += '<a href="' + item.homepage + '" style="font-size:' + (1)*15 + 'px">' +
        item.name + '</a>';
    if(i < merged.length) {parsed += ",\t ";}
  }
  parsed += "</p>";
  $("#coauthors").html(parsed);
</script>
