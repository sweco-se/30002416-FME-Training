---
description: Clipping Raster.
---

# Exercise 5

Another colleague needs your help. She has created a workspace that clips a Raster with a geometry that comes from an Autocad file. She gets a request to do this several times a week and automating it with FME Flow could save her a lot of time. (The persons requesting it from her can then do it themselves instead.)

Open: C:\FMEData2025\Workspaces\FMEFlowAuthoring\Exercise5\_TiffClipper.fmw

**Assignment:**

Upload the Workspace to FME Flow so that the users that will use it automatically get the clipped Raster as a download. They must be able to upload a DWG File themselves. Think about how you will upload the data to FME Flow.

<details>

<summary>Tips:</summary>

* There are Autocad DWG files to clip with in: C:\FMEData2025\Data\SCB\DWG\\

- The Raster is located at C:\FMEData2025\Data\Lantmateriet\sverigekartan\s1milj.tif.\
  You will need to upload this to FME Flow.

* When uploading the file from the Wizard. Does the source in the Reader matter?

- When publishing the workspace as a Download service, does the output destination matter?

</details>

<details>

<summary>Bonus:</summary>

Once you’ve uploaded the workspace through the wizard. Try to find the Raster in the workspace repository.

Saving data in the repository itself can have some downsides. If you look at Files & Connections, Resources, Data, you can see the Raster is also saved here. Edit your workspace so it reads the file from this location and remove the file from the Workspace Repository.

Test and see to it that the workspace still works.

</details>

{% hint style="info" %}
There are several places where you can save data on FME Flow. In repositories, in Shared resources and any location the FME Flow can read files from. Each of these methods has its pro’s and con’s. A few rules of thumb could be as followed:

* Files “physically” close to the server are read faster and increase performances.
* Files that can be used by several workspaces should not be saved in a repository.
* Files that are workspace specific can be saved in a repository.
* Each type influences permissions that are required to read them.
{% endhint %}
