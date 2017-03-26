---
title: notes on gpx GPS Exchange Format
layout:page
---

(wikipedia)[https://en.wikipedia.org/wiki/GPS_Exchange_Format]

- waypoint points without sequential relation

- track order list describes a path with time

- route order list of waypoints 

## Time format

(ISO 8601)[https://en.wikipedia.org/wiki/ISO_8601]


## Track

minimal gpx example

```
<gpx xmlns="http://www.topografix.com/GPX/1/1" xmlns:gpxx="http://www.garmin.com/xmlschemas/GpxExtensions/v3" xmlns:gpxtpx="http://www.garmin.com/xmlschemas/TrackPointExtension/v1" creator="Oregon 400t" version="1.1" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.topografix.com/GPX/1/1 http://www.topografix.com/GPX/1/1/gpx.xsd http://www.garmin.com/xmlschemas/GpxExtensions/v3 http://www.garmin.com/xmlschemas/GpxExtensionsv3.xsd http://www.garmin.com/xmlschemas/TrackPointExtension/v1 http://www.garmin.com/xmlschemas/TrackPointExtensionv1.xsd">
  <trk>
    <name>Example GPX</name>
    <trkseg>
      <trkpt lat="47.644548" lon="-122.326897">
        <time>2009-10-17T18:37:26Z</time>
      </trkpt>
      <trkpt lat="47.644548" lon="-122.426897">
        <time>2009-10-17T18:37:31Z</time>
      </trkpt>
      <trkpt lat="47.744548" lon="-122.426897">
        <time>2009-10-17T18:37:34Z</time>
      </trkpt>
    </trkseg>
  </trk>
</gpx>
```
## Analize

http://utrack.crempa.net/


## Clojure

(data.xml)[https://github.com/clojure/data.xml]
