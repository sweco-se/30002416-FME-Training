---
description: Creating a Workspace Response 101
---

# Exercise 4

You've set up the API framework and made a manual endpoint to give out information about the API. Now its time to make the real magic happen with FME and Data Virtualization to create dynamic API's.

This is done by making workspace responses!

_**From this point on you might need to do a lot of tests on your API. Since we are working on a training machine, disable Authentication for now on your rest API. This to make working with it during the course a bit more easy. You can do this in the "Security" tab within Data Virtualization.**_

## **Assignment 1**:

Make a new endpoint with the following characteristics:

| Field    | Value     |
| -------- | --------- |
| path     | getFiles  |
| Method   | GET       |
| Response | Workspace |

In the Response, set the following schema ("Create Schema"):

| Name      | Type   | Required |
| --------- | ------ | -------- |
| name      | String | x        |
| path      | String | x        |
| type      | String | x        |
| extension | String | x        |

{% hint style="info" %}
Schema's dont limit you on the data you can return with a FME Workspace endpoint. This because the workspace simply returns a "Response body" which can contain anything. However, it is best practice to use schema's to help the end-user understand what they can expect from your API call. By creating schema's you automatically update your Swagger documentation. The same Schema can also be used in several API calls. So if you need to update them, you only need to do so in 1 place.
{% endhint %}



Make sure to fill in all the required fields to make it a proper documented API endpoint. Think of; Tags, summaries, descriptions, HTTP Status Codes etc.

Since you are now developing an endpoint that will return production data. Make sure to enable Security for the FMEUser, FMEAuthor and FMEAdmin role.

## Assignment 2:

Generate a workspace and open it in FME Form.

In this workspace you need to read all the file information of the folder: C:\FMEData2025 this folder will be our filesystem that the API will communicate with.

Make sure to read all the files in this folder and all its subfolders with a "Directory and File Path Names" format.&#x20;

Make sure that you take care of the required attributes as set in the Schema for the response.body.content and that you also set the other required attributes like for instance "response.status\_code".

What happens when the FMEData2025 folder doesnt exist and a features comes from the "\<Rejected>" port? Create a proper error response.

<details>

<summary>Tips:</summary>

* A FeatureReader is a perfect transformer to start reading input data with when you start off with a Data Virtualization Feature-Type.
* The JSONTemplater can be used to properly create a Json with 1 root and several nested sub-templates.
  *   In the Json Templater you have to write some information yourself. In general you can see it like this:

      * Root: This is the top level from your Json, it will be printed once per feature you send in. So if you only want to create 1 Json (like we do in our case) then you have to make sure that only 1 feature is send in. If it receives 5 features, it will create 5 Json's.
      * Sub-template: the Json you write in here is merged into the Root. This is where you normaly send your features to.

      <figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>



      * For this particular case you can take the following Root and Sub-template. Keep in mind that you have to properly name the sub-template.

```json
//Root
[
fme:process-features("SEARCHRESULT")
]

//Sub-Template with the name: "SEARCHRESULT"

{
   "name":fme:get-attribute("path_rootname"),
   "path":fme:get-attribute("path_windows"),
   "type":fme:get-attribute("path_type"),
   "extension":fme:get-attribute("path_extension")
}
```

* There is a custom transformer, called the: "DataVirtualizationResponseSetter" that can take care of the status codes for your.

</details>
