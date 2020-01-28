---
layout: leafletPage
---

Visit Dr. Burns's personal website [here](http://burnsr77.github.io/), if you'd like.

# Web mapping demo


## This first map is an example of an open JavaScript library called Leaflet. 

Leaflet is free to use, and quick to set up. It's a very powerful library with lots of functionality for those with more advanced coding skills, but for beginners there are really just three things you need to understand about the platform as you see it below. The **first** is that the map goes into your specified "container" on the page (called a *div object*), and that you stylize the container itself - the box and its elements like scale bar and layer control - in a few lines of code at the top of the page (the "style" marker, if you hit CTRL+U to see the page code). **Second**, Leaflet doesn't have any data itself; you pull in data from other sources, like OpenStreetMap, a platform API, or your own datasets. **Third**, it's possible to stylize those datasets and offer those stylizations to the web for others to use. And that's what you see going on in this map below - each of the layers is a stylization of OpenStreetMap data. I'm basically "asking" Mapbox, Stamen, and Thunderforest - three private data companies - to use their stylizations here, and providing them a sort of "key" (technically called an *access token*) telling them who I am (or that you're a user on my platform). 

*Interact with the map by panning and zooming, and switching between layers.*

<div id="mapid"></div>
<script>
	//Mapbox base layer
	var mapbox_base = L.tileLayer('https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token={accessToken}', {
		attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
		id: 'mapbox/streets-v11',
		accessToken: 'pk.eyJ1IjoiYnVybnNyNzciLCJhIjoiY2lqYWgyZzJ3MDA5enU5bHhndDl0OGk3ZiJ9.E60cOEL952IkbYp44iPDaw'
	});	
	
	//OpenStreetMap base layer
	var osm_base = L.tileLayer('http://{s}.tile.osm.org/{z}/{x}/{y}.png', {
		attribution: '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors'
	});


	//Stamen base layer
	var STL = L.tileLayer('https://stamen-tiles-{s}.a.ssl.fastly.net/toner-lite/{z}/{x}/{y}{r}.{ext}', {
		attribution: 'Map tiles by <a href="http://stamen.com">Stamen Design</a>, <a href="http://creativecommons.org/licenses/by/3.0">CC BY 3.0</a> &mdash; Map data &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
		ext: 'png'
	});
	
	//Thunderforest base layer
	var TSM = L.tileLayer('https://{s}.tile.thunderforest.com/spinal-map/{z}/{x}/{y}.png?apikey={apikey}', {
		attribution: '&copy; <a href="http://www.thunderforest.com/">Thunderforest</a>, &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
		apikey: '66f365dd1ecd4241aac7d62f2cd216e0',
		maxZoom: 22
	});

	var mymap = L.map('mapid', {
		center: [54.7767, -1.5749], 
		zoom: 14,
		layers: [mapbox_base]
	});


	var baseMaps = {
		"mapbox": mapbox_base,
		"osm": osm_base,
		"stamen toner lite": STL,
		"spinal map": TSM
	};

			
	L.control.layers(baseMaps).addTo(mymap);

</script>


### Discussion question 1: *how do the different layers represent your city differently?*

### Discussion question 2: *what does it mean that private companies can use volunteer-generated datasets like OpenStreetMap to generate revenues? Who sees that revenue, and who enabled it? Did you enable it by using the company's services?*


## This next map is an Esri Online map

In terms of profit motive, this example is a little more straightforward: Esri is a private company, and charges a (quite expensive, in most cases!) fee to use their services. However, to create an online map such as this one requires even fewer technical skills than the Leaflet map, and Esri has strong name recognition from its tradition of geographic technology sector dominance. For many low-resourced institutions, the cost of hiring a web developer for a Leaflet map *might* be higher than to pay the license fee for Esri software. In any case, your choice of platform pigeonholes you into particular frameworks and technical limitations - for example, Esri software was far behind most open-source platforms in its adoption of the GeoJSON file format, and still gives you little aesthetic feedom. 

Below, I'm visualizing my volunteered running data that I created with the Runkeeper app over the 2015-2016 academic year. The symbols are a little difficult to see, but the hue changes from yellow to red to symbolize earlier to later dates. My goal was to run every street in South Philadelphia over the course of the year, and there will be *absolutely no gaps no matter how closely you look!* (Kidding - look closely!)

