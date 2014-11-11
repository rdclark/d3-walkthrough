% D3 Walkthrough
% Richard Clark

# Introducing D3.js

[D3.js Homepage](http://d3js.org)

## Hello, World using D3

[Tutorial](http://bost.ocks.org/mike/bar/)

```html
<!DOCTYPE html>
<meta charset=utf-8>
<title>Hello!</title>
<script src="http://d3js.org/d3.v3.min.js" charset="utf-8"></script>
<body>
  <script>
	var body = d3.select("body");
	var h1 = body.append("h1");
	h1.html("Hello, world!");
  </script>
</body>
```

## Multiple sections

[Tutorial](http://bost.ocks.org/mike/bar/)

```html
<!DOCTYPE html>
<meta charset=utf-8>
<title>Hello!</title>
<script src="http://d3js.org/d3.v3.min.js" charset="utf-8"></script>
<body>
  <section></section>
  <section></section>
  <script>
	var sections = d3.selectAll("section");
	var h1 = sections.append("h1");
	h1.html("Hello, world!");
  </script>
</body>
```

## Add some style

[Tutorial](http://bost.ocks.org/mike/bar/)

```html
<!DOCTYPE html>
<meta charset=utf-8>
<title>Hello!</title>
<script src="http://d3js.org/d3.v3.min.js" charset="utf-8"></script>
<body>
  <section></section>
  <section></section>
  <script>
	var sections = d3.selectAll("section");
	var h1 = sections.append("h1").style('color', 'red');
	h1.html("Hello, world!");
  </script>
</body>
```

## Let's create a SVG graph

```html
<!DOCTYPE html>
<meta charset=utf-8>
<title>Simple graph (path)</title>
<style>
	svg { border: 1px solid lightgrey }
	.line { fill: none; stroke: steelblue; stroke-width: 1.5px }
</style>
<script src="http://d3js.org/d3.v3.min.js" charset="utf-8"></script>
<body>
  <svg width=100 height=100 />
  <script>
    var points = [[0, 100], [25, 50], [50, 0], [75, 50], [100, 100]];
	var svg = d3.select("svg");
	var line = d3.svg.line();
	var path = line(points);
	svg.append('path').attr('class', 'line').attr('d', path);
  </script>
</body>
```

## D3 will call `line` if we supply the data

```javascript
var points = [[0, 100], [25, 50], [50, 0], [75, 50], [100, 100]];
var svg = d3.select("svg");
var line = d3.svg.line();

svg.append('path')
	.datum(points)		// remember the points...
	.attr('class', 'line')
	.attr('d', line); 	// calls line(points) on our behalf
```

## Scaled data, accessors

```javascript
var points = [0, 0.5, 1, 0.5, 0];
var svg = d3.select("svg");
var x = d3.scale.linear().domain([0, points.length - 1]).range([0, 100]);
var y = d3.scale.linear().range([100, 0]);
var line = d3.svg.line()
	.x(function (d, i) { return x(i) } )
	.y(function (d, i) { return y(d) });
svg.append('path').datum(points).attr('class', 'line').attr('d', line);
```

## Practice

> 1. Take one of the examples, have D3 add the `svg` element dynamically (`.append('svg')`)
> 2. Set the height and width of that element (see the D3 tutorials)
> 3. (Extra) Can you graph a set of circles instead?
