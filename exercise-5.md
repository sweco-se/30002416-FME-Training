---
description: Author an Endpoint Response in FME Form
---

# Exercise 5

In this part, you'll continue building the GET /wildfires endpoint by defining its response logic in FME Form. After downloading the WildfireEndpoints.fmw workspace from FME Flow, you'll customize it to control how the endpoint processes and returns data.

&#x20;

This includes using the Data Virtualization reader and writer, querying the internal SQLite database, and adding transformers to format the data to match the expected schema. These steps ensure the endpoint returns accurate, real-time wildfire data and connects the API to the live data source.

#### &#x20;Understanding Input Templates

&#x20;This part uses Input Templates to build and test the Data Virtualization workspace in FME Workbench. Input Templates are automatically generated JSON files that define the expected structure of both the request and response for a specific endpoint. These templates outline the key elements of an API request, including the HTTP method, request path, headers, and parameters.

&#x20;Example template structure:

```json
{
"path": "/myendpoint/{pathparameter}",
"pathParameters": {"mypathparameter": "<string>"},
"headers": {"myheaderparameter": ["<string>"]},
"method": "GET",
"parameters": {"myqueryparameter": ["<string>"]}
}

```

These templates can be used with the Data Virtualization reader to simulate real API calls. By filling in the placeholders with sample values, authors can test how the workspace behaves with different inputs without needing to send actual requests to the API. Input Templates are essential for:

&#x20;

* Testing how request parameters are handled
* Validating response formatting
* Debugging workspace logic before deployment

### &#x20;Open a Data Virtualization Workspace in FME Workbench

Open FME Workbench. On the Start tab, click Data Virtualization. (Data Virtualization can also be accessed via File > "Open from FME Flow Data Virtualization")

The FME Workbench Data Virtualization wizard allows you to download endpoint workspaces generated in FME Flow for editing and updating in FME Workbench. To start, make sure your "Training FME Flow" connection is selected.

Once connected to FME Flow, select the WildfireEndpoints.fmw from the Environmental Impact and Response API then click Open.

&#x20;A warning dialog will popup stating that the workspace must be republished to FME Flow for the endpoints to be updated. Click **OK** to close the dialog.

&#x20;The WildfireEndpoints.fmw workspace will open.

All endpoint workspaces in FME Form are automatically generated with a Data Virtualization reader and writer, which represents the API request and response, respectively.

The Data Virtualization reader appears on the canvas as one or more feature types, depending on the number of endpoints selected in FME Flow. Since only one endpoint was selected, the canvas contains a single feature type: GET /wildfires. Expanding this reveals key request details such as the endpoint path (request.path) and any defined parameters.

In contrast, the Data Virtualization writer always appears as a single feature type: **http\_response**.

Its schema is consistent across all Data Virtualization workspaces and includes the standard elements of an API response: status code, headers, and a response body (NOTE: You may need to scroll the workspace to the right to find the Writer Feature Types bookmark, depending on your screen size. If you do have to scroll, click and drag the Writer Feature Types bookmark to the left so it can be seen at the same time as the Reader Feature Type bookmark).

The template workspace is just a shell, it’s up to the author to add the necessary transformers that handle incoming API requests and construct appropriate responses. The primary goal is to define workspace logic that:

* Handles request parameters sent by the client
* Filters, transforms, or structures data according to the defined response schema
* Directs the output to the correct status code, based on whether the request was successful or encountered issues

By building this logic into the workspace, you ensure that every API request returns clear, validated, and properly structured responses that are aligned with the design and expectations of your Data Virtualization API.

### Download Endpoint Template

To build an FME workspace, it's easier if you can work with real data. But since Data Virtualization workspaces use live API requests as their input, and you can't trigger those directly in FME Workbench, we need another way to test.

&#x20;FME Flow gives you input templates that act like real API requests. You can use these to test your workspace locally with sample data.

Open or return to FME Flow in a browser. Then navigate to the Data Virtualization Environmental

Impact and Response API. In the Workspaces tab, for the GET /wildfires endpoint, click the ellipsis under Actions and select Download Input Template.

The request\_template.json file will automatically be saved to your local Downloads folder. In the File Explorer window, locate the request\_template.json file and open it in a text editor, like Notepad++.

The JSON text represents how FME Flow receives and processes API requests. It will be used to simulate API input during development in FME Workbench.

