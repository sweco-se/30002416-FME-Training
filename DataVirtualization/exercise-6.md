---
description: Get specific Folder
---

# Exercise 6

Next up, you want the user to be able to navigate down into folders to see all the files that are within it. This is why you need to create another GET endpoint that gets all the files within the specified folder.

## Assignment 1:

Create a new endpoint:

| Field    | Value     |
| -------- | --------- |
| path     | getFiles  |
| Method   | GET       |
| Response | Workspace |

Make sure to fill in the rest of the information as you please and add a Tag that you can use to group this endpoint into a proper group. For instance: FileManagement

For the Parameters, this time you want to create a Path query parameter that the user will automatically fill by clicking on a directory:

| Name | Type   | Required |
| ---- | ------ | -------- |
| path | String | x        |

In the Response, make sure to set it on Workspace and add a proper HTTP Status code. For the Schema, you can reuse the schema you've created earlier. This since you will still return information about the files.

## Assignment 2:

For the workspace you will go trough sort of the same process as before. However, this time you don't need to filter on the name, extension and limits but only on the path.

{% hint style="info" %}
Since it's sort of the same process, we can add this new API endpoint into the same workspace. You are free to create a new workspace. This is up to you. For training purposes, we will explain this exercise with the idea that you put this endpoint into the same workspace. This so that you get a better understanding of having 1 workspace for several API endpoints.
{% endhint %}

Go to the "Workspaces" tab and select your new endpoint. Assign the **previously created** workspace to it.

The status will now change to "Needs Updating".

Open your model in FME Workbench. The workspace should now have a new FeatureType called "GET/getFiles".

In this workspace you will first check if the "query.path" has a value. If so, you can let the featuereader read from that folder. If it doesn't have a value, let it read the entire C:\FMEData2025 catalog again. You will use the same type of featureReader as before, Directory and File Pathnames.

For this endpoint, we don't need to do extra filtering afterwards so you can immediately continue with a JSONTemplater and set the proper response codes.

Make sure to take care of "rejected" features as well from the FeatureReader.

{% hint style="info" %}
In this particular case we are simply creating a Parallel flow besides the original. You could integrate the two streams with proper tests to then handle everything with transformers in series. However, in this course we don't want to focus too much on workspace development but more on the possibilities of FME's Data Virtualization. So we want to keep the workspaces as simple and straightforward as possible.
{% endhint %}

Once you are done creating your model. Upload it back to FME Flow and test it.

You can test it in the App by clicking on a directory and see if you get a result. For instance:

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

<details>

<summary>Tips:</summary>

* You will first need to test if the "query.path" parameter has a value. This can for instance be done with an AttributeManager and Conditional Values on a new "\_path" attribute. If the parameter has a value, we can set the output of the "\_path" attribute to it. If it does not have a value, we default it back to the "C:\FMEData2025" catalog.

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

* For the JsonTemplater you can reuse the one we already have in the model. This because you will still return the same attributes in the response.
* It shouldn't be possible for the user to send a "non-existing" path while using the web-app. However, if they would use swagger and send in an invalid path you do need to take care of the "rejected" port. Make sure to add a proper status code to the output of the rejected port and inside your API.

</details>

{% hint style="info" %}
This is going to very specific for this use case. But it is important in general when working with FME and Data Virtualization (and anything for that matter): **Security!**

In our app, we can only choose folders that are present inside the C:\FMEData2025 catalog. However, in the Swagger interface, we can type in any path.

Here we could for instance look in: "C:\Users\Administrator\AppData\Local\Microsoft". The workspace behind this API will run as normal and return all the files in this catalog. This catalog can store sensitive information like user credentials.

For this training, this is not so important since these machines are temporary. But when creating a real life production environment. Make sure to build in checks and build in proper security.

This can both be done in several ways:

1. Use Data Virtualization's Authentication.
2. Build in proper tests in your workspace.
3. Limit the access that the Service account of FME Flow has.
{% endhint %}
