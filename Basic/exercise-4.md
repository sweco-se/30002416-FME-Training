---
description: Transformations in parallel.
---

# Exercise 4

Your colleagues are impressed of everything you’ve done so far! Since you managed to dissolve all the municipality they wonder if you can do the same for all the Län in Sweden.

Assignment:

* Write an extra shape file as: C:\FMEData2025\Output\Lan\_sverige.shp.
* Again, the geometries should be dissolved. This time, based on Lanskod/namn. Each län should also get the area calculated, rounded on 2 decimals.
* Make sure the schema looks as followed:

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption><p>Schema for the Län shape file.</p></figcaption></figure>

<details>

<summary>Tips:</summary>

* Since you will be using some of the same transformers you can select 1 or several and use CTRL+D to duplicate them.

- One shape writer is not limited to writing 1 shape. You can use the above tip on the Shape file writers featuretype as well.

</details>

{% hint style="info" %}
If you pay close attention you can see that when you sort data or group data, the transformers don’t let any features pass through it until everything is in. Before you’ve added these transformers or settings, features were sent through them almost instantly.

FME will always try to send a feature through the workspace as far as possible. But when it needs to sort data or group data, it must ensure all data is there before it can determine the sort order or determine if a group is complete and ready for processing. These type of transformers or settings make a transformer a “Blocking Transformer”
{% endhint %}