&#x20;This template serves as a substitute for the API request: http://\<FME Flow>/api/EnvironData/wildfires

&#x20;Re-save the template as “GETWildfires.json” and close.

&#x20;(This file can also be found in "C:\FMEData2025\Resources\DataVirtualization\Make a Workspace Endpoint\Templates\ GETWildfires.json")

### &#x20;Read an Input Template

Back in FME Workbench, single-click the GET /wildfires feature type to open the mini menu and click the edit button.

In the Edit ‘spec \[DATAVIRTUALIZATION]’ dialog, expand the Sample Data section. For Sample Data Request File, use the file explorer to select the downloaded input template.

Click **OK**. Before proceeding, ensure that Feature Caching is enabled by clicking on the drop-down arrow next to the Run button on the toolbar.

Open the mini menu again on the GET /wildfires feature type, then click **Run Just This**.

The Translation Parameter Values dialog will appear and prompt you for a Destination Data Virtualization Folder.

Set the destination folder to “C:\FMEData2025\Resources\DataVirtualization\Make a Workspace Endpoint\Responses”.

Select the new Responses folder.

Select Run and inspect the cached data. For this simple GET request with no parameters, only

the endpoint path will be present (“request.path”).

### &#x20;Connect to a Data Source

In an endpoint workspace, the Data Virtualization Reader only represents the incoming API request. It doesn’t connect to the real data. To return actual results, we need to bring in the real data sources.

The next step is to build a workflow that reads from the SQLite database and formats the data to match the WildfireResponse schema. This makes sure the response is accurate, structured, and ready for the API.

To do this, we use the FeatureReader transformer. It lets the workspace access data during translation, based on the request input. This is important for API workflows, where the Data Virtualization Reader stands in for a regular reader. The FeatureReader uses request parameters to query the database at runtime and return customized results.

Add a FeatureReader transformer to the canvas and connect it to the GET /wildfires reader feature type. In the parameters, select SQLite as the Format. Select the events.sqlite file as the Dataset (C:\FMEData2025\Data\Wildfires\events.sqlite).

In Feature Types to Read, click on the ellipsis, then select the fires table.

Close the FeatureReader and Use Run to This on the FeatureReader’s mini menu. Inspect the fires output port. The SQLite fires data table is returned.

### Review the Output Template

Now that the data source is in the workspace, we can build the workflow that creates the endpoint response. This means using transformers to format the wildfire data to match the schema set in FME Flow. That includes the right status codes, response body, and headers. This step makes sure the output meets the endpoint’s requirements and shows the data correctly to users.

To see what the response should look like, check the attributes in the Data Virtualization writer. The writer shows what attributes we need to create.

Expand the Data Virtualization writer to view the attributes that make up the API response data. Not all writer attributes are required, but there are a few that we will almost always create in the workspace:

* response.status\_code will have the value of one of the endpoint’s status codes.
* response.body.content will contain the requested data in the format of the response schema.
* response.body.content\_type will contain the response data format, typically application/json.

We can also use an Output Template to understand how the response data should be formatted.

Back in FME Flow, navigate back to the Workspace Endpoints tab. This time, download the Output Template for GET /wildfires. It’ll automatically download to the Downloads folder.

Locate the result\_template.json in the Downloads folder and open it in a text editor.

The Output Template shows what the endpoint's response looks like in JSON format. Note the parameters and status codes that we configured in FME Flow.

* For the 200 status code, the 'body.content' values (severity, name, location, id) match the WildfireResponse schema.
* For the 204 status code, no properties or schema were assigned.       &#x20;

As we build the Data Virtualization workspace for the GET /wildfires endpoint, our task is to set up these two status codes correctly and format the fires data into the JSON schema from the Output Template. This ensures our responses are properly structured and formatted to align with our API's design.

Return to FME Workbench.

### Test for Expected Data

FME must find data in the SQLite table in order to produce a 200 response for a GET /wildfires request. To ensure this, we need to verify that the FeatureReader returns data as expected. Add a Tester to the canvas and connect it to the FeatureReader’s \<initiator> port. Open the Tester and add one Test Clause:

| Left Value      | Operator | Right Value |
| --------------- | -------- | ----------- |
| matched records | !=       | 0           |

This test clause ensures that a feature will pass if the FeatureReader returns 1 or more records.

Run the workspace to the Tester to confirm the data exits the Passed port.

