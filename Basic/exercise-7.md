---
description: Writing demographic Data.
---

# Exercise 7

The data you created in the last exercise looks good! You now need to make sure you write it to a file.

Since it’s not just the Geo-department who’s going to use this data you need to write it to both a spatial dataset and to a non-spatial dataset.

The Geo-department would like to have this data in the GML format the non-spatial variant should be written to Excel.

_If you didn’t finish exercise 6 you can open: C:\FMEData2026\Workspaces\FMEFormBasic\Exercise7\_WritingDemographicData\_begin.fmw_

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

It should be written to: C:\FMEData2026\Output\Sweden\_Pop.gml

&#x20;Excel:

o   ID

o   Kommunkod

o   Kommunnamn

o   Lankod

o   Lannamn

o   area

o   Total\_Population

It should be written to: C:\FMEData2026\Output\Sweden\_Pop.xlsx

<details>

<summary><em>Tips:</em></summary>

* Writers can be added on several ways.
  * You can click the Writer icon in the menu.
  * You can click “Writers” in the top menu bar and choose “add writer”
  * You can search for the format like with a transformer. Make sure to choose writers. The first popup is often the reader.
* You can pick a name for the feature type yourself. Pick something that seems meaningful to you.
* You’re already familiar with different ways to set the output schema. Make sure to set it correct. Don’t worry too much about the Type and Width
* Since the schemas of both datasets are the same you can use the following trick to only create the schema once!
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

<figure><img src=".gitbook/assets/image (5) (1).png" alt=""><figcaption><p>One FeatureType per sheet.</p></figcaption></figure>

*   Change 1 simple setting.

    * Open the FeatureType for the existing Excel Writer that you’ve created.
    * Click on the arrow next to the “Sheet Name” parameter.
    * Choose “Attribute Value” and choose “Lannamn”.
    * You will see the following\*:

    <figure><img src=".gitbook/assets/image (6) (1).png" alt=""><figcaption><p>Fanout*</p></figcaption></figure>



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

<details>

<summary>Step-By-Step instructions (Try not to use this!)</summary>

#### If you have trouble doing the exercise on your own, you can use these step-by-step instructions to complete the exercise.

For these steps, we've assumed that you have finished exercise 6. If you have not finished this exercise, you can open: C:\FMEData2026\Workspaces\FMEFormBasic\Exercise7\_WritingDemographicData\_begin.fmw

1. Click on the "Writer" button in the top menu to add a Writer.\
   ![](<.gitbook/assets/image (42).png>)
2. For the "Format" choose the "OGC GML(Geography Markup Language)" as the format.
3. For the "Dataset" click on the 3 dots. Name the file and choose the correct output folder C:\FMEData2026\output\Exercise7\Sweden\_pop.gml\
   ![](<.gitbook/assets/image (43).png>)
4. Click on "OK". A new Popup will appear to let you define the GML's FeatureType. Change the "Feature Type Name" to "Population" and then click on "OK".\
   ![](<.gitbook/assets/image (44).png>)
5. Since we also have to Write the data to an Excel file. Add a writer with the format "Microsoft Excel" and take the same steps as mentioned above for the GML.
6. Right now, the data contains a lot of attributes that we do not want to write. You can either add an "AttributeManager", "AttributeKeeper" or "AttributeRemover" to remove all the unnecessary attributes.
7. Now connect the output of the "AttributeManager, AttributeKeeper or AttributeRemover" to the newly added Writer FeatureTypes. This should automatically take care of the output schema.\
   ![](<.gitbook/assets/image (45).png>)
8. You can now run the workspace and see if the data gets written correctly.

#### Bonus:

You now need to change the Excel writer to write out 1 sheet per Län that only contains the municipalities that belong to that particular Län.

There are 2 ways of doing this. One of these takes a lot of work and the other way only makes you change 1 little setting. We will explain both. However, **make sure to only pick 1 method.**

#### Method 1:

1. Add an "AttributeFilter" on the line between the last transformer and the Excel FeatureType.\
   ![](<.gitbook/assets/image (46).png>)
2. Double click the "AttributeFilter" and set the "Attribute to Filter by" on "lannamn"
3. Then click on "Import" and choose "From Data Cache...". If this option is not available. Make sure to run your workspace until the previous transformer with Feature caching enabled.\
   ![](<.gitbook/assets/image (47).png>)
4. Choose "lannamn" for the "Values" and click on "Next"\
   ![](<.gitbook/assets/image (48).png>)
5. Make sure that all are selected and click on "Import" and then on "OK".
6. It should now look like this:\
   ![](<.gitbook/assets/image (49).png>)
7. Remove the connection line that comes out of the "\<Empty>" port. Instead choose the first "Län" and connect that to the Excel Feature Type. For instance Blekinge.\
   ![](<.gitbook/assets/image (50).png>)
8. Now double click on the orange "Population" feature type and rename the "Sheet Name" to "Blekinge" and click on "OK".\
   ![](<.gitbook/assets/image (51).png>)
9. Right click the "Blekinge" feature type and choose "Duplicate". Double click the newly added feature type and give it the name of the next län, in the case above, "Dalarna" and draw a line from the "AttributeFilter" Dalarna output port to the newly added Dalarna Feature Type.\
   ![](<.gitbook/assets/image (52).png>)
10. You would now have to repeat step 9 for every Län in order to create 1 sheet per län.

#### Method 2:

For this Method we will use a so called "FanOut" (see information block above) that will automatically create your sheets based on the unique attribute values.

1. Double click the "Population" Feature Type of the Excel writer.
2. Click the arrow next to the "Sheet Name".
3. Choose "Attribute Value" and pick "Lannamn" and click on "OK"
4. The name of the Feature Type will now change to "@Value(Lannamn)".\
   ![](<.gitbook/assets/image (53).png>)
5. Run the model and check the results.

</details>
