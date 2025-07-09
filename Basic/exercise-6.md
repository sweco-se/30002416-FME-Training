---
description: Reading Demographic Data.
---

# Exercise 6

After delivering the data to the EU’s open data portal, you have to get back to your daily projects as a data analyst.

SCB (Statistikmyndigheten) in Sweden has published new data regarding the demographic structure of the country for 2025.&#x20;

**Assignment**:

It is up to you to read this data and _join/merge_ this data with the output you’ve gotten with the dissolver and area calculator so far. Then calculate the total population per municipality by writing an _expression_.

Open C:\FMEData2025\Workspaces\FMEFormBasic\Exercise6\_ReadingDemographicData\_begin.fmw.

The file that contains the demographic information is located in:

C:\FMEData2025\Data\Demografiska\_statistikomraden\Folkmängd\_per\_lan\_och\_region\_2025.xlsx

<details>

<summary>Tips:</summary>

* There are several ways to add a new file as a reader to your workspace.

- Always look at the “Parameters” when adding a new reader.
  * Does the data look as you expect it?
  * Do you need all the data?

*   &#x20;     Drawing a lot of lines to 1 transformer can take a lot of time and have a bad impact on your patience. Luckily FME understands that your time is valuable! Try and follow the following steps (_After you’ve added the file to read.):_

    * Click in the menu on the top on “View”
    * Hoover your mouse on “Windows”
    * Click on “Feature Type Connections” to make sure it is checked on.
    * Now find the “Feature Type Connections” window in FME Workbench. Most likely it is behind your “Translation Log” or “Visual Preview”.



    <figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

    * If you open this screen you will see 3 columns: Sources, Destinations and Connections.
    * Select all the sources you want to quick connect (you can Drag your mouse, hold ctrl or use shift just like in a normal windows explorer screen).
    * Once you’ve selected all the sources you want to connect, choose a destination port in the “destinations” column.
    * Then click the “Connect” button to automatically let FME draw all the lines.

- When you perform a _join/merge_ on data you need a common attribute. What do these 2 datasets have in common?
- Adding values together in FME works the same as with a calculator. You can simply write an _Expression_ like: attribute1 + attribute2 + attribute3

</details>

<details>

<summary>Bonus:</summary>

Reading a lot of “FeatureTypes” from 1 file (for instance the excel you’ve just read with 22 sheets) quickly fills up your Canvas.&#x20;

Try and add the reader again. This time check the setting “Single Merged Feature Type” in the “Add Reader” settings. See what happens and try to understand what FME does.

In this case, if you “don’t” read the “read me” sheet, all the columns are the same. What do you expect happens if the sheets have different columns?

</details>
