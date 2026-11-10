# NYC Open Data — Postman Collection

General-purpose Postman collection for **[NYC Open Data](https://opendata.cityofnewyork.us/)** (data.cityofnewyork.us): search the whole catalog, inspect any dataset's columns, and query or download any of its ~2,400 datasets through the Socrata APIs. No API key needed.

## Import
Postman → **Import** → paste:
`https://raw.githubusercontent.com/mikeyeves/NYC-Open-Data-Postman/main/NYC_Open_Data.postman_collection.json`

## Workflow
| Folder | What it does | API |
|---|---|---|
| 1. Discover datasets | Keyword search, by agency, recently updated, most viewed, categories, tags, facets | [Socrata Discovery API](https://dev.socrata.com/docs/other/discovery) |
| 2. Dataset metadata | Columns (field names & types), full metadata, row count | `/api/views/{id}` |
| 3. Query any dataset | First rows, SoQL `$select/$where/$order`, equality filter, full-text, group & count, CSV / GeoJSON / full export | [SODA 2.1](https://dev.socrata.com/docs/queries/) |
| 4. SODA3 | Newer POST query endpoint (needs a free app token) | `/api/v3/views/{id}/query.json` |
| 5. Ready-made examples | PLUTO by address & by block, DOB job filings, landmark sites, 311 near a point, births index | |

The discovery search saves the first result's ID to `dataset_id`, so you can go straight from **Search** → **Columns** → **Query**. Results render as tables in Postman's **Visualize** tab.

## Variables
| Variable | Default | Used by |
|---|---|---|
| `search` | `landmark` | catalog & full-text search |
| `agency` | DORIS | datasets from one agency |
| `dataset_id` | `64uk-42ks` (PLUTO) | all metadata / query requests |
| `where` | `yearbuilt < 1900 AND borough='MN'` | SoQL query |
| `filter_field` / `filter_value` | `zipcode` / `10011` | equality filter |
| `group_field` | `landuse` | group & count |
| `lat` / `lon` | 30 Greenwich Ave | 311 geo example |
| `app_token` | | optional; enable the `X-App-Token` header (required for SODA3) |

Get a free app token at https://data.cityofnewyork.us/profile/edit/developer_settings.

## SoQL tips
- Strings use single quotes; text comparisons are case-sensitive, so use `upper(col)=upper('value')`.
- `$limit` max is 50,000 per request; page with `$offset` and a stable `$order` (e.g. `:id`).
- Geo: `within_circle(location, lat, lon, metres)` on point columns.

## Related collections
- [NYC Historical Vital Records](https://github.com/mikeyeves/NYC-Historical-Vital-Records-Postman)
- [Unified Census ED Finder](https://github.com/mikeyeves/Unified-Census-ED-Finder-Postman)
- [Federal Register & National Archives Catalog APIs](https://github.com/mikeyeves/US-Federal-Register-National-Archives-Catalog-APIs)
- [Hebcal Jewish Calendar APIs](https://github.com/mikeyeves/Hebcal-Jewish-Calendar-APIs)
