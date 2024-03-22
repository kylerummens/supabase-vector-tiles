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

## Serving Dynamic Vector Tiles
