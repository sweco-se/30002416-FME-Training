---
description: Precipitation calculation.
---

# Exercise 2

Climate researchers have seen an increase in extreme weather events like increasing heat waves, heavy precipitation, droughts, and wildfires over the last few years because of global warming. You have been asked to prepare precipitation data for further research.

**Assignment**:

You have received a file containing data on rainfall in your city. Unfortunately, the data is cumulative, and you need a figure per month. Fortunately, FME and adjacent feature attributes are here to help!

You will find input data here:

C:\FMEData2025\Data\Prepared\_data\Precipitation.xlsx

Your goal is to create an excel file with the same data, plus a column for each month containing average rainfall for that month. In other words, you want the cumulative rainfall for that month, minus the cumulative rainfall of the month before. Store the new file here:

C:\FMEData2025\Output\Exercise2

<details>

<summary>Tips:</summary>

* Remember that you are dealing with numeric attributes. You need the arithmetic editor.

- &#x20;You need to _enable adjacent feature attributes_ to have access to them.

* When enabled, you will find attributes of adjacent features under the “FME Feature Attributes” tab in the attribute editor window. Feature\[-1] is the feature before the current one, feature\[+1] is the feature after.
* Find the “Substitute Missing, Null and Empty” setting and give it a sensible value. Where will it be used and what do you want it to do there?

</details>

<details>

<summary>Bonus:</summary>

Create a HTML report with a line diagram and a table showing monthly and cumulative precipitation over the year.

</details>

{% hint style="info" %}
From this exercise, you’ve hopefully learnt:

* How to use adjacent feature attributes
{% endhint %}
