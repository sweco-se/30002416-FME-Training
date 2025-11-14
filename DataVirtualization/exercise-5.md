---
description: App Integration
---

# Exercise 5

Now that you have your first API up and running, lets test it in the application that your colleague has developed. This to see what Data Virtualization can do together with 3th party apps.

Navigate to "C:\app\MappArkiv" in a windows explorer.

Once you are in this folder, click the bar that contains the path and type "cmd":

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Press "Enter".

A Command line screen will open that is active in this current path. Write or copy the following code in:

```
npm run dev
```

After a little while you will see the following:

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

You can now minimize this screen, **don't close it!**

Open a new browser and navigate to the link: [http://localhost:5173/](http://localhost:5173/)

This should now open the following website:

<figure><img src=".gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

Clicking on the "Search" button will run your newly created Data Virtualization model showing the results.

You can play around with the filters in the top to see if your model is working as expected:

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

This shows how Data Virtualization can integrate different applications with FME. You now have a webapp that is able to dynamically browse a folder on your PC.

{% hint style="info" %}
As you might see, the app is prepared to have more functions, you can for instance click on the "Name" of folders to look what's inside of these folders.

There is also a "download" button behind every file to be able to download it.

These functions don't work just yet. So lets continue building our Data Virtualization further.
{% endhint %}
