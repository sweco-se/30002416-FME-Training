---
description: Creating a Workspace Response 101
---

# Exercise 4.1 - FME Flow

## **Assignment 1**:

For this exercise we are going to use a so called "Schema" for the response. Schema's are not mandatory but are considered best practice. They can be re-used and function as form of documentation for your API. They simply tell the end-user what data they can expect back from a successful rest call.

In the Data Virtualization interface, click on the "Schemas" tab and choose "Create". Give your schema a name and description. You can leave the "JSON Type" on "Object".

For the properties, create the following Schema:

| Name      | Type   | Required |
| --------- | ------ | -------- |
| name      | String | No       |
| path      | String | No       |
| type      | String | No       |
| extension | String | No       |

Now that you have your Schema, lets create the actual rest API.

Go back to the "Endpoints" tab and make a new endpoint with the following characteristics:

| Field    | Value           |
| -------- | --------------- |
| path     | getFiles/search |
| Method   | GET             |
| Response | Workspace       |

Make sure to fill in the rest of the information as you please and add a Tag that you can use to group this call into a proper group. For instance: FileManagement

For the Parameters, you need to use Query Parameters. These will allow the user to filter the results for specific file/folder names, extensions and be able to set limits.

Use the following Query parameters:

| Name      | Type    | Required |
| --------- | ------- | -------- |
| q         | String  | No       |
| extension | String  | No       |
| limit     | Integer | No       |

In the Response, choose to add a response code for 200. For the Response Structure, choose the Schema you just created.

{% hint style="info" %}
Schema's dont limit you on the data you can return with a FME Workspace endpoint. This because the workspace simply returns a "Response body" which can contain anything. However, it is best practice to use schema's to help the end-user understand what they can expect from your API call. By creating schema's you automatically update your Swagger documentation. The same Schema can also be used in several API calls. So if you need to update them, you only need to do so in 1 place.
{% endhint %}

Make sure to fill in all the required fields to make it a proper documented API endpoint. Think of; Tags, summaries, descriptions, HTTP Status Codes etc.
