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
  * C:\FMEData2026\Data\Stockholm\Addresses.xml
* A GeoJSON (Geographic JavaScript Object Notation)file with the Stockholm area as a polygon.
  * C:\FMEData2026\Data\Stockholm\Stockholm.json
* An Autocad DWG file that contain the OpenStreetMap data from Sweden
  * C:\FMEData2026\Data\OpenStreetMaps\OpenStreetMap\_Roads.dwg
  * They tell you that the creator forgot to put a coordinate system on it but that the coordinates are in the: LL84 coordinate system.
  * &#x20;The Tele 2 arena wants to stress the importance of traffic violations. They tell you that the path you create cannot use:
    * Cycleways
    * Motorways(\_links)
    * Primary(\_links)
    * Trunk(\_links)

Create a workspace that takes these input files and calculates the shortest path between the 2 points of interest by foot. Write the path to an HTML File.

They want you to write the output to:

C:\FMEData2026\Output\ShortestPath.html

<details>

<summary>Tips:</summary>

* The DWG File contains data for the whole of Sweden. You only need a little part. Can you _filter_ the data _spatially_ to optimize the reading?
* Simply adding the XML with the addresses will make your workspace crash! The XML for the start point and end point needs to be flattened in the parameters when reading the data. This so you can use the attributes easily. Flatten them on the level that “contains” the attributes. Flatten settings are found under “Elements to match”
* _Geocoding_ is a method where you can create a geometry out of an address. OpenStreetMap has a free _Geocoding_ service that works great!
* To be able to create a path between 2 points you first need to _build a line_ between the 2 points.
* The road network that comes from the DWG is by default not ready to be used. The roads represented by lines do not contain a vertex at an intersection. Therefore, FME doesn’t know that you could change street or direction when another line meets. This must be solved:

<figure><img src=".gitbook/assets/image (7) (1).png" alt=""><figcaption><p>Vertexes missing at intersections</p></figcaption></figure>

* By clicking on the coordinates in the Data Inspector you can see that there is a break point at each of these circles. You would want to _chop_ the lines at 2 vertices.
* Once you’ve prepared the Network and created a line between the start and end point you need to find the _shortest path_.
* The topology of the road network might not be a 100% perfect. FME can snap to a road with a certain tolerance to avoid nuances like this. A snapping tolerance of 1 should suffice.
* Creating a HTML can be done by using an HTMLReportGenerator.
* To show a map and geometries in a HTML Report. A “Map” can be used as the _page content_. Esri Leaflet has a great map that does not require an account.
* A HTML writer only accepts 1 attribute called: html\_content.

</details>

<details>

<summary>Bonus:</summary>

Just showing a map in an HTML page is quite easy in FME. However, you have the possibility to make quite nice reports with relative ease. Let’s see if we can make the output a bit nicer.

* Give the page a title.
* &#x20;Add the C:\FMEData2026\Resources\Webmap\Tele2ArenaHeader.jpg image as an image at the top of your page.
* Write a “header” that tells the user what the site shows them.
* Show the map with the path.
* Add a line of text that tells the _length_ of the path in meters, _rounded_ at 0 decimals.

An HTML file can be opened in any browser, including phones. A workspace that writes to an HTML file can be easily published to FME Server to directly show the output on a screen. FME could even utilize the position of the phone to give you a navigation from your current position!

</details>



<details>

<summary>Step-By-Step instructions (Try not to use this!)</summary>

#### If you have trouble doing the exercise on your own, you can use these step-by-step instructions to complete the exercise.

1. Start with an empty workspace.
2. Click on the Reader button at the top menu.\
   ![](<.gitbook/assets/image (54).png>)
3. For the Format, choose: "XML (Extensible Markup Language)"
4. For the dataset, choose: C:\FMEData2026\Data\Stockholm\Addresses.xml
5. Click on Parameters. In this popup, click on the "..." behind "Elements to Match. A new popup will appear. Click on the arrow before "Address" and then check the "PoI" box. This will ensure we can read the attributes that are found under this element.\
   ![](<.gitbook/assets/image (55).png>)
6. Keep pressing "OK" untill the "PoI" feature type appears on the canvas.
7. Right now, you only have 2 addresses from this dataset. In order to get a geometry you need to add a transformer called a "Geocoder" and connect it.
8. Double click the newly added "Geocoder" and set the "Geocoding Service" to "OpenStreetMap (Nominatim). Change the "Mode" to "Forward" and for the "Street Address" take the "Address" attribute. It will look like this:\
   ![](<.gitbook/assets/image (56).png>)
9. By running this, the 2 features now each have a point on the correct location in the LL84 coordinate system.
10. In order to make a shortest path analysis we cannot send in a start and end point. We need to create a line between these points.
11. Add a "LineBuilder" transformer behind the Geocoder. Run the workspace and you should get 1 line from it:\
    ![](<.gitbook/assets/image (57).png>)
12. Before we can continue, we need to read the road network data in order to be able to construct a route.\
    Because the road data set contains data for the whole country, we only want to read a part of it. This will be done by using a spatial filter in a featureReader where we send in the Stockholm area.
