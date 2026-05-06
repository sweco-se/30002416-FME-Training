---
description: Transformations with Transformers.
---

# Exercise 3

Look at the shape file that you’ve just created in the previous exercise in the Data inspector. As you can see the Area column values all say \<missing>\*. This means we need to do something with this to make sure it’s useful.

Also, your colleagues think the data is a bit too detailed. Each municipality is split up into different towns and neighborhoods but only contain information on the municipality level.

_If you want to see this, you can look at the data in the data inspector. Search for any municipality and you will see it is duplicated quite often._

You say that it won’t be a problem to fix this, and you get back to your workspace!

**Assignment**:

* You need to _dissolve_ all the features with the same Kommunkod into 1 feature.
* You need to _calculate_ the _area_ of each municipality (Kommun) _rounded_ at 2 decimals.

<details>

<summary>Tips:</summary>

* There are several transformers to _dissolve_ geometries together based on a common attribute. In this case there is 1 that works better than the others.
* When _dissolving_ geometries, all geometries will, by default, be dissolved into 1 geometry if they touch each other. (So, Sweden’s mainland and Gotland will each become a single geometry). In this case you will need a “_Group By_” function which is often build into the transformers.
* There is a very useful transformer to _calculate_ the _area_ of a geometry.
* &#x20;The calculation of the area returns a very precise number. _Rounding_ it at 2 decimals might be advised to make it more readable.

</details>

<details>

<summary>Bonus:</summary>

Right now, we are taking all the source data through the entire workspace. From the 7 attributes we are reading we only need 4. Removing unnecessary data as soon as possible in your workspace is great for performances. Try to clean up the data as soon as possible inside your workspace so you don’t have to save the data through each transformation

</details>

{% hint style="info" %}
in FME means that the attribute really does not “exist” on this particular feature. However, the schema of the dataset says that it “could” be there. This is different from “null”. That is when the attribute exists but just doesn’t have a value.
{% endhint %}

<details>

<summary>Step-By-Step instructions (Try not to use this!)</summary>

#### If you have trouble doing the exercise on your own, you can use these step-by-step instructions to complete the exercise.

For these steps, we've assumed that you have finished exercise 2 (including the bonus).

1. If you have not completed the bonus of exercise 2 (and you don't want to lose your schema mapping. Right-click on the line that connects the reader with the writer and click on "Replace Link with AttributeManager"\
   ![](<.gitbook/assets/image (15).png>)\
   If you did do the bonus of exercise 2, you can skip this step.
2. Add the following transformer: "Dissolver"\
   ![](<.gitbook/assets/image (16).png>)
3. Connect your "AttributeManager" to the "Dissolver":\
   ![](<.gitbook/assets/image (17).png>)
4. Now double-click on the "Dissolver". Enable "Group Processing."\
   ![](<.gitbook/assets/image (18).png>)
5. In the "Group By" field, choose "kommunkod" by clicking on the arrow pointing down. Leave "Complete Groups" to "When All Features Received"\
   ![](<.gitbook/assets/image (19).png>)
6.  Add transformers "AreaCalculator" and "AttributeRounder"\
    ![](<.gitbook/assets/unknown (1).png>)

    &#x20;

    ![](<.gitbook/assets/unknown (2).png>)
7. Connect the transformers in the right order with the correct ports: Dissolver(Area Output) -> Area Calculator -> AttributeRounder.\
   ![](<.gitbook/assets/image (20).png>)
8. Double-click on the "AttributeRounder" and change the "Attribute to Round" and "Decimal Places" to the "Area" attribute you've created and to 2 decimal places.\
   ![](<.gitbook/assets/image (21).png>)
9. Run your workspace and see if it works as you expect.

#### Bonus:

This bonus exercise is intended to teach you about different transformers. You can add three transformers mentioned below and see how they work.

Add any of the following transformers below to your workflow. Either one of them works. Read their description to understand the differences.

![](<.gitbook/assets/unknown (3).png>)

&#x20;![](<.gitbook/assets/unknown (4).png>)

&#x20;![](<.gitbook/assets/unknown (5).png>)

&#x20;![](<.gitbook/assets/unknown (6).png>)

</details>

