---
title: "How I Wrote a Python Script to Parse Google Timeline Data Instead of Just Installing a Mileage App"
slug: "google-timeline-mileage-python-script"
date: 2026-02-15
description: "How I reverse-engineered Google Maps Timeline JSON data with a Python script to extract months of business mileage instead of installing a tracking app."
tags: ["python", "automation", "workflow"]
---

My wife runs a small antique business. She's a vendor at a couple of local shops, which means regular trips to drop off inventory, rearrange displays, and do all the things that keep a booth looking fresh. At tax time, those trips add up to a meaningful mileage deduction — if you've been tracking them.

She had not been tracking them.

So I did what any reasonable developer with 30 years of programming experience would do: I spent an evening reverse-engineering Google Maps Timeline data and writing a Python script to extract the mileage retroactively.

Could we have just installed a mileage tracking app months ago? Absolutely. Would that have been the sensible, responsible, adult thing to do? Without question. But here we are.

## The Good News: Your Phone Already Knows

If you have Google Maps installed with Timeline enabled, your phone has been quietly logging every place you've visited, every route you've driven, and the distance of each trip. It's a little unsettling when you think about it, but extremely convenient when you need to reconstruct six months of business travel.

The data lives on your phone — not in the cloud. Google moved Timeline to on-device-only storage in late 2024, which means there's no web interface anymore. You can't pull this up on your laptop. It also means that if you haven't checked your auto-delete settings, you might only have 90 days of history. Google quietly changed the default retention period to 3 months. Check that setting immediately — before you lose data you might need.

## Exporting the Data

The export option is buried in your phone's Settings app, not in Google Maps itself:

**Settings → Location → Location services → Timeline → Export Timeline data**

This produces a single JSON file. In our case, it was about 79 MB covering data back to 2013. The file contains three types of segments:

**Visits** — places you stopped, identified by a Google Place ID and GPS coordinates, with timestamps. No street addresses, no business names.

**Activities** — travel between visits, with start/end coordinates and the driving distance in meters.

**Timeline paths** — raw GPS breadcrumbs. Less useful for mileage purposes.

The key detail: visits don't include human-readable addresses. They have a Google Place ID (a string like `ChIJhUm_folx5IcRtI-ZrEzFigU`) and a latitude/longitude pair. So you can't just search the file for "123 Main Street."

## Matching Locations by Coordinates

Here's where it gets practical. If you search for a business on Google Maps, the URL contains the GPS coordinates:

```
https://www.google.com/maps/place/Some+Business/@41.9845258,-91.6566567,17z/...
```

Those coordinates after the `@` sign are what you need. The script uses the haversine formula to calculate the distance between each visit's coordinates and your target location. Anything within 100 meters is a match.

## The Script

The Python script is straightforward. You configure a few variables at the top:

- Home coordinates and a friendly label
- Destination coordinates and a friendly label
- The Timeline JSON filename
- A date range to filter by
- A maximum trip distance cap (more on that in a second)

It walks through every segment in the file, finds visits that match the destination coordinates, then checks the adjacent activity segments for the driving distance Google recorded. The output is a CSV with columns for timestamp, origin, destination, and miles — plus a totals row at the bottom and a monthly summary printed to the terminal.

## The Distance Cap

Google's recorded distances aren't always a clean point-A-to-point-B measurement. If you stopped for gas on the way home, or took a detour through a drive-through, that distance gets rolled into the activity segment. We saw a 57.9-mile "return trip" from a store that's 2 miles from the house. We apparently ran some errands that day.

A simple cap variable solves this. Set it to a reasonable maximum for the route (we used 3 miles) and anything above that gets clamped down. It's not forensically precise, but it's defensible and conservative — which is what you want for expense reporting.

## The Results

For the period we checked, the script found 73 individual trip legs across about four months, totaling just over 250 miles. Broken out by month, it gives a clean summary that maps directly to an expense report.

## The Honest Takeaway

If you need mileage tracking going forward, install a mileage app. MileageWise, Everlance, Hurdlr, TripLog — pick one, set it up, forget about it. It will do a better job than reconstructing data after the fact.

But if you're staring down a stack of expense reports that needed to be filed yesterday, and you happen to have Google Timeline enabled on your phone, there's a 79 MB JSON file sitting on your device that might just save your afternoon.

Or you could write a Python script to parse it. Either way.

Want a copy of the script? Ping me on LinkedIn. If there's enough interest maybe I'll put it on GitHub.
