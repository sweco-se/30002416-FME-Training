---
description: Endpoint Parameters
---

# Exercise 6

Data Virtualization supports endpoint parameters, which allow users to refine API requests and customize responses. These parameters help specify which resources to access (path parameters), how to filter or modify the results (query parameters), and include additional instructions or metadata (header parameters), such as authentication details.

Parameters are first defined when creating the endpoint metadata in FME Flow. Then, inside the Data Virtualization workspace, you can use readers, writers, and transformers to apply the parameters.

These components handle the filtering, transformation, and routing based on the values sent in the request.

### &#x20;Endpoint Parameters

&#x20;Data Virtualization supports all major types of HTTP parameters:

* &#x20;Path parameters modify the URL path to identify a specific resource (e.g. /users/{userId}).
* Query parameters are appended to the URL to filter, sort, or control response content (e.g. /search?query=keyword).
* Header parameters provide additional instructions, such as authentication tokens or metadata (e.g. Authorization: Bearer {token}).

Most parameters can be optional, giving users the flexibility to tailor API responses to their specific needs while improving performance and usability.

### Update an Endpoint with Query Parameters in FME Flow

The EnvironData Coordination Oﬃce defines the limit and status query parameters in FME Flow. This step sets up how the API will accept input from users, including the parameter names, data types, and where they appear in the HTTP request. These definitions prepare the endpoint for dynamic filtering and controlled result sets in later stages of the workflow.

### Updating a Data Virtualization Endpoint

Once a data virtualization workspace is published, any changes to its endpoint metadata in FME Flow will set the workspace status to “Needs Updating.” This status signals that you have to redownload the workspace into FME Workbench. The metadata updates will reflect in the reader, writer, and templates. From there, it’s up to the author to update the workflow to support the new metadata and then republish the workspace to FME Flow.

### Add Query Parameters to an Existing Endpoint

In FME Flow, open the Data Virtualization EnvironData API and navigate to the Endpoints tab. Select the GET /wildfires endpoint. Navigate to the Parameters tab.

Next to Query Parameters, click Add. Add and complete two query parameters for ‘limit’ and ‘status’. Leave these parameters as not required, the end user can choose to include them in the request as needed:

| Name   | Type    | Description                                                                             | Required |
| ------ | ------- | --------------------------------------------------------------------------------------- | -------- |
| limit  | Integer | Limit the number of returned results                                                    | no       |
| status | string  | <p>Filter wildfire events by status (e.g., "active", "contained",</p><p>"resolved")</p> | no       |

### Create a New Status Code in FME Flow

Introducing parameters to the request also introduces potential failure points. To handle cases where users provide invalid parameter values, we will implement an additional status code to ensure clear and appropriate responses.

Navigate to the Response tab. Click Add Status Code Configure a "400 - Bad Request" status code, which will apply when a user submits an invalid value for the “status” parameter.

| Name             | Value                   |
| ---------------- | ----------------------- |
| HTTP Status Code | 400 - Bad Request       |
| Description      | Invalid parameter value |
| Content Type     | Application/json        |
| Input Type       | Create Properties       |

Instead of using predefined schemas, responses can also be defined by creating custom properties. This approach is best suited for endpoints with simple or unique response structures that do not require a shared schema. Properties function the same way as schemas in terms of how responses are structured and returned. They will appear in your API documentation as examples of expected responses, providing clarity for end users without the need for a separate, reusable schema definition.

Click the Create button next to Properties to define a new property.

| Name          | Type   |
| ------------- | ------ |
| Error Message | String |

Review the completed parameters and Save.

Updating an endpoint configuration in FME Flow automatically triggers a warning message. This simply indicates that the associated workspace must be updated to reflect the new configuration changes.

Click **Save** to continue.

### Configure an Updated Data Virtualization Workspace

&#x20;After updating an endpoint configuration in FME Flow, the endpoint workspace must also be updated and republished for the changes to take effect. Until this is done, the configuration updates remain incomplete in the Web UI.

To verify, go to the Workspaces tab and locate the GET /wildfires endpoint. The Workspace Status will have changed from "Assigned" (its previous status) to "Needs Updating", indicating that the workspace requires an update before the changes are applied. In the next exercise, we will update the workspace.

&#x20;

