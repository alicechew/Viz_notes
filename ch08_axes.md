＃ Chapter 8 Axes
Axis functions are SVG-specific.

## Set Up An Axis
```javascript
    svg.append("g")
        .attr("class", "axis")
        .attr("transform", "translate(0," + (h - padding) + ")")		//pushing the axis group to the bottom
        .call(xAxis);
```

### g
A **g** element is a group element. Group elements are invisible. They help us in two ways:
+ Contain (or "group") other elements;
+ We can apply transformations to g elements. It will affect the whole group.

### call
[call()](https://github.com/d3/d3-selection/blob/master/README.md#selection_call) takes the incoming selection, as received from the prior link in the chain, and hands that selection off to any function.

### Style
When use CSS rules to style SVG elements, only [SVG attribute](https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute) names--not regular CSS properties--should be used. For example, use **fill** instead of **color**:

```css
text {
	fill: olive;
}
```

## Check for Ticks
`ticks()`
D3 interprets the `ticks()` value as merely a **suggestion** and will override your suggestion with what it determineds to be the most clean and human-readable values.

`tickFormat()`

```javascript
var formatAsPercentage = d3.format(".1%");	//says to treat values as percentages with one decimal point precision. (0.23 --> 23.0%)
xAxis.tickFormat(formatAsPercentage);
```