The Tester confirms that the endpoint request has successfully found data in the fires table and the workflow can proceed to the next steps of the 200 response workflow. In the next steps, we will format the ‘fires’ data into the expected response schema, Pastry Schema.

### Format Data into Schema

Recall, the API documentation for a 200 status code returns the WildfireResponse schema. Therefore, we need to transform the SQLite "fire" data to match this expected schema.

The JSONTemplater is a versatile transformer capable of converting attributes and values into JSON format. This transformer is particularly effective for structuring endpoint response schemas within the workspace, making it an essential resource for formatting data precisely according to schemas.

Add a JSONTemplater to the canvas. Connect the Tester’s Passed port to the JSONTemplater’s Root port.

In the JSONTemplater parameters, enable the Sub Template. Use the + button to insert a row. In the new row, replace the default Port value with WILDFIRES.

Click the ellipsis on the WILDFIRES port to open the Template text editor.

In the PASTRIES Template Expression dialog box, write or copy the WildfireResponse schema:

```json
{
"severity": "<string>",
"cause": "<string>",
"location": "<string>",
"id": "<string>",
"confirmed": "<boolean>",
"status": "<string>"
}
```

Note that this schema can also be copied from the Swagger documentation or the output template file (response\_template.json).

Paste the content into the Template Expression text editor.

This template will not work as is. In the next steps, we finish the sub template by updating the placeholder values (e.g. “\<string>”). For now, click OK to close the text editor.

Under Root Template, use the ellipsis to open the text editor for Template.

In the editor, build or paste the following:

```json
[
fme:process-features("WILDFIRES”)
]
```

This template format will format the templated WILDFIRES data in a JSON array. Click OK to close the ROOT Template Expression editor.

Update the Output Attribute Name to response.body.content. Recall, response.body.content is one of the expected response attributes on the Data Virtualization writer.

Click OK to close the JSONTemplater.

The newly created PASTRIES input port will appear on the JSONTemplater.

Connect the FeatureReader "fires" output port to the JSONTemplater "WILDFIRES" port.

Once connected, reopen the JSONTemplater to finish the WILDFIRES sub template configuration.

Open the WILDFIRES sub template by clicking on the ellipsis.

Replace the placeholder text (e.g. “\<string>”) with the corresponding FME Feature Attributes.

FME Feature Attributes are located on the left-hand menu and can be double-clicked or dragged into the text body. When creating a JSON template, do not use any quotation marks or other formatting characters, as FME applies them automatically.

For example, replace the value for “name” with fme:get-attribute(“name”). Repeat the process for the entire schema. The final Template Expression should have FME Feature Attributes for all the schema values.

```json
{
"severity": fme:get-attribute("severity"),
"cause": fme:get-attribute("cause"),
"location": fme:get-attribute("location"),
"id": fme:get-attribute("fire_id"),
"confirmed": fme:get-attribute("confirmed"),
"status": fme:get-attribute("status")
}
```

Review the completed template.

Note that the schema defined for the endpoint response does not exactly match the schema of the SQLite fires table. This is common in API design. Sometimes, attribute names need to be adjusted to improve clarity for end users or to meet the formatting requirements of another system or application.

Click OK twice to close the JSONTemplater.

Run the workspace to the JSONTemplater, then inspect the results.

Double-click the response.body.content attribute in Visual Preview to view the formatted response.

The JSON is not pretty-printed by default, click the ABCXYZ button in the bottom left corner and select JSON.

The new response.body.content attribute contains a list of wildfires, formatted to the Pastry Schema schema and populated with the SQLite fires data.

### Create Status Code and Response Body Attribute

In addition to the response.body.content, the Data Virtualization writer expects values for the status code (response.status\_code) and content type (response.body.content\_type). To finish the workflow for the ‘200’ response, we must create those attributes.

Add an AttributeCreator to the canvas and connect it to the JSONTemplater. Open it up to create two response attributes.

The first attribute will produce the status code:

| Output Attribute      | Value |
| --------------------- | ----- |
| Response.status\_code | 200   |

The second attribute will define the content type:

| Output Attribute            | Value            |
| --------------------------- | ---------------- |
| Response.body.content\_type | application/json |

<details>

<summary> Tips</summary>

When building endpoint workspaces, you’ll often create the same attributes. To save time, consider creating a Parameter Preset. This lets you quickly reuse your AttributeCreator settings in future workspaces.

</details>

