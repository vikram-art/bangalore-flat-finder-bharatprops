# Editing the Flat Finder data

The site reads four files. Edit them, upload them to GitHub, and the site updates.

- **projects.csv**: one row per project.
- **units.csv**: one row per unit type (2 BHK, 3 BHK...) of a project.
- **places.csv**: tech parks, malls, railway stations and the airport.
- **metro_stations.csv**: every metro stop.

Open them in Google Sheets or Excel. When saving from Excel, choose **CSV UTF-8 (Comma delimited)**.

## Rules that matter

- Do not rename or delete the header row. You can reorder columns or leave cells blank.
- A project needs four cells at minimum: `name`, `latitude`, `longitude`, `home_type`. A row missing any of these is skipped.
- Prices are in lakh: 95 means ₹95 L, 250 means ₹2.5 Cr.
- Lists use ` | ` between items, for example `2 | 3 | 4`.
- For a new project, leave `id` blank. In units.csv, also leave `project_id` blank and type the exact project name in `project_name`.

## projects.csv columns

| Column | What to type |
|---|---|
| id | Leave as is. Blank for new projects. |
| name | Project name |
| builder_full, builder_short | "Brigade Group", "Brigade". The short one is used by the builder filter. |
| locality, corridor | Corridor must be one of: Whitefield / Sarjapur / KR Puram & Old Madras Rd / Bellandur, Varthur & ORR |
| latitude, longitude | From Google Maps: right-click the site, copy the two numbers |
| pin_code | Optional |
| home_type | apartment, villa or plot |
| stage | new launch, under construction or ready to move. Blank = worked out from possession_year (2029+ new launch, 2027-28 under construction, else ready). |
| sold_out | yes or no |
| price_from_lakh, price_to_lakh | Numbers in lakh |
| bhk | `2 | 3 | 3.5` |
| possession_text, possession_year | "Dec 2030 Onwards" and 2030. The year drives the filters. |
| land_text, land_acres, towers, floors, total_units, units_text | Size of the project |
| rera_number, rera_status | Status: registered or awaited |
| amenity_tags | Tags the filter uses: pool, gym, clubhouse, kids, jogging, courts, tennis, basketball, badminton, squash, cricket, indoor, spa, yoga, amphi, theatre, pet, cowork, party, retail, cycling, library |
| amenities_full | The builder's full list, shown on the project page |
| metro_station, metro_km | Blank = the site finds the nearest open station itself |
| tech_parks | `ITPL 7 | Bagmane Tech Park 13.3`. Blank = worked out by the site. |
| schools / hospitals / shops / parks columns | Counts and nearest one. Blank = that line is hidden. |
| bharatprops_slug | Last part of the page link: bharatprops.com/project/**this-part** |
| photo_url | Full link to the project photo |

## units.csv columns

`project_id, project_name, unit_name, bedrooms, size_sqft, price_lakh`

Price per sq ft and the price comparison are calculated from these rows, so a unit needs both size and price to count.

## places.csv columns

| Column | What to type |
|---|---|
| name | "ITPL", "Phoenix Marketcity" |
| type | tech park, mall or station (use station for railway stations and the airport) |
| latitude, longitude | From Google Maps |
| popular | yes = shown as a quick shortcut under "Popular tech parks". Keep it to about five. |

## metro_stations.csv columns

| Column | What to type |
|---|---|
| name | Station name, without the word "metro" |
| line | purple, green, yellow, pink or blue |
| latitude, longitude | From Google Maps |
| status | open or opening later. Only open stations count for "nearest metro". |

The coloured metro lines and the roads drawn on the map are not in a sheet. They are thousands of map points and live in basemap.json; adding a station here puts a stop on the map but does not extend the line.

## Watch out for

- Excel can turn text like "Jun 2027" into a date. Check `possession_text` before saving.
- Keep a copy of the file before a big edit. One broken header stops the whole site from loading.
