---
description: Practical Transformer Use.
---

# Exercise 9

News about the amazing work you’ve done for all the different departments and organizations spread like a wildfire and new projects keep coming in. Your next project will be to help the Stockholm’s Tele 2 arena with an analysis.

_This is a complex project! Don’t hesitate to discuss the project with other FME’ers!_

Every time after an important match in the stadium the streets around the stadium are filled with people that want to find the way back to the central train station.&#x20;

**Assignment**_:_

The Tele 2 arena has asked you if you can make a HTML page that shows the shortest path from the stadium to the central station by foot.

You receive the following information from the Tele 2 arena:

* An XML file with the start and end point address. (Tele 2 arena and the Stockholm Central Station).
  * C:\FMEData2025\Data\Stockholm\Addresses.xml
* A Json file with the Stockholm area as a polygon.
  * C:\FMEData2025\Data\Stockholm\Stockholm.json
* An Autocad DWG file that contain the OpenStreetMap data from Sweden
  * C:\FMEData2025\Data\OpenStreetMaps\OpenStreetMap\_Roads.dwg
  * They tell you that the creator forgot to put a coordinate system on it but that the coordinates are in the: LL84 coordinate system.
  * &#x20;The Tele 2 arena wants to stress the importance of traffic violations. They tell you that the path you create cannot use:
    * Cycleways
    * Motorways(\_links)
    * Primary(\_links)
    * Trunk(\_links)

Create a workspace that takes these input files and calculates the shortest path between the 2 points of interest by foot. Write the path to an HTML File.

They want you to write the output to:

C:\FMEData2025\Output\ShortestPath.html

<details>

<summary>Tips:</summary>

* The DWG File contains data for the whole of Sweden. You only need a little part. Can you _filter_ the data _spatially_ to optimize the reading?
* Simply adding the XML with the addresses will make your workspace crash! The XML for the start point and end point needs to be flattened in the parameters when reading the data. This so you can use the attributes easily. Flatten them on the level that “contains” the attributes. Flatten settings are found under “Elements to match”
* _Geocoding_ is a method where you can create a geometry out of an address. OpenStreetMap has a free _Geocoding_ service that works great!
* To be able to create a path between 2 points you first need to _build a line_ between the 2 points.
* The road network that comes from the DWG is by default not ready to be used. The roads represented by lines do not contain a vertex at an intersection. Therefore, FME doesn’t know that you could change street or direction when another line meets. This must be solved:

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption><p>Vertexes missing at intersections</p></figcaption></figure>

* By clicking on the coordinates in the Data Inspector you can see that there is a break point at each of these circles. You would want to _chop_ the lines at 2 vertices.
* Once you’ve prepared the Network and created a line between the start and end point you need to find the _shortest path_.
* The topology of the road network might not be a 100% perfect. FME can snap to a road with a certain tolerance to avoid nuances like this. A snapping tolerance of 1 should suffice.
* Creating a HTML can be done by using an HTMLReportGenerator.
* To show a map and geometries in a HTML Report. A “Map” can be used as the _page content_. Google is the only service that does not require an API key and is therefore suitable to use for this exercise.
* A HTML writer only accepts 1 attribute called: html\_content.

</details>

<details>

<summary>Bonus:</summary>

Just showing a map in an HTML page is quite easy in FME. However, you have the possibility to make quite nice reports with relative ease. Let’s see if we can make the output a bit nicer.

* Give the page a title.
* &#x20;Add the C:\FMEData2025\Resources\Webmap\Tele2ArenaHeader.jpg image as an image at the top of your page.
* Write a “header” that tells the user what the site shows them.
* Show the map with the path.
* Add a line of text that tells the _length_ of the path in meters, _rounded_ at 0 decimals.

An HTML file can be opened in any browser, including phones. A workspace that writes to an HTML file can be easily published to FME Server to directly show the output on a screen. FME could even utilize the position of the phone to give you a navigation from your current position!

</details>
