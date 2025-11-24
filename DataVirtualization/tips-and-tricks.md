---
description: For those of you who want that little extra edge!
---

# Tips & Tricks

During this course, you've been working with a system that has already been developed by a frond-end developer. Normally this might not be the case. It would give you more freedom regarding parameters you send in and what kind of methods and paths you use. However, testing might become a bit harder since you are often stuck with the Swagger UI or programs like Postman.

Here we'll try to give you some tips and tricks that you can use during development.

## Loggers!!!

When working with DataVirtualization (and even with normal workspaces) in FME Flow. You cannot always clearly see what data comes in and what value the attributes have. It can be worth adding a "logger" transformer in your workspace. For instance directly after the "Reader Feature Types":

<figure><img src=".gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

This will force FME Flow to write out the entire feature in the Job Log. This allows you to see all the attributes and the values coming in. In this case for instance for: "request.path and query.path".

You can then copy and paste these values into FME form when you try to run the workspace there for test purposes.

<figure><img src=".gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

## DevTools

In our example case we have a web-app in a browser that allows us to run the commands. This opens up a whole new world of analyzing our API requests. We can use the browser "DevTools" to analyze our requests. This function has a different name in browsers. For Google Chrome in Swedish it is called "Verktyg för programmerare".

In almost every browser you can simply open it by using the "F12" button. If that does not work, its often found in the settings:

<figure><img src=".gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

When you open this, a new screen in your browser will open. It might look quite complex but its great once you get it!

For Data-Virtualization you are mostly interested in the "Network" tab. If you go to this tab and click on anything, you will see all the requests that your browser makes appear and you can analyze each one of them.

For this example, we've activated  "authentication" on the "/delete" endpoint.&#x20;

If we now press on the "delete" button, nothing will happen. When we look in FME Flow, we won't even see a log file. So what happend?

Lets look at the DevTools:

<figure><img src=".gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

In here we can see that 1 call is marked red which means it failed to process. We can also instantly see the Status code which is 401 (unauthorized).

By clicking on "name" that went wrong, we can see all the details of the call that the browser tried to send.

In the "Headers" tab, we can see all the details about the call. Here we can also directly see why it failed.

The Payload tab will show us the query parameters or content body that we tried to send:

