---
description: Coordinate systems.
---

# Exercise 5

The data you created is well received by upper management. They now want to use this data for an international project. They need to deliver this data to the European Union’s open data portal.

However, since this is an international project there are extra requirements that need to be met regarding the coordinate system.

**Assignment**:

Right now, your data has the SWEREF99-TM coordinate system. They want you to write your output shape file in LL84.

_Edit the workspace that you’ve made in exercise 4 (or open: C:\FMEData2025\Workspaces\FMEFormBasic\Exercise4\_TransformationsInParallel.fmw) and make sure the data is written with the “LL84” coordinate system._

You can write the data to: _C:\FMEData2025\Output_

<details>

<summary><em>Tips:</em></summary>

* Your colleagues who gave you the data tell you that the original coordinate system used to be: SWEREF-99-TM. Make sure to _set_ the _coordinate system_ to this if FME does not set this itself.

- LL84 is a common coordinate system using Latitude and Longitude.

* To go from one coordinate system to another you can _reproject_ it in FME.

- Add a background map in your Data inspector to see if the results are as you expect.

* Look at the area that is calculated. What happened with the values and how could you solve this if needed?

- You might want to write this data to: C:\FMEData2025\Output. If you have the setting “Prompt for user parameters” on, you can always choose the output location when you run your workspace and don’t need to edit it in the writer settings.

&#x20;

</details>

<details>

<summary>Bonus:</summary>

There are several ways of performing this action. Try out a few if you can and think of which one you prefer and why.

</details>

{% hint style="info" %}
FME can perform a lot of the same tasks in different ways. This is where personal preferences, experience and best practice comes into play. In general, we can give you the following tips regarding actions like the one above:

* Is the workspace for personal use: Do whatever feels best for you.
* Is the workspace shared with colleagues: Talk with your team and determine which types of rules you all want to up live when it comes down to developing workspaces.
* Is the workspace for an external customer: Try and make your workspace as easy to read as possible.
{% endhint %}
