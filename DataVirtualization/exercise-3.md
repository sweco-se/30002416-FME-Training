---
description: Build a Manual Response for an Endpoint
---

# Exercise 3

You've created the framework for your API. At this stage, you have not configured any endpoints yet. Which means you cannot actually use your API yet. In this exercise you will create your first endpoint which will give the user information about the API. This will be a static API response.

## Assignment 1:

Create a manual "About" endpoint that returns the following information to the end user:

```json
//This code goes into the "Response Message"
{
"name": "FME Training Filesystem",
"description": "This Filesystem allows you to interact with the FMEData2026 catalog that is hosted on the server",
"options": [
"File Overviews",
"Downloading Files",
"Uploading Files",
"Deleting Files"
],
"contact": "<YourEmailAdress/DummyAdress>",
"operatingHours": "Mon–Fri 8:30 AM to 5:30 PM",
"contactNumber": "+46 712 345 678"
}
```

For this endpoint you will have to use the "GET" method. Make sure that you properly document it, give it a proper "Tag" and make sure you implement the correct type of "HTTP Status Code"

## Assignment 2:

Open the Swagger documentation and test your API call. Did you get the expected result? Also, go back to FME Flow and look at the "Jobs" menu. Did anything happen? Why is this?

<details>

<summary><strong>Tips:</strong></summary>

**Assignment 1:**

This is a manual response that will always return the JSON you've written. Therefore a simple 200 HTTP response will be good. There is not much that can go wrong here!

**Assignment 2:**

Manual responses always return the same result. This means that no workspace has to run since FME already knows what it should return and doesn't have to run a workspace to generate data. So you shouldn't see anything in the "Jobs" site.

</details>
