---
description: Transformations in parallel.
---

# Exercise 4

Your colleagues are impressed of everything you’ve done so far! Since you managed to dissolve all the municipality they wonder if you can do the same for all the Län in Sweden.

Assignment:

* Write an extra shape file as: C:\FMEData2026\Output\Lan\_sverige.shp.
* Again, the geometries should be dissolved. This time, based on Lanskod/namn. Each län should also get the area calculated, rounded on 2 decimals.
* Make sure the schema looks as followed:

<figure><img src=".gitbook/assets/image (2) (1) (1).png" alt=""><figcaption><p>Schema for the Län shape file.</p></figcaption></figure>

<details>

<summary>Tips:</summary>

* Since you will be using some of the same transformers you can select 1 or several and use CTRL+D to duplicate them.
* One shape writer is not limited to writing 1 shape. You can use the above tip on the Shape file writers featuretype as well.

</details>

{% hint style="info" %}
If you pay close attention you can see that when you sort data or group data, the transformers don’t let any features pass through it until everything is in. Before you’ve added these transformers or settings, features were sent through them almost instantly.

FME will always try to send a feature through the workspace as far as possible. But when it needs to sort data or group data, it must ensure all data is there before it can determine the sort order or determine if a group is complete and ready for processing. These type of transformers or settings make a transformer a “Blocking Transformer”
{% endhint %}

<details>

<summary>Step-By-Step instructions (Try not to use this!)</summary>

#### If you have trouble doing the exercise on your own, you can use these step-by-step instructions to complete the exercise.

For these steps, we've assumed that you have finished exercise 3.

1. Add one more "Dissolver" transformer and connect the output of your "AttributeManager" to it\
   ![](<.gitbook/assets/image (22).png>)
2. Double-click on the newly added "Dissolver" Enable "Group Processing", then click on the three dots and choose "lankod"\
   ![](<.gitbook/assets/image (23).png>)
3. Add another "AreaCalculator". Connect the second "Dissolver" to the newly added "AreaCalculator".
4. Add another AttributeRounder. Connect the second "AreaCalculator" to the newly added "AttributeRounder" Configure it the same way as the first one ("Attributes to Round"= area and "Decimal Places"= 2).\
   Your workspace should now look like this:\
   ![](<.gitbook/assets/image (24).png>)
5. You now need to write an extra shape file. 1 shapefile Writer can write more then one shapefile if the output catalogue and settings are the same. This is done by adding an extra "FeatureType".\
   Right click the existing FeatureType on your canvas (Demografiska\_statistikomraden) and choose "Duplicate" or Copy and Paste it.\
   ![](<.gitbook/assets/image (26).png>)
6. Double click the newly added FeatureType that is now called: Demografiska\_statistikomraden00 and change the "Shapefile Name" to "Lander\_Sverige".
7. Go to the "User Attributes" tab and remove the "Kommunnamn" and "Kommunkod" attributes. Then click on "OK".\
   ![](<.gitbook/assets/image (28).png>)
8. Connect the second "AattributeRounder" to the newly added FeatureType (Lander\_Sverige). Then you can run your workspace and see if it works as expected.\
   <br>

</details>

