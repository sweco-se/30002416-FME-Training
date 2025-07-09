---
description: Web based weather
---

# Exercise 6

You just bought a boat and want to take it sailing this weekend. In order to help you decide where to go, you want to make use of freely available online data and FME (of course). The goal is to present your sailing buddies with a nice map showing the areas where you are most likely to find good weather for your trip.

There is a polygon dataset of all sea areas along the coast of Sweden available for download here: [https://opendata-download.smhi.se/svar/Havsomraden\_2016.zip](https://opendata-download.smhi.se/svar/Havsomraden_2016.zip)

Your boat is in Göteborg, so you can’t go too far from there. A bounding box of 250000, 6350000, 350000, 6450000 will give you a reasonable selection.

You could download the dataset, unzip it, open it with FME, create a bounding box geometry and clip the dataset. But you’re in the advanced course now, and you know all of this can be done right in the reader. (If there is any trouble with the link, there is a backup copy of the data in the course data catalog).

You want to make sure you go somewhere the temperature is nice and warm. You have been told there is an open API you can call at: [https://opendata-download-metfcst.smhi.se/api/category/pmp3g/version/2/geotype/point/lon/\<LON>/lat/\<LAT>/data.json](https://opendata-download-metfcst.smhi.se/api/category/pmp3g/version/2/geotype/point/lon/%3CLON%3E/lat/%3CLAT%3E/data.json)

This will give you the weather forecast for a certain point as a JSON file.

You want to create a nice map of the top three warmest areas to go and save this as a pdf. If you have access to a good background map service, please use it. You might for instance have an account to use Lantmäteriets WMTS. Otherwise there is a WMS version of OpenStreetMap at [https://ows.terrestris.de/osm/service?](https://ows.terrestris.de/osm/service?) which works without an account.

Make a pdf of your map and upload it to google drive so your sailing buddies can see it. (Use your own drive if you want, or ask the instructor for details on one.)

<details>

<summary>Tips:</summary>

* Try to figure out what geometry type and coordinate system is required for the API call, and then how to get there from you input data. You will need to _replace_ each polygon with its _center point_, and _reproject_ it.

- The all-star of this workspace will be the HTTPCaller transformer. In order not to overwhelm it while you’re trying things out, consider limiting the number of features it receives. The Sampler is your friend! Remember to remove it before you’re done.

* FME is very generous with the decimal places on coordinates. The API documentation does not actually mention this, but we’ve found 6 decimals to be a good number for the API call.

- FME has a lot of tools to handle JSON, but it can be a bit tricky if you’ve never done it before. As it’s not really supposed to be the focal point of this exercise, there is a workspace under: \
  C:\FMEData2025\Workspaces\FMEFormAdvanced\Exercise6\_start.fmw. This contains some useful JSON wrangling transformers. If you feel confident with JSON, or up for a challenge, please feel free to start with a blank canvas.

* There is a user parameter called DATE in the starting workspace which needs to be set to something that is actually in the forecast, like next Saturday.

- A Sorter and a Sampler will help you filter out the areas with the highest forecast temperature.

* If you want, you can stop there. If you want to include a background map, a Reprojector, BoundingBoxAccumulator and Bufferer will help you get a reasonable area to send to a FeatureReader. Make sure to look up which coordinate system your map service requires.
* You will note there is no option to write immediately to Google Drive. You need to write to a temporary file, using for instance a pdf FeatureWriter, and then upload the file using a connector transformer.

</details>

<details>

<summary>Bonus:</summary>

See if you can extract two more weather parameter from the reply (they are described here: [http://opendata.smhi.se/apidocs/metfcst/parameters.html](http://opendata.smhi.se/apidocs/metfcst/parameters.html)), and add to your dataset. Use the Google Sheets writer to write your table directly to an online spreadsheet.

</details>

{% hint style="info" %}
From this exercise, you’ve hopefully learnt:

* How to read from and write to resources online
* How to interact with APIs using the HTTP Caller
* How to handle JSON data in FME
{% endhint %}
