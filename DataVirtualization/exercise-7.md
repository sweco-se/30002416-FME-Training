---
description: Using the POST method to download a file.
---

# Exercise 7

So far the app has been using the GET method for all your API endpoints. These are by far the easiest to work with since you can simply send your parameters in the endpoint URL. However, sometimes you actually need to send data to the API. In that case you would want to use a POST.

For a POST call you always send the information in your "request body" when you do so, you will also need to set an extra header for "Content-Type" to explain what your type of data your request body contains.

In the previous exercise you've created a GET endpoint that sends a query parameter with the PATH:

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

&#x20;This endpoint could also work as a POST if we would  have configured it like that. We would then use the Method POST and the request could look something like this:

* **Request URL**: http://fmetraining/api/filesystem/getFiles
* **Method**: POST
* **Headers**:
  * Content-Type: application/json
* **Request-body**:&#x20;
  * {"path":"C:\FMEData2025\Data\Demografiska\_statistikomraden"}

GET is the more obvious path to take here since you are Requesting data. But the possibility is there!

## Assignment:

You need to create a new endpoint that uses the POST method. With this post we are going to download a certain file. (_This can be done with GET as well but we want to practice with POST_).

For this endpoint you will need to use the following settings:



&#x20;

&#x20;

&#x20;

&#x20;

&#x20;

&#x20;



