---
description: Create a new API
---

# Exercise 2

Now that you know how a basic API works, its time to create our own! You are going to create an API that will allow users to check a file system, download files, upload files and even remove files by using GET, POST and DELETE.&#x20;

A developer has already created a front-end application that the users will use to interact with the file system. It is up to you to create the back-end code that will use the Data Virtualization API's to perform these tasks.

<kbd>_**Because the developer has already created the front-end application, it's very important that you use the correct names and paths to the API calls in order for it to work!**_</kbd>

## **Assignment 1**:

Open FME Flow, go to Data Virtualization and choose "Create API". &#x20;

When we choose this option you are asked to fill in the API Details. This is an important step because this is the first information that a user/developer will see when they try to create an application on top of your API. Use the following template/settings:

### API Details

| Field           | Value                 | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --------------- | --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| API Title       | \<Up To You>          | <p>The header for the documentation page and will</p><p>label any automatically generated Data</p><p>Virtualization workspaces.</p>                                                                                                                                                                                                                                                                                                                                        |
| Namespace       | filesystem            | <p>A unique identifier for your API and is included in the API's URL path. Since it forms part of the endpoint URLs, it's recommended that you do not change it after it's been set. For easier integration and cleaner URLs, it is best practice to choose a short, clear, and descriptive namespace.</p><p> </p><p>Based on this, all requests to the Data Virtualization API will take the general URL form: https://&#x3C;FMEFlow>/api/filesystem/&#x3C;endpoint>.</p> |
| Versioning      | 1.0.0                 | <p>Allows you to track iterations of the Data</p><p>Virtualization API.</p>                                                                                                                                                                                                                                                                                                                                                                                                |
| Summary         | \<Up To You>          | A short summary of the API that will appear in the documentation.                                                                                                                                                                                                                                                                                                                                                                                                          |
| Description     | \<Up To You>          | A short description of the API that will appear in the documentation.                                                                                                                                                                                                                                                                                                                                                                                                      |
| Job Queues      | Leave this unselected | Allow all requests to the API to be routed to a specific engine. Leaving this blank will use the Default queue.                                                                                                                                                                                                                                                                                                                                                            |
| Job Expiry Time | 2 minutes             | Determines how long can elapse between the initial request and delivery of the response. That means user requests will receive an expiry error if their requests exceed 2 minutes. For an API that will have requests that will run processes that exceed 2 minutes, like complex transformations or large data sources, extend this time.                                                                                                                                 |

{% hint style="info" %}
### Job Queues can be great if you have more than 1 FME Flow Engine and have a heavy load on your FME Flow and API. If you expect a lot of calls to your API it could happen that there are constantly FME Workspaces running on your engines. Other workspaces that come from Schedules, automations, apps etc won't get a change to start since the engine is busy all the time (they will get queued). On the other hand, if all your engines are running time consuming jobs, your API wont be able to get hold of an engine and run the calls that are made to your API. Job Queues allow you to dedicate engines to your API or other processes depending on your needs.
{% endhint %}

### Contact

| Field | Value        |
| ----- | ------------ |
| Name  | \<Up To You> |
| URL   | \<Up To You> |
| Email | \<Up To You> |

{% hint style="info" %}
Contact information appears on the API documentation page and helps end users know who to reach out to with questions, issues, or feedback. This can be the details of an organization or a specific administrator responsible for the API. While optional, providing contact information adds professionalism and supports user trust. You can enter your own details or use the (fictional) sample data provided below.
{% endhint %}

### Endpoint Security

| Field         | Value                                                               | Why                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Access level  | Authenticated                                                       | This means all endpoints require authentication by default.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Allowed Roles | “fmeadmin”, “fmeauthor”, and “fmeuser”                              | This will allow all users in these roles (and the tokens they create) to access API endpoints by default.                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Allowed Users | Select your own user account, for example, “admin” in this example. | <p>By default, only selected users and the tokens they generate are granted access to specific API endpoints.</p><p> </p><p>Your own account is not automatically granted access. To ensure you can access all necessary endpoints, explicitly assign access to your user account. In some cases, you may choose not to grant yourself access to all endpoints.</p><p>For example, if different departments manage distinct areas of the API and your role is limited to overall administration rather than direct interaction with specific data.</p> |

{% hint style="info" %}
Security is very important. Especially for a filesystem that allows users to see, download, upload and remove files. After API creation, access can be managed and updated per individual endpoint. However, in this case we would suggest you set at least a basic level of authentication!
{% endhint %}

### Caching

| Field           | Value | Description                                                                                                                                                                                                                                                              |
| --------------- | ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Cache Responses | No    | <p>We are not going to work with heavy processes and the results we get will differ every time (files can be uploaded and removed for instance) so this is not something we want to do here.<br>Later on; caching can be managed and updated per individual endpoint</p> |

{% hint style="info" %}
Every time you make a call to the API FME Flow will run your model (if its a workspace call) and process it as a new request. This takes up an engine. If its a slow process that always returns the same results, you can choose to cache it. Then FME will run the first time as normal to create the cache. Afterwards when the same call is used. FME will simply return the cache as its response. It will no longer use an engine but the results will always be the same.

FME will rerun the process once the TTL (Time to Live) has expired.
{% endhint %}

### Asynchronous Processing

| Field                        | Value | Description                                                                                                                                                 |
| ---------------------------- | ----- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Return Asynchronous Response | No    | When enabled, endpoints will immediately return a status and URL for viewing the results once the job is complete. You can override this for each endpoint. |

{% hint style="info" %}
Asynchronous Processing is great when a workspace endpoint is called that takes a long time to run. The end-user will get a URL that can be used later on to get the results. However, in our case we are not going to work with time-consuming processes so we do not want to enable this. You can later on overwrite this setting for each endpoint.
{% endhint %}

## **Assignment 2:**

Once you are done creating your API, click the "View Documentation" link and check if everything looks as expected!

{% hint style="info" %}
The Swagger documentation will be the main reference for users. It will show available endpoints, data formats, security rules, and other API details. Right now, there are no endpoints. The next step in our Data Virtualization work is to build and publish the first one.&#x20;

This Swagger documentation is based on the "OpenAPI" standard. When exported, it can used in the "OpenAPICaller" transformer of FME to simply import the API and make working with it easier.
{% endhint %}
