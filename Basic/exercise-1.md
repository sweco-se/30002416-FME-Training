---
description: Your first translation.
---

# Exercise 1

You just started working for the Swedish government as a Data analyst.

It is your first day and they already have a task for you that seems to fit your profile perfectly.

Your new colleagues heard that you are a true hero when it comes to working with different kind of data sources and converting them to whatever is required.

They received data about all the demographic statistic areas in Sweden, in the form of an OGC GeoPackage (gpkg). Your colleagues can’t work with this format and asked you if you can try and read it and maybe write it out to a shape file.

**Assignment**:

Read the Geopackage and convert it to a shape file.

**The Geopackage lies in the following location:**

C:\FMEData2025\Data\Demografiska\_Statistikomraden\Demografiska\_statistikomraden.gpkg

**They want you to write it to a new shape file which should be saved as:**

C:\FMEData2025\Output\Demografiska\_statistikomraden.shp

<details>

<summary><strong>Tips:</strong></summary>

* There are different ways to read a file in FME.
  1. Browse by Format.
  2. Browse by File
  3. Drag and Drop.

- Writers can be added on different ways. For instance, by clicking on the “Writer” button in the menu bar.

* Do you need to Transform the data or could “Generate workspace” be a good solution?

- When writing to a shape file, you choose a folder to write the file to. The name of the file can be changed in the “FeatureType”**\***.



</details>

<details>

<summary><strong>Bonus:</strong></summary>

One of your colleagues needs this data in another format and would like to get a GML file. Try to add a second writer to the same workspace and write the same data as a GML fil&#x65;**\*\***.

The data can be saved in the same folder: C:\FMEData2025\Output\Demografiska\_statistikomraden.gml



</details>

{% hint style="info" %}
**\***&#x41; shape is a “folder based” format. 1 shapefile exists out of multiple files (for instance .shp, .dbf, .prj). For Folder based formats you have to choose a folder to write to when adding a writer and set the filename in the FeatureType settings.
{% endhint %}

{% hint style="info" %}
**\*\***&#x41; GML file is a “file based” format. All information regarding the date is saved in a single file. Therefore, you will have to instantly write a Filename when adding the writer.
{% endhint %}
