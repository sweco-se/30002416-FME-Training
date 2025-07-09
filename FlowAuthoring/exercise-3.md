---
description: Upload and run a workspace on FME Flow.
---

# Exercise 3

Now that the FME Flow is set up and ready to use, your colleagues have been eager to use it.

Your colleague Ryan has created a workspace for Gävle. It takes features from Gävle’s basemap geopackage and transforms it to a shape file. It lets the user choose what types of features and the coordinate system for the output. He has uploaded it to FME Flow but it crashes all the time. He says it works fine in FME Desktop on his computer, but it keeps crashing when he tries to run it on FME Flow.

He asks you to help him solve this problem.

**Assignment**:

Make sure the workspace that Ryan has uploaded to FME Flow works.

<details>

<summary>Tips:</summary>

* You can Run the workspace to recreate the error or you can maybe see if there is already a log file for this workspace where it failed to run.
  * The workspace can be found in the “Ryan” repository.

- Try to understand the log and find out why the workspace fails.

* You can download the workspace from the FME Flow interface, or you can download it from FME Form.

- After you’ve fixed the problem. You must republish the workspace. Look at the Wizard and make sure you understand the settings.

* You might need to create a new web connection to connect to FME Flow.

</details>

<details>

<summary>Bonus:</summary>

Think about the different Services you can use, which ones would be possible or best to use here?:

* Data Download

- Data Streaming

* Job Submitter

- KML Network Link

* Notification Service

</details>
