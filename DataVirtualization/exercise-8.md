---
description: Using the DELETE method.
---

# Exercise 8

Last but not least, lets also take a look at the DELETE method for an endpoint.

You want the user to be able to delete files from via this file-system. To make it clear that they are going to perform a delete, we are going to use the method that is also called "DELETE".

{% hint style="info" %}
As explained the in previous exercise, this can also be achieved with a GET or POST. However, we want to use best practice and make it clear in our automated documentation that this endpoint will remove a file. In that case it's best to use the method that is specified for this action.
{% endhint %}

## Assignment 1:

Create a new endpoint in your rest interface with the method DELETE. Use the following settings:

| Field    | Value     |
| -------- | --------- |
| Path     | /delete   |
| Method   | DELETE    |
| Response | Workspace |

&#x20;All other settings we will leave up to you. Look at what tabs you have available and what settings you can set. Keep in mind that you have to send in the search path to the file in some way!

## **Assignment 2**:

Generate the workspace and modify it. There are several ways to delete a file with FME. For best practice purposes we would suggest to use a "File Copy" writer.

As always, take care of the attributes required by the http\_response and test your model in the file-browser app.
