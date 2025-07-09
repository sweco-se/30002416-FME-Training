---
description: Structural Transformations.
---

# Exercise 2

Your colleagues are psyched about the job you did! The managed to read the shapes and can now work with the data.

They do notice that some of the columns in the shape have confusing names or contain data that they don’t really need. They ask you to clean up the data, so it better fits their needs.

**Assignment**:

They would like you to change the so called “schema”\* in the following way:

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption><p>Desired output Schema</p></figcaption></figure>

They would also like the columns in the schema in a different order. The order should look as followed:

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption><p>Schema order</p></figcaption></figure>

<details>

<summary>Tips:</summary>

* Once you’ve edited the Schema, you will notice some yellow and red errors on the featuretypes for both the reader and the writer. You will have to do some “feature mapping”.

- Your feature mapping will be lost once you unlink the featuretypes or place a certain type of transformer in between them.

</details>

<details>

<summary>Bonus:</summary>

If you place an “AttributeKeeper” between the 2 featuretypes or you accidentally disconnect the line between them, your feature mapping will be lost.&#x20;

To avoid this, make the required feature mapping and then right click on the thick black line between the feature types. Choose “Replace link with attribute manager”. Open the Attribute manager by clicking on the cogwheel and try to understand what happened.

</details>

{% hint style="info" %}
A **Schema** defines the structure of a dataset. Each dataset has its unique schema; it includes layers, attributes, and other rules that define or restrict its content.
{% endhint %}
