---
description: Structural Transformations.
---

# Exercise 2

Your colleagues are psyched about the job you did! The managed to read the shapes and can now work with the data.

They do notice that some of the columns in the shape have confusing names or contain data that they don’t really need. They ask you to clean up the data, so it better fits their needs.

**Assignment**:

They would like you to change the so called “schema”\* in the following way:

<figure><img src=".gitbook/assets/image (1) (1).png" alt=""><figcaption><p>Desired output Schema</p></figcaption></figure>

They would also like the columns in the schema in a different order. The order should look as followed:

<figure><img src=".gitbook/assets/image (2) (1).png" alt=""><figcaption><p>Schema order</p></figcaption></figure>

<details>

<summary>Tips:</summary>

* Once you’ve edited the Schema, you will notice some yellow and red errors on the featuretypes for both the reader and the writer. You will have to do some “feature mapping”.
* Your feature mapping will be lost once you unlink the featuretypes or place a certain type of transformer in between them.

</details>

<details>

<summary>Bonus:</summary>

If you place an “AttributeKeeper” between the 2 featuretypes or you accidentally disconnect the line between them, your feature mapping will be lost.&#x20;

To avoid this, make the required feature mapping and then right click on the thick black line between the feature types. Choose “Replace link with attribute manager”. Open the Attribute manager by clicking on the cogwheel and try to understand what happened.

</details>

{% hint style="info" %}
A **Schema** defines the structure of a dataset. Each dataset has its unique schema; it includes layers, attributes, and other rules that define or restrict its content.
{% endhint %}

<details>

<summary>Step-By-Step instructions (Try not to use this!)</summary>

#### If you have trouble doing the exercise on your own, you can use these step-by-step instructions to complete the exercise.

For these steps, we've assumed that you have finished exercise 1 (excluding the bonus).

1. Double-click on "Demografiska\_statistikomraden"
2. Go to "User Attributes" and make sure the "Schema Definition" is set to "Manual"
3. Double click on the fields you want to modify and type in the new name.\
   ![](<.gitbook/assets/image (8).png>)
4. For "uuid", "deso", and "version", you can just delete the fields(by clicking on that specific field and then clicking "Remove row"\
   ![](<.gitbook/assets/image (10).png>)
5. To add the new Attribute "Area" click on the "+" sign and give it the correct name. For the Type you can choose "Float".
6. You can fix the desired order of the attributes by clicking on the "Move Up" and "Move Down" buttons\
   ![](<.gitbook/assets/image (11).png>)
7. Once you are done with your changes, click on "OK".
8. Now your workflow should look like this:\
   ![](<.gitbook/assets/image (12).png>)

#### Bonus:

1. Once you've performed the steps above, Right-click on the line that connects the reader with the writer. Click on "Replace Link with AttributeManager"\
   <img src=".gitbook/assets/image (13).png" alt="" data-size="original">
2. As you can see below, your mapping has been moved inside the "AttributeManager".\
   By mapping, we are referring to the individual connections between the attributes. For example, id -> ID. \
   ![](<.gitbook/assets/image (14).png>)
3. You can double click on the AttributeManager to see that it performs different actions on the attributes within the transformer.<br>



</details>

