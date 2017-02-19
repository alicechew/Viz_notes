# Chapter 7 Scale

## Domain & Range
+ input -- domain
+ output -- range

## Normalization
Mapping a numeric value to a new value between 0 and 1.

## Scale
In v4.0, use `d3.scaleLinear` instead of d3.scale.linear.

### Set domain and range
Using arrays.

```javascript
scale.domain([10, 500]);
scale.domain([100, 300]);
```

### Max & Min
`max()` takes two arguments, one is the dataset, the second argument is the accessor function to tell **max()** which specific values we want to compare.

```javascript
d3.max(dataset, function(d){
	return d[0];
});
```


#Example
```javascript
    var dataset = [
        [5, 20],
        [480, 90],
        [250, 50],
        [100, 33],
        [330, 95],
        [410, 12],
        [475, 44],
        [25, 67],
        [85, 21],
        [220, 88],
        [600, 100]
    ];

    var w = 500,
        h = 300;

    var svg = d3.select("body").append("svg")
        .attr("width", w)
        .attr("height", h);

    /**	
   		Setting Scales 
    **/
    var xMax = d3.max(dataset, function(d) {
        return d[0];
    });

    var yMax = d3.max(dataset, function(d) {
        return d[1];
    });

   

    var padding = 20;	//avoid cutting at the edges

    var xScale = d3.scaleLinear()
        .domain([0, xMax])
        .range([padding, w - padding * 2]); //output range is set to the SVG's width

    var yScale = d3.scaleLinear()
        .domain([0, yMax])
        .range([h - padding, padding]);

    var rScale = d3.scaleLinear()
    .domain([0, d3.max(dataset, function(d){
    	return d[1];
    })])
    .range([2, 5]);

    /**
    	Draw Circles
    **/
    svg.selectAll("circle")
        .data(dataset)
        .enter()
        .append("circle")
        .attr("cx", function(d) {
            return xScale(d[0]);
        })
        .attr("cy", function(d) {
            return yScale(d[1]);
        })
        .attr("r", function(d) {
            return rScale(d[1]);
        });

    svg.selectAll("text")
    .data(dataset)
    .enter()
    .append("text")
    .text(function(d){
    	return d[0] + "," + d[1];
    })
    .attr("x", function(d){
    	return xScale(d[0]);
    })
    .attr("y", function(d){
    	return yScale(d[1]);
    })

```