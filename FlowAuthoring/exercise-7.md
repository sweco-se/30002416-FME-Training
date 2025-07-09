---
description: Geometry Picker.
---

# Exercise 7

Your colleague has changed the workspace so that it now writes to a PDF instead of an image.

People also told you they don’t like to upload a file to clip with all the time. They find it quite hard and user unfriendly.

In a webinar you’ve seen recently, you saw the possibility to draw a geometry directly in FME Flow instead of uploading a file which contains a clip geometry. You think this functionality can be very helpful in the workspace you’ve uploaded in the previous exercises to make it more user friendly.

**Assignment**:

Open the workspace: C:\FMEData2025\Workspaces\FMEFlowAuthoring\Exercise7\_TiffClipper2PDF\_Begin.fmw

Change the Workspace in such a way that the user can draw a polygon or box to clip with instead of uploading a clipping dwg.

<details>

<summary> Tips:</summary>

* There is a Geometry User parameter available.
* The Geometry picker returns a GeoJSON string.
* The GeoJSON comes in the LL84 coordinate system.

</details>

<details>

<summary>Bonus:</summary>

The colleague also changed the workspace so that the PDF has a title and a footer which says when the pdf was created.

It looks good but most of the changes are hardcoded and therefore not useful.

* Can you create an extra parameter so that the user can choose the title themselves?

- Now the date is added to the title by a parameter the user needs to fill in. FME has a lot of smart date functions, can you make so that today’s date is filled in automatically by FME and remove the user parameter “TODAY\_DATE”?

</details>

