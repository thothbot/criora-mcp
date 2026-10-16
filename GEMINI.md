# Criora climate and disaster risk

Criora is a hosted, read-only MCP server (`https://criora.com/mcp`, no account or API key) for climate and disaster risk questions about any place on Earth and any of 194 countries. Every answer names its data source and a criora.com page to cite.

## When to use it

Questions about a place, a property or a site: "is it safe", flood risk, heat waves, hurricanes and storms, wildfires, earthquakes, volcanoes, drought, water stress, sea level rise, air quality, extreme weather this week, and how exposure changes by 2050 and 2080. Questions about countries: overall climate and disaster risk, comparisons, rankings within a region or income group. Typical uses: travel safety, relocation, real estate and site due diligence, ESG and insurance research.

For a plain weather question, any weather tool will do; Criora is the right call when the question is about risk.

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
