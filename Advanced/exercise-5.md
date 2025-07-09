---
description: Parameters to rule the world.
---

# Exercise 5

You’re working on a series of thematic maps, and have downloaded some nice, stylized background maps as GeoJSON from [https://www.projectlinework.org/](https://www.projectlinework.org/) that you want to use. You realise you keep making the same edits to your dataset over and over, and decide to make a parameterized workspace to do it for you.

There are three different datasets in the folder:

C:\FMEData2025\Data\projectlinework

**Assignment**:

You want to be able to work with all three using the same workspace. Create a reader and a parameter that lets you choose which dataset to use, and that reads all three correctly.

As it’s GeoJSON, it’s lat-long coordinates, which is generally not a particularly good choice for visualisation. You want to be able to set the coordinate system, so create a parameter that does this.

While experimenting with coordinate systems, you realize that this dataset gets silly when approaching the poles in a lot of projections. A common way of solving this is to simply cut the dataset off at 80-85 degrees north/south. For some parts of your project, you are only looking at Europe, and it would be nice to always have the same bounding box. Create a parameter to let you choose the extent of the dataset.

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption><p>Choice with Alias parameter.</p></figcaption></figure>

Decide what you want to do with output and create the appropriate parameters.

Once you are happy with your choices, you want to create a log file of which settings you’ve used for which project. Create a parameter to turn logging on or off. If your logging parameter is checked, parameters with the proper type for project name, date, log output folder should appear. Write all of your parameters to a csv. Make sure that you only write to the log when you parameter is checked, and that you don’t overwrite the output from your previous runs!

<details>

<summary>Tips:</summary>

* A choice parameter doesn’t need to have the same display name as value. Use this to make your file selection parameter more user-friendly.

- Consider using private scripted parameters to control the search envelope in the reader. If you’re not used to writing python, there is a snippet for inspiration in: C:\FMEData2025\Resources\example\_scripted\_parameter.txt

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption><p>Scripted Parameters</p></figcaption></figure>

* If scripted parameters feel unnecessarily complex, it is also possible to use a tester to test the value of your extents parameter, and then clip the linework to a bounding box based on the result.

- You don’t want to append a line to your log file until you’re sure your geodatabase was written correctly. How do you ensure that?

</details>

{% hint style="info" %}
From this exercise, you’ve hopefully learnt:

\-          How to set up and use different types of parameters in FME

\-          How to create scripted parameters
{% endhint %}
