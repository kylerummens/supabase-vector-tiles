# Static and Dynamic Map Vector Tiles with Supabase
Map vector tiles have become essential components for building dynamic and efficient mapping applications that handle large geospatial datasets. Unlike conventional raster images, vector tiles offer a lightweight alternative, comprising scalable data packaged into small, pre-rendered vector data. This approach facilitates quick loading times and seamless zooming capabilities, enhancing the overall user experience.

Let's build a mapping application using technologies provided by the [Supabase](https://supabase.com/) platform.

## The Application
This tutorial will outline the steps to build a ride-sharing application with the following features:
- Display a static map layer representing 
- Dynamically display the current location of drivers
- Update driver locations in real-time
- Display a popup with driver information when selected

## The Stack
For this application we will use:
- [Next.js](https://nextjs.org/) for the front-end
- [MapLibre](https://maplibre.org/) mapping library
- [Supabase Database ](https://supabase.com/database) (Postgres) with the [PostGIS extension](https://postgis.net/)
- [Supabase Storage](https://supabase.com/storage) to store static vector tiles
- [Supabase Edge Functions](https://supabase.com/edge-functions) to create a proxy to serve the static vector tiles
- [Supabase Realtime](https://supabase.com/realtime) to listen to real-time changes from the database and update the map

## Getting Started
The code for this project is available at https://github.com/kylerummens/supabase-vector-tiles

You will need [Docker](https://www.docker.com/) installed on your machine to run the application.

## Render Static Vector Tiles From 
Note: This step is here just to demonstrate how you could render static vector tiles for a map. It is not necessary to host your own street map

## Prepare Database to Serve Dynamic Vector Tiles
In order to dynamically serve vector tiles from Supabase, we need to get our database prepped.

First, ensure that you have the PostGIS extension enabled. You can use [this guide](https://supabase.com/docs/guides/database/extensions/postgis) for instructions on enabling the extension.

Next, let's create the tables we need. The real-time data for our ride-sharing application will be the drivers and their current locations:

```sql
create table drivers (
  id uuid primary key,
  name text not null,
  vehicle text not null,
  available boolean not null default false,
  location geometry(point, 4326)
);

create index drivers_location_idx on drivers using gist (location);
```

Two important things to note here: we are creating a column called `location` that is of type `geometry`, then creating a geospatial index using the GIST index method. Storing the driver locations as a geospatial type will allow us to utilize some more PostGIS utilities later on to render our tiles.

## Serving Dynamic Vector Tiles
