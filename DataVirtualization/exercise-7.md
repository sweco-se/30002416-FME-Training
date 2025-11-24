---
description: Using the POST method to download a file.
---

# Exercise 7

So far the app has been using the GET method for all your API endpoints. These are by far the easiest to work with since you can simply send your parameters in the endpoint URL. However, sometimes you actually need to send data to the API. In that case you would want to use a POST.

For a POST call you always send the information in your "request body" when you do so, you will also need to set an extra header for "Content-Type" to explain what your type of data your request body contains.

In the previous exercise you've created a GET endpoint that sends a query parameter with the PATH:

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

&#x20;This endpoint could also work as a POST if we would  have configured it like that. We would then use the Method POST and the request could look something like this:

* **Request URL**: http://fmetraining/api/filesystem/getFiles
* **Method**: POST
* **Headers**:
  * Content-Type: application/json
* **Request-body**:&#x20;
  * {"path":"C:\FMEData2025\Data\Demografiska\_statistikomraden"}

GET is the more obvious path to take here since you are Requesting data. But the possibility is there!

In this assignment you are going to create a POST request to download a file. You will set up the endpoint and in the request-body you will specify which file you want to download.

## Assignment 1:

You need to create a new endpoint that uses the POST method. With this post we are going to download a certain file. (_This can be done with GET as well but we want to practice with POST_).

For this endpoint you will need to use the following settings:

| Field    | Value              |
| -------- | ------------------ |
| Path     | /getFiles/download |
| Method   | POST               |
| Response | Workspace          |

&#x20;As you will see, when you choose the "POST" method, a different tab is added named "Request Body". Here you have the option to specify how a request body should look and what it should contain. In this case, the request body should contain a very simple JSON that has the "path" parameter that will contains the search-path to the file.

Because the front-end developer has already created the code. All you have to do is make sure that FME Flow takes care of it. In the Request Body tab, make sure it is set to "Required" and add a property called "path" as a required string.

Keep the Content Type on "application/json"

## Assignment 2:

Generate a new workspace for this endpoint and open it in FME Form.

In your new workspace you will see that you've now got some extra attributes coming in from the request compared to a "GET":

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

We no longer have the query parameters that are found in the endpoint itself since we didn't set any. Instead. you'll now have request body attributes and the content type.

The content\_type is set to "Application/json" since we wanted that as our input type. The request.body itself will have the value of the path that we are interested in. For instance:

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

The request body contains the whole JSON that is getting send in. For FME to download the file, we only need the search path. You can use different transformers to extract the value of this search path from the JSON.

You can for instance use a StringSearcher or StringReplacer with regex or you could simply use a JSONExtractor to get the value of the Path.

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

&#x20;Now that you have the path to the file to be downloaded, FME will simplify things for you. You can set the "response.body.content\_file\_path" to this value. FME will then automatically understand it should send the content of this file.

Make sure to also set the other properties for the http\_response feature type. For the other settings, the Body Content Type is very important. You must set this to "application/octet-stream".

{% hint style="info" %}


Application/octet-stream is a general-purpose MIME (Multipurpose Internet Mail Extensions) type used to denote binary data. It doesn't specify a particular file format, so it can be used for any kind of binary file, such as executables, images, or audio files. Here are a few key points:

* **Binary Data**: It's typically used for arbitrary binary data that doesn't fit a specific MIME type.
* **File Download**: Often used for file downloads to ensure the browser treats the file as binary and prompts the user to save it instead of trying to display it.
* **Flexibility**: Since it’s a general type, it offers flexibility but requires the receiver to know how to handle the specific file properly.

you need to use this content type here since the user can download all kind of file formats. By using a binary format, the extension of the file will determine what kind of file we are working with.
{% endhint %}



&#x20;

&#x20;

&#x20;



