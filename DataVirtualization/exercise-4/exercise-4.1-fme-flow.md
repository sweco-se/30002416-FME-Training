---
description: Creating a Workspace Response 101
---

# Exercise 4.1 - FME Flow

## **Assignment 1**:

Make a new endpoint with the following characteristics:

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

In the Response, choose to add a response code for 200 and set the following schema ("Create Schema"):

| Name      | Type   | Required |
| --------- | ------ | -------- |
| name      | String | No       |
| path      | String | No       |
| type      | String | No       |
| extension | String | No       |

{% hint style="info" %}
Schema's dont limit you on the data you can return with a FME Workspace endpoint. This because the workspace simply returns a "Response body" which can contain anything. However, it is best practice to use schema's to help the end-user understand what they can expect from your API call. By creating schema's you automatically update your Swagger documentation. The same Schema can also be used in several API calls. So if you need to update them, you only need to do so in 1 place.
{% endhint %}

Make sure to fill in all the required fields to make it a proper documented API endpoint. Think of; Tags, summaries, descriptions, HTTP Status Codes etc.