### Connect Data Virtualization Writer and Run Workspace

Connect the Output port of the AttributeCreator to the Data Virtualization writer feature type. Notice that some, but not all, of the attributes are highlighted in green. These green attributes, such as response.status\_code, response.body.content, and response.body.content\_type, are the ones we created in the workspace. Remember, not every response requires all attributes to be filled.

Run the workspace.

Upon completion, we can inspect the full response that will be created in FME Flow. Navigate to the folder that we created for the Data Virtualization writer (e.g. “Responses”). Or, click on the Open Containing Folder button in the writer feature type mini menu.

Inside the folder, open the dv\_output.json file in a text editor. Inspect the result.

This file includes the full endpoint response, including the status and the body, in JSON format. It's formatted just like the output template we looked at before, which confirms that we've successfully set up the workflow for the ‘200’ response code.

It's important to remember that while this file contains everything FME needs to generate an endpoint response, it is not what the end user will see. Since clients interact with the endpoint via an API client, they’ll receive this same information as an HTTP response rather than a text file. Later in the lesson, we will demonstrate how to make this request to this API endpoint.

### Author for Alternate Status Code

Data Virtualization authors are responsible for implementing the workspace logic that handles all status codes defined in the endpoint configuration. In FME Flow, we previously defined both a 200 – OK and a 204 – No Content status code for the GET /wildfires endpoint.

The 204 response is intended to indicate: “Could not find the requested resource.”

To complete the endpoint workspace, we need to build logic that covers scenarios where no data is returned from the database query.

In the current workspace, the Tester transformer is used to evaluate whether the FeatureReader successfully retrieves any records from the SQLite fires table.

* If records are found, the data flows to the JSONTemplater, which formats the response for a 200 – OK status.
* If no records are found, we must direct the workflow to generate a 204 – No Content response instead.

This conditional branching ensures the API returns appropriate feedback based on the presence or absence of data, maintaining accuracy and consistency in how responses are handled.

&#x20;To do this, add another AttributeCreator to the workspace and connect it to the Tester’s "Failed" port.

&#x20;Open the AttributeCreator\_2 parameters to set up a new status code and response, using the settings from the FME Flow endpoint configuration.

| Output Attribute      | Value |
| --------------------- | ----- |
| Response.status\_code | 204   |

Recall that for the '200' response, we configured a schema for the response. However, the ‘204’ response was not configured with a schema, therefore, we do not have to create a response body.

&#x20;Close and connect the AttributeCreator\_2 Output port to the http\_response writer feature type.

### Publish the Data Virtualization Workspace to FME Flow

To complete the process of authoring a Data Virtualization Endpoint, the workspace must be published to FME Flow.

But before publishing, save a local copy of the workspace to your machine. In FME Workbench, select File > Save As. Locate the tutorial folder, "C:\FMEData2025\Resources\Data Virtualization".

Create a new folder called "WorkingCopies". Save the Fetch WildfireEndpoints.fmw file.

From the FME Workbench ribbon menu, select Publish. The publishing wizard for Data Virtualization workspaces is slightly different compared to standard FME workspaces.

Verify the default API and the workspace name. Disable Upload data files, then click Next.

The next dialog allows us to select any connection dependencies. For the first publish, keep the "Training FME Flow" Web Connection as selected.

Click **Publish** to finish.

### Confirm Workspace Status in FME Flow

Open or return to FME Flow. Navigate to the Workspaces tab in the Data Virtualization Environmental Impact and Response API.

Refresh if already open.

The Workspace Status for GET /wildfires has been updated to "Assigned", with a green check mark. This confirms that a workspace has been published for this endpoint and no edits have been made to the endpoint configuration since last published.

It does not, however, confirm that the endpoint workspace is successful. To confirm the endpoint returns an expected response, we can test the request from an API client.

### Test the Endpoint Request in Swagger Documentation

The endpoint can be tested from any API client that can reach FME Flow (Postman, HTTPCaller, etc.), but the easiest method for a GET request is from the Swagger documentation.

If not already open, open the Swagger Documentation. Again, confirm that the URL is "HTTP://fmetraining/" .... not "HTTP://localhost/..." .

Find the GET /wildfires endpoint and click to expand. Click Try it Out, then click Execute. You may be prompted for your username and password.

Below, the response will appear. If successful, it will include a ‘200’ response and an array of pastries.

The GET /wildfires endpoint is now complete.
