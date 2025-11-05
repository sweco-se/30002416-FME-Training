---
description: Make your first API call
---

# Exercise 1

Before we start to create our own API, we should at least test one out ourselves first.

Skolverket has a great free to use API that we can use to get our toes wet.

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

## **Assignment 1**:

Make an API call to: `https://api.skolverket.se/skolenhetsregistret/v2/school-units` and see what you get as a result.

There are a few different programs that you can use to make this API call. Try to use the following 3:

1. Your Browser
2. cURL
3. FME

{% hint style="info" %}
Your browser is limited to the "GET" method. Since this call is specified as a "GET" you can get the results in your browser. This wouln't work with any other method!
{% endhint %}

{% hint style="info" %}
cURL is a command-line tool and library for transferring data with URLs. It supports various protocols like HTTP, HTTPS, FTP, and more. With cURL, you can make web requests, download files, and perform many other internet-related tasks from the terminal. It's commonly used for testing APIs and interacting with web services.
{% endhint %}

{% hint style="info" %}
&#x20;We are going to use FME to create an API but FME is also a great tool to intergrate with API's. It can do so by using the HTTPCaller  or the OpenAPICaller (out of scope for now).
{% endhint %}

## **Assignment 2**:

API's can often be chained after each other to get more detailed information. The call we made in the first assignment gave us all the schools in Sweden. We now want to get more details about the following school: "Stockholm Science & Innovation School 78433202, SSIS"

Make a new request using the following API call to get detailed information about this school:

`https://api.skolverket.se/skolenhetsregistret/v2/school-units/{schoolUnitCode}`&#x20;

You can choose the program you want to use!

<details>

<summary>Tips:</summary>

**Browser**: Since your browser will always automatically make a GET request, you can simply copy and paste the URL into your browser.&#x20;

**cURL**: cURL is a powerfull tool often used to test API's and interact with web services. You can use it directly in the command line. To open the command line interface, click on the search button in windows and type "cmd". You can then simply write: curl \<the url> and press enter. By doing so, the results will be the same as when you would use a browser. It can however be hard to read since it does not apply a "pretty print".

**FME**: in FME we can use a "creator" followed by a "HTTPCaller". Make sure to set the correct "HTTP Method":

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

</details>

{% hint style="info" %}
The Skolverket API only has "GET" calls as a method. These are relativly easy to use. Later on in this course we will work with different methods once we've created our own API with FME's Data Virtualization. The Browser method will then no longer work and we will start using FME or the Data Virtualization Swagger UI instead. These make it easier to test our API
{% endhint %}
