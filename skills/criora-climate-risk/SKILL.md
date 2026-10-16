---
name: criora-climate-risk
description: Climate and disaster risk for any place, property or country with the Criora MCP server. Use for flood risk, heat waves, hurricanes and storms, wildfires, earthquakes, drought, sea level rise, extreme weather this week, long-term climate exposure to 2050/2080, country risk comparisons, travel safety, relocation, real estate due diligence and ESG questions.
---

# Criora climate and disaster risk

Criora is a hosted, read-only MCP server (`https://criora.com/mcp`, no account or API key) for climate and disaster risk questions about any place on Earth and any of 194 countries. Every answer names its data source and a criora.com page to cite.

## When to use it

Questions about a place, a property or a site: "is it safe", flood risk, heat waves, hurricanes and storms, wildfires, earthquakes, volcanoes, drought, water stress, sea level rise, air quality, extreme weather this week, and how exposure changes by 2050 and 2080. Questions about countries: overall climate and disaster risk, comparisons, rankings within a region or income group. Typical uses: travel safety, relocation, real estate and site due diligence, ESG and insurance research.

For a plain weather question, any weather tool will do; Criora is the right call when the question is about risk.

## What data each tool returns

**`get_climate_profile`: 55 long-term layers at the point**, filtered with `categories`:

- `temperature`: heat and cold extremes of the latest year (hottest day, hot days >35 °C, tropical nights, frost nights), UTCI felt temperature, warming to 2050/2080 (CMIP6).
- `precipitation`: heavy-rain days and wettest day, rainfall change to 2050/2080, drought risk (WRI), SPI-12 drought index, aridity index, snow cover, snow water equivalent, snowmelt.
- `wind`: strongest gust, gale/storm/hurricane-force gust days, mean wind, CAPE (thunderstorm energy).
- `water`: baseline and future water stress (WRI Aqueduct), soil moisture, humidity, vapour pressure deficit, evapotranspiration, surface water occurrence (JRC, Landsat), lakes and wetlands, distance to coast.
- `flooding`: river and coastal flood depth for a 100-year flood today and in 2050/2080 (WRI Aqueduct), GloFAS 30-day flood forecast, sea level rise to 2050/2100 (IPCC AR6).
- `vegetation`: NDVI vegetation index (MODIS), leaf area index (ERA5-Land), burned area by wildfire (GFED).
- `terrain`: elevation, slope and ruggedness (Copernicus DEM), land subsidence rate and probability.
- `landcover`: land cover class (MODIS), built-up surface share (JRC GHSL).
- `misc`: Köppen climate zone now and in 2050/2080, solar radiation, surface runoff.

The full list with layer ids, bands, units, cell size, period and source: `references/data-catalog.md` (also
https://github.com/thothbot/criora-mcp/blob/main/docs/data-catalog.md). So to answer "what is the NDVI of X", call
`get_climate_profile` with `categories=["vegetation"]` and read the `ndvi/annual` layer (annual mean, min, max, std dev).

**`get_forecast`**: 7 days, per day min/max temperature, peak rain rate, peak gust and a risk class with its hazard.
**`get_hazards_near`**: wildfires (NASA FIRMS), earthquakes, floods, tropical cyclones, volcanoes and droughts (GDACS),
US NWS warnings, air quality (OpenAQ), with severity, distance and time.
**Country tools**: 194 countries, overall score and five dimensions (climate, nature, social, governance, adaptation),
126 indicators from the INFORM Risk Index, ND-GAIN and the World Bank.

Limits: climate layers are read at one raster cell (0.25 to 111 km, given as `cell_km`); NDVI and ERA5 layers are annual,
not current; there is no imagery and no time series.

## Which tool

- `assess_place`: the first call for a general question about one place ("is it safe", "what are the risks"). This week's forecast risk by day, hazards nearby, headline climate exposure and the country's risk.
- `get_forecast`: 7-day weather and weather risk (heat and cold stress, wind gusts, heavy rain, snow).
- `get_hazards_near`: events happening now near a point: wildfires, earthquakes, floods, tropical cyclones, volcanoes, droughts, air quality.
- `get_climate_profile`: long-term exposure: flood depth, sea level rise, extreme heat, warming to 2050 and 2080, drought, water stress.
- `get_country_profile`, `compare_countries`, `rank_countries`: one country, 2 to 10 side by side, or the most or least at risk.
- `find_place`: resolve an ambiguous place name to coordinates first.
- `search` and `fetch`: read a country, a place, or the methodology and sources pages as citable markdown.
- `show_risk_map`: an interactive map of the place, in clients that display MCP Apps.

Place tools take latitude and longitude, or a place name; the answer says what the name was resolved to. A layer with `applicable=false` does not describe the place (sea level rise inland), and `available=false` means no value, not zero. Forecast risk uses five classes: Very low, Low, Medium, High, Critical.
