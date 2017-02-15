# Chapter 5 Data
##Binding Data
Bind data (in CSV or JSON) to DOM element:`selection.data()`

###Load CSV File
`d3.csv()`
Each value in from the CSV is stored as a **string**.
Note that d3.csv() (also d3.json()) is an *asynchronous* method. So it's better to use a global variable to store the data, so that it's available to all of the subsequent functions. For example:
```javascript
var dataset;

d3.csv("food.csv", function(data){
	//once loaded, copy to dataset.
	dataset = data;

	//Then call other functions that depend on data being present.
	generateVis();
	hideLoadingMsg();
});
```

To handle possible error, an optional *error* parameter can be included in the callback function. If there is a problem loading the file, then error will be set to the error message returned by the web server, and data will be undefined.
```javascript
var dataset;

d3.csv("food.csv", function(error, data) {

        if (error) {  //If error is not null, something went wrong.
          console.log(error);  //Log the error.
        } else {     
      //Include other code to execute after successful file load here
      dataset = data;

      generateVis();
      hideLoadingMsg();
        }

});
```

For tab-separated data in a TSV file, use `d3.tsv()`.

### Load JSON Data
`d3.json()`
d3.json("food.json", function(data){
	console.log(data);
});

### Create Data Bound Elements
`enter()`
> This method looks at the current DOM selection, and then at the data being handed to it. If there are more data values than corresponding DOM elements, then enter() creates a new placeholder element on which you can work your magic. It then hands off a reference to this new placeholder to the next step in the chain.

For example:
```javascript
d3.select("body").selectAll("p").data(dataset).enter().append("p").text("New paragraph!");
```
When d3 binds data to an element, the data exists in the memory as a **__data__** attribute of that element.

### Using the Data
 >When chaining methods together, anytime after you call data(), you can create an anonymous function that accepts d as input. The magical data() method ensures that d is set to the corresponding value in your original dataset, given the current element at hand.

 For example:
 ```javascript
d3.select("body").selectAll("p").data(dataset).enter().append("p").
    text(function(d) {
        return d;
    });
 ```