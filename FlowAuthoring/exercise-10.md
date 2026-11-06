---
description: Automations.
---

# Exercise 10

Your organization is very happy with the apps and gallery apps you’ve created. It makes working with FME Flow very user friendly and as an extra benefit, it also takes a lot of stress away from you.

However, at this point everything still needs to be triggered manually. For some processes this is unnecessary. For that reason you have decided to start using automations.

One of these processes is converting GeoJSON files to Shapefiles. A few times a day you get a request from a colleague to convert a GeoJSON file they have into a Shapefile. This takes you a lot of time.

**Assignment**:

Create an automation that does the following:

* Keeps track of a folder
* Whenever a new file is created in the Shared resources Temp catalogue. Your automation should pick it up and send it into the “GeoJson2Shapefile” workspace which is created by your colleague Ryan.

<details>

<summary>Tips:</summary>

* There are quite a lot of triggers available for automations. Make sure you pick the right one.&#x20;
* Inspect your choosen trigger, is there any information from the trigger that the workspace can utilize?
* Check out the action "Log a message" if you want to write out something specific in the automation log while testing, maybe you want to learn the value of some output attributes and parameters?
* Look at the workspace parameters. Where should it write data?
* When uploading the workspace. What Service would be best for automations which are triggered automatically?
* A test file can be found in: C:\FMEData2026\Data\Skåne\_GeoJson

</details>

<details>

<summary>Bonus:</summary>

You will now expand your automation further!&#x20;

1. Update your automation to only trigger the workspace if the picked up file in the trigger is of the type json.&#x20;
2. Create a new workspace that will be triggered by your automation – but ONLY if the first workspace succeeds. The new workspace should populate a log file in Excel format. The log file should contain:

* The name of the automation
* The Job ID of the first workspace that triggers the logging workspace
* The time of when the first workspace was triggered/started
* The time of when the first workspace finished

You can write out the Excel log to the resource data catalogue. The Excel logfile should always get new information inserted, it should never be overwritten.

**Tip**: Make a copy of your first automation before starting the bonus assignment.

</details>
