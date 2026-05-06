---
description: Reading Demographic Data.
---

# Exercise 6

After delivering the data to the EU’s open data portal, you have to get back to your daily projects as a data analyst.

SCB (Statistikmyndigheten) in Sweden has published new data regarding the demographic structure of the country for 2025.&#x20;

**Assignment**:

It is up to you to read this data and _join/merge_ this data with the output you’ve gotten with the dissolver and area calculator so far. Then calculate the total population per municipality by writing an _expression_.

Open C:\FMEData2026\Workspaces\FMEFormBasic\Exercise6\_ReadingDemographicData\_begin.fmw.

The file that contains the demographic information is located in:

C:\FMEData2026\Data\Demografiska\_statistikomraden\Folkmängd\_per\_lan\_och\_region\_2025.xlsx

<details>

<summary>Tips:</summary>

* There are several ways to add a new file as a reader to your workspace.
* Always look at the “Parameters” when adding a new reader.
  * Does the data look as you expect it?
  * Do you need all the data?
*   &#x20;     Drawing a lot of lines to 1 transformer can take a lot of time and have a bad impact on your patience. Luckily FME understands that your time is valuable! Try and follow the following steps (_After you’ve added the file to read.):_

    * Click in the menu on the top on “View”
    * Hoover your mouse on “Windows”
    * Click on “Feature Type Connections” to make sure it is checked on.
    * Now find the “Feature Type Connections” window in FME Workbench. Most likely it is behind your “Translation Log” or “Visual Preview”.



    <figure><img src=".gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

    * If you open this screen you will see 3 columns: Sources, Destinations and Connections.
    * Select all the sources you want to quick connect (you can Drag your mouse, hold ctrl or use shift just like in a normal windows explorer screen).
    * Once you’ve selected all the sources you want to connect, choose a destination port in the “destinations” column.
    * Then click the “Connect” button to automatically let FME draw all the lines.
* When you perform a _join/merge_ on data you need a common attribute. What do these 2 datasets have in common?
* Adding values together in FME works the same as with a calculator. You can simply write an _Expression_ like: attribute1 + attribute2 + attribute3

</details>

<details>

<summary>Bonus:</summary>

Reading a lot of “FeatureTypes” from 1 file (for instance the excel you’ve just read with 22 sheets) quickly fills up your Canvas.&#x20;

Try and add the reader again. This time check the setting “Single Merged Feature Type” in the “Add Reader” settings. See what happens and try to understand what FME does.

In this case, if you “don’t” read the “read me” sheet, all the columns are the same. What do you expect happens if the sheets have different columns?

</details>



<details>

<summary>Step-By-Step instructions (Try not to use this!)</summary>

#### If you have trouble doing the exercise on your own, you can use these step-by-step instructions to complete the exercise.

1. in FME Workbench open: \
   C:\FMEData2026\Workspaces\FMEFormBasic\Exercise6\_ReadingDemographicData\_begin.fmw
2. Click on the "Reader" button in the top menu to add an extra reader:\
   ![](<.gitbook/assets/image (32).png>)
3. For the "Format" choose "Microsoft Excel".
4. For the "Dataset" click the 3 dots and choose "C:\FMEData2026\Data\Demografiska\_statistikomraden\Folkmängd\_per\_lan\_och\_region\_2025.xlsx". It should look like this.\
   ![](<.gitbook/assets/image (33).png>)
5. Click on the "Parameters..." button. This will give you a preview of what the Excel looks like. By clicking the the different sheets, you will notice that they all contain the same type of information, except for the "ReadMe" sheet.
6. Uncheck the "ReadMe" sheet. We do not want this one. Then click on "OK" and on "OK" again.\
   ![](<.gitbook/assets/image (34).png>)
7. You should now see the following:\
   ![](<.gitbook/assets/image (35).png>)
8. Now add the transformer "FeatureJoiner".
9. Connect the "AttributeRounder" to the "Left" port of the "FeatureJoiner".
10. Connect all the new FeatureTypes with the "Län" to the "Right" port of the "FeatureJoiner"\
    ![](<.gitbook/assets/image (36).png>)
11. Double-click on "FeatureJoiner". Under "Left" enter "kommunkod", under "Right", enter "kommun" and under "Comparison Mode", choose "Automatic".\
    ![](<.gitbook/assets/image (37).png>)
12. Now add the transformer "ExpressionEvaluator" and connect it with the "FeatureJoiner" "Joined" port.
13. Double-click on the "ExpressionEvaluator" and edit it so it looks like the one below. Click on the arrow in front of "FME Feature Attributes" to get access to all the Attributes. You can then simply double click them in order to add them in the Expression.\
    ![](<.gitbook/assets/image (38).png>)

#### Bonus:

1. Remove the Excel Reader and all its FeatureTypes.
2. Add a new Excel Reader and click on Parameters.
3. Just like before, uncheck the "ReadMe" sheet and click on "OK".
4. Under "Workflow Options", choose the "Single Merged Feature Type" and click on "OK"\
   ![](<.gitbook/assets/image (40).png>)
5. It will now look like the image below. But it will contain the same data as before. \
   ![](<.gitbook/assets/image (41).png>)
6. You can now connect this new "\<All>" FeatureType with the "FeatureJoiner" "Right" port and run the workspace as before.

</details>

