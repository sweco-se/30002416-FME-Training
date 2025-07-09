---
description: Visual Workspace Compare.
---

# Exercise 8

The workspace you’ve created in the previous project is used quite a lot. It is your workspace, and you maintain it. Therefore, you’ve saved it in a secure location (C:\FMEData2025\Workspaces\Exercise7\_WritingDemographicData.fmw).

However, your colleague Anton thought it could use some changes. He copied your workspace and made some modifications to it. He tells you it’s mostly annotations to make the workspace clearer and some tests to ensure the quality of the data.

You doubt this though!

He saved the changes he made into a new workspace located in: C:\FMEData2025\Resources\Exercise8\_WritingDemographicData\_Anton.fmw

**Assignment**:

It is now up to you as the personal responsible for this workspace to look at Anton's changes and decide if they are for the better or worse and to decide what to do with them!

Open C:\FMEData2025\Workspaces\Exercise7\_WritingDemographicData.fmw

Once you’ve opened workbench. Open the “Compare Workspaces…” under “Tools”. Then choose the original workspace as “Editable (left)” and his workspace as a comparison workspace “Read-only (right)”.

The comparison screen will open in FME Workbench (You might have to move it around and make it bigger to visually see the differences).&#x20;

It is now up to you to look at the changes and decide if they are good or not. If you think they indeed improve the workspace you can merge them into your workspace.

<details>

<summary>Tips:</summary>

* Not all changes are for the better. If you think they are wrong. You can simply ignore them.

- The order of the changes you process are important! You cannot merge a connection line into your workspace if one of the transformers is still missing from the workspace. You will first need to transfer the transformer itself.

</details>

{% hint style="info" %}
The Comparison tool in FME allows users to compare two workspaces simultaneously. These differences are represented visually, allowing the user to compare the two workspaces efficiently. Users can choose to copy over elements into the Editable canvas to make changes based on the differences.
{% endhint %}
