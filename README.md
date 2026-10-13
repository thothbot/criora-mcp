# Criora — climate and disaster risk MCP server

[![Criora MCP connector](https://glama.ai/mcp/connectors/com.criora/criora/badges/score.svg)](https://glama.ai/mcp/connectors/com.criora/criora)

Criora is a hosted, remote [Model Context Protocol](https://modelcontextprotocol.io) server that answers climate and disaster risk questions for any place on Earth: this week's weather risk, hazards happening nearby, long-term climate exposure and country risk.

- **Endpoint:** `https://criora.com/mcp`
- **Transport:** Streamable HTTP
- **Authentication:** none, no account or API key
- **Access:** read-only, free
- **Registry name:** `com.criora/criora` in the [official MCP registry](https://registry.modelcontextprotocol.io)

This repository holds the documentation and registry metadata for the hosted server. The server itself runs at criora.com; there is nothing to install.

## Connect

**Claude (claude.ai, Claude Desktop):** Settings → Connectors → Add custom connector, then paste `https://criora.com/mcp`.

**Claude Code:**

```bash
claude mcp add --transport http criora https://criora.com/mcp
```

**Cursor** (`~/.cursor/mcp.json`) and other clients that use an `mcpServers` file:

```json
{
  "mcpServers": {
    "criora": { "url": "https://criora.com/mcp" }
  }
}
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

## Tools

Place tools take latitude and longitude, or a place name that they resolve to the best match and report back. Every tool is read-only and publishes its output schema; answers at their defaults stay under about 8,000 tokens.

| Tool | What it answers |
| --- | --- |
| `assess_place` | Everything about a place in one answer: forecast risk by day, hazards nearby, headline climate exposures and the country's risk profile. The best first call for a general question. |
| `get_forecast` | Seven-day weather and weather risk, by local day or step by step. Each day carries a risk class with the hazard behind it (heat, cold, wind, rain, snow, freezing rain). |
| `get_hazards_near` | Wildfires, earthquakes, floods, tropical cyclones, volcanic eruptions, droughts, US NWS warnings and air quality near a place, most severe and most recent first. |
| `get_climate_profile` | Long-term exposure: floods, sea level rise, heat, drought, water stress and more, with warming and rainfall change projected to 2050 and 2080. |
| `get_country_profile` | A country's overall risk score and its climate, nature, social, governance and adaptation scores; on request about 160 indicators with world and regional benchmarks. |
| `compare_countries` | Two to ten countries side by side on overall risk and each dimension, with their ranks. |
| `rank_countries` | The countries most or least at risk, overall or on one dimension, optionally within a region, subregion or income group, each with its score, risk class and rank. |
| `find_place` | Coordinates for a place name, when a name is ambiguous. |
| `search` | Find countries, places and Criora reference pages by name; returns ids for `fetch`. Built to the shape ChatGPT deep research and company knowledge expect. |
| `fetch` | A readable document for a `search` id (`country:BGD`, `place:<lat>,<lon>`, `page:methodology`), with a link to the Criora page it comes from. |

## Resources

| URI | What it holds |
| --- | --- |
| `criora://country/{iso3}` | A country's risk scores and classes as JSON (template; ISO3 codes autocomplete). |
| `criora://methodology` | How Criora scores country risk (markdown). |
| `criora://sources` | The datasets behind every answer, with licences (markdown). |

## Prompts

| Prompt | Arguments | Purpose |
| --- | --- | --- |
| `assess_trip` | `destination`, `dates` (optional) | How risky a trip is: weather risk on the travel days, hazards nearby, seasonal exposure. |
| `compare_places_to_live` | `places` (semicolon-separated) | Long-term climate exposure and country risk of several places side by side. |
| `country_briefing` | `country` (name or ISO3, autocompleted) | One country's climate and disaster risk against its region and the world. |

## Example questions

- "How exposed is Ghana to climate disasters?"
- "What is the weather risk in Lisbon this week?"
- "Are there any wildfires or earthquakes near Tokyo right now?"
- "Compare climate risk for Spain and Portugal."
- "I'm going to Seville from 3 to 6 October — how risky is that trip?"

## Data sources

Every answer names its source. Main sources: forecast from Environment and Climate Change Canada; place names from OpenStreetMap Nominatim (ODbL); hazards from NASA FIRMS, GDACS, the US National Weather Service and OpenAQ; climate layers from ERA5, CMIP6 and IPCC AR6 among others; country indicators from the INFORM Risk Index, ND-GAIN and the World Bank. See [Data Sources](https://criora.com/docs/references/data-sources) for the full list and licences.

## Limits

- Place-name lookups go through OpenStreetMap Nominatim, which allows one request per second for all of Criora together, so pass coordinates where you have them.
- Forecasts change when a new model run is published, twice a day.

## JSON API

The same data is available as a plain JSON API under `https://criora.com/api/v1`. See [Data API and AI agents](https://criora.com/docs/references/api-and-agents).

## Terms

Criora publishes data, not advice. Use of the service is governed by the [Terms of Service](https://criora.com/terms) and the [Privacy Policy](https://criora.com/privacy). When you publish or redistribute data from Criora, credit Criora and follow the licence of the source each answer names.

The [MIT licence](LICENSE) in this repository covers the files in this repository (documentation and metadata) only.

## Contact

Issues and questions: open an issue in this repository or write to thothbot@gmail.com.
