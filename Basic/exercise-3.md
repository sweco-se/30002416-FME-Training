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

- When _dissolving_ geometries, all geometries will, by default, be dissolved into 1 geometry if they touch each other. (So, Sweden’s mainland and Gotland will each become a single geometry). In this case you will need a “_Group By_” function which is often build into the transformers.
- There is a very useful transformer to _calculate_ the _area_ of a geometry.
- &#x20;The calculation of the area returns a very precise number. _Rounding_ it at 2 decimals might be advised to make it more readable.

</details>

<details>

<summary>Bonus:</summary>

Right now, we are taking all the source data through the entire workspace. From the 7 attributes we are reading we only need 4. Removing unnecessary data as soon as possible in your workspace is great for performances. Try to clean up the data as soon as possible inside your workspace so you don’t have to save the data through each transformation

</details>

{% hint style="info" %}
in FME means that the attribute really does not “exist” on this particular feature. However, the schema of the dataset says that it “could” be there. This is different from “null”. That is when the attribute exists but just doesn’t have a value.
{% endhint %}