<style>.embed-container {position: relative; padding-bottom: 60%; height: 0; max-width: 100%;} .embed-container iframe, .embed-container object, .embed-container iframe{position: absolute; top: 0; left: 0; width: 100%; height: 100%;} small{position: absolute; z-index: 40; bottom: 0; margin-bottom: -15px;}</style><div class="embed-container"><iframe width="1000" height="600" frameborder="0" scrolling="no" marginheight="0" marginwidth="0" title="Philadelphia running" src="//www.arcgis.com/apps/Embed/index.html?webmap=7e06039a1148436b9bb29b9ed1d75a5c&extent=-75.2222,39.9003,-75.1211,39.9433&zoom=true&previewImage=false&scale=true&legend=true&disable_scroll=true&theme=light"></iframe></div>	

### Discussion question 3: **what other "digital traces" like these do you or others leave, and how might they be thought of as "geographical" beyond their clear cartographic basis?**


## And finally, this is a map rendered in D3.

D3 is more like Leaflet than Esri Online. It's an information visualization library broadly conceived, with some spatial capabilities. Since it's made for many purposes rather than focussed simply on mapping, its syntax is a bit more challenging than Leaflet. At the same time, it's been designed with aesthetics in mind, and in some ways its maps are "prettier". It's also far more powerful than Leaflet, because you can design topological maps divorced from Euclidean geometries, you can interact with different projections or map shapes (some maps are 2D renderings of 3D models!), and you can more efficiently display large datasets. D3 uses a display format called "svg", a vector format (remember your GIS modules?) that plays well with the latest HTML 5 format - what this means is that it is highly interactive when combined with JavaScript. Its interactivity also means that it enables far more representational capacity than Leaflet, enabling you to think more outside of the traditional map format you're used to seeing and that you saw in the two examples above.

Below, click on individual states to zoom to its "bounding box" - the extent of its coordinates. *To be completely transparent, I merely adapted the below example from user mbostock; I did not originate it as I did the above examples.*

<div id="d3div"></div>
<script>

var width = 960,
    height = 500,
    active = d3.select(null);

var projection = d3.geo.albersUsa()
    .scale(1000)
    .translate([width / 2, height / 2]);

var path = d3.geo.path()
    .projection(projection);

var svg = d3.select("#d3div").append("svg")
    .attr("width", width)
    .attr("height", height);

svg.append("rect")
    .attr("class", "background")
    .attr("width", width)
    .attr("height", height)
    .on("click", reset);

var g = svg.append("g")
    .style("stroke-width", "1.5px");

d3.json("./assets/us.json", function(error, us) {
  if (error) throw error;

  g.selectAll("path")
      .data(topojson.feature(us, us.objects.states).features)
    .enter().append("path")
      .attr("d", path)
      .attr("class", "feature")
      .on("click", clicked);

  g.append("path")
      .datum(topojson.mesh(us, us.objects.states, function(a, b) { return a !== b; }))
      .attr("class", "mesh")
      .attr("d", path);
});

function clicked(d) {
  if (active.node() === this) return reset();
  active.classed("active", false);
  active = d3.select(this).classed("active", true);

  var bounds = path.bounds(d),
      dx = bounds[1][0] - bounds[0][0],
      dy = bounds[1][1] - bounds[0][1],
      x = (bounds[0][0] + bounds[1][0]) / 2,
      y = (bounds[0][1] + bounds[1][1]) / 2,
      scale = .9 / Math.max(dx / width, dy / height),
      translate = [width / 2 - scale * x, height / 2 - scale * y];

  g.transition()
      .duration(750)
      .style("stroke-width", 1.5 / scale + "px")
      .attr("transform", "translate(" + translate + ")scale(" + scale + ")");
}

function reset() {
  active.classed("active", false);
  active = d3.select(null);

  g.transition()
      .duration(750)
      .style("stroke-width", "1.5px")
      .attr("transform", "");
}

</script>

### Discussion question 4: *using open-source, non-proprietary tools opens a whole world of possibilities, but requires some really strong skills. What might be the implications of this?*

### Discussion question 5: *how far are **you** willing to go?*