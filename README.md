# UFOs

The objective of this project is to create an interactive table that allows the users to filter out the data according to the currently deployed filters in a webpage deployed in github. The deployed website can be found [here](https://daniel-sanudo.github.io/UFOs/)

## Overview

It's necessary to coordinate html and javascript options such as classes and ids in order to create a table with the provided information that allows for filtering. Moreover, the site must be simple so that the users can easily follow along.

By using html, css, bootstrap and javascript, it's possible to fulfill these criteria. The result is the following:

![Deployed_Website](/static/images/Deployed_site.png)

The filters at the left side of the table allow the user to look for specific information so they're able to investigate more about the sightings.

## Results

![Filtered_Table](/static/images/Applied_Filters.png)

This image shows the results of the implementation of the javascript filtering functions by using the input id to attach a listener to it. The html input id is the same as the key of the respective entry in the data.js, 

Date
~~~~
<input type="text" class="form-control" placeholder="1/10/2010" id="datetime" />
~~~~

City
~~~~
<input type="text" class="form-control" placeholder="El Cajon" id="city" />
~~~~

State
~~~~
<input type="text" class="form-control" placeholder="CA" id="state" />
~~~~

Country
~~~~
<input type="text" class="form-control" placeholder="US" id="country" />
~~~~

Shape
~~~~
<input type="text" class="form-control" placeholder="Light" id="shape" />
~~~~

Each of these IDs matches the format of the data javascrit object which is the following:
~~~~
    datetime: "1/1/2010",
    city: "el cajon",
    state: "ca",
    country: "us",
    shape: "triangle",
    durationMinutes: "6 minutes",
    comments: "On New Years Eve I went outside to hear the celebration and fireworks in my neighbor hood. And noticed 3 red lights above my house and"
~~~~

Using the key of the javacript object as the input ID facilitates the following process of attaching a listener filtering the table. 

### Filter functions

As mentioned previously, the event listener calls the updateFilters whenever the user changes the input in any of the fields in this segment:

~~~~
d3.select("#datetime").on("change",updateFilters);
d3.select("#city").on("change",updateFilters);
d3.select("#state").on("change",updateFilters);
d3.select("#country").on("change",updateFilters);
d3.select("#shape").on("change",updateFilters);
~~~~

The updateFilters function grabs the event element, id, and value and stores it within a javascrip object, using the retrieved ID as the key and the retrieved value as the object's value.

Then, the filterTable function is used to loop through the javascript object as shown here:

~~~~
Object.entries(filters).forEach(([key,value]) => {
    filteredData = filteredData.filter(tableEntry => tableEntry[key] === value);
});
~~~~

This means that the filters javascript object is updated to the current information in the filters input field.

### User guide

![Clear_Filters](/static/images/Clear_Filters.png)

These 5 fields work receive the input that the user might want to use. There's a placeholder in each that has an example of the input that should be received. The user must be careful since these are case sensitive. Once anything has been typed inside the input fields, the user only needs to click somewhere else, or press the tab button in their keyboard.

For example, if we were interested in the sightings in california, where the witness reports seeing a light, we'd input "ca" as the state filter, and light as the shape filter

![CA_Light_Filters](/static/images/ca_light_filters.png)

If then, we want to look at all the light shaped filters, regardless of the state, we'd only have to erase the state input information and the table would update to show all sightings with a reported light shape

![Light_Filter](/static/images/Light_Filter.png)

And that's all the requirements to filter the information! Just type the place, date or shape of interest and click somewhere outside of the input field to allow the table to refresh. This program will remember the filter as long as it's typed in a field.

## Summary

One drawback of this page is its case sensitivity, this could be confusing for the users, specially because the state information is given as an abbreviation and these are normally typed in uppercase.

Further implementations could make the filters non-case sensitive, add the option to filter according to multiple inputs of the same category by reading the input and splitting it, then looping through the array. The table could also be split into pages to avoid having a really long webpage instead of having all the entries displayed at once.