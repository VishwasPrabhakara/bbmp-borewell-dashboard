Bangalore OpenStreetMap Sensor Dashboard

Run start_dashboard.ps1 to open the live dashboard.

The live dashboard starts a local server. When the page opens it triggers the KH downloader, loads the latest UID latitude/longitude file and latest water-level file, and updates the map.

Shapefile:
- bbmpwards.zip is bundled with the dashboard and loads automatically on top of OpenStreetMap.
- You can still upload another .zip shapefile with the override control.
- A shapefile ZIP should contain .shp, .shx, .dbf and preferably .prj.

Sensors:
- The latest downloaded Borewell_Location_Lat_Long CSV loads automatically.
- Clicking a sensor shows UID, ward number, ward name and coordinates.
- Green markers have matching water-level history.
- Grey markers do not have matching water-level history.
- Clicking a ward shows ward number, ward name, sensor count and ward attributes.

Charts:
- Selecting a borewell shows water level below surface over time.
- The water-level Y axis is reversed so 0 is at the top and depth increases downward.
- Time filters: last week, last month, last three months, all time.
- Every available data point in the selected time range is plotted.
- The discharge chart appears only when the downloaded CSV contains a discharge/flow column.

Layout:
- The left borewell list and right chart panel are collapsible.

Included file:
- bbmpwards.zip is the bundled BBMP ward shapefile.
- KH_Data_Downloader contains the downloader and downloaded weekly data.
