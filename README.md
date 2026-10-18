# Criora — climate and disaster risk MCP server

[![Criora MCP connector](https://glama.ai/mcp/connectors/com.criora/criora/badges/score.svg)](https://glama.ai/mcp/connectors/com.criora/criora)
[![M8ven Verified](https://m8ven.ai/badge/mcp/thothbot-criora-mcp-i8tnim?v=419f3f3e004edbd5e8b48ab09c3c542e&variant=verified)](https://m8ven.ai/mcp/thothbot-criora-mcp-i8tnim?s=readme)

Criora is a hosted, remote [Model Context Protocol](https://modelcontextprotocol.io) server that answers climate and disaster risk questions for any place on Earth: this week's weather risk, hazards happening nearby, long-term climate exposure and country risk. In assistants that display MCP Apps, such as Claude, it can also show an interactive map of the place right in the conversation.

- **Endpoint:** `https://criora.com/mcp`
- **Transport:** Streamable HTTP
- **Authentication:** none, no account or API key
- **Access:** read-only, free
- **Registry name:** `com.criora/criora` in the [official MCP registry](https://registry.modelcontextprotocol.io)

This repository holds the documentation and registry metadata for the hosted server. The server itself runs at criora.com; there is nothing to install.

## Use cases

- **Travel safety:** "is it safe to travel to Dubai next week?": heat, storms and heavy rain on the travel days, and disasters happening nearby.
- **Property, real estate and site due diligence:** flood risk (river and coastal flood depth by scenario), sea level rise, extreme heat, drought, water stress, wildfire and subsidence at an address or coordinates, with warming to 2050 and 2080.
- **Relocation:** compare the long-term climate exposure of several cities side by side.
- **ESG, insurance and investment research:** country climate and disaster risk for 194 countries (INFORM Risk Index, ND-GAIN, World Bank), rankings within a region or income group, ~160 indicators against regional and world benchmarks.
- **Disaster monitoring:** wildfires, earthquakes, floods, hurricanes and typhoons, volcanoes, droughts and air quality near any place right now.

## Connect

**Claude (claude.ai, Claude Desktop):** Settings → Connectors → Add custom connector, then paste `https://criora.com/mcp`.

**Claude Code:**

```bash
claude mcp add --transport http criora https://criora.com/mcp
```

or as a Claude Code plugin (MCP server plus a skill that tells Claude when to use which tool):

```bash
/plugin marketplace add thothbot/criora-mcp
/plugin install criora@criora
```

**Cursor** (`~/.cursor/mcp.json`) and other clients that use an `mcpServers` file:

```json
{
  "mcpServers": {
    "criora": { "url": "https://criora.com/mcp" }
  }
}
```

**Google Antigravity** (App, CLI, IDE): install the plugin from this repository (MCP server plus a skill that tells the agent when to use which tool):

```bash
agy plugin install https://github.com/thothbot/criora-mcp
```

or add the server to `mcp_config.json` yourself:

```json
{
  "mcpServers": {
    "criora": { "serverUrl": "https://criora.com/mcp" }
  }
}
```

**Gemini CLI:**

```bash
gemini extensions install https://github.com/thothbot/criora-mcp
```

**VS Code** (`.vscode/mcp.json`):

```json
{
  "servers": {
    "criora": { "type": "http", "url": "https://criora.com/mcp" }
  }
}
```

**ChatGPT** and other assistants: add `https://criora.com/mcp` as a custom connector / remote MCP server.

## Data catalog

The server reads 55 long-term climate layers (heat, rain, drought, wind, water stress, flood depth, sea level rise, NDVI, land cover, terrain and more), the 7-day forecast, hazard events from NASA FIRMS, GDACS, the US NWS and OpenAQ, and 126 country indicators. The full list with units, resolution, period and source is in [docs/data-catalog.md](docs/data-catalog.md).

## Tools

Place tools take latitude and longitude, or a place name that they resolve to the best match and report back. Every tool is read-only and publishes its output schema; answers at their defaults stay under about 8,000 tokens.

| Tool | What it answers |
| --- | --- |
| `assess_place` | Everything about a place in one answer: forecast risk by day, hazards nearby, headline climate exposures and the country's risk profile. The best first call for a general question. |
| `get_forecast` | Seven-day weather and weather risk, by local day or step by step. Each day carries a risk class with the hazard behind it (heat, cold, wind, rain, snow, freezing rain). |
| `get_hazards_near` | Wildfires, earthquakes, floods, tropical cyclones, volcanic eruptions, droughts, US NWS warnings and air quality near a place, most severe and most recent first. |
| `get_climate_profile` | Long-term exposure from 55 layers: flood depth, sea level rise, heat, drought, water stress, wind, NDVI and other satellite layers, terrain, land cover, with warming and rainfall change projected to 2050 and 2080. Narrow it with `categories` or `layers` (ids in `criora://layers`). |
| `get_country_profile` | A country's overall risk score and its climate, nature, social, governance and adaptation scores; on request about 160 indicators with world and regional benchmarks. |
| `compare_countries` | Two to ten countries side by side on overall risk and each dimension, with their ranks. |
| `rank_countries` | The countries most or least at risk, overall or on one dimension, optionally within a region, subregion or income group, each with its score, risk class and rank. |
| `find_place` | Coordinates for a place name, when a name is ambiguous. |
| `search` | Find countries, places and Criora reference pages by name; returns ids for `fetch`. Built to the shape ChatGPT deep research and company knowledge expect. |
| `fetch` | A readable document for a `search` id (`country:BGD`, `place:<lat>,<lon>`, `page:methodology`), with a link to the Criora page it comes from. |
| `show_risk_map` | An interactive map of a place in the conversation: this week's forecast risk, or the rain, temperature or wind forecast hour by hour, under the hazards nearby. Clients without apps get the same summary as text. |

## Interactive map

`show_risk_map` is an [MCP App](https://modelcontextprotocol.io/docs/extensions/apps): in clients that display apps (Claude on the web, desktop and mobile, and other MCP Apps hosts) it draws a map under the answer, on NASA Blue Marble imagery:

- this week's worst forecast risk with its hazard symbols, or one forecast hour of it;
- the precipitation, temperature or wind forecast instead (`layer`), with animated wind streams and a key;
- hazard events nearby as markers the reader can tap for the event's details;
- a timeline of the week under the field switch: the risk hour by hour with each day's main hazard, or the temperature, wind or rain at the place, with the reading for the hour shown.

The reader can pan, zoom, open the map full screen, tap or scrub the timeline, play the week hour by hour and switch between the four fields; the map tells the assistant what the reader is looking at. The card follows the host's own theme and type, light or dark. Clients that do not display apps get the same answer as text, with a link to the place on Criora's own map.

## Resources

| URI | What it holds |
| --- | --- |
| `criora://country/{iso3}` | A country's risk scores and classes as JSON (template; ISO3 codes autocomplete). |
| `criora://methodology` | How Criora scores country risk (markdown). |
| `criora://sources` | The datasets behind every answer, with licences (markdown). |
| `criora://layers` | Every long-term climate layer `get_climate_profile` reads, with its id, unit, years and source (markdown). |
| `criora://indicators` | The country indicators by risk dimension and source (markdown). |

## Prompts

| Prompt | Arguments | Purpose |
| --- | --- | --- |
| `assess_trip` | `destination`, `dates` (optional) | How risky a trip is: weather risk on the travel days, hazards nearby, seasonal exposure. |
| `compare_places_to_live` | `places` (semicolon-separated) | Long-term climate exposure and country risk of several places side by side. |
| `country_briefing` | `country` (name or ISO3, autocompleted) | One country's climate and disaster risk against its region and the world. |
| `site_due_diligence` | `site`, `purpose` (optional) | Climate and disaster risk of a property or site: flooding, heat, drought, wildfire, subsidence, hazards nearby. |
| `esg_country_screen` | `countries` or `region` (optional) | Screen countries on climate and disaster risk for ESG, investment or supply-chain decisions. |

## Example questions

- "How exposed is Ghana to climate disasters?"
- "What is the weather risk in Lisbon this week?"
- "Are there any wildfires or earthquakes near Tokyo right now?"
- "Compare climate risk for Spain and Portugal."
- "I'm going to Seville from 3 to 6 October — how risky is that trip?"
- "Show me the wind forecast on a map around Brest."
- "What is the flood risk and sea level rise exposure for a house in Rotterdam by 2050?"
- "Is there a heat wave or a hurricane coming to Miami this week?"
- "Which low-income countries are most exposed to climate risk, for an ESG screen?"

## Data sources

Every answer names its source. Main sources: forecast from Environment and Climate Change Canada; place names from OpenStreetMap Nominatim (ODbL); hazards from NASA FIRMS, GDACS, the US National Weather Service and OpenAQ; climate layers from ERA5, CMIP6 and IPCC AR6 among others; country indicators from the INFORM Risk Index, ND-GAIN and the World Bank. See [Data Sources](https://criora.com/docs/references/data-sources) for the full list and licences.

## Limits

- Place-name lookups go through OpenStreetMap Nominatim, which allows one request per second for all of Criora together, so pass coordinates where you have them.
- Forecasts change when a new model run is published, twice a day.

## JSON API

The same data is available as a plain JSON API under `https://criora.com/api/v1`. See [Data API and AI agents](https://criora.com/docs/references/api-and-agents).

## What is sent

The plugin runs nothing on your machine: it adds the hosted server and a skill that tells Claude when to use it. When Claude calls a Criora tool, the tool's arguments (a place name or coordinates, a country, a search phrase) go to `https://criora.com/mcp` over HTTPS, with the usual request data (IP address, client name and user agent). Criora logs these requests to run and secure the service and keeps the logs for up to 30 days. Place names are looked up with OpenStreetMap Nominatim; nothing else is passed on. No account, API key or other personal data is asked for.

## Terms

Criora publishes data, not advice. Use of the service is governed by the [Terms of Service](https://criora.com/terms) and the [Privacy Policy](https://criora.com/privacy). When you publish or redistribute data from Criora, credit Criora and follow the licence of the source each answer names.

The [MIT licence](LICENSE) in this repository covers the files in this repository (documentation and metadata) only.

## Changelog

- **1.4.1** (2026-10-18, Claude Code plugin only; the server stays 1.4.0): the plugin manifest names its icon (`./icon.png`), and this README says what is sent.
- **1.4.0** (2026-10-16): the tools say what data they hold: `get_climate_profile` takes `layers` by id (55 layers, e.g. `ndvi/annual`) and its `categories` argument lists each category's layers; resources `criora://layers` and `criora://indicators`; `search`/`fetch` find the data catalogue (`catalog:layers`, `catalog:indicators`); descriptions and titles rewritten to the directories' rules; prompts `site_due_diligence` and `esg_country_screen`.
- **1.3.1** (2026-10-15): the map card redesigned to the hosts' own look, in the card and full screen, with the week's timeline under the field switch; clearer hazard icons; Very low in the risk key; a lighter risk wash so the land shows; the forecast read is retried after a failure; the map keeps drawing when a host reports the card off screen; the server description names the map.
- **1.3.0** (2026-10-15): `show_risk_map`, an interactive map of a place in the chat (risk, rain, temperature, wind).

## Contact

Issues and questions: open an issue in this repository or write to thothbot@gmail.com.
