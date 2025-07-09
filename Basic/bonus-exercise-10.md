---
description: All in!
---

# Bonus Exercise 10

You’ve done it! You’ve proven everyone that you are a true FME master and the jobs keep rolling in.

Your next assignment is do a flood analysis for the Stockholm municipality.

In recent years we’ve seen the effect of climate change all over the world. Extreme weather events are becoming more common every year. Including heavy rainfall and floods. Even well-developed countries are dealing with problems of water rising after heavy rainfall or sea level rise in general.

Therefore, the Stockholm municipality started an initiative to inform real-estate owners that own property that might be affected by these extreme events.

Real-estate owners who wanted to join this program could fill in a form that resulted in an excel file. In this form they registered their personal information and their property numbers.

It is now up to you to analyze which properties are in the risk zone and if the owner is on the list to be informed if needed.

**You are going to use the following data:**

* An excel file that contains the personal information of the people that wanted to join in this initiative.
  * “C:\FMEData2025\Data\Stockholm\Personsuppgifter.xlsx”\*
  * This data can be looked at using the FME Data Inspector.
  * \*The data in this Excel file is generated with AI and is not real!
* A GeoJson file that contains the water areas around Stockholm.
  * “C:\FMEData2024\Data\Stockholm\Vatten.json”
  * This data can be looked at using a Notepad program or the FME Data inspector.
  * This data comes from OpenStreetMaps.
* A Shape file that contains the buildings and their ID’s in Stockholm.
  * “C:\FMEData2024\Data\Stockholm\Fastigheter.shp”
  * This data can be looked at using the FME Data Inspector.
  * This data comes from OpenStreetMaps.

**A few things to keep in mind:**

* When people applied for the initiative, they had to register using their person-number. This is not data we want to keep due to GDPR rules (Dataskyddsförordningen). Therefore, you must remove the last 4 digits from the personal number. The first 8 characters are oke to keep since they can be used in other analysis based on the owner’s age.
* Not all water areas form the same level of risk. Reservoirs for instance can be ignored in this analysis because they are meant to hold extra water in case of an extreme event. Other water types like Drains are less risky to flood compared to a river etc. An overview of the risk per type is found further below.
* We are now working with a limited dataset but when reading the buildings, you might not need to read the whole dataset.

## **The model:**

Start by adding a reader to your model. The first data you are going to work with is the excel file.

Choose Excel as a format or simply browse directly for the file and FME will understand it is an excel. Before you click on “OK” make sure to click on the parameter button to see if the table is read the correct way. You might need to change the field names row and cell ranges. You can see a Preview in this menu.

## **GDPR**

We want to remove the sensible personal data as soon as possible to ensure we comply with GDPR rules. There are several ways to do this. One very stable way would be with a “StringReplacer” using Regular expressions.

In the StringReplacer you can set the mode to “Replace Regular Expression”. Then click on the arrow next to “Text to replace”. Here you can choose the “Open Regex editor…” to open a new window.

In this window you can enter a test string and work on your regex. You can even find references in the menu below.

For this regex we must find a common pattern in the data. For Swedish personal numbers we know there is a pattern. It is always build as: Year, month, day of birth, followed by a “-“ and then followed by 4 digits.

Since you want to remove the – and the last 4 digits you want to make a regex that matches this pattern. AI bots like Chat GPT are great in generating regex code for you if you don’t know how to do it yourself. Simply ask the AI bot and try to figure out if the suggested code could work for you.

If you don’t have access to an AI bot, FME has a build in Regex Editor that contains a test string box and a Reference guide to help you develop and test your regex expressions.

FME now also has a build in AI. This can be used in the regex editor by clicking on "AI assist".

Once we have a pattern like this you can click on “ok” and set up the rest of the transformer. In this case we want to replace it with nothing. Therefore, you can leave the “replacement text” blank and click on “ok”.

Make sure to double check the results.

## &#x20;**Real Estates**

