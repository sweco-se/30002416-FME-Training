---
description: Automations.
---

# Exercise 10

Your organization is very happy with the Apps and Gallery Apps you’ve created. They make working with FME Flow very user friendly and as an extra benefit, it also takes a lot of stress away from you.

However, at this point everything still needs to be triggered manually. For some process this just seems unnecessary. Therefor you figured you should start using Automation.

One of these process is converting GeoJSON files to Shapefiles. A few times a day you get a request from a colleague to convert a GeoJSON file they have into a shapefile. This takes you a lot of time.

**Assignment**:

Create an automation that does the following:

* Keep track of a folder
* Whenever a new file is created in Shared resources Temp catalogue. Your automation should pick it up and send it into the “GeoJson2Shapefile” workspace which is created by your colleague Ryan.

<details>

<summary>Tips:</summary>

* There are quite a lot of triggers available for Automations. Make sure you pick the right one.
* Look at the workspace. Where should it write data?
* When uploading the workspace. What Service do you recon would be best for automations which are triggered automatically?
* A test file can be found in: C:\FMEData2025\Data\Skåne\_GeoJson

</details>

<details>

<summary>Bonus:</summary>

You will now expand you automation further! Create a new workspace that will be triggered by your automation – but ONLY if the first workspace succeeds. The new workspace should populate a log file in excel format. The log file should contain:

* The name of the automation

- The Job ID of the first workspace that triggers the logging workspace

* The time of when the first workspace was triggered/started

- The time of when the first workspace finished

You can write out the excel log to the Resource Data catalogue. The Excel logfile should always get new information inserted, it should never be overwritten.

**Tip**: Make a copy of your first automation before starting the bonus assignment.

</details>
