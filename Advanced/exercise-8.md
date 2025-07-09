---
description: Custom transformers
---

# Exercise 8

Your team has been working a lot with hydrological data recently, for a project. You’re using the SMHI dataset for catchment areas, found here:

C:\FMEData2025\Data\SMHI\Delavrinningsområden\_2016

The data is fine, but you’ve noticed an irritant: a lot of the columns contain data kept in codes, and need a code list to be useful for presentation and human readability. The code list is found in a PDF document, and you all spend an annoying amount of time copy-pasting from this. In one case, you also need data from another shapefile.

You decided to solve the problem once and for all, moved the data to excel, and created a workspace that does the decoding, found at:

C:\FMEData2025\Workspaces\ FMEFormAdvanced\exercise8\_start.fmw

**Assignment**:

Now you want to share this with your colleagues, and you’ve heard a good way to do that is to create a custom transformer. You’ve also decided to add some more functionality.

Look at the workspace, understand what it does. If you’re not familiar with the InlineQuerier, take time to read up on it, it’s a useful tool in some scenarios. Turn it all into a custom transformer and give your transformer a reasonable name and a description.

Inspect the input and output ports that are created automatically. You will always want the same input data for the codelists, so don’t give your colleagues a chance to get that wrong.

If you look at the decoded data, you’ll notice some null values, that are caused by input keys simply missing from the codelists. These sometimes cause issues further downstream, so you want to give your co-workers a choice of how to handle these: drop them from the dataset, replace the NULL values with a dummy text, or leave the data as is. Implement with a user parameter on your custom transformer, and the appropriate changes to the code.

Make one more change to the functionality of your custom transformer. Be as lazy or ambitious and as serious or silly as you like!

<figure><img src=".gitbook/assets/image (6).png" alt=""><figcaption><p>Example of the result.</p></figcaption></figure>

<details>

<summary>Tips:</summary>

* Replacing your code list readers with feature readers gives you a chance to “hide them” inside your transformer. Note that this is only a good idea if you are sure everyone who is going to use this has access to the same file system!
* Look at the user parameters that are automatically created. Try to get a feel for how they work. Try to think in general terms: what does your transformer need to have passed to it in order to work as intended?

</details>

<details>

<summary>Bonus:</summary>

Export your transformer to an .fmx file. See how it changes color on the canvas? Open a blank workspace and make sure your transformer is accessible through quick-add. What steps to you need to take to make sure it’s available to your co-workers, and that they all use the same version?

</details>

{% hint style="info" %}
From this exercise, you’ve hopefully learnt:

* How to create and edit a custom transformer
* How to interact with a custom transformer using parameters
* How to use the InlineQuerier
{% endhint %}
