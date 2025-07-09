---
description: Divide and conquer.
---

# Exercise 4

The city of Stockholm has released a LOD1 3D model of large parts of the city as open data.&#x20;

**Assingment**:

Your employer has asked you to use this to identify office buildings with a volume of over 50 000 cubic meters for participation in an exciting new research program. You will need to calculate the volumes of all buildings identified as offices, and then filter out the relevant candidates to pass on to your colleagues.The 3D data can be found here:

C:\FMEData2025\Data\Stockholm\_3D\DWG

You’ll notice it’s been divided into multiple files, to keep them of a manageable size. As 3D-processing is quite resource demanding, we’re going to make use of that division.

The general idea is to set up a child workspace that does the processing for one file, and then a parent workspace that uses a WorkspaceRunner transformer to run that workspace once for each file.

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption><p>WorkspaceRunner setup.</p></figcaption></figure>

<details>

<summary>Tips:</summary>

* Start with the child. Make sure you can run it through without errors for more than one file before starting on the parent.
* These are DWG files. They do have attributes that classify the buildings as residential, office, public etc, but they’re not immediately visible. They need to be _exposed_ to be useful in the workspace. Make sure you filter out the office buildings before you start the 3D processing.
* We want to calculate volumes, so the _VolumeCalculator_ seem like logical place to start. Read the help for this, inspect your data, and consult the [FME Geometry model](https://docs.safe.com/fme/html/FME-Form-Documentation/FME-Form/!FME_Geometry/FME_Geometry_Model.htm). What is the geometry type of your data? What geometry type is required for the VolumeCalculator to work as expected? How can you _build_ the second from the first?

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

* Filter out the buildings of the required volume and write the data to a useful format. How do you make sure you don’t overwrite your output when you run the workspace with multiple inputs?
* Once your child workspace is done, move on to the parent. We want to run our child workspace for all the _file path names_ in a certain directory. What do you think the appropriate reader is called?
* Read up on the WorkspaceRunner and make sure you understand what the different parameters do. If you have the time, play around and compare logs, running times and resource consumption. What does “succeeded” mean in the different scenarios?

</details>

<details>

<summary>Bonus:</summary>

After all the child workspaces have been run (how do you know?), have your parent workspace read your results, and send them to a geocoding service to get a list of addresses. Please read up on the service terms of your chosen geocoder, and use samplers and decelerators judiciously.

</details>

{% hint style="info" %}
From this exercise, you’ve hopefully learnt:

\-          How to use the WorkspaceRunner

\-          How to work with 3D geometries
{% endhint %}
