---
description: Creating a Workspace Response 101
---

# Exercise 4.2 - FME Form

## Assignment 2:

Generate a workspace and open it in FME Form.

In this workspace you need to read all the file information of the folder: C:\FMEData2026 this folder will be our filesystem that the API will communicate with.

Make sure to read all the files in this folder and all its subfolders with a "Directory and File Path Names" format.&#x20;

{% hint style="info" %}
It is important that you use a **FeatureReader** to do this. This so that you can use the input attributes that you get from the Rest API in your reader.
{% endhint %}

Because the end-user can send in filters, make sure to **Merge Initiator and Result** in the featureReader so that you keep these filter attributes in the result. This setting is found under "_Attribute and Geometry Handling_" in the FeatureReader.

### Now, lets create the workspace. Since this is the first one, lets take it a bit easier:

* After reading the files with a featureReader, you can use a **StringSearcher** to look for any specified name filters:

<figure><img src="../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>



* Now test if the user has added an Extension filter. You can use a **TestFilter** for this:

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* If the user has specified an extension, check it versus the files with a **tester**:

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* The Last parameter to take care of, is the "limit". First add a **Counter** starting at 1 to give all the files a number. Then add a **Tester** to check if query.limit > 0. If query.limit is bigger than 1, add another **Tester** that checks: \_count <= query.limit. This will give you the right results.
* Add a **JsonTemplater** to create the proper Json, making sure you take care of all the attributes you defined in the Schema before. If you are not familiar with this transformer, there is some help in the "**Tips**" below.

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption><p>Your workspace should now look something like this.</p></figcaption></figure>

* Make sure to take care of all the required attributes for the output, for instance "response.status\_code"&#x20;

What happens when the FMEData2026 folder doesn't exist and a features comes from the "\<Rejected>" port? Create a proper error response.

Once your workspace is ready, publish it back to FME Flow and test your new API-call in the Swagger interface.&#x20;

You can test different calls. For instance; one with no filters, one with extension = 'dwg', one with q=Demo and one with limit = 10.

<details>

<summary>Tips:</summary>

* A FeatureReader is a perfect transformer to start reading input data with when you start off with a Data Virtualization Feature-Type.
* The JSONTemplater can be used to properly create a Json with 1 root and several nested sub-templates.
  *   In the Json Templater you have to write some information yourself. In general you can see it like this:

      * Root: This is the top level from your Json, it will be printed once per feature you send in. So if you only want to create 1 Json (like we do in our case) then you have to make sure that only 1 feature is send in. If it receives 5 features, it will create 5 Json's.
      * Sub-template: the Json you write in here is merged into the Root. This is where you normally send your features to.

      <figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>



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
* When testing your workspace, keep in mind, that by default, FME sets the parameters itself to strings like: "\<string>". These will not work when testing. You either have to set a value or leave them empty as in: "".

</details>
