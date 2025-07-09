---
description: Automated Flow documentation.
---

# Exercise 4

Everybody is eager to start working with FME Flow. However, to keep everything nice and organized you receive the task to create a documentation of the FME Flow. This means that you need to write down which workspaces are on the server, which schedules are running and when they run.

Since this information can change at any moment (new workspaces and schedules can be added at any time) you would like to automate this.

Luckily you know a consultant at Sweco who has done something like this before and gave you a workspace to automate this.

&#x20;The workspace still needs to be adjusted to work but that is something you can handle!

**Assignment**:

&#x20;Open the workspace: Exercise4\_FMEFlowDocumentation.fmw in: C:\FMEData2025\Workspaces\FMEFlowAuthoring\\

Create a new schedule which creates a server documentation automatically every day at xx:xx (pick a time that you want. However, you should be able to see if it works)

<details>

<summary>Tips:</summary>

* Make the following changes to enable the workspace to run:
  * Create Web Connection with "superuser" role (to be able to document all Workspaces and schedules)
  * Select the Web Connection in private parameters
  * Set the published parameter DOCUMENTATION\_DIR (if needed)

- Publish the workspace to the repository you’ve created in exercise 2

* Create a schedule for this workspace. It should run once per day.

- Test the schedule by triggering it manually.

</details>

<details>

<summary>Bonus:</summary>

CRON expressions can be used to create more complex schedules. Try to change the schedule to run every first Monday of the month at 20:00.

For help with CRON expressions you can visit:  [http://www.cronmaker.com/](http://www.cronmaker.com/)

</details>
