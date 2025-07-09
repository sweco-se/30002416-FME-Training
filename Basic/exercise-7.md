---
description: Writing demographic Data.
---

# Exercise 7

The data you created in the last exercise looks good! You now need to make sure you write it to a file.

Since it’s not just the Geo-department who’s going to use this data you need to write it to both a spatial dataset and to a non-spatial dataset.

The Geo-department would like to have this data in the GML format the non-spatial variant should be written to Excel.

_If you didn’t finish exercise 6 you can open: C:\FMEData2025\Workspaces\FMEFormBasic\Exercise7\_WritingDemographicData\_begin.fmw_

**Assignment:**

Write the data to a GML file and an Excel file. The output should contain the following:

GML:

* ID
* Kommunkod
* Kommunnamn
* Lankod
* Lannamn
* area
* Total\_Population

It should be written to: C:\FMEData2025\Output\Sweden\_Pop.gml

&#x20;Excel:

o   ID

o   Kommunkod

o   Kommunnamn

o   Lankod

o   Lannamn

o   area

o   Total\_Population

It should be written to: C:\FMEData2025\Output\Sweden\_Pop.xlsx

<details>

<summary><em>Tips:</em></summary>

* Writers can be added on several ways.
  * You can click the Writer icon in the menu.
  * You can click “Writers” in the top menu bar and choose “add writer”
  * You can search for the format like with a transformer. Make sure to choose writers. The first popup is often the reader.

- You can pick a name for the feature type yourself. Pick something that seems meaningful to you.
- You’re already familiar with different ways to set the output schema. Make sure to set it correct. Don’t worry too much about the Type and Width
- Since the schemas of both datasets are the same you can use the following trick to only create the schema once!
  * Create the schema for 1 of the writer FeatureTypes.
  * &#x20;Add a new writer for the second output file.
  * Once you’ve picked a location where to write the file, just click Next or Ok on all the other screens until a FeatureType for the new writer appears on your canvas.
  * You can leave this newly added FeatureType for now.
  * Select the FeatureType from the previous writer that you’ve set up correctly.
  * Right click it and choose “Duplicate” (or select it and press “CTRL + D” or copy and paste it).
  * Open the copied FeatureType and on the second setting “Writer” change it to the newly added writer.
  * This copied FeatureType now belongs to the writer you've just added.
  * Once this is done you can delete the FeatureType that was added when adding the new Writer (the empty one you didn't do anything with).



</details>

<details>

<summary>Bonus:</summary>

The Non-Geo departments looked at your data and they are not pleased with it. The excel used to have 1 sheet per Lan and now everything is saved into 1 sheet. They say it will be too much work for them to split up everything.

Obviously, you are a bit annoyed by their comment, but you are a FME Guru now! You can easily fix this!

There are 2 options to do this:

* Add 20 more FeatureTypes to your canvas (1 for each Lan), rename them and filter your data using an AttributeFilter transformer, sending the right output port to the right FeatureType.

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption><p>One FeatureType per sheet.</p></figcaption></figure>

*   Change 1 simple setting.

    * Open the FeatureType for the existing Excel Writer that you’ve created.
    * Click on the arrow next to the “Sheet Name” parameter.
    * Choose “Attribute Value” and choose “Lannamn”.
    * You will see the following\*:

    <figure><img src=".gitbook/assets/image (6).png" alt=""><figcaption><p>Fanout*</p></figcaption></figure>



&#x20;

</details>

{% hint style="info" %}
The second action you performed in the bonus exercise is called a “Fanout”. A fanout is a tool applied to a writer or featuretype in FME. It is a way for the workspace author to write data divided into groups of features. Groups are defined by either the value of a single attribute or a string constructed from a combination of attributes and fixed values.

Depending on the format you are writing to, a fanout can be either a FeatureType fanout or a Dataset fanout (or a combination if the file type allows it).

For example:

\-          A Shape file will write 1 shape file per fanout group --> Dataset fanout

\-          An Excel will write 1 sheet per fanout group --> FeatureType fanout

\-          A combination could be several Excel files with more than 1 sheet per file.
{% endhint %}
