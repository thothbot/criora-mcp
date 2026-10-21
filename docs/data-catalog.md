# Criora data catalog

What the Criora MCP server (`https://criora.com/mcp`) and the JSON API (`https://criora.com/api/v1`) return.
Generated from live answers on 2026-10-16. Every value names its source; licences are in
[Data sources](https://criora.com/docs/references/data-sources).

## 1. Long-term climate layers at a point — `get_climate_profile` (55 layers in 9 categories)

`get_climate_profile` returns every layer below for one point; `categories` narrows it to one or more categories.
`assess_place` returns only the headline layers (marked ★). Each layer gives its bands, unit, the size of the raster
cell read at the point (`cell_km`), its year or period, and its source.

| Category | Layer id | What it is | Bands | Unit | Cell | Period | Source |
|---|---|---|---|---|---|---|---|
| temperature | `cmip6_climate_delta/tmax_warm` | Change in max temperature of the warmest month vs 1970-2000 (5-model median) | ssp245_2050, ssp245_2080, ssp585_2050, ssp585_2080 | C | 18.55 km | baseline + 2050/2080(2100), SSP scenarios | WorldClim 2.1 CMIP6 downscaled bioclimatic projections |
| temperature | `cmip6_climate_delta/tmean` | Change in mean temperature vs 1970-2000 (5-model median) | ssp245_2050, ssp245_2080, ssp585_2050, ssp585_2080 | C | 18.55 km | baseline + 2050/2080(2100), SSP scenarios | WorldClim 2.1 CMIP6 downscaled bioclimatic projections |
| temperature | `cmip6_climate_delta/tmin_cold` | Change in min temperature of the coldest month vs 1970-2000 (5-model median) | ssp245_2050, ssp245_2080, ssp585_2050, ssp585_2080 | C | 18.55 km | baseline + 2050/2080(2100), SSP scenarios | WorldClim 2.1 CMIP6 downscaled bioclimatic projections |
| temperature | `era5_extremum/climate_days` | Climate day counts: hot days >35 °C, tropical nights, summer days, frost nights, ice days | hot_days, tropical_nights, summer_days, cold_days, frost_nights, total | days | 27.83 km | 2025 | ERA5 Single Levels Daily Statistics |
| temperature | `era5_extremum/temperature_max` | Hottest daily maximum of the year | max | C | 27.83 km | 2025 | ERA5 Single Levels Daily Statistics |
| temperature | `era5_extremum/temperature_min` | Coldest daily minimum of the year | min | C | 27.83 km | 2025 | ERA5 Single Levels Daily Statistics |
| temperature | `era5_monthly/temperature` | Temperature: annual mean, lowest and highest month | mean, min, max | C | 11.13 km | 2025 | ERA5-Land Monthly Averaged Reanalysis |
| temperature | `era5_monthly/utci` | UTCI felt temperature of the average day: annual mean, coldest and hottest month | mean, max, min | C | 27.83 km | 2025 | ERA5 Monthly Averaged Data on Single Levels |
| precipitation | `aqueduct_water_stress/drr` | Drought risk: likelihood and impact of drought on people, assets and the economy | value |  | 5.57 km | static | Aqueduct 4.0 Water Risk Framework |
| precipitation | `aridity_index/annual` | UNEP-WMO Aridity Index (P/PET) — multi-decade climatology, absolute measure of chronic water availability. | value | P/PET × 10000 | 0.93 km | static | Global Aridity Index and Potential Evapotranspiration v3.1 |
| precipitation | `cmip6_climate_delta/precip_annual` | Change in annual precipitation vs 1970-2000 (5-model median) | ssp245_2050, ssp245_2080, ssp585_2050, ssp585_2080 | mm | 18.55 km | baseline + 2050/2080(2100), SSP scenarios | WorldClim 2.1 CMIP6 downscaled bioclimatic projections |
| precipitation | `cmip6_climate_delta/precip_dry` | Change in precipitation of the driest quarter vs 1970-2000 (5-model median) | ssp245_2050, ssp245_2080, ssp585_2050, ssp585_2080 | mm | 18.55 km | baseline + 2050/2080(2100), SSP scenarios | WorldClim 2.1 CMIP6 downscaled bioclimatic projections |
| precipitation | `cmip6_climate_delta/precip_wet` | Change in precipitation of the wettest quarter vs 1970-2000 (5-model median) | ssp245_2050, ssp245_2080, ssp585_2050, ssp585_2080 | mm | 18.55 km | baseline + 2050/2080(2100), SSP scenarios | WorldClim 2.1 CMIP6 downscaled bioclimatic projections |
| precipitation | `era5_extremum/extreme_precip` | Heavy-rain days (>=10...100 mm) and the wettest day | days_ge_10mm, days_ge_20mm, days_ge_30mm, days_ge_35mm, days_ge_50mm,  | days, mm | 27.83 km | 2025 | ERA5 Single Levels Daily Statistics |
| precipitation | `era5_monthly/precipitation` | Precipitation: annual mean, lowest and highest month | mean, min, max | mm/month | 11.13 km | 2025 | ERA5-Land Monthly Averaged Reanalysis |
| precipitation | `era5_monthly/precipitation_max` | Mean daily precipitation of the wettest month | max | mm/day | 11.13 km | 2025 | ERA5-Land Monthly Averaged Reanalysis |
| precipitation | `era5_monthly/snow_albedo` | Snow albedo: annual mean, lowest and highest month | mean, min, max | % | 11.13 km | 2025 | ERA5-Land Monthly Averaged Reanalysis |
| precipitation | `era5_monthly/snow_cover` | Snow cover: annual mean, lowest and highest month | mean, min, max | % | 11.13 km | 2025 | ERA5-Land Monthly Averaged Reanalysis |
| precipitation | `era5_monthly/snow_water_equivalent` | Snow water equivalent: annual mean, lowest and highest month | mean, min, max | mm | 11.13 km | 2025 | ERA5-Land Monthly Averaged Reanalysis |
| precipitation | `era5_monthly/snowmelt` | Snowmelt: annual mean, lowest and highest month | mean, min, max | mm/month | 11.13 km | 2025 | ERA5-Land Monthly Averaged Reanalysis |
| precipitation | `spi_12/observed` | 12-month Standardized Precipitation Index for drought monitoring | value |  | 5.57 km | 2025 | GDO Standardized Precipitation Index (SPI-12) |
| wind | `era5_extremum/storm_days` | Gale, storm and hurricane-force gust days (Beaufort 7-12) | gale_days, storm_days, strong_gale_days, severe_storm_days, violent_st | days | 27.83 km | 2025 | ERA5 Single Levels Daily Statistics |
| wind | `era5_extremum/wind_max` | Strongest wind gust of the year | max | m/s | 27.83 km | 2025 | ERA5 Single Levels Daily Statistics |
| wind | `era5_monthly/cape` | Annual Mean Convective Available Potential Energy | mean_cape | J/kg | 27.83 km | 2025 | ERA5 Monthly Averaged Data on Single Levels |
| wind | `era5_monthly/wind` | Wind speed: annual mean, lowest and highest month | mean, min, max | m/s | 27.83 km | 2025 | ERA5 Monthly Averaged Data on Single Levels |
| water | `aqueduct_water_future/ws` | WRI Aqueduct 4.0 future water-stress category projections (SSP scenarios, 2050/2080) | 2050_ssp126, 2050_ssp370, 2050_ssp585, 2080_ssp126, 2080_ssp370, 2080_ |  | 5.57 km | baseline + 2050/2080(2100), SSP scenarios | Aqueduct 4.0 Water Risk Framework — future projections |
| water | `aqueduct_water_stress/bws` | Baseline water stress: water withdrawals as a share of available renewable supply | value |  | 5.57 km | static | Aqueduct 4.0 Water Risk Framework |
| water | `distance_to_coast/distance` | Distance from coastline in kilometers (NASA/PacIOOS). Negative=land, positive=ocean. | value | km | 11.13 km | static | Distance to Nearest Coastline |
| water | `era5_monthly/humidity` | Relative humidity: annual mean, lowest and highest month | mean, min, max | % | 11.13 km | 2025 | ERA5-Land Monthly Averaged Reanalysis |
| water | `era5_monthly/potential_evapotranspiration` | Potential evaporation from an open water surface: annual mean, lowest and highest month | mean, min, max | mm/month | 11.13 km | 2025 | ERA5-Land Monthly Averaged Reanalysis |
| water | `era5_monthly/soil_moisture` | Soil moisture of the top 7 cm: annual mean, lowest and highest month | mean, min, max | m3/m3 | 11.13 km | 2025 | ERA5-Land Monthly Averaged Reanalysis |
| water | `era5_monthly/vpd` | Vapour pressure deficit: annual mean, lowest and highest month | mean, min, max | kPa | 11.13 km | 2025 | ERA5-Land Monthly Averaged Reanalysis |
| water | `glwd/classification` | Main lake or wetland class of the cell | value |  | 0.46 km | static | Global Lakes and Wetlands Database (GLWD) version 2.0 |
| water | `glwd/coverage` | Share of the cell covered by lakes, rivers and wetlands | value | % | 0.93 km | static | Global Lakes and Wetlands Database (GLWD) version 2.0 |
| water | `jrc_surface_water/occurrence` | JRC Global Surface Water occurrence (1984-2021) - percentage of time water was detected over 38 years of satellite observations | value | % | 0.25 km | 1984-2021 | JRC Global Surface Water v1.4 |
| flooding | `flood_coastal/inundation` | Coastal flood inundation depth for 100-year return period (WRI Aqueduct Floods v2) | historical, 2050_ssp245, 2050_ssp585, 2080_ssp245, 2080_ssp585 | meters | 0.93 km | baseline + 2050/2080(2100), SSP scenarios | Aqueduct Floods Hazard Maps |
| flooding | `flood_forecast/glofas` | Global flood forecasting from Copernicus Emergency Management Service (GloFAS) | flood_summary, rapid_mapping | intensity | 11.13 km | next 30 days | GloFAS - Global Flood Awareness System |
| flooding | `flood_riverine/inundation` | River flood inundation depth for 100-year return period (WRI Aqueduct Floods v2) | historical, 2050_ssp245, 2050_ssp585, 2080_ssp245, 2080_ssp585 | meters | 0.93 km | baseline + 2050/2080(2100), SSP scenarios | Aqueduct Floods Hazard Maps |
| flooding | `slr_projections/projections` | IPCC AR6 sea level rise projections — median total SLR (mm), medium confidence | ssp245_2020, ssp245_2050, ssp245_2100, ssp585_2050, ssp585_2100 | mm | 111.32 km | baseline + 2050/2080(2100), SSP scenarios | IPCC AR6 Sea Level Projections |
| vegetation | `burned_area/annual` | Share of the cell burned in 2023 | value | % burned | 0.56 km | 2023 / 2002-2023 | Global Biomass Burning at 500 m (GFED500) |
| vegetation | `burned_area/climatology_22yr` | Mean share of the cell burned each year, 2002 to 2023 | value | % mean annual burned | 27.83 km | 2023 / 2002-2023 | Global Biomass Burning at 500 m (GFED500) |
| vegetation | `era5_monthly/lai_high` | Leaf area index of high vegetation: annual mean, lowest and highest month | mean, min, max | m2/m2 | 11.13 km | 2025 | ERA5-Land Monthly Averaged Reanalysis |
| vegetation | `era5_monthly/lai_low` | Leaf area index of low vegetation: annual mean, lowest and highest month | mean, min, max | m2/m2 | 11.13 km | 2025 | ERA5-Land Monthly Averaged Reanalysis |
| vegetation | `ndvi/annual` | Annual NDVI statistics from MODIS at 10km resolution (mean, min, max, stdDev) | mean, min, max, stdDev | NDVI | 11.13 km | 2024 | MODIS Vegetation Index (MOD_NDVI_M) |
| terrain | `dem/elevation` | Surface elevation above sea level, including buildings and trees | value | m | 0.25 km | static | Copernicus DEM GLO-90 |
| terrain | `dem/slope` | Terrain slope in degrees, computed from the surface elevation | value | ° | 0.25 km | static | Copernicus DEM GLO-90 |
| terrain | `dem/tri` | Terrain ruggedness index: mean elevation difference to the neighbouring cells | value | m | 0.25 km | static | Copernicus DEM GLO-90 |
| terrain | `subsidence/prediction` | Predicted land subsidence rate class, 2013 to 2019 | value |  | 2.23 km | 2013-2019 | Global Land Subsidence Mapping Reveals Widespread Loss of Aquifer Storage Capacity |
| terrain | `subsidence/probability` | Probability that the land subsides faster than 1 cm a year, 2013 to 2019 | value | probability | 2.23 km | 2013-2019 | Global Land Subsidence Mapping Reveals Widespread Loss of Aquifer Storage Capacity |
| landcover | `ghsl_built_up/built_up` | Built-up surface fraction from JRC GHSL R2023A (Sentinel-2 + Landsat, ~1km) | value | % | 0.93 km | 2025 | JRC Global Human Settlement Layer — Built-up Surface |
| landcover | `modis_land_cover/igbp` | MODIS MCD12Q1 IGBP land cover classification at 500m resolution (17 classes) | value |  | 0.46 km | static | MODIS Land Cover Type (MCD12Q1) v061 |
| misc | `era5_monthly/runoff` | Surface runoff: annual mean, lowest and highest month | mean, min, max | mm/month | 11.13 km | 2025 | ERA5-Land Monthly Averaged Reanalysis |
| misc | `era5_monthly/solar_radiation` | Solar radiation: annual mean, lowest and highest month | mean, min, max | MJ/m2 | 11.13 km | 2025 | ERA5-Land Monthly Averaged Reanalysis |
| misc | `era5_monthly/solar_radiation_max` | Mean daily solar radiation of the sunniest month | max | MJ/m2/day | 11.13 km | 2025 | ERA5-Land Monthly Averaged Reanalysis |
| misc | `koppen/climate` | Global climate classification based on vegetation and precipitation patterns | historical, current, 2050_ssp245, 2050_ssp585, 2080_ssp245, 2080_ssp58 |  | 0.93 km | baseline + 2050/2080(2100), SSP scenarios | High-resolution (1 km) Köppen-Geiger maps for 1901–2099 |

★ headline layers (in `assess_place`): `cmip6_climate_delta/tmean`, `era5_extremum/climate_days`, `era5_extremum/temperature_max`, `aqueduct_water_stress/drr`, `era5_extremum/extreme_precip`, `aqueduct_water_future/ws`, `aqueduct_water_stress/bws`, `flood_coastal/inundation`, `flood_riverine/inundation`, `slr_projections/projections`, `burned_area/climatology_22yr`, `koppen/climate`.

Satellite-derived layers: NDVI (MODIS), land cover (MODIS MCD12Q1), burned area (GFED500, MODIS), built-up surface
(JRC GHSL, Sentinel-2 + Landsat), surface water occurrence (JRC GSW, Landsat 1984-2021), elevation, slope and ruggedness
(Copernicus DEM GLO-90), land subsidence (InSAR-based model).

Notes: values are read from the raster cell that contains the point; a layer with `applicable=false` does not describe
the place (sea level rise inland); `available=false` means no value, not zero; flood depths are undefended (no dikes).

## 2. This week's forecast — `get_forecast`

ECCC GDPS global model, 15 km cell, 7 days: hourly for day 1, then 3-hourly, then 6-hourly. Per local day: min/max
temperature, peak precipitation rate, peak wind gust, and a risk class (Very low, Low, Medium, High, Critical) with the
hazard behind it (heat, cold, wind, rain, snow, freezing rain) and its reading (UTCI felt temperature, gust m/s, rain
rate mm/h). `hourly=true` adds every step. `show_risk_map` draws the same forecast (risk, rain, temperature, wind).

## 3. Hazard events and warnings in force — `get_hazards_near`, `list_hazards`

| Event type | Source |
|---|---|
| official warnings for every natural hazard (US) | US National Weather Service |
| official warnings in Europe (wind, snow and ice, thunderstorms, fog, heat, cold, coastal, rain, flood, fire danger, avalanche) | MeteoAlarm national services, through WMO WIS2 |
| earthquake (depth, felt reports, intensity, PAGER alert) | USGS |
| tsunami bulletins | NOAA tsunami warning centres |
| tropical cyclones (Atlantic, East and Central Pacific) with cone and forecast track | NOAA National Hurricane Center |
| tropical cyclones elsewhere, flood, volcano, drought | GDACS (EC JRC / UN OCHA) |
| wildfire | NASA FIRMS active fire detections (VIIRS, MODIS) |
| air_quality | OpenAQ reference monitors |

Each event: kind (occurrence or warning), type, severity (low, medium, high, critical), time; a warning also its issuer,
onset and expiry and whether the place lies inside its area (`get_hazards_near`). `get_hazards_near` searches a radius
of 1-500 km over the last 1-30 days; `list_hazards` covers a country or territory, a region (`bbox`) or the world.

## 4. Country risk — `get_country_profile`, `compare_countries`, `rank_countries`

194 countries. Overall score 0-100 (higher = more risk) and five dimensions, each with a class and a rank. With
`include_indicators=true`, 126 indicators with value, year, source and the medians of the world, region,
subregion and income group.

| Dimension | Indicators | Sources (rows, incl. aggregate scores) | Indicator names |
|---|---|---|---|
| nature | 49 | inform: 2, ndgain: 46, worldbank: 13 | Earthquake Risk; Tsunami Risk; Projected Cereal Yield Change; Projected Population Change; Food Import Dependency; Rural Population; Agricultural Capacity; Child Malnutrition; Projected Annual Runoff Change; Projected Groundwater Change; Freshwater Withdrawal Rate; Water Dependency Ratio; Dam Capacity; Access to Reliable Drinking Water; Projected Climate-Related Deaths; Projected Vector Disease Change; Dependency Ratio; Slum Population; Health Expenditure Per Capita; Access to Improved Sanitation; Projected Biome Distribution Change; Projected Marine Biodiversity Loss; Ecological Footprint; Natural Capital Dependency; Protected Biome Areas; Environmental Treaties Engagement; Projected Flood Hazard Change; Projected Warm Period Change; Urban Concentration; Age Dependency Ratio; Quality of Trade Infrastructure; Paved Roads; Projected Hydropower Change; Projected Sea Level Rise Impact; Energy Import Dependency; Population Below 5m; Electricity Access; Disaster Preparedness; Food Production Index; Forest Depletion; Natural Resource Depletion; Forest Area; Agricultural Land; Tree Cover Loss; Agriculture GDP Share; Threatened Mammal Species; Water Stress; Protected Areas; Freshwater Withdrawal |
| governance | 15 | inform: 8, worldbank: 12 | Healthcare Access; Communication Infrastructure; Physical Infrastructure; Disaster Risk Reduction; INFORM Governance Index; Government Effectiveness; Control of Corruption; Political Stability; Rule of Law; Regulatory Quality; Voice and Accountability; Legal Rights Strength; Patent Applications; Women in Parliament; Scientific Articles |
| social | 34 | inform: 12, worldbank: 32 | Aid Dependency; Development and Deprivation; Food Security; Health Conditions; Recent Shocks; Children Under 5; Uprooted People; Overweight Adults; Unmet Contraception Need; Access to Electricity; GDP Growth; Gini Coefficient; Poverty Rate (National); School Gender Parity; Under-5 Mortality Rate; Safe Drinking Water; Fertility Rate; Gender Labor Ratio; Communicable Disease Deaths; Hospital Beds; Undernourishment; Internet Users; Population Density; Income Share Bottom 20%; Net Migration; ESG Performance Score; Labor Participation; Adult Literacy Rate; Life Expectancy; Sanitation Access; Aging Population; Unemployment Rate; Primary School Enrollment; Education Expenditure |
| adaptation | 9 | ndgain: 13 | Doing Business Score; Political Stability (Readiness); Control of Corruption (Readiness); Rule of Law (Readiness); Regulatory Quality (Readiness); Social Inequality (Readiness); ICT Infrastructure; Education (Readiness); Innovation (Readiness) |
| climate | 19 | inform: 3, worldbank: 20 | Flood Risk; CO2 Emissions Per Capita; N2O Emissions Per Capita; Energy Intensity; Land Surface Temperature; Renewable Electricity Share; Energy Imports; Methane Emissions Per Capita; PM2.5 Air Pollution; Renewable Energy Share; Cooling Degree Days; Days with Heat Index Above 35°C; Access to Clean Fuels; Heating Degree Days; Coastal Protection Needed; Fossil Fuel Consumption; Energy Use Per Capita; Drought Index (SPEI); Coal Electricity Share |

## 5. Documents — `search`, `fetch`, resources

`country:<ISO3>`, `place:<lat>,<lon>`, `page:methodology`, `page:sources` as citable markdown; resources
`criora://country/{iso3}`, `criora://methodology`, `criora://sources`.
