# Chapter 6 Draw With Data
## Attr
Add attribute: `.attr("class", "bar")`.

## Class
Add/Remove class: `.classed("bar", true)`, `.classed("bar", false)`.

## Setting Styles
```javascript
.style("height", function(d){
	var barHeight = d * 5;
	return barHeight + "px";	
});
```

## Drawing SVGs
All of SVG elements' properties are specified as attributes.

### Circle
+ cx
+ cy
+ rx
+ ry
+ r

### Bar 
Make bars grow upward from the bottom edge:
```javascript
.attr("y", function(d){
	return h - d;	//h = svg's height
})
```

Encode the data values as color:
```javascript
.attr("fill", function(d){
	return "rgb(0, 0, " + (d * 10) + ")";
});
```

### Multivalue Maps
Phew! Finally I don't have to type so many "attr".

> Multi-value maps are supported on the following methods: selection.attr, selection.style, selection.classed, selection.property, selection.on, transition.attr and transition.style. 
[Details](https://bl.ocks.org/mbostock/3305515)

**Notes**: Things are different in v4.0. Here you need the library [d3-selection-multi](https://github.com/d3/d3-selection-multi) and use `attrs()` instead of attr()!!!
```javascript
svg.selectAll("rect")
   .data(dataset)
   .enter()
   .append("rect")
   .attrs({
        x: function(d, i) { return i * (w / dataset.length); },
        y: function(d) { return h - (d * 4); },
        width: w / dataset.length - barPadding,
        height: function(d) { return d * 4; },
        fill: function(d) { return "rgb(0, 0, " + (d * 10) + ")"; }
   });
```

### Scatterplot
Represents two sets of corresponding values on two different axes.
**Notes**: Make sure to encode the values as area, not as a circle’s radius.
```javascript
.attr("r", function(d) {
    return Math.sqrt(h - d[1]);
});
```


### Label
```javascript
svg.selectAll("text")
        .data(dataset)
        .enter()
        .append("text")
        .text(function(d) {
            return d[0] + "," + d[1];
        })
        .attr("x", function(d) {
            return d[0];
        })
        .attr("y", function(d) {
            return d[1];
        })
        .attr("font-family", "sans-serif")
        .attr("font-size", "11px")
        .attr("fill", "red");
```
