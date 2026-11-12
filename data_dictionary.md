# Data Dictionary

This file explains the columns of the CSV files in this dataset. The database is designed as a set of linked tables to analyze ice avalanche dynamics. Events are linked to glaciers via `glacier_id`.

General conventions:
* Coordinates: Swiss coordinate system CH1903+/LV95 (EPSG:2056), in meters.
* Dates: ISO 8601, YYYY-MM-DD.
* Times: HH:MM, always in UTC (not local time).
* Empty cell = unknown / not available.

## glaciers.csv (Metadata)
One row per glacier.
* **glacier_id** (text): Unique identifier of the glacier in this database. Format: country code + 3 letters (e.g. CH-TRI).
* **sgi_id** (text): Identifier of the glacier in the Swiss Glacier Inventory (SGI), used to link to GLAMOS data (e.g. A54m-03).
* **name** (text): Common name of the glacier, with the mountain in brackets if needed.
* **canton** (text): Swiss canton where the glacier is located.
* **x_LV95** (number, m): Easting of a reference point on the glacier, LV95.
* **y_LV95** (number, m): Northing of a reference point on the glacier, LV95.
* **elevation_min_m** (integer, m a.s.l.): Minimum elevation of the glacier.
* **elevation_max_m** (integer, m a.s.l.): Maximum elevation of the glacier.
* **years_covered** (text): Period covered by the event catalog for this glacier (e.g. 2018-2025).
* **corr_weather_stat** (text): Corresponding weather station, used to link weather data to events.

## events.csv (Ice Avalanche Catalog)
One row per ice avalanche event. One file per glacier.
* **event_id** (integer): Unique number of the event (1, 2, 3, ...). Never reused.
* **glacier_id** (text): Glacier where the event occurred; refers to `glacier_id` in glaciers.csv.
* **sector** (text): Sector of the glacier where the event released. Sector definitions per glacier: to be added.
* **date_min** (date, YYYY-MM-DD): Earliest possible date of the event (last image before the event).
* **date_max** (date, YYYY-MM-DD): Latest possible date of the event (first image after the event). Same as date_min if the date is known exactly.
* **time_min** (time, HH:MM, UTC): Earliest possible time of the event, if captured by monitoring cameras.
* **time_max** (time, HH:MM, UTC): Latest possible time of the event, if captured by monitoring cameras.
* **magnitude_vol_m3** (number, m³): Estimated volume of the ice avalanche.
* **notes** (text): General observations, e.g. geometry of the release area before the event (wedge / slab).
* **trigger_type** (text): Suspected mechanism controlling the release.
* **image_reference** (text): File name of the camera image capturing the event.
* **data_source** (text): Origin of the cataloged event (e.g. monitoring camera, Geoformer preliminary catalog, published literature).
