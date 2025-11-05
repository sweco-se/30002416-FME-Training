---
description: Control Response Size with Limiting Parameters
---

# Exercise 7

In this part, we’ll configure a limit query parameter for the EnvironData Coordination Oﬃce. This parameter controls how many wildfire records are returned in each API response. It helps keep responses manageable and gives users control over the amount of data they get.

We'll set up the limit parameter in FME Form by updating the workspace to read the input value and use it in the SQLite query.

### Update an Endpoint Workspace in FME Form

Open FME Workbench.

When an endpoint configuration is updated in FME Flow, the associated workspace must be redownloaded or manually updated to reflect those changes. There are two ways to proceed, depending on your setup:

* If the WildfireEndpoints.fmw workspace is not already open in FME Workbench: Open FME Workbench, then go to the Data Virtualization menu and download the workspace. This will retrieve the updated version of the workspace based on the latest endpoint configuration in FME Flow. Once downloaded, proceed to the next step.\

* If the workspace is already open or you are using a locally saved copy: If you already have the previous version of the workspace open, click the Publish button in the ribbon menu. The publishing wizard will detect that the workspace is no longer compatible with the updated endpoint configuration. It will prompt you with an Update Reader option. Click Update Reader to synchronize the Data Virtualization reader with the latest configuration from FME Flow. Once updated, you can continue authoring the workspace as needed.

Once updated, expand the GET /wildfires feature type on the Data Virtualization reader type. Notice the addition of two new attributes: query.limit and query.status. In the next steps, the workflow will be updated to handle these additional parameters.

### Update the Input Template

Due to the changes to the endpoint metadata, the Input Template we used in the previous lesson is no longer compatible.

In FME Flow, navigate to the Workspaces tab. From the GET /wildfires endpoint, download the updated input template.

Open the new template in a text editor and review. Notice the new query parameters have been added to the template.

We can use input templates to test the workspace with potential query parameter values.

Replace the placeholder values with test values: replace “\<integer>” with “3” and delete the “status” parameter.

```json
{
"path": "/wildfires",
"method": "GET",
"parameters": {
"limit": ["3"]
}
}
```

This template serves as a substitute for the API request: http://\<FMEFlow>/api/EnvironData/wildfires?limit=3

Since we will author for the “limit” parameter first, this template now represents a request sent with only the limit parameter applied. Save the file as “GETwildfireslimit.json”.

In FME Workbench, open the Navigator window and expand the Data Virtualization Reader. Expand the Parameters and double-click on Sample Data Request File.

### &#x20;Update the Sample Data Request File to use the GETwildfireslimit.json file.

(This file can also be found in “C:\FMEData2025\Resources\DataVirtualization\Endpoint Parameters\Templates\GETwildfireslimit.json”)

Once the template file is configured, select “Run Just This” on the GET /wildfires feature type. When the translation is finished, review the Visual Preview window to find the new attributes: the query parameters and any test values from the input template.

Now that the query parameters are available in the FME workspace as attributes, we can use them to author an endpoint response.

### Use a Query Parameter to Limit the Number of Results

The "limit" query parameter lets users set the maximum number of results they want in the response.

There are different ways to filter data in FME, but the best way is to filter it before it loads into the workspace. You can do this by using built-in reader options like WHERE clauses, SELECT statements, or spatial filters. You can also use database transformers like InlineQuerier, SQLExecutor, or DatabaseJoiner. These methods are faster than using downstream tools like the Tester or Sampler, which only filter data after it's already loaded.

In this example, we will apply the filter directly on the FeatureReader. Open the FeatureReader. In the Constraints section, click the drop-down menu next to Max Features to Read. From Attribute Values, select the query.limit attribute.

Click **OK** to apply.

To test the parameter, run the entire workspace. Once the translation is finished, locate the written data. Open dv\_output.json in a text editor.

This time, only 3 of the 4 rows in the SQLite fires table have been returned in the response. This confirms the limit parameter has been successfully applied in the workspace.

We can also confirm this directly in the workspace. Note that the FeatureReader has only passed 3 features from the fires port.

The FeatureReader’s Max Features to Read parameter can filter by any value greater than 1, even those that are missing. Setting the value to 0 or removing the limit query parameter value returns all records by default.

### Building in Logic for Optional Query Parameters

Now that we've set up the limit parameter, we can focus on time. The time query parameter lets users filter the wilfire results by their recommended time to eat stored in the database. We'll eventually use a WHERE clause in the FeatureReader to apply it.

But first, we need to handle two things. One, time is optional, so users might not include it. A WHERE clause needs a value to work, so we must check if one was provided. Two, if a value is sent, it must match a valid time in the dataset.

The TestFilter transformer is one transformer that is great for this kind of conditional logic.

Add a TestFilter to the workspace. If needed, make space on the canvas and connect it right after the GET /wildfires feature type.

Open the TestFilter to configure.

The first condition will determine if the time parameter is valid. Recall, the valid values for time in our ‘fires’ table are: “active”, “contained”, or “resolved”.

Double-click on the If row to open the Test Conditions dialog. Create the following tests:

| Logic | Left Value   | Operator | Right Value |
| ----- | ------------ | -------- | ----------- |
|       | query.status | =        | active      |
| OR    | query.status | =        | contained   |
| OR    | query.status | =        | resolved    |

The completed Test Clauses table should have a test for all the values. Update the Output Port value to “Status” and click OK.

Back in the main TestFilter parameters, create a new Else If row to configure another condition.

This time, create a test for a request that does not have a value for the status query parameter with the “Attribute is Missing” Operator.Set the Output Port value to “No Status” and click OK.

To handle all other requests, label the last Output Port as Invalid.

Click **OK** to save.

The updated TestFilter now has 3 output ports, one for each scenario. Connect the Status port to the FeatureReader.

All requests that contain a value for the status query parameter will be sent to the FeatureReader.

### Complete the ‘status’ Query Parameter Workflow

If the request doesn’t include a status value, we need to use a second FeatureReader.

Both FeatureReaders will be almost the same, except for the WHERE clause. To save time, just duplicate the first one. Right-click it and choose Duplicate.

FeatureReader\_2 will be added to the canvas. Connect the TestFilter No Status output port to FeatureReader\_2.

Configure the FeatureReader\_2 downstream connections. They will be identical to the original FeatureReader.

* &#x20;Connect the FeatureReader\_2 \<Initiator> output port to the Tester
* Connect the FeatureReader\_2 fires output port to the JSONTemplator WILDFIRES port.

Recall that our input template (GETwildfireslimit.json) does not contain a value for the status query parameter. Therefore, we can use it to test our workspace logic for a “No Time” request.

Rerun the workspace.

The workspace now successfully routes a request when the client does not submit a status query parameter.

&#x20;

&#x20;

&#x20;

&#x20;

&#x20;

&#x20;

&#x20;

&#x20;



