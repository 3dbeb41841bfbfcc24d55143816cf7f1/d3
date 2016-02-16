#D3 -- Data Driven Documents (Intro!)

[D3](http://d3js.org/) is a fantastic, robust JavaScript library that lets you pair data with visuals. It's the brainchild of Mike Bostock, who developed it while working as a researcher at the Stanford Vis Group (and who currently maintains, expands, and teaches it as a member of the New York Times' graphics team).

- [bl.ocks](http://bl.ocks.org/mbostock)
- [D3.js](http://d3js.org/)
- [Mike's site](http://bost.ocks.org/mike/)
- [Bézier Curves](http://www.jasondavies.com/animated-bezier/)
- [D3 Tree](http://animateddata.co.uk/lab/d3-tree/)
- [D3 Tetris](http://d3tetris.herokuapp.com/)
- [D3 Wiki](https://github.com/mbostock/d3/wiki)

##What we're going to do today:

###Lesson time:

- Talk about why and when D3 can be useful
- [Walk through](./d3_walkthrough/template.html) some basic D3
- Inspect elements and change things around

###Lab time: 

- We've got a [template page](./d3_walkthrough/template.html) that you can use as your playground. It's set up in the same general format as the walkthrough pages -- HTML up top, D3 magic below, button to toggle the magic. (Feel free to make your own page as well!)
- Have FUN. Make shapes, make graphs, make a lot of *weird stuff* with data.
- Need some ideas?
	- Try making a set of circles with radii that correspond to data points.
	- Try making a Venn diagram. 
	- Try using JSON data instead of an array to populate a dataset (hint: this is what you'll need to do if you choose to use D3 in your Project 3!).
- If you need a little kick start, Mike Bostock has collected a [wide range of tutorials](https://github.com/mbostock/d3/wiki/Tutorials) on his wiki.


###More:

- D3 is a powerful library with tons of potential (its creator uses it at his day job to create super spiffy infographics, and many other developers use it to communicate information in novel or more expressive manners).
- We'll be coming back to this during weeks 10-12 as an advanced topic. There's a lot you can do with complex graphs, mathematical structures, and maps!
- Play around in the [documentation](https://github.com/mbostock/d3/wiki) if you'd like to learn more; we'd love to see some Project 4s with D3! 


##Lesson Walk-Thru


- Reset() - What if we add a reset function so we can add multiple buttons:

```javascript
function reset(){
	d3.selectAll("p").style("color", "white");
	d3.selectAll("p").style("background-color", "black");
}

function applyD3Intervals(){
  reset();
	setInterval(function(){
		d3.selectAll("p").style("width", function() {
		  return (Math.random()*15 + 100)+"px";
		});
	},200);
}
```

- DRY up the code:

```javascript
var start = d3.selectAll("p")
```
	
	
Selection
---
(for using jsFiddle, make sure youselect D3 on the dropdown)

JS:

```javascript
function applyD3Selectors(){
	d3.selectAll("p").style("color", "white");
	d3.selectAll("p").style("background-color", "black");
}
			
```

HTML:

```html
<h3>Example:</h3>
		<p>One</p>
		<p>Two</p>
		<p>Three</p>
		<p>Four</p>

<button onclick="applyD3Selectors()">Select and Style With D3</button><br>
```

Dynamic Properties
---

JS:

```javascript
d3.selectAll("p").style("color", "white");
d3.selectAll("p").style("background-color", "black"); 
function applyD3Intervals(){
	setInterval(function(){
		d3.selectAll("p").style("width", function() {
		  return (Math.random()*15 + 100)+"px";
		});
	},200);
}
function applyD3Colors(){
	d3.selectAll("p").style("background-color", function() {
  		return "hsl(" + Math.random() * 360 + ",100%,50%)";
	});
}

```

HTML:

```html
<h3>Example:</h3>
<p>One</p>
<p>Two</p>
<p>Three</p>
<p>Four</p>
		
<button onclick="applyD3Intervals()">Set Intervals With D3</button><button onclick="applyD3Colors()">Set Colors With D3</button><br>

		
```

Data
---

JS:

```javascript
d3.selectAll("p").style("color", "white");
d3.selectAll("p").style("background-color", "black");

function applyD3Selectors(){
	var barLength = [500, 200, 300, 400, 500, 600];
	d3.selectAll("p")
	    .data(barLength)
	    .style("width", function(d) { return d + "px"; });
	}
```
	
HTML:

```html
<h3>Example:</h3>
<p>100</p>
<p>200</p>
<p>300</p>
<p>400</p>
<p>500</p>
<p>600</p>
<button onclick="applyD3Selectors()">Match Bar Lengths to Values</button><br>

```

Transitions
---

JS:

```javascript
d3.selectAll("p").style("color", "white");
d3.selectAll("p").style("background-color", "black");
d3.selectAll("p").style("width", "200px");

function applyD3Selectors(){
	d3.selectAll("p").transition()
	    .duration(7500)
	    .delay(function(d, i) { return i * 2000; })
	    .style("margin-left", function(d,i) { return (100+30*i)+"px"; });
}
```

HTML:

```javascript
d3.selectAll("p").style("color", "white");
d3.selectAll("p").style("background-color", "black");
d3.selectAll("p").style("width", "200px");

function applyD3Selectors(){
	d3.selectAll("p").transition()
	    .duration(7500)
	    .delay(function(d, i) { return i * 2000; })
	    .style("margin-left", function(d,i) { return (100+30*i)+"px"; });
}
```




SVG
---

HTML:

```html
<h3>Basic SVG:</h3>
	<p>The basic shapes have their own elements:</p>
	<ul>
		<li>
            Circle:<br>	
            <svg width="100" height="100">
                <circle cx="50" cy="50" r="25"/>
            </svg>

        </li>
        <li>
            Ellipse:<br>	
            <svg width="100" height="100">
                <ellipse cx="50" cy="50" rx="40" ry="20"/>
            </svg>
            
        </li>
        <li>
            Rectangle:<br>	
            <svg width="100" height="100">
                <rect x="10" y="10" width="80" height="80"/>
            </svg>
        </li>
        <li>
            Line:<br>	
            <svg width="100" height="100">
                <line x1="20" y1="0" x2="90" y2="80" stroke="black"/>
            </svg>
        </li>
    </ul>

<h3>Styling and Rendering</h3>
		The <code>fill</code> attribute lets us set the color of the SVG element
		<ul>
			<li>
				Circles:<br>	
				<svg width="100" height="100">
					<circle cx="10" cy="50" r="10" fill="rgba(128, 0, 128, 1.0)"/>
					<circle cx="30" cy="50" r="15" fill="rgba(0, 0, 255, 0.75)"/>
					<circle cx="50" cy="50" r="20" fill="rgba(0, 255, 0, 0.5)"/>
					<circle cx="70" cy="50" r="15" fill="rgba(255, 255, 0, 0.25)"/>
					<circle cx="90" cy="50" r="10" fill="rgba(255, 0, 0, 0.1)"/>
				</svg>
				
			</li>
		</ul>
```


CSS: `svg { border: 2px solid red;}`

D3, SVG, Transitions
---

JS:

```javascript
function applyD3Selectors(){
	var dataset = [ 40, 60, 80, 60, 40 ];
	var svg = d3.select('svg');
	var circles = svg.selectAll("circle")
    	.data(dataset)
    	.enter()
    	.append("circle");


    circles.attr("fill", function() {
		return "rgba(" + Math.round(Math.random() * 255) + "," + Math.round(Math.random() * 255) + "," + Math.round(Math.random() * 255) + ","+Math.random()+")";
		});

    circles.attr("cx", function(d, i) {
            return (i * 80) + 40;
        })

       .attr("cy", 80)
       .transition()
       .duration(500)
       .delay(function(d, i){ return i * 100; })

       .attr("r", 150).transition()
       .duration(750)

       .attr("r", function(d){
            return d;
       })

       .attr("r", d).transition()
       .duration(750)

       .attr("r", function(d){
            return 0;
       })

       ;

}
```

##Bonus - Pull data from external JSON source

First, we need to start our server to avoid any CORS errors: `python -m SimpleHTTPServer 8080`.

This will start a simple Python server that already exists on your machine.