If you take a good look at the data, you will see that some persons own several real estates. To join the real estates with the personal data you will need to split these id’s and make a separate row for each of them.

Add an AttributeSplitter to the canvas and set it up properly. Inspect the data and try to understand what FME has done. Make sure to click on the little paper with the “i” icon on it to open the feature information tab if you are using the build in “visual preview” of FME.

FME has created a list (often known as an Array) which contains the splitted attributes each having their own index.

To expose these as attributes you must expose them manually for each index with for instance an AttributeExposer or (in this case) you can simply use a “ListExploder”.

The list exploder will duplicate the record for each index in the List. Take a look at “William Fransson” and you will see that he now has 3 records in your data instead of 1. Each having one of the property ID’s as a new attribute.

You are now ready to join this data. But to do so, you must first find out if they have properties that are at risk.

## Water risk zones

To analyze the risk zones, add another reader to the canvas. This time choose “GeoJson” as the format and choose the “Vatten.Json” as the dataset.

Even though a .Json is a text file, FME understands that it contains geometries and should take care of everything itself.

First you will need to filter out data we are not going to analyze. “reservoirs” are not interesting for this analysis since their purpose is to store extra water. Add a transformer to your canvas to filter out these reservoirs.

As said above, not all waters have the same risk value. A river causes a lot more flooding risk then a drain. To determine the risk, we assume they can flood a certain area in meters. You can use the following table to determine the flood area per water type:

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Type</td><td valign="top">Flood area in meters</td></tr><tr><td valign="top">Drain</td><td valign="top">0,5</td></tr><tr><td valign="top">Stream</td><td valign="top">1</td></tr><tr><td valign="top">Canal</td><td valign="top">10</td></tr><tr><td valign="top">River</td><td valign="top">10</td></tr><tr><td valign="top">Riverbank</td><td valign="top">10</td></tr><tr><td valign="top">Dock</td><td valign="top">10</td></tr><tr><td valign="top">Water</td><td valign="top">50</td></tr><tr><td valign="top">Wetland</td><td valign="top">50</td></tr></tbody></table>

&#x20;Your first job will be to create a new attribute that contains the flood area in Meters per water type. There are several ways to do this. However, using conditional values in the AttributeManager is a great way to perform this task without duplicating to many transformers.

In an AttributeManager, add a new attribute (for instance “\_buffer”). For the value, click on the arrow pointing downwards and choose “Conditional Value…”.

In this screen you can set up a simple “if” and “Else if” statement. Double click the first Row and set your test. For instance: fclass = drain. Then choose the corresponding value for drain, in this case: 0.5.

Do this for all types. Keep in mind that types with the same flood area can be grouped by using an “OR” logic in the test.

Run your workspace up to this point to see if the results are as, you expect them to be.

Your next job will be to use this new attribute to buffer the waters correctly.

Add a “bufferer” to your workspace.

You can buffer in 2D. For the buffer distance, use the attribute that you’ve created.

One very important setting on the bufferer is the “ground units”. When the bufferer is using ground units, it will look at the coordinate system of the data and buffer by the units of the coordinate systems. Sweref99-TM will for instance buffer in Meters. However, this dataset is using the LL84 coordinatesystem which uses Latitude and Longitude. You do not want to buffer waters with those units (then we’re all at risk!). Make sure to set this setting to Meters.

The result you get from the bufferer might look a bit messy. Geometries will start overlapping and contain each other.

When we perform the analysis, we do not want to create duplicates on the real estates. They are either at risk or not. Therefor you can clean up the geometry by using a “Dissolver”. The Dissolver will create a new geometry of all the geometries that touch or overlap. Making the data easier to work with in this case.

You now have the water part complete. They consist of buffered polygons that will overlap with buildings in range if analyzed.

The next step will be to look at all the real estates that fall within or touch the risk areas.

## &#x20;Real estate data:

The real estate data of Stockholm contains a lot of buildings. Since you are only interested in the real estates that are being touched or contained in the water areas there is no need to read all of it. For performances it is always recommended to read as little data as possible as long as you get everything you need.

