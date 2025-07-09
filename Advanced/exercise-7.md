---
description: Dynamic database exports
---

# Exercise 7

You’ve created a database with different data from SCB on all the Swedish municipalities. You’ve made it accessible to your colleagues, and they find it very useful but… they all want the data in different formats, and they’re all interested in different subsets of the columns, and you’re getting tired of doing slightly different exports over and over. Enter FME and dynamic writing!

**Assignment**:

You want to create a workspace where a user can pick their format and which columns they’re interested in, and the customised dataset is exported from the database.

Your data is in a PostGIS database located at:

**host**: localhost\
**port**: 5432\
**database**: FME\
**user**: FME\
**password**: FMElearnings#1\
**schema**: advanced\
**table**: kommuner

<details>

<summary>Tips:</summary>

* You’ll need a few different user parameters. Note that the choice type has an Import button which might make your life easier. Let your users choose an output format, and the columns they want.

- Rule number one when working with databases is to let the database do the heavy lifting. In this case, how can you send the input from the parameters on to the database, and get only the data you need back? One way is to use the SQLExecutor to create a view, and then read the contents of your view back into your workspace. You might need some Text Editor magic to get your column name user parameter to behave as valid SQL:

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption><p>SQL example</p></figcaption></figure>

* The schema feature from the Feature reader is a great help in dynamic workflows, so see if you can utilize that.

- What type of writer can handle both different output formats and different output schemas?

</details>

<details>

<summary>Bonus:</summary>

Add a function where the user can limit their area of interest geographically by specifying a bounding box or by supplying a geometry. Also give them a chance to specify a name for their file.

</details>

{% hint style="info" %}
From this exercise, you’ve hopefully learnt:

* How to interact with your database with FME rather than just reading it
* How to use the generic and dynamic writing capabilities of FME
{% endhint %}
