---
description: Build a Manual Response for an Endpoint
---

# Exercise 3

You've created the framework for your API. At this stage, you have not configured any endpoints yet. Which means you cannot actually use your API yet. In this exercise you will create your first endpoint which will give the user information about the API. This will be a static API response.

## Assignment 1:

Create a manual "About" endpoint that returns the following information to the end user:

```json
{
"name": "FME Training Filesystem",
"description": "This Filesystem allows you to interact with the FMEData2025 catalog that is hosted on the server",
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

Make sure that you properly document it, give it a proper "Tag" and make sure you implement the correct type of "HTTP Status Code"

## Assignment 2:

Open the Swagger documentation and test your API call. Did you get the expected result? Also, go back to FME Flow and look at the "Jobs" menu. Did anything happen? Why is this?