13. Add another like you did above. This time, for the "Format" choose "GeoJson (Geographic JavaScript Object Notation).&#x20;
14. For the Dataset, choose "C:\FMEData2026\Data\Stockholm\Stockholm.json" and click on "OK".\
    ![](<.gitbook/assets/image (58).png>)
15. If you run this "Stockholm" feature type, you will see that it contains 1 polygon with the Stockholm municipality.
16. Add a "FeatureReader" and draw a connection line from the "Stockholm" feature type to the "Initiator" port.
17. Double click the "FeatureReader" and apply the following settings.
18. Set the "Format" to "Autodesk AutoCAD DWG/DXF"
19. Set the "Dataset" to "C:\FMEData2026\Data\OpenStreetMaps\OpenStreetMap\_Roads.dwg"
20. Click on "Parameters" and make sure that you set the "Coordinate System" to "LL84" under the "Spatial" Menu. Then click on "OK"\
    ![](<.gitbook/assets/image (60).png>)
21. Click the "..." behind "Feature Types to Read" (this can take some time).
22. Check all the feature types that we are allowed to use as a road to walk on and then click on "OK".\
    ![](<.gitbook/assets/image (59).png>)
23. You only want to read roads that are in the Stockholm geometry we send in through the "initiator" port. For the "Spatial Filter" setting, choose "Initiator OGC - Contains Result"\
    ![](<.gitbook/assets/image (61).png>)
24. Because the Autocad file does not contain attributes we are interested in, and we dont want to have an output port for every feature type on its own, check the "Single Output Port - \<Generic>" setting under "Output Ports" then click on "OK"\
    ![](<.gitbook/assets/image (62).png>)
25. Run the workspace to this point so that you have an updated feature cache. You should get about 46 285 features from the FeatureReader "\<Generic>" port.
26. You cannot use this data for the shortest path just yet, a lot of lines dont have proper break points.
27. Add a "Chopper" transformer and connect the \<Generic> output port to it.
28. Double click on the "Chopper" transformer and set "mode" to "By Vertex" and the "Maximum Vertices" to "2". Then click on "OK". This will break every line that has more than 2 coordinates into a line with a maximum of 2 coordinates.
29. Your workspace should now look like this:\
    ![](<.gitbook/assets/image (63).png>)
30. Next, add a "ShortestPathFinder" transformer.
31. Connect both the "Chopped" and "Untouched" port from the "Chopper" to the "Network" input port of the "Shortest Path Finder". \
    Connect the "Line" output port from the "LineBuilder" to the "From-To" port of the "Shortest Path Finder"\
    ![](<.gitbook/assets/image (64).png>)
32. Double click the "ShortestPathFinder" to open its settings. Under the Snapping menu, set "From-To and Network Snapping" to "Yes". Set the "Snapping Tolerance" to "1". Click on "OK" and run the transformer. You should now get 1 feature from the "Path" port.\
    ![](<.gitbook/assets/image (65).png>)
33. Add a transformer "HTMLReportGenerator" and connect the "Path" port to it.
34. Double-click on it, and under "Page Contents", choose "Map (Esri Leaflet)"\
    ![](<.gitbook/assets/image (66).png>)
35. Click on "OK"
36. Add a Writer by clicking on the "Writer" button in the top menu. For the "Format" choose "HTML". For the "Dataset", set it to: "C:\FMEData2026\Output\Exercise9\ShortestPath.html". Then click on "OK".
37. Connect the "Output" port of the "HTMLReportGenerator" to the newly added "HTML" feature Type and run the workspace.
38. Check the result in your Firefox browser.

#### Bonus:

1. Add the transformer "Reprojector" and place it behind the "ShortestPathFinder" transformer and connect it to the "Path" port.
2. Double click it and in "Destination Coordinate System" choose "SWEREF-99-TM".\
   ![](<.gitbook/assets/image (67).png>)
3. After the "Reprojector" add a "LenghtCalculator" and connect it. You don't need to change its settings.
4. After the "LenghtCalculator" add an "AttributeRounder". Connect them and double click the "AttributeRounder". Set "Attributes to Round" to "\_length" and leave the rest as default.&#x20;
5. You can reuse the "HTMLReportGenerator" from before. Connect the output of the "AttributeRounder" to it. Then double click it to open its Parameters.
6. First make sure to add a proper "Page Title".&#x20;
7.  Then add the following under "Page Contents".

    Image, "Attachment Method" should be changed to "Embed", then locate the image file and select it from C:\FMEData2026\Resources\Webmap\Tele2ArenaHeader.jpg.
8. Add a "Header" under Page content and set the "Text" to "This is your shortest path to the station".
9. Add a "Header" under Page content and set the "Text" to "The length of your route is: @Value(\_length) meters."
10. You can add "Seperators" in the Page Contents to make the results a bit more clear.
11. Rearange the order to make it look like this:\
    ![](<.gitbook/assets/image (68).png>)
12. Then click on "OK" and connect it to the "HTML" writer feature type.
13. Your workspace will now look like this:\
    ![](<.gitbook/assets/image (69).png>)
14. Run the model and check your results! Feel free to play around with the "HTMLReportGenerator" to get it to your liking.

</details>
