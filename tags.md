---
layout: page
title: Tags
permalink: /tags/
---
<div class="home">
	<ul>
		{% for sitetag in site.tags %}
			{% assign siteslug = sitetag | first %}
			{% assign posts = sitetag | last %}
			
			{% for data_tag in site.data.tags %}
        	    {% if data_tag.slug == siteslug %}
        	        {% assign tag = data_tag %}
        	    {% endif %}
        	{% endfor %}	
			
			{% if tag %}
				<li>	
					<a href="/tag/{{ tag.slug }}/">{{ tag.name }} [ {{ posts | size }} ]</a>
				</li>
			{% endif %}
		{% endfor %}
	</ul>
</div>