You can achieve this by using a “FeatureReader”.

Add a FeatureReader to the canvas.

For the Format, choose Esri Shapefile. As the dataset, choose the “fastigheter.shp”.

Now the cool part comes; since you only want to read data that is contained or intersects with the water, set the spatial filter to “Initiator OGC-Intersects Results”.

In this case, the water area’s are the “initiators” so FME will only read the real estates that intersect with these water polygons. This setting enables you to increase performances by an enormous amount.

When you now run the analysis, you might not get a result at all. Look at the water data and the shape you want to read (for instance in the data inspector). They seem to be in the same location and should therefore overlap. However, you are comparing 2 entirely different coordinate systems.

To do this analysis properly, you first must make sure the coordinate systems match.

Add a “Reprojector” to the canvas before the “FeatureReader” and set the destination coordinate system to “Sweref-99-TM” s

Now run the FeatureReader again and it should now read the Real Estates that are in the “risk zones”.

If you look at the data that is read, you can see that all these real estates are near water. This is what you expect. However, the data also shows what type of real estate it is. You can sort the data on Type by simply clicking on the column in the data inspector or visual preview. 2 Types don’t really mind a bit of extra water.

Filter out “Ships” and “Boats” from the result data.

## &#x20;Finding the owner:

You now have 2 transformations in parallel. It is now time to join this data together. You have the list of all the persons owning real estates with the corresponding ID and a list with all the real estates that are at risk with their ID.

To join this data together, there are 2 transformers you can use. The FeatureJoiner and FeatureMerger. In general, the FeatureJoiner is recommended to use since it is faster than the FeatureMerger.

Add a FeatureJoiner into the workspace.

For the Left data input: Take the Person data.

For the Right data input: Take the Real estate data.

In the FeatureJoiner you must specify a column to “Join On”. In this case you want to join the data on the “\_list” and “id” since they contain the Real estate ID that tells you which person owns which real estate.

Run the transformer and look at the result. You will notice that there is output coming out of 3 different ports:

* Joined: These persons have 1 or more real estates that are in a risk zone.
* UnjoinedLeft: This is a person that has a real estate that is not in a risk zone. (It wasn’t in the right dataset).
* UnjoinedRight: These are all real estates in risk zones that didn’t have a person connected to it. These are all real estates of people that didn’t sign up for the program.

## Finish up:

You now have all the information that you want! It is now time to clean up the data and finish up the workspace.

Add an AttributeManager perform the following steps:

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Input Attribute</td><td valign="top">Output Attribute</td><td valign="top">Action</td></tr><tr><td valign="top">Fastigheter</td><td valign="top"> </td><td valign="top">Remove</td></tr><tr><td valign="top">_list</td><td valign="top"> </td><td valign="top">Remove</td></tr><tr><td valign="top">_element_index</td><td valign="top"> </td><td valign="top">Remove</td></tr><tr><td valign="top">Id</td><td valign="top">Fastigheter</td><td valign="top">Rename</td></tr><tr><td valign="top">Flcass</td><td valign="top"> </td><td valign="top">Remove</td></tr><tr><td valign="top">Name</td><td valign="top"> </td><td valign="top">Remove</td></tr></tbody></table>

&#x20;

These steps are made since you do not want to keep unnecessary data in your workflow (it slows down FME).

The reason why you want to keep ID with the name from the other Fastigheter attribute is because the ID contains the single real estate ID compared to the concatenated string in the original Fastigheter attribute.

Now that the data is cleaned up you can write it out.

For this project you will write it to 2 different formats.

* A GeoJson. This format is often used in web-based services.
* A SQlite Database.&#x20;
  * Organizations often use databases to store data. However, for a lot of database formats you need extra software installed on your pc or you need an existing database. SQLite is a simple file-based database that uses the same principles. Therefore, you will use an SQLite Database for this exercise.

## &#x20;GeoJson:

Add a Writer to the canvas:

