---
description: Customize Response Data with Filtering Parameters.
---

# Exercise 8

In this part, we help the EnvironData Coordination Oﬃce add a second query parameter, status, to filter wildfire records by their status (like active, contained, or resolved). This lets users request only the data that matters to them.

We’ll also add error handling. If a user sends an invalid time, the workspace will catch it and return a 400 Bad Request.

This gives clear feedback when input doesn’t match what’s expected.

These updates make the EnvironData API more reliable, flexible, and user-friendly.

### Update the Input Template

To author the workflow for the status query parameter, we will update the input template with a test value. Open the original request\_template.json in a text editor. (If you no longer have it, then redownload it from the Workspaces tab in FME Flow).

This time, remove the “limit” query parameter and update the “status” value to “active”:

```json
{
"path": "/wildfires",
"method": "GET",
"parameters": {
"status": ["active"]
}
}
```

Save the template file as GETwildfiresstatus.json.

(A preconfigured file can also be found in C:\FMEData2025\Resources\DataVirtualization\Endpoint Parameters\Templates\GETwildfiresstatus.json)

In FME Workbench, update the Sample Data Request File to GETwildfiresstatus.json.

Click Run Just This on the GET /wildfires reader feature type in order to refresh the parameter values.

Review the Visual Preview window to confirm the attribute values have been updated. Now the query.limit value is missing and the query.status value is active.

### Use a Query Parameter to Filter Results by Attribute

We’ll use the query.status attribute to filter the SQLite “fires” table.

Open the original FeatureReader transformer (connected to the “Status” port). Within the Constraints group, find the WHERE Clause. Enter a statement that is compatible with SQLite:

&#x20;`"time" = '@Value(query.status)'`

Click **OK** to save.

On the FeatureReader, click Run To This. Inspect the cache on the pastries port. Only 2 features are returned, each with a “active” value for its status attribute.

This confirms that our WHERE Clause has successfully been applied.

Similarly, rerunning the entire workspace and inspecting the dv\_output.json file confirms that the response body contains only the filtered results.

### Testing with Data Entry Errors

It’s good practice to test with as many endpoint parameters as possible to build strong, reliable workspaces. This not only helps ensure accurate status codes but also gives a chance to handle common input errors or data mismatches between systems.

To do this, we will purposely test with an invalid value.

Again, open the original request\_template.json in a text editor. Replace the time value with “ACTIVE” and set the limit value to “3”.

```json
{
"path": "/wildfires",
"method": "GET",
"parameters": {
"limit": ["3"],
"status": ["ACTIVE"]
}
}
```

Save as ““GETwildfiresstatuslimit.json”.

This template serves as a substitute for the request: http://\<FME Flow>/api/EnvironData/wildfires?limit=2\&status=ACTIVE

Notice that the status value doesn't match our data source, as it uses uppercase instead of lowercase. Database queries, like a WHERE Clause, are often case sensitive.

**Save** the file.

In FME Workbench, update the Sample Data Request File value with the updated template, GETwildfiresstatuslimit.json.

(This file can also be found in C:\FMEData2025\Resources\DataVirtualization\Endpoint Parameters\Templates\GETwildfiresstatuslimit.json)

Run the workspace with the new values. The workspace doesn't complete because the uppercase status value is routed to the “Invalid” port by the TestFilter.

Formatting issues can come from user mistakes or differences between systems. For example, one app might use uppercase for status values, while another uses lowercase. FME can fix this by adjusting the data before querying the SQLite database, making it easier to connect systems that don’t match exactly.

### Build in Solutions for Expected Errors

To handle mismatched cases, add a StringCaseChanger to the canvas. Making room if needed, connect it between the GET /wildfires feature type and the TestFilter.

Open the StringCaseChanger to configure the parameters.

Use the ellipsis to open Selected Attributes. Expand ‘query’ to select ‘status’.

Click **OK**. Beside Case Change, select “**lowercase**”.

The updated workflow can now process query parameter values sent in an incorrect case. This prevents clients from receiving inaccurate error responses due to incorrect data entry.

Rerun the entire workspace to verify.

### Create an Invalid Query Parameter Response

So far, the workspace handles requests with no query parameters, valid ones, and small input errors. But if a client sends an invalid value, the API should respond with a clear error.

In this final step, we’ll set up the workspace to catch invalid query values and return a 400 Bad Request. We already set up this status code in FME Flow. Sending a 400 lets the client know their input isn’t valid, which improves error handling and protects data quality.

Add another AttributeCreator to the workspace. Connect the new AttributeCreator\_3 to the TestFilter Invalid output port.

Open the AttributeCreator\_3 to configure the response attributes.

| Ouput Attribute              | Value                                         |
| ---------------------------- | --------------------------------------------- |
| response.status\_code        | 400                                           |
| response.body.content        | {“ErrorMessage”:”Invalid ‘status’ parameter”} |
| response.body\_content\_type | application/json                              |

Review the parameters.

Recall that, for the previous '200' status code response, we used a JSONFormatter to create the response.body.content.

This time, we've manually set up the response.body.content attribute directly in the AttributeCreator. This approach is best suited for shorter responses that do not require dynamic formatting, such as responses without arrays or nested objects. It offers a straightforward alternative when the response structure is simple and static.

Click **OK** to close.

Finally, connect the AttributeCreator\_3 Output port to the http\_response writer feature type to complete the workflow.

To test the invalid response, update the GETwildfiresstatuslimit.json template's status value to “Closed”:

```json
}
"path": "/wildfires",
"method": "GET",
"parameters": {
"limit": ["3"],
"status": ["closed"]
}
}
```

**Save**.

(This file can also be found in C:\FMEData2025\Resources\DataVirtualization\Endpoint Parameters\Templates\GETwildfiresstatusinvalid.json)

In FME Workbench, select "Rerun Entire Workspace"

View the dv\_output.json to confirm the expected response

**Save** the workspace.

### Republish to FME Flow

Publish the workspace to FME Flow to apply the endpoint workspace updates.

Follow the steps as before, this time ensuring that files and web connections are not selected for upload. Once published, open FME Flow and navigate to the Workspaces tab. Once again, the GET /wildfires endpoint Workspace Status is Assigned.

### Test Request in Documentation

Use the Swagger documentation or another API client to make a request to the endpoint that includes parameters.

In swagger, verify that the URL begins with "http://fmetraining/...", not [http://localhost/...](http://localhost/...)

In the GET /wildfires endpoint, notice the query parameters that we created are now available.

Click **Try it Out** to enter the query parameters value:

* &#x20;limit: 2
* time: RESOLVED

For example, test the results for the request: http://\<FME Flow>/api/EnvironData/wildfires?limit=2\&status=RESOLVED

Click **Execute**

Review the response to confirm the requested data.

We can also test our error messages. Try entering an invalid query parameter value for status, like closed. The “400” code and error message is returned.

&#x20;