For the Format, choose GeoJson. For the Dataset, choose a location where you want to save the output File.

When writing to a file, it is always recommended to look at the Parameters that come with the Writer. These differ for most formats and especially when writing to a new format it is recommended to look at this.

In this case for instance, you want to make sure that “Formatting Type” is set to “Pretty Print”. This will make the output easier to read in a text editor.

Another setting you might want to look at for GeoJson is: “Reproject to WGS84”.

GeoJson is a standard often used for online applications. By default, GeoJson’s always come in the WGS84 coordinate system. In this workspace you are working with Sweref-99-TM. When writing to GeoJson FME will now automatically transform this data back to WGS84.

The Feature Type Definition will determine which attributes you will write to the output. By default this is set to “Copy From Reader…”. If you keep it like this, you will have to choose 1 of your readers in the next step to copy the attributes from. You don’t want this because you are using attributes from both readers in your output. Set it to “Automatic…”. Automatic will take any attribute you send to the writer and write it.

Once you click on OK you will get a new settings screen. The previous screen was for the settings of the Writer. The screen you see now, is for the FeatureType. 1 GeoJson Writer can write several datasets (feature Types) to 1 GeoJson File.

In this case we are only going to write one, so in this case for the Feature Type name you can simply fill in a name of your choosing and click on “ok”.

The FeatureType with the name you specified will now be added onto the canvas with no attributes. Simply drag a line from the AttributeManager to the GeoJson FeatureType and since it’s set to “Automatic…” the attributes that are in the AttributeManager will be send to the GeoJson.

You can now run this writer and see the results written out to the file and folder you specified. Since it’s a version of a Json File you can look at it in a Text Editor.

## SQLite:

Add another writer to the canvas. For the Format choose: SQLite.

Because an SQLite database is a file-based database, you must choose a dataset location again, say where you want to save your SQLite database and give it a name.

For this reader, the parameters are not very interesting so you can leave them as default.

Again, you can set the Feature Type Definition to “Automatic…”

Just like with the GeoJson writer, you get a new popup. The same as before applies to this Writer. You’ve just set the settings for the SQLite writer. One SQLite writer can write data to several Tables inside the Database (Feature Types). You must now set up the first Table.

First fill in a Table Name.

**The next settings are extremely important when working with databases:**

* **Feature Operation:** This says what we are going to do with the data in the table. Since this is new data, you can set it on “Insert”.
* **Table Handling**: This is the most important setting when working with databases, in this case, you are writing data to a new table that is empty. Therefore, you can set it to “Create if Needed”. If you would have been writing to an existing database that already has the table, it is recommended to pick “Use Existing”. Always be very careful with “Truncate Existing” and “Drop and Create”. These two operations will delete data or tables before writing. This could cause a loss of existing data!

Once you’ve set the correct settings. Click on “ok” and connect the AttributeManager to the newly added FeatureType.

Take a good look at the attributes that are going to be written as columns to the database table. You will notice that “Förnamn” contains a Swedish Ö. It is a very bad idea to write characters like öäå to databases (in general any format) since it can cause quite some troubles when querying the data later.

You can change this by either renaming the column in the AttributeManager or by opening the settings of the FeatureType and going to the tab “User Attributes”.

In this Tab, you can set the Attribute Definition to “Manual”. If you do this, you can manually change the Name of the attribute.

When you do so, and click on “ok” you will notice that the arrow in front of “Fornamn” becomes Red. That means that it is not getting in any data, and you must manually Map it.

This is done by clicking on the little white arrow in on the attributeManager in front of the “Output”. Once you’ve clicked on it. Drag a line from the green arrow behind “Förnamn” to the red arrow in front of “Fornamn”.

You’ve now manually mapped the attribute, and everything is green again.

Now run the workspace so that the data is written.

Unlike with the GeoJson you cannot simply open this file in a Text Editor. To see if the data is written correctly, look at it in the FME Data Inspector. Make sure that you choose the correct table under Parameters when you try to read it.
