# CLMS collections in the Copernicus Browser

**Generated 2026-08-26.** Band tables, ids and coverage are a snapshot of the CDSE
documentation on that date. CLMS onboarding continues, so treat anything missing as
"not yet listed" rather than "does not exist", and follow the `[docs]` link on a row
before relying on it.

A flat reference to the **Copernicus Land Monitoring Service** products that appear in the
Copernicus Browser's Default theme: what each one is, its **collection id**, its **bands**,
its **coverage** and a link to its documentation page.

The official docs hold every fact here and hold it better. What they do not have is a flat
view: 3 components, 13 subcategories, 33 groups, 136 product pages. Fine for a website,
painful when you want to know what bands a product exposes without clicking through four
levels. That is the only gap this file fills.

**Everything here is extracted, nothing is authored.** Follow the `[docs]` link on any row
for the authoritative version.

## Three things worth knowing before you use it

### 1. The id does not always tell you the coverage

**`clms_global_` is the CLMS *Global Land component* namespace, not a coverage claim.** Six
ids say `global` for products the documentation scopes to Europe or the northern hemisphere:

| Browser id | the id implies | the docs say |
|---|---|---|
| `clms_global_lie_250m_v2_daily_geotiff` | `global` | **europe** |
| `clms_global_lie_500m_v1_daily_geotiff` | `global` | **northern hemisphere** |
| `clms_global_sce_500m_v1_daily_geotiff` | `global` | **europe** |
| `clms_global_ssm_1km_v1_daily_geotiff` | `global` | **europe** |
| `clms_global_swe_5km_v1_daily_geotiff` | `global` | **northern hemisphere** |
| `clms_global_swe_5km_v2_daily_geotiff` | `global` | **northern hemisphere** |

**Coverage in this file comes from the doc title, not the id.**

### 2. `RT` is the consolidation period, and each level is a separate collection

The same ten days, recomputed as more observations arrive. The official metadata puts it
plainly: the product is *"provided in Near Real Time and consolidated in the next six
periods."*

| Level | What went into it |
|---|---|
| `RT0` | The Near Real Time estimate, as soon as the dekad ends |
| `RT1` | Recomputed after one more dekad |
| `RT2` | After two. Already close to the final values |
| `RT5`, `RT6` | Later consolidations. `RT6` is the reference version |

⚠️ **Each level is a distinct collection with its own UUID**, not a request parameter, and
**some products have no plain version to fall back on** — for DMP 300m v2 you must pick a
level. Rows below collapse the variants into one entry and list the levels available.

⚠️ Not every product carries every level. The Browser exposes `RT0`, `RT1`, `RT2`, `RT5`
and `RT6`; `RT3` and `RT4` do not appear.

### 3. A Browser id is not a CDSE STAC id

The same product is named differently in each catalogue —
`clms_global_lcc_100m_v3_yearly_geotiff` in the Browser and Sentinel Hub,
`clms_lc_100m_global_yearly` in CDSE STAC. **One will not work in the other.** The ids in
this file are **Browser / Sentinel Hub ids**.

## How to read a row

- **Rows are product families.** `_rt0`/`_rt1`/`_rt2`/`_rt6` variants collapse into one
  entry, with the levels shown.
- ⚠️ on an entry means something about it will catch you out: the id disagrees with the
  documented coverage or cadence, there is no plain id to fall back on, or the product has
  no documentation page yet.
- ⚠️ **These are Default-theme entries, not a collection count.** The list is long because
  it holds every version and every RT level of each product.

---

## The entries

Each entry carries the Browser id, the **BYOC UUID** (`input.data.type = "byoc-<uuid>"`), coverage, cadence, what the product measures, and **every band with its meaning and units**. Band names appear nowhere in the Browser UI and assembling them by hand means visiting 185 doc pages — that is the whole reason this file exists.

**If you script against one of these**, paste its entry into your assistant first. Without the band list a model invents plausible names (`CLP`, `CLM` — neither exists on CDSE).

### Global, 52 product families

#### Bio-geophysical parameters › Evapotranspiration

##### Evapotranspiration 10-daily v1

`eta_global_300m_10daily_v1`  ·  BYOC `24fd5fde-b9db-44f1-a32b-e5dc3a0c5b9b`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/evapotranspiration/eta_global_300m_10daily_v1.html)  
global · 300m · 2025 - present

> The Evapotranspiration product group provides global actual evapotranspiration (ETA) estimates at 300 m spatial resolution with a frequency of 10-daily for ET, E and T and at a daily frequency for H and LE, combining outputs from two modelling frameworks and an Ensemble model.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `GFD` | Per pixel average gap-filling distance (in days) for cloudy pixels in a given dekad. Unit in days | days | `UINT8` | 0.0-60.0 | 1 | 0 |
| `FLAG` | Per pixel annotation flag indicating quality or other limitations | — | `UINT8` | — | — | — |
| `NOBS` | Per pixel number of cloud free observations in a given dekad. | — | `UINT8` | 0.0-11.0 | 1 | 0 |
| `E_STD` | Per pixel standard deviation between TSEB-PT and ETLook model E. Unit: mm/day | mm/day | `UINT8` | 0.0-20.0 | 1/10 | 0 |
| `T_STD` | Per pixel standard deviation between TSEB-PT and ETLook model T. Unit: mm/day | mm/day | `UINT8` | 0.0-20.0 | 1/10 | 0 |
| `ET_STD` | Per pixel standard deviation between TSEB-PT and ETLook model ET. Unit: mm/day | mm/day | `UINT8` | 0.0-20.0 | 1/10 | 0 |
| `E_ETLOOK` | Soil evaporation calculated by the ETLook model. Unit: mm/day | mm/day | `UINT8` | 0.0-20.0 | 1/10 | 0 |
| `E_TSEBPT` | Soil evaporation calculated by the TSEB-PT model. Unit: mm/day | mm/day | `UINT8` | 0.0-20.0 | 1/10 | 0 |
| `T_ETLOOK` | Canopy transpiration calculated by the ETLook model. Unit: mm/day | mm/day | `UINT8` | 0.0-20.0 | 1/10 | 0 |
| `T_TSEBPT` | Canopy transpiration calculated by the TSEB-PT model. Unit: mm/day | mm/day | `UINT8` | 0.0-20.0 | 1/10 | 0 |
| `ET_ETLOOK` | Actual evapotranspiration calculated by the ETLook model. Unit: mm/day | mm/day | `UINT8` | 0.0-20.0 | 1/10 | 0 |
| `ET_TSEBPT` | Actual evapotranspiration calculated by the TSEB-PT model. Unit: mm/day | mm/day | `UINT8` | 0.0-20.0 | 1/10 | 0 |
| `E_ENSEMBLE` | Soil evaporation calculated by the Ensemble model. Unit: mm/day | mm/day | `UINT8` | 0.0-20.0 | 1/10 | 0 |
| `T_ENSEMBLE` | Canopy transpiration calculated by the Ensemble model. Unit: mm/day | mm/day | `UINT8` | 0.0-20.0 | 1/10 | 0 |
| `ET_ENSEMBLE` | Actual evapotranspiration calculated by the Ensemble model. Unit: mm/day | mm/day | `UINT8` | 0.0-20.0 | 1/10 | 0 |

##### Heat Flux daily v1

`hf_global_300m_daily_v1`  ·  BYOC `5e16244f-3357-46c8-9ddc-28d182aec8e5`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/evapotranspiration/hf_global_300m_daily_v1.html)  
global · 300m · 2025 - present

> Provides latent and sensible heat fluxes with one auxiliary information. Estimates are provided for each Sentinel-3 overpass in near real time at global scale in the spatial resolution of about 300 m from November 2025 onwards in version 1.0.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `H_TSEBPT` | Sensible heat flux calculated by the TSEB-PT model. Unit: W/m² | W/m² | `INT16` | -100.0-1000.0 | 1 | 0 |
| `LE_TSEBPT` | Latent heat flux calculated by the TSEB-PT model. Unit: W/m² | W/m² | `INT16` | -100.0-1000.0 | 1 | 0 |

#### Bio-geophysical parameters › Snow

##### SCE daily v1

`sce_global_1km_daily_v1`  ·  BYOC `84c1669b-a51f-4193-bf9d-e470e46efea8`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/snow/snow-cover-extent/sce_global_1km_daily_v1.html)  
global · 1km · 2025 - present

> Provides for global land areas (excluding Antarctica) daily maps of the fraction of snow cover on ground (also in forested areas) per pixel in percentage (0% – 100%). The data is available in near real time with a pixel spacing of about 1 km and with the temporal extent from December 2025 to present.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `SCE` | Snow Cover Extent | % | `INT16` | 0.0-254.0 | 1 | -100 |
| `UNC` | Snow Cover Extent Uncertainty | % | `INT16` | 0.0-254.0 | 1 | -100 |

#### Bio-geophysical parameters › Temperature and reflectance

##### LST (TCI) 10-daily v1

`clms_global_lst_5km_v1_10daily-tci_geotiff`  ·  BYOC `2dd2d9e0-8f02-4adc-8b14-dea6c56e8d2b`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/temperature-and-reflectance/land-surface-temperature/lst-tci_global_5km_10daily_v1.html)  
global · 5km · 2017 - 2021

> Provides a statistical overview of the land surface temperature over each 10-day compositing period regardless of any specific hour and every geostationary sensor image pixel. The data are available at global scale in the spatial resolution of about 5 km and covers the period from January 2017 to January 2021.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `TCI` | Thermal Condition Index for the 10-day composite period | — | `INT16` | 0.0-1.0 | 1/10000 | 0 |
| `FRAC_VALID_OBS` | Fraction of valid observations | — | `INT16` | 0.0-1.0 | 1/100 | 0 |
| `MAX` | Maximum LST values observed during the 10-day compositing period | K | `INT16` | 203.15-353.15 | 1/100 | 273.15 |
| `MEDIAN` | Median LST values observed during the 10-day compositing period | K | `INT16` | 203.15-353.15 | 1/100 | 273.15 |
| `MIN` | Minimum LST values observed during the 10-day compositing period | K | `INT16` | 203.15-353.15 | 1/100 | 273.15 |

##### LST (TCI) 10-daily v2

`clms_global_lst_5km_v2_10daily-tci_geotiff`  ·  BYOC `d216f9f3-a7bd-45d6-bdd3-820f8223ebc4`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/temperature-and-reflectance/land-surface-temperature/lst-tci_global_5km_10daily_v2.html)  
global · 5km · 2021 - present

> Statistical overview of the land surface temperature over each 10-day compositing period

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `TCI` | Thermal Condition Index for the 10-day composite period | — | `INT16` | 0.0-1.0 | 1/10000 | 0 |
| `FRAC_VALID_OBS` | Fraction of valid observations | — | `INT16` | 0.0-1.0 | 1/100 | 0 |
| `MAX` | Maximum LST values observed during the 10-day compositing period | K | `INT16` | 203.15-353.15 | 1/100 | 273.15 |
| `MEDIAN` | Median LST values observed during the 10-day compositing period | K | `INT16` | 203.15-353.15 | 1/100 | 273.15 |
| `MIN` | Minimum LST values observed during the 10-day compositing period | K | `INT16` | 203.15-353.15 | 1/100 | 273.15 |

##### LST 3km hourly V3

`lst_global_3km_hourly_v3`  ·  BYOC `12225aec-26dd-4e2c-bbfd-994c253c1ba8`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/temperature-and-reflectance/land-surface-temperature/lst_global_3km_hourly_v3.html)  
global · 3km · 2018 - present

> Provides Land Surface Temperature estimates at global scale, at a spatial resolution of ~3 km. More information here.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `LST` | Land Surface Temperature [K]. | [K] | `INT16` | -203.15-353.15 | 1/100 | 273.15 |
| `ERRORBAR` | Error bar for LST [K]. | [K] | `INT16` | 0.0-50.0 | 1/100 | 0 |
| `TDELTA` | Time between the observation time and the reference time written in the output file name [min]. | [min] | `INT16` | -30.0-30.0 | 1 | 0 |
| `QFLAG` |  | — | `INT16` | 0.0-60.0 | 1 | 0 |

##### LST Daily Cycle 10-daily v1

`clms_global_lst_5km_v1_10daily-daily-cycle_geotiff`  ·  BYOC `3069a818-ac7f-4b8d-9369-22f91887fd02`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/temperature-and-reflectance/land-surface-temperature/lst-daily-cycle_global_5km_10daily_v1.html)  
global · 5km · 2017-01 - 2021-01

> Provides a statistical overview of the land surface temperature daily cycle for each 10-day compositing period and every geostationary sensor image pixel.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `MEDIAN` | Median LST values observed during the 10-day compositing period | K | `INT16` | 203.15-353.15 | 1/100 | 273.15 |
| `FOBS` | Fraction of valid observations | — | `INT16` | 0.0-1.0 | 1/100 | 0 |
| `MIN` | Minimum LST values observed during the 10-day compositing period | K | `INT16` | 203.15-353.15 | 1/100 | 273.15 |
| `MAX` | Maximum LST values observed during the 10-day compositing period | K | `INT16` | 203.15-353.15 | 1/100 | 273.15 |

##### LST Daily Cycle 10-daily v2

`clms_global_lst_5km_v2_10daily-daily-cycle_geotiff`  ·  BYOC `07aa0606-7c61-41a2-9c37-7272e9d3d934`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/temperature-and-reflectance/land-surface-temperature/lst-daily-cycle_global_5km_10daily_v2.html)  
global · 5km · 2021 - present

> Provides a statistical overview of the land surface temperature daily cycle for each 10-day compositing period and every geostationary sensor image pixel.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `MEDIAN` | Median LST values observed during the 10-day compositing period | K | `INT16` | 203.15-353.15 | 1/100 | 273.15 |
| `FOBS` | Fraction of valid observations | — | `INT16` | 0.0-1.0 | 1/100 | 0 |
| `MIN` | Minimum LST values observed during the 10-day compositing period | K | `INT16` | 203.15-353.15 | 1/100 | 273.15 |
| `MAX` | Maximum LST values observed during the 10-day compositing period | K | `INT16` | 203.15-353.15 | 1/100 | 273.15 |

##### LST Daily Cycle 3km 10-daily V3

`lst-daily-cycle_global_3km_10daily_v3`  ·  BYOC `7f175dfe-eee2-4c4c-93a6-db8072e76a44`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/temperature-and-reflectance/land-surface-temperature/lst-daily-cycle_global_3km_10daily_v3.html)  
global · 3km · 2018 - present

> Provides Land Surface Temperature estimates at global scale, at a spatial resolution of ~3 km. More information here.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `MIN` | Minimum of Land Surface Temperature observed during the 10-days period, per hour. | K | `INT16` | -203.15-353.15 | 1/100 | 273.15 |
| `MEDIAN` | Median of Land Surface Temperature observed during the 10-days period, per hour. | K | `INT16` | -203.15-353.15 | 1/100 | 273.15 |
| `MAX` | Maximum of Land Surface Temperature observed during the 10-days period, per hour. | K | `INT16` | -203.15-353.15 | 1/100 | 273.15 |
| `FOBS` | Fraction of valid observations, per hour. | — | `INT16` | 0.0-1.0 | 1/100 | 0 |

##### LST TCI 3km 10-daily V3

`lst-tci_global_3km_10daily_v3`  ·  BYOC `21ee9e5d-bfca-4553-98d8-62f9fa07eedf`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/temperature-and-reflectance/land-surface-temperature/lst-tci_global_3km_10daily_v3.html)  
global · 3km · 2018 - present

> Provides Land Surface Temperature estimates at global scale, at a spatial resolution of ~3 km. More information here.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `MEDIAN` | Median of Land Surface Temperature observed during the 10-days period, regardless the time of the day. | [K] | `INT16` | -203.15-353.15 | 1/100 | 273.15 |
| `TCI` | Thermal Condition Index for the compositing period. | — | `INT16` | 0.0-1.0 | 1/10000 | 0 |
| `FOBS` | Fraction of valid observations. | — | `INT16` | 0.0-1.0 | 1/100 | 0 |
| `MIN` | Minimum of Land Surface Temperature observed during the 10-days period, regardless the time of the day. | [K] | `INT16` | -203.15-353.15 | 1/100 | 273.15 |
| `MAX` | Maximum of Land Surface Temperature observed during the 10-days period, regardless the time of the day. | [K] | `INT16` | -203.15-353.15 | 1/100 | 273.15 |

##### LST hourly v1

`clms_global_lst_5km_v1_hourly_geotiff`  ·  BYOC `2950f0fb-22ab-4ed7-98f9-a90ac841092b`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/temperature-and-reflectance/land-surface-temperature/lst_global_5km_hourly_v1.html)  
global · 5km · 2010 - 2021

> Hourly land surface temperature from geostationary sensors observations

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `LST` | Land Surface Temperature | K | `INT16` | 203.15-353.15 | 1/100 | 273.15 |
| `ERRORBAR` | Error bar for LST | K | `INT16` | 0.0-50.0 | 1/100 | 0 |
| `PPP` | Percentage of processed pixels used in the data fusion step | % | `INT16` | 0.0-100.0 | 1 | 0 |
| `QFLAG` | Bitwise quality information | — | `INT16` | 0.0-64.0 | 1 | 0 |
| `TDELTA` | Time between the pixel observation time and the reference time | Minutes | `INT16` | -30.0-30.0 | 1 | 0 |

##### LST hourly v2

`clms_global_lst_5km_v2_hourly_geotiff`  ·  BYOC `41dad7d0-e730-45fe-a974-a9c718fd08af`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/temperature-and-reflectance/land-surface-temperature/lst_global_5km_hourly_v2.html)  
global · 5km · 2021 - present

> Hourly land surface temperature from geostationary sensors observations

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `LST` | Land Surface Temperature | K | `INT16` | 203.15-353.15 | 1/100 | 273.15 |
| `ERRORBAR` | Error bar for LST | K | `INT16` | 0.0-50.0 | 1/100 | 0 |
| `PPP` | Percentage of processed pixels used in the data fusion step | % | `INT16` | 0.0-100.0 | 1 | 0 |
| `QFLAG` | Bitwise quality information | — | `INT16` | 0.0-64.0 | 1 | 0 |
| `TDELTA` | Time between the pixel observation time and the reference time | Minutes | `INT16` | -30.0-30.0 | 1 | 0 |

##### Lake Surface Water Temperature 10-daily, Near Real Time v1

`lswt_nrt_global_1km_10daily_v1`  ·  BYOC `401ca642-a169-4783-b1cf-cbd33e98eccb`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/temperature-and-reflectance/lake-surface-water-temperature/lswt-nrt_global_1km_10daily_v1.html)  
global · 1km · 2016 - present

> Provides the temperature of the water at the lake surface. The near real time observations (every 10 days) are available at global scale at spatial resolution of ~1 km and with the temporal extent from 2016 to present.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `LSWT` | Lake surface skin temperature, weighted average over the aggregation period. | Kelvin | `INT16` | -200.0-5000.0 | 0.01 | 273.15 |
| `UNC` | Uncertainties on LSWT | Kelvin | `INT16` | 0.0-10000.0 | 0.001 | 0 |
| `STDEV` | Standard deviation of the LSWT observations within the aggregation time period | Kelvin | `INT16` | — | 0.001 | 0 |
| `NOBS` | Number of LSWT observations contributing to the average | — | `INT8` | 0.0-21.0 | 1 | 0 |
| `QLEVEL` | Quality level | Quality flags: 0=no_data, 1=bad_data, 2=worst_quality, 3=low_quality, 4=acceptable_quality, 5=best_quality | `INT8` | — | 1 | 0 |
| `TOBS` | Bitwise observation time | Bit flags for days 1-11 within dekad | `INT16` | — | 1 | 0 |

#### Bio-geophysical parameters › Vegetation

##### Burnt Area daily v3.1

`clms_global_ba_300m_v3_daily_geotiff`  ·  BYOC `c698beab-cdb7-4b41-857a-63fc9a8d8c07`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/vegetation/burnt-area/ba_global_300m_daily_v3.html)  
global · 300m · 2023 - present

> Maps burn scars, surfaces which have been sufficiently affected by fire to display significant changes in the vegetation cover (destruction of dry material, reduction or loss of green material) and in the ground surface (temporarily darker because of ash).

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `day_of_burn` | Burned area | Day of burn in the year | `INT16` | 0.0-366.0 | 1 | 0 |

##### Burnt Area daily v4

`ba_global_300m_daily_v4`  ·  BYOC `162ee729-86a7-45bc-9cfe-c01f718e3216`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/vegetation/burnt-area/ba_global_300m_daily_v4.html)  
global · 300m · 2025 - present

> Maps burn scars, surfaces which have been sufficiently affected by fire to display significant changes in the vegetation cover (destruction of dry material, reduction or loss of green material) and in the ground surface (temporarily darker because of ash).

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `BF` | Fraction of pixel surface affected by fire at the day of the burn detection | — | `INT16` | 0.0-1.0 | 1/1000 | 0 |
| `CP` | Probability that the burn detection corresponds to an actual burn | — | `INT16` | 0.0-1.0 | 1/1000 | 0 |
| `DOB` | Day of burn in year (1-366), no burn (0) or flag (<0) | day | `INT16` | 0.0-366.0 | 1 | 0 |
| `LFP` | Probability that the fractional burned area is above 0.1 | — | `INT16` | 0.0-1.0 | 1/1000 | 0 |

##### Burnt Area monthly - version 3.1

`clms_global_ba_300m_v3_monthly_geotiff`  ·  BYOC `16f8b33d-9b6c-440f-bc8c-ee7b1ccb1009`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/vegetation/burnt-area/ba_global_300m_monthly_v3.html)  
global · 300m · 2019 - present

> Maps burn scars, surfaces which have been sufficiently affected by fire to display significant changes in the vegetation cover (destruction of dry material, reduction or loss of green material) and in the ground surface (temporarily darker because of ash).

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `day_of_burn` | Burned area | Day of burn in the year | `INT16` | 0.0-366.0 | 1 | 0 |

##### Burnt Area monthly - version 4

`ba_global_300m_monthly_v4`  ·  BYOC `b8b617c6-182f-427e-a86c-23fc36ac6098`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/vegetation/burnt-area/ba_global_300m_monthly_v4.html)  
global · 300m · 2018 - present

> Maps burn scars, surfaces which have been sufficiently affected by fire to display significant changes in the vegetation cover (destruction of dry material, reduction or loss of green material) and in the ground surface (temporarily darker because of ash).

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `BF` | Fraction of pixel surface affected by fire at the day of the burn detection | — | `INT16` | 0.0-1.0 | 1/1000 | 0 |
| `CP` | Probability that the burn detection corresponds to an actual burn | — | `INT16` | 0.0-1.0 | 1/1000 | 0 |
| `DOB` | Day of burn in year (1-366), no burn (0) or flag (<0) | day | `INT16` | 0.0-366.0 | 1 | 0 |
| `LFP` | Probability that the fractional burned area is above 0.1 | — | `INT16` | 0.0-1.0 | 1/1000 | 0 |

##### DMP 10-daily v2

`clms_global_dmp_1km_v2_10daily_geotiff`  
**BYOC collection ids — one per RT level, they are different collections:**  
**no-RT** `12a01750-273b-4ed0-bd8d-da317cdd802a` · **RT0** `431e908c-90c3-4d0f-9814-b2e2b815c6b0` · **RT1** `3f2a6a77-5065-4a3a-be79-97188adabec1` · **RT2** `ab5ef5c2-6b77-437b-9a59-a1a26e8871a7` · **RT6** `e37b5696-d158-41d9-b077-05c79768c76d`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/vegetation/dry-gross-dry-matter-productivity/dmp_global_1km_10daily_v2.html)  
global · 1km · 1999 - 2020

> DMP represents the overall growth rate or dry biomass increase of the vegetation and is directly related to ecosystem Net Primary Production (NPP), however with units customized for agro-statistical purposes (kg/ha/day). Every 10-days estimates are available at global scale in the spatial resolution of about 1km and with the temporal extent from 1999 to June 2020.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `DMP` | Dry Matter Productivity | kg/ha/day | `INT16` | 0.0-327.67 | 1/100 | 0 |
| `QFLAG` | Bitwise quality flag | — | `UINT8` | — | 1 | 0 |

##### DMP 10-daily v2

**Each RT level is a separate Browser layer *and* a separate BYOC collection.** ⚠️ There is **no bare `dmp_global_300m_10daily_v2` id** — you must pick a level.

| RT | Browser id | BYOC collection id |
|---|---|---|
| RT0 | `dmp_global_300m_10daily_v2_rt0` | `de3e1b9c-58c4-457a-a3e7-917ec20fc29b` |
| RT1 | `dmp_global_300m_10daily_v2_rt1` | `9d27c360-674c-44e2-b846-4be236c39c7e` |
| RT2 | `dmp_global_300m_10daily_v2_rt2` | `d8bbfd31-82da-4a02-bc1c-8f34387954f7` |
| RT6 | `dmp_global_300m_10daily_v2_rt6` | `d888548d-2c56-47ed-847c-17c654e61a03` |
global · 300m · 2014 - present · RT0, RT1, RT2, RT6

> Provides information about the overall growth rate, or net dry biomass increase, of the vegetation. It is equivalent to Net Primary Production (NPP) but expressed in kg of dry matter per hectare and per day. Every 10-days, estimates are available at global scale, at a spatial resolution of ~300 m, from January 2014 to the present.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `DMP` | Dry Matter Productivity (kg DM/ha/day) | kg/ha/day | `INT16` | 0.0-327.67 | 1/100 | 0 |
| `QFLAG` | Bitwise quality flag | — | `UINT8` | — | 1 | 0 |

##### FAPAR 10-daily v1

`clms_global_fapar_300m_v1_10daily_geotiff`  
**BYOC collection ids — one per RT level, they are different collections:**  
**no-RT** `302c25ab-3d8c-4783-8123-9a231660e98a` · **RT0** `4dcb63e9-9527-4293-a3b8-74b763887d04` · **RT1** `b4e696d6-d622-4157-871b-99b599a1f6cc` · **RT2** `6492eee5-ea96-4cef-a11b-a8aaa7b6a180` · **RT6** `453f68c6-f2a9-462c-8bc6-74343fc4f638`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/vegetation/vegetation-properties/fapar_global_300m_10daily_v1.html)  
global · 300m · 2014 - present

> Quantifies the fraction of the solar radiation absorbed by live plants for photosynthesis. Every 10-days estimates are available in near real time at global scale in the spatial resolution of about 300 m from January 2014 to June 2020 based upon PROBA-V data with version 1.0 and from July 2020 onwards based upon Sentinel-3/OLCI data with version 1.1.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `FAPAR` | Fraction of Absorbed Photosynthetically Active Radiation | — | `UINT8` | 0.0-0.94 | 1/250 | 0 |
| `RMSE` | RMSE on FAPAR | — | `UINT8` | 0.0-0.94 | 1/250 | 0 |
| `QFLAG` | Quality flag | — | `UINT8` | — | 1 | 0 |
| `NOBS` | Number of available valid instantaneous estimates in the compositing window | — | `UINT8` | 0.0-40.0 | 1 | 0 |
| `LENGTH_BEFORE` | Length in days of semi-period before D | — | `UINT8` | 15.0-210.0 | 1 | 0 |
| `LENGTH_AFTER` | Length in days of semi-period after D | — | `UINT8` | 0.0-60.0 | 1 | 0 |

##### FAPAR 10-daily v2

`clms_global_fapar_1km_v2_10daily_geotiff`  
**BYOC collection ids — one per RT level, they are different collections:**  
**no-RT** `288befb5-6ce6-4aae-9fb8-e6e4531216a1` · **RT0** `c59b1cb0-50ef-4737-a863-463c1056c66c` · **RT1** `e9a0a9ec-5614-4747-bcdb-e4942d5af0b2` · **RT2** `8bf7f8a0-09d5-4167-a53b-9e3f6676a488` · **RT6** `990a6aca-4a63-4d47-94e2-6b948af1b603`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/vegetation/vegetation-properties/fapar_global_1km_10daily_v2.html)  
global · 1km · 1999 - 2020

> FAPAR quantifies the fraction of the solar radiation absorbed by live plants for photosynthesis. Every 10-days estimates are available at global scale in the spatial resolution of about 1 km covering the period from 1999 to June 2020 from SPOT/VEGETATION and PROBA-V data.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `FAPAR` | Fraction of Absorbed PAR | — | `UINT8` | 0.0-0.94 | 1/250 | 0 |
| `RMSE` | Uncertainty on the FAPAR | — | `UINT8` | 0.0-0.94 | 1/250 | 0 |
| `QFLAG` | Quality flag | — | `UINT16` | — | 1 | 0 |
| `NOBS` | Number of valid observations during the synthesis period | — | `UINT8` | 0.0-120.0 | 1 | 0 |
| `LENGTH_BEFORE` | Length in days of the semi-period before the dekadal date of the compositing window | — | `UINT8` | 5.0-60.0 | 1 | 0 |
| `LENGTH_AFTER` | Length in days of the semi-period after the dekadal date of the compositing window | — | `UINT8` | 5.0-60.0 | 1 | 0 |

##### FCOVER 10-daily v1

`clms_global_fcover_300m_v1_10daily_geotiff`  
**BYOC collection ids — one per RT level, they are different collections:**  
**no-RT** `c6ba4fc2-7e42-4cae-9795-c6227424b917` · **RT0** `9feb4b1a-831f-4380-aca9-e423c238d136` · **RT1** `5bcd67b1-fe83-49ed-babc-d08048cb45a2` · **RT2** `8785d93b-a8bb-4e00-9cf6-8fb18fea11ef` · **RT6** `934fe7d4-d90a-48e0-9c7d-691519c946c6`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/vegetation/vegetation-properties/fcover_global_300m_10daily_v1.html)  
global · 300m · 2014 - present

> FCOVER corresponds to the fraction of ground covered by green vegetation. It quantifies the spatial extent of the vegetation. Every 10-days estimates are available at global scale in the spatial resolution of about 1 km covering the period from 1999 to June 2020 from SPOT/VEGETATION and PROBA-V data.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `FCOVER` | Fraction of green vegetation cover | — | `UINT8` | 0.0-1.0 | 1/250 | 0 |
| `RMSE` | RMSE on FCover | — | `UINT8` | 0.0-1.0 | 1/250 | 0 |
| `QFLAG` | Quality flag | — | `UINT8` | — | 1 | 0 |
| `NOBS` | Number of available valid instantaneous estimates in the compositing window | — | `UINT8` | 0.0-60.0 | 1 | 0 |
| `LENGTH_BEFORE` | Length in days of semi-period before D | — | `UINT8` | 15.0-210.0 | 1 | 0 |
| `LENGTH_AFTER` | Length in days of semi-period after D | — | `UINT8` | 0.0-60.0 | 1 | 0 |

##### FCOVER 10-daily v2

`clms_global_fcover_1km_v2_10daily_geotiff`  
**BYOC collection ids — one per RT level, they are different collections:**  
**no-RT** `44f54dfc-a372-4a22-988b-4b054880bb2a` · **RT0** `8f6a4b38-934c-4363-ac20-8427f20760c0` · **RT1** `3e88055a-b8c3-4c68-acc6-4b93509b1f14` · **RT2** `80fc6bcf-bcdc-4ede-94f8-b47d096d734c` · **RT6** `c58a4f07-86b9-4e62-b955-808cdc820599`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/vegetation/vegetation-properties/fcover_global_1km_10daily_v2.html)  
global · 1km · 1999 - 2020

> FCOVER corresponds to the fraction of ground covered by green vegetation. It quantifies the spatial extent of the vegetation. Every 10-days estimates are available at global scale in the spatial resolution of about 1 km covering the period from 1999 to June 2020 from SPOT/VEGETATION and PROBA-V data.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `FCOVER` | Fraction of green vegetation cover | — | `UINT8` | 0.0-1.0 | 1/250 | 0 |
| `RMSE` | Uncertainty on the FCover | — | `UINT8` | 0.0-1.0 | 1/250 | 0 |
| `QFLAG` | Quality flag | — | `UINT16` | — | 1 | 0 |
| `NOBS` | Number of valid observations during the synthesis period | — | `UINT8` | 0.0-120.0 | 1 | 0 |
| `LENGTH_BEFORE` | Length in days of the semi-period before the dekadal date of the compositing window | — | `UINT8` | 5.0-60.0 | 1 | 0 |
| `LENGTH_AFTER` | Length in days of the semi-period after the dekadal date of the compositing window | — | `UINT8` | 5.0-60.0 | 1 | 0 |

##### Fraction of Green Vegetation Cover 10-daily v2

**Each RT level is a separate Browser layer *and* a separate BYOC collection.** ⚠️ There is **no bare `fcover_global_300m_10daily_v2` id** — you must pick a level.

| RT | Browser id | BYOC collection id |
|---|---|---|
| RT0 | `fcover_global_300m_10daily_v2_rt0` | `4fea1f4f-7438-4e19-9890-2674347a278d` |
| RT1 | `fcover_global_300m_10daily_v2_rt1` | `b5617f5b-69a0-4054-a14b-d831fd43babf` |
| RT2 | `fcover_global_300m_10daily_v2_rt2` | `47f6a6cc-0a44-4561-a6dc-05433be56d07` |
| RT6 | `fcover_global_300m_10daily_v2_rt6` | `23bfb3d0-a265-4e3a-8203-23e4f09de82c` |
global · 300m · 2014 - present · RT0, RT1, RT2, RT6

> Provides information about the fraction of ground covered by green vegetation. Every 10-days estimates are available at global scale in the spatial resolution of ~ 300 m from January 2014 to the present.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `FCOVER` | Fraction of Green Vegetation Cover | — | `UINT8` | 0.0-1.0 | 1/250 | 0 |
| `RMSE` | Root Mean Square Error on FCOVER | — | `UINT8` | 0.0-1.0 | 1/250 | 0 |
| `NOBS` | Number of available valid instantaneous FCOVER | — | `UINT8` | 0.0-60.0 | 1 | 0 |
| `LBEFORE` | Length of the semi-period before the date [days] | days | `UINT8` | 0.0-210.0 | 1 | 0 |
| `LAFTER` | Length of the semi-period after the date [days] | days | `UINT8` | 0.0-60.0 | 1 | 0 |
| `QFLAG` | Bitwise quality flag | Quality Flag on Fraction of green Vegetation Cover | `UINT8` | 0.0-254.0 | 1 | 0 |

##### GDMP 10-daily v2

`clms_global_gdmp_1km_v2_10daily_geotiff`  
**BYOC collection ids — one per RT level, they are different collections:**  
**no-RT** `7bf3dc12-3662-4844-ac8f-cc120710731a` · **RT0** `f35460ee-178b-404f-85d5-0349c9ec6e7c` · **RT1** `c8ce04cf-5bca-41a3-b90c-8904e9655ce4` · **RT2** `075d7c80-8170-4f65-b7cf-39976219e74a` · **RT6** `f20cd28d-6d06-430e-8deb-5abce20a6700`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/vegetation/dry-gross-dry-matter-productivity/gdmp_global_1km_10daily_v2.html)  
global · 1km · 1999 - 2020

> GDMP is equivalent to Gross Primary Production (GPP). Every 10-days estimates are available at global scale in the spatial resolution of about 1km and with the temporal extent from 1999 to June 2020.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `GDMP` | Gross Dry Matter Productivity | kg/ha/day | `INT16` | 0.0-655.34 | 1/50 | 0 |
| `QFLAG` | Bitwise quality flag | — | `UINT8` | — | 1 | 0 |

##### GDMP 10-daily v2

**Each RT level is a separate Browser layer *and* a separate BYOC collection.** ⚠️ There is **no bare `gdmp_global_300m_10daily_v2` id** — you must pick a level.

| RT | Browser id | BYOC collection id |
|---|---|---|
| RT0 | `gdmp_global_300m_10daily_v2_rt0` | `b30949ba-bde1-4ac8-adf7-1126b9473b51` |
| RT1 | `gdmp_global_300m_10daily_v2_rt1` | `2f76a954-18ff-4207-ab17-0ee6f78f7a76` |
| RT2 | `gdmp_global_300m_10daily_v2_rt2` | `949eecb5-7592-4812-9c76-5f8995626358` |
| RT6 | `gdmp_global_300m_10daily_v2_rt6` | `bfc9927a-9cb9-4c15-bb7e-4cd85c24b008` |
global · 300m · 2014 - present · RT0, RT1, RT2, RT6

> Provides information about the total amount of dry matter produced by land plants per unit time through photosynthesis. It is equivalent to Gross Primary Production (GPP) but expressed in kg of dry matter per hectare and per day. Every 10-days estimates are available at global scale, at a spatial resolution of ~ 300 m, from January 2014 to the present.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `GDMP` | Gross Dry Matter Productivity | kg/ha/day | `INT16` | 0.0-655.34 | 1/50 | 0 |
| `QFLAG` | Bitwise quality flag | — | `UINT8` | — | 1 | 0 |

##### GPP 10-daily v2

**Each RT level is a separate Browser layer *and* a separate BYOC collection.** ⚠️ There is **no bare `gpp_global_300m_10daily_v2` id** — you must pick a level.

| RT | Browser id | BYOC collection id |
|---|---|---|
| RT0 | `gpp_global_300m_10daily_v2_rt0` | `eacf6c34-a3db-4b3b-bdf9-0feba8eed996` |
| RT1 | `gpp_global_300m_10daily_v2_rt1` | `f37f3647-c076-4dc1-9b0e-3ad129521bf4` |
| RT2 | `gpp_global_300m_10daily_v2_rt2` | `42d86587-3a2b-4394-8588-7d5e0238574d` |
| RT6 | `gpp_global_300m_10daily_v2_rt6` | `7e2d31f2-80ef-4d9c-bd81-da59e40b0eea` |
global · 300m · 2014 - present · RT0, RT1, RT2, RT6

> Provides information about the total amount of carbon compounds produced by photosynthesis of plants in an ecosystem in a given period of time, expressed in gC/m²/day. Every 10-days, estimates are available at global scale, at a spatial resolution of ~ 300 m, from January 2014 to the present.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `GPP` | Gross Primary Production value | gC/m²/day | `INT16` | 0.0-32.767 | 1/1000 | 0 |
| `QFLAG` | Quality flag indicator | — | `UINT8` | — | 1 | 0 |

##### LAI 10-daily v1

`clms_global_lai_300m_v1_10daily_geotiff`  
**BYOC collection ids — one per RT level, they are different collections:**  
**no-RT** `b6317fa9-c341-4c7f-a81f-24615f57c868` · **RT0** `6c90d3aa-4e57-4f08-a837-23ba6df3429a` · **RT1** `2cb83160-105c-4072-9fb3-51e47ddc9f1a` · **RT2** `8d7a4caa-b58c-4658-9aa0-ca155b670662` · **RT6** `559b2871-ddbd-41f9-8ab0-5242a454e411`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/vegetation/vegetation-properties/lai_global_300m_10daily_v1.html)  
global · 300m · 2014 - present

> Defined as half the total area of green elements of the canopy per unit horizontal ground area. Every 10-days estimates are available in near real time at global scale in the spatial resolution of about 300 m from January 2014 to June 2020 based upon PROBA-V data with version 1.0 and from July 2020 onwards based upon Sentinel-3/OLCI data with version 1.1.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `LAI` | Leaf Area Index | — | `UINT8` | 0.0-7.0 | 1/30 | 0 |
| `LENGTH_BEFORE` | Length in days of semi-period before D | — | `UINT8` | 15.0-210.0 | 1 | 0 |
| `LENGTH_AFTER` | Length in days of semi-period after D | — | `UINT8` | 0.0-60.0 | 1 | 0 |
| `NOBS` | Number of available valid instantaneous estimates in the compositing window | — | `UINT8` | 0.0-60.0 | 1 | 0 |
| `RMSE` | RMSE on LAI | — | `UINT8` | 0.0-7.0 | 1/30 | 0 |
| `QFLAG` | Quality Flag | — | `UINT8` | — | 1 | 0 |

##### LAI 10-daily v2

`clms_global_lai_1km_v2_10daily_geotiff`  
**BYOC collection ids — one per RT level, they are different collections:**  
**no-RT** `4e9b1791-0529-4cbe-82dd-ccbd1d346f60` · **RT0** `f134123b-9723-45f0-965e-82c2554e4a92` · **RT1** `e8416d4f-ef2a-4ae0-ba1b-0ae21f669871` · **RT2** `44920340-5ca8-41be-93e0-4f0f1f85c646` · **RT6** `2121b136-37fe-4b24-8791-ff569ff39d4a`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/vegetation/vegetation-properties/lai_global_1km_10daily_v2.html)  
global · 1km · 1999 - 2020

> Defined as half the total area of green elements of the canopy per unit horizontal ground area. Every 10-days estimates are available in near real time at global scale in the spatial resolution of about 300 m from January 2014 to June 2020 based upon PROBA-V data with version 1.0 and from July 2020 onwards based upon Sentinel-3/OLCI data with version 1.1. More information here.*

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `LAI` | Leaf Area Index | — | `UINT8` | 0.0-7.0 | 1/30 | 0 |
| `RMSE` | Uncertainty on the LAI | — | `UINT8` | 0.0-7.0 | 1/30 | 0 |
| `QFLAG` | Quality flag | — | `UINT16` | — | 1 | 0 |
| `NOBS` | Number of valid observations during the synthesis period | — | `UINT8` | 0.0-120.0 | 1 | 0 |
| `LENGTH_BEFORE` | Length in days of the semi-period before the dekadal date of the compositing window | — | `UINT8` | 5.0-60.0 | 1 | 0 |
| `LENGTH_AFTER` | Length in days of the semi-period after the dekadal date of the compositing window | — | `UINT8` | 5.0-60.0 | 1 | 0 |

##### LSP 300m Yearly V1

`clms_global_lsp_300m_v1_yearly_geotiff`  ·  BYOC `3c49e431-5d28-4920-a6ef-684fc7617df6`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/vegetation/vegetation-phenology-and-productivity-parameters/lsp_global_300m_yearly_v1.html)  
global · 300m · 2023 - 2024

> Land Surface Phenology (LSP) is the term for land surface vegetation phenology estimated from remotely sensed data. It involves the analysis of time series of vegetation indices, which provide quantitative measures of green biomass and photosynthetic activity. LSP is an invaluable indicator in ecosystem studies and climate research.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `TPROD_S2` | Provides the growing season integral computed as the time-integrated Plant Phenology Index values between the dates of the season start and end. | m2 × m-2 × day | `INT16` | 0.0-2000.0 | 1 | 0 |
| `LENGTH_S2` | Provides the number of days between the start and end dates of the vegetation growing season. | Day | `INT16` | 0.0-730.0 | 1 | 0 |
| `SOSV_S2` | Provides the value of the Plant Phenology Index at the start of the vegetation growing season. | PPI unit m2 × m-2 | `INT16` | 0.0-5000.0 | 1/1000 | 0 |
| `RSLOPE_S1` | Provides the rate of change in the values of the Plant Phenology Index at the day when the vegetation growing season ends. | m2 × m-2 × day-1 | `INT16` | -1000.0-1000.0 | 1/1000 | 0 |
| `LENGTH_S1` | Provides the number of days between the start and end dates of the vegetation growing season. | Day | `INT16` | 0.0-730.0 | 1 | 0 |
| `LSLOPE_S2` | Provides the rate of change in the values of the Plant Phenology Index at the day when the vegetation growing season starts. | m2 × m-2 × day-1 | `INT16` | -1000.0-1000.0 | 1/1000 | 0 |
| `AMPL_S2` | Provides the difference between the maximum and minimum Plant Phenology Index values reached during the season. | PPI unit m2 × m-2 | `INT16` | 0.0-5000.0 | 1/1000 | 0 |
| `QA_S2` | Indicates the quality of the global Vegetation Phenology and Productivity Parameters, in the form of a confidence level. | — | `UINT8` | — | 1 | 0 |
| `SPROD_S1` | Provides the growing season integral computed as the time-integrated Plant Phenology Index values between the dates of the season start and end, minus their base level value. | m2 × m-2 × day | `INT16` | 0.0-2000.0 | 1 | 0 |
| `LSLOPE_S1` | Provides the rate of change in the values of the Plant Phenology Index at the day when the vegetation growing season starts. | m2 × m-2 × day-1 | `INT16` | -1000.0-1000.0 | 1/1000 | 0 |
| `QA_S1` | Indicates the quality of the global Vegetation Phenology and Productivity Parameters, in the form of a confidence level. | — | `UINT8` | — | 1 | 0 |
| `EOSD_S2` | Provides the day of the year when the vegetation growing season ends in the time profile of the Plant Phenology Index. | Day-Of-Year | `INT16` | 0.0-730.0 | 1 | 0 |
| `MAXV_S2` | Provides the maximum (peak) value that the Plant Phenology Index reaches during the vegetation growing season. | PPI unit m2 × m-2 | `INT16` | 0.0-5000.0 | 1/1000 | 0 |
| `MAXD_S2` | Provides the day of the year in the vegetation growing season when the maximum Plant Phenology Index value is reached. | Day-Of-Year | `INT16` | 0.0-366.0 | 1 | 0 |
| `MINV_S2` | Provides the average Plant Phenology Index value of the minima on left and right sides of each season. | PPI unit m2 × m-2 | `INT16` | 0.0-5000.0 | 1/1000 | 0 |
| `EOSV_S2` | Provides the value of the Plant Phenology Index at the end of the vegetation growing season. | PPI unit m2 × m-2 | `INT16` | 0.0-5000.0 | 1/1000 | 0 |
| `SOSD_S2` | Provides the day of the year when the vegetation growing season starts in the time profile of the Plant Phenology Index. | Day-Of-Year | `INT16` | -365.0-365.0 | 1 | 0 |
| `SOSD_S1` | Provides the day of the year when the vegetation growing season starts in the time profile of the Plant Phenology Index. | Day-Of-Year | `INT16` | -365.0-365.0 | 1 | 0 |
| `EOSD_S1` | Provides the day of the year when the vegetation growing season ends in the time profile of the Plant Phenology Index. | Day-Of-Year | `INT16` | 0.0-730.0 | 1 | 0 |
| `RSLOPE_S2` | Provides the rate of change in the values of the Plant Phenology Index at the day when the vegetation growing season ends. | m2 × m-2 × day-1 | `INT16` | -1000.0-1000.0 | 1/1000 | 0 |
| `SOSV_S1` | Provides the value of the Plant Phenology Index at the start of the vegetation growing season. | PPI unit m2 × m-2 | `INT16` | 0.0-5000.0 | 1/1000 | 0 |
| `SPROD_S2` | Provides the growing season integral computed as the time-integrated Plant Phenology Index values between the dates of the season start and end, minus their base level value. | m2 × m-2 × day | `INT16` | 0.0-2000.0 | 1 | 0 |
| `TPROD_S1` | Provides the growing season integral computed as the time-integrated Plant Phenology Index values between the dates of the season start and end. | m2 × m-2 × day | `INT16` | 0.0-2000.0 | 1 | 0 |
| `MAXD_S1` | Provides the day of the year in the vegetation growing season when the maximum Plant Phenology Index value is reached. | Day-Of-Year | `INT16` | 0.0-366.0 | 1 | 0 |
| `MINV_S1` | Provides the average Plant Phenology Index value of the minima on left and right sides of each season. | PPI unit m2 × m-2 | `INT16` | 0.0-5000.0 | 1/1000 | 0 |
| `EOSV_S1` | Provides the value of the Plant Phenology Index at the end of the vegetation growing season. | PPI unit m2 × m-2 | `INT16` | 0.0-5000.0 | 1 | 0 |
| `MAXV_S1` | Provides the maximum (peak) value that the Plant Phenology Index reaches during the vegetation growing season. | PPI unit m2 × m-2 | `INT16` | 0.0-5000.0 | 1/1000 | 0 |
| `AMPL_S1` | Provides the difference between the maximum and minimum Plant Phenology Index values reached during the season. | PPI unit m2 × m-2 | `INT16` | 0.0-5000.0 | 1/1000 | 0 |

##### LSP 300m Yearly V2

`clms_global_lsp_300m_v2_yearly_geotiff`  ·  BYOC `e96968cf-34f9-42e4-993e-ed312cd6ca05`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/vegetation/vegetation-phenology-and-productivity-parameters/lsp_global_300m_yearly_v2.html)  
global · 300m · 2014 - present

> Describes the seasonal growth patterns of vegetated land surface. Provides 13 phenology metrics for up to two growing seasons per year.  Annual estimates are available globally at a spatial resolution of about 300 m, from 2014 to the present. More information here.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `TPROD_S1` | Growing season integral computed as the time-integrated Plant Phenology Index values between the dates of the season start and end. | [m². day/m²] | `INT16` | 0.0-2000.0 | 1 | 0 |
| `TPROD_S2` | Growing season integral computed as the time-integrated Plant Phenology Index values between the dates of the season start and end. | [m².day/m²] | `INT16` | 0.0-730.0 | 1 | 0 |
| `SPROD_S1` | Growing season integral computed as the time-integrated Plant Phenology Index values between the dates of the season start and end minus their base level value. | [m².day/m²] | `INT16` | 0.0-2000.0 | 1 | 0 |
| `SPROD_S2` | Growing season integral computed as the time-integrated Plant Phenology Index values between the dates of the season start and end minus their base level value. | [m².day/m²] | `INT16` | 0.0-2000.0 | 1 | 0 |
| `SOSD_S1` | Day of the year when the vegetation growing season starts in the time profile of the Plant Phenology Index. | [Day-Of-Year] | `INT16` | -365.0-365.0 | 1 | 0 |
| `SOSD_S2` | Day of the year when the vegetation growing season starts in the time profile of the Plant Phenology Index. | [Day-Of-Year] | `INT16` | -365.0-365.0 | 1 | 0 |
| `EOSD_S1` | Day of the year when the vegetation growing season ends in the time profile of the Plant Phenology Index. | [Day-Of-Year] | `INT16` | 0.0-730.0 | 1 | 0 |
| `EOSD_S2` | Day of the year when the vegetation growing season ends in the time profile of the Plant Phenology Index. | [Day-Of-Year] | `INT16` | 0.0-730.0 | 1 | 0 |
| `MAXD_S1` | Day of the year in the vegetation growing season when the Plant Phenology Index reaches its maximum value. | [Day-Of-Year] | `INT16` | 0.0-366.0 | 1 | 0 |
| `MAXD_S2` | Day of the year in the vegetation growing season when the Plant Phenology Index reaches its maximum value. | [Day-Of-Year] | `INT16` | 0.0-366.0 | 1 | 0 |
| `SOSV_S1` | Value of the Plant Phenology Index at the start of the vegetation growing season. | [m² / m²] | `INT16` | 0.0-5000.0 | 0.0001 | 0 |
| `SOSV_S2` | Value of the Plant Phenology Index at the start of the vegetation growing season. | [m² / m²] | `INT16` | 0.0-5000.0 | 0.0001 | 0 |
| `EOSV_S1` | Value of the Plant Phenology Index at the end of the vegetation growing season. | [m² / m²] | `INT16` | 0.0-5000.0 | 0.0001 | 0 |
| `EOSV_S2` | Value of the Plant Phenology Index at the end of the vegetation growing season. | [m² / m²] | `INT16` | 0.0-5000.0 | 0.0001 | 0 |
| `MINV_S1` | The average of the Plant Phenology Index value of the minima on left and right sides of the season. | [m² / m²] | `INT16` | 0.0-5000.0 | 0.0001 | 0 |
| `MINV_S2` | The average of the Plant Phenology Index value of the minima on left and right sides of the season. | [m² / m²] | `INT16` | 0.0-5000.0 | 0.0001 | 0 |
| `MAXV_S1` | Maximum value that the Plant Phenology Index reaches during the vegetation growing season i.e. value of the Plant Phenology Index at the maximum season date. | [m² / m²] | `INT16` | 0.0-5000.0 | 0.0001 | 0 |
| `MAXV_S2` | Maximum value that the Plant Phenology Index reaches during the vegetation growing season i.e. value of the Plant Phenology Index at the maximum season date. | [m² / m²] | `INT16` | 0.0-5000.0 | 0.0001 | 0 |
| `AMPL_S1` | Difference between the Season Maximum value and the Season Minimum Value. | [m² / m²] | `INT16` | 0.0-5000.0 | 0.0001 | 0 |
| `AMPL_S2` | Difference between the Season Maximum value and the Season Minimum Value. | [m² / m²] | `INT16` | 0.0-5000.0 | 0.0001 | 0 |
| `LENGTH_S1` | Number of days between the start and the end of the growing season. | [days] | `INT16` | 0.0-730.0 | 1 | 0 |
| `LENGTH_S2` | Number of days between the start and the end of the growing season. | [days] | `INT16` | 0.0-730.0 | 1 | 0 |
| `LSLOPE_S1` | Value of the increasing rate of Plant Phenology Index during vegetation green-up. | [m² / m² /day] | `INT16` | -1000.0-1000.0 | 1 | 0 |
| `LSLOPE_S2` | Value of the increasing rate of Plant Phenology Index during vegetation green-up. | [m² / m² /day] | `INT16` | -1000.0-1000.0 | 1 | 0 |
| `RSLOPE_S1` | Absolute value of the decreasing rate of Plant Phenology Index during vegetation green-down. | [m² / m² /day] | `INT16` | -1000.0-1000.0 | 1 | 0 |
| `RSLOPE_S2` | Absolute value of the decreasing rate of Plant Phenology Index during vegetation green-down. | [m² / m² /day] | `INT16` | -1000.0-1000.0 | 1 | 0 |
| `QA_S1` | Indicate the quality of the start, peak and end of the growing season, as well as the overall quality of the three phases, in a form of a certainty level. | — | `UINT8` | — | 1 | 0 |
| `QA_S2` | Indicate the quality of the start, peak and end of the growing season, as well as the overall quality of the three phases, in a form of a certainty level. | — | `UINT8` | — | 1 | 0 |

##### NDVI 10-daily v1

`clms_global_ndvi_300m_v1_10daily_geotiff`  ·  BYOC `41f33765-18a0-4e1a-ade2-b4093254ce68`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/vegetation/vegetation-indices/ndvi_global_300m_10daily_v1.html)  
global · 300m · 2014 - 2020

> NDVI is an indicator of the greenness of the biomass.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `NDVI` | NDVI is an indicator of the greenness of the biomass. | — | `UINT8` | -0.08-0.92 | 1/250 | -0.08 |

##### NDVI 300m 10-daily V2

`clms_global_ndvi_300m_v2_10daily_geotiff`  ·  BYOC `ab0e1e8e-508c-4faa-9b5b-c9c4734ef29e`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/vegetation/vegetation-indices/ndvi_global_300m_10daily_v2.html)  
global · 300m · 2020 - 2025

> Provides information on the Normalized Difference Vegetation Index, a spectral index quantifying the amount and vigour of vegetation. Every 10-days, estimates are available at global scale, at a spatial resolution of ~300m.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `NDVI` | Normalized Difference Vegetation Index | — | `UINT8` | -0.08-0.92 | 1/250 | -0.08 |
| `NOBS` | Number of clear-sky surface reflectance in the dekad time window. | — | `UINT8` | 0.0-32.0 | 1 | 0 |
| `QFLAG` | Quality flag associated to NDVI | — | `UINT8` | — | 1 | 0 |
| `UNC` | Uncertainty on NDVI | — | `INT16` | 0.0-1.0 | 1/1000 | 0 |

##### NDVI LTS 1km 10-daily V3

`clms_global_ndvi_1km_v3_statistics_geotiff`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/vegetation/vegetation-indices/ndvi-lts_global_1km_10daily_v3.html)  
global · 1km

> Provides the Long-Term Statistics of the Normalized Difference Vegetation Index. Every 10-days, minimum, median, maximum and mean are available at global scale, at a spatial resolution of ~1km over the 21-years period 1999-2019.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `NDVI` | Normalized Difference Vegetation Index | — | `UINT8` | -0.08-0.92 | 1/250 | -0.08 |
| `NOBS` | Number of clear-sky surface reflectance in the dekad time window. | — | `UINT8` | 0.0-32.0 | 1 | 0 |
| `QFLAG` | Quality flag associated to NDVI | — | `UINT8` | — | 1 | 0 |
| `UNC` | Uncertainty on NDVI | — | `INT16` | 0.0-1.0 | 1/1000 | 0 |

##### NPP 10-daily v2

**Each RT level is a separate Browser layer *and* a separate BYOC collection.** ⚠️ There is **no bare `npp_global_300m_10daily_v2` id** — you must pick a level.

| RT | Browser id | BYOC collection id |
|---|---|---|
| RT0 | `npp_global_300m_10daily_v2_rt0` | `40fdc188-1ba7-4c62-a2f8-5d057451dcf9` |
| RT1 | `npp_global_300m_10daily_v2_rt1` | `4c50c693-ff8f-4a44-a095-ef4dfec3e234` |
| RT2 | `npp_global_300m_10daily_v2_rt2` | `48ada5a5-b721-4181-b87b-68957e7b1c8a` |
| RT6 | `npp_global_300m_10daily_v2_rt6` | `c1390928-f7ee-4d50-af81-b0872e0aceff` |
global · 300m · 2014 - present · RT0, RT1, RT2, RT6

> Provides information about the net amount of biomass, or carbon, produced by plants per unit area and time, expressed in gC/m²/day. It is equal to the difference between the Gross Primary Production (GPP), i.e. the total amount of carbon produced through photosynthesis, and the amount of energy used for plant respiration. Every 10-days, estimates are available at global scale, at a spatial resolution of ~ 300 m, from January 2014 to the present.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `NPP` | Net Primary Production (gC/m²/day) | gC/m²/day | `INT16` | 0.0-16.3835 | 1/2000 | 0 |
| `QFLAG` | Quality Flag on Net Primary Production | — | `UINT8` | — | 1 | 0 |

#### Bio-geophysical parameters › Water bodies

##### LWQ 10-daily v1

`clms_global_lwq_100m_v1_10daily-nrt_geotiff`  ·  BYOC `8894d46b-a451-4abf-838e-292b4bcacae1`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/water-bodies/lake-water-quality/lwq-nrt_global_100m_10daily_v1.html)  
global · 100m · 2019 - 2024

> Provides semi-continuous observations for a large number of medium and large-sized lakes.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `FOBS` | Number of days from the start of the sensing period until the first cloud-free observation | Days since the start of the observation period | `FLOAT32` | 0.0-10.0 | 1 | 0 |
| `LOBS` | Number of days from the start of the sensing period until the last cloud-free observation | Days since the start of the observation period | `FLOAT32` | 0.0-10.0 | 1 | 0 |
| `NOBS` | Number of observations | — | `INT16` | 0.0-- | 1 | 0 |
| `RW1375` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW1610` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW2190` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW443` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW490` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW560` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW665` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW705` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW740` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW783` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW842` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW865` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW945` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `TMEAN` | Mean turbidity | NTU | `FLOAT32` | 0.0-- | 1 | 0 |
| `TOBS` | Trophic State Index | — | `FLOAT32` | 1.0-11.0 | 1 | 0 |
| `TSI` | Mean of total suspended matter | — | `FLOAT32` | 0.0-100.0 | 1 | 0 |

##### LWQ 10-daily v1

`clms_global_lwq_300m_v1_10daily-nrt_geotiff`  ·  BYOC `71b198f7-eec7-45aa-bcb9-87a28b5c4e73`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/water-bodies/lake-water-quality/lwq-nrt_global_300m_10daily_v1.html)  
global · 300m · 2002 - 2012

> Provides semi-continuous observations for a large number of medium and large-sized lakes.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `FOBS` | Number of days from the start of the sensing period until the first cloud-free observation | Days since the start of the observation period | `FLOAT32` | 0.0-10.0 | 1 | 0 |
| `LOBS` | Number of days from the start of the sensing period until the last cloud-free observation | Days since the start of the observation period | `FLOAT32` | 0.0-10.0 | 1 | 0 |
| `NOBSQRS` | Number of observations that were not masked but which have an increased risk or dubious (possibly sub-pixel) result | — | `FLOAT32` | — | 1 | 0 |
| `NOBS` | Number of observations | — | `INT16` | 0.0-- | 1 | 0 |
| `RW1020` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW400` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW412` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW443` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW490` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW510` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW560` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW620` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW665` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW674` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW681` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW709` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW754` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW760` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW764` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW767` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW779` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW865` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW885` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW900` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW940` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `TMEAN` | Mean turbidity | NTU | `FLOAT32` | 0.0-- | 1 | 0 |
| `TNOBS` | Number of observations used to estimate Turbidity | — | `FLOAT32` | — | 1 | 0 |
| `TOBS` | Trophic State Index | — | `FLOAT32` | 1.0-11.0 | 1 | 0 |
| `TSINOBS` | Number of observations used to estimate Trophic State Index | — | `FLOAT32` | — | 1 | 0 |
| `TSI` | Mean of total suspended matter | — | `FLOAT32` | 0.0-100.0 | 1 | 0 |
| `TSTDEV` | Standard deviation of Turbidity | — | `FLOAT32` | — | 1 | 0 |

##### LWQ 10-daily v1

`clms_global_lwq_300m_v1_10daily-reproc_geotiff`  ·  BYOC `bc5c3c52-d88d-4756-9793-524dce1cd6a4`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/water-bodies/lake-water-quality/lwq-reproc_global_300m_10daily_v1.html)  
global · 300m · 2002 - 2012

> Provides semi-continuous observations for a large number of medium and large-sized lakes

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `FOBS` | Number of days from the start of the sensing period until the first cloud-free observation | Days since the start of the observation period | `FLOAT32` | 0.0-10.0 | 1 | 0 |
| `LOBS` | Number of days from the start of the sensing period until the last cloud-free observation | Days since the start of the observation period | `FLOAT32` | 0.0-10.0 | 1 | 0 |
| `NOBSQRS` | Number of observations that were not masked but which have an increased risk or dubious (possibly sub-pixel) result | — | `FLOAT32` | — | 1 | 0 |
| `NOBS` | Number of observations | — | `INT16` | 0.0-- | 1 | 0 |
| `RW412` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW443` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW490` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW510` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW560` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW620` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW665` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW681` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW709` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW754` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW760` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW779` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW865` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW885` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW900` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `TMEAN` | Mean turbidity | NTU | `FLOAT32` | 0.0-- | 1 | 0 |
| `TNOBS` | Number of observations used to estimate Turbidity | — | `FLOAT32` | — | 1 | 0 |
| `TOBS` | Trophic State Index | — | `FLOAT32` | 1.0-11.0 | 1 | 0 |
| `TSINOBS` | Number of observations used to estimate Trophic State Index | — | `FLOAT32` | — | 1 | 0 |
| `TSI` | Mean of total suspended matter | — | `FLOAT32` | 0.0-100.0 | 1 | 0 |
| `TSTDEV` | Standard deviation of Turbidity | — | `FLOAT32` | — | 1 | 0 |

##### LWQ 10-daily v2

`clms_global_lwq_300m_v2_10daily-nrt_geotiff`  ·  BYOC `5c2c9b2c-2893-41d9-b2bc-fbd6e5b8b31d`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/water-bodies/lake-water-quality/lwq-nrt_global_300m_10daily_v2.html)  
global · 300m · 2024 - present

> Provides semi-continuous observations for a large number of medium and large-sized lakes.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `CHLAMEAN` | Mean of chlorophyll a concentration | mg/m³ | `FLOAT32` | 0.0-- | 1 | 0 |
| `CHLAUNC` | Mean of relative uncertainty of chlorophyll a concentration | % | `FLOAT32` | 0.0-1000.0 | 1 | 0 |
| `FCBPROB` | Probability of floating cyanobacteria | Average probability of presence in the observed period | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `FOBS` | Number of days from the start of the sensing period until the first cloud-free observation | Days since the start of the observation period | `INT16` | 0.0-10.0 | 1 | 0 |
| `LOBS` | Number of days from the start of the sensing period until the last cloud-free observation | Days since the start of the observation period | `INT16` | 0.0-10.0 | 1 | 0 |
| `NOBS` | Number of observations | — | `INT16` | 0.0-- | 1 | 0 |
| `QFLAG` | Flag band showing why input observations to a pixel have been included. | — | `UINT16` | — | 1 | 0 |
| `RW1020` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW400` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW412` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW443` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW490` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW510` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW560` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW620` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW665` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW674` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW681` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW709` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW754` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW779` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW885` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW900` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `TMEAN` | Mean turbidity | NTU | `FLOAT32` | 0.0-500.0 | 1 | 0 |
| `TOBS` | Age in days after the start of the observation period | — | `FLOAT32` | 1.0-11.0 | 1 | 0 |
| `TSI` | Trophic State Index | — | `FLOAT32` | 0.0-100.0 | 1 | 0 |
| `TSMMEAN` | Mean of total suspended matter | g/m³ | `FLOAT32` | 0.0-500.0 | 1 | 0 |
| `TSMUNC` | Mean of relative uncertainty of total suspended matter | % | `FLOAT32` | 0.0-200.0 | 1 | 0 |
| `UNCUB` | Relative unbiased uncertainty | % | `FLOAT32` | -10000.0-10000.0 | 1 | 0 |
| `UNC` | Relative uncertainty | % | `FLOAT32` | -10000.0-10000.0 | 1 | 0 |

##### LWQ 10-daily v2

`lwq-nrt_global_100m_10daily_v2`  ·  BYOC `c320caa8-4d97-40e1-90c6-e34dd5e42b8b`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/water-bodies/lake-water-quality/lwq-nrt_global_100m_10daily_v2.html)  
global · 100m · 2024 - present

> Provides semi-continuous observations for a large number of medium and large-sized lakes, according to the Global Lakes and Wetlands Database (GLWD) or otherwise of specific environmental monitoring interest. 10-daily observations are available in near real time at 100 m spatial resolution from September 2024 to present.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `CHLAMEAN` | Mean of chlorophyll-a concentration | mg/m3 | `FLOAT32` | 0.0-0.0 | 1 | 0 |
| `FCBPROB` | Probability of floating cyanobacteria | Average probability of presence in the observed period | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `FOBS` | Number of days from the start of the sensing period until the first cloud-free observation | Days since the start of the observation period | `FLOAT32` | 0.0-10.0 | 1 | 0 |
| `LOBS` | Number of days from the start of the sensing period until the last cloud-free observation | Days since the start of the observation period | `FLOAT32` | 0.0-10.0 | 1 | 0 |
| `NOBS` | Number of observations | — | `INT16` | 0.0-0.0 | 1 | 0 |
| `QFLAG` | Flag band showing why input observations to a pixel have been included. | — | `UINT16` | 0.0-0.0 | 1 | 0 |
| `RW1375` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW1610` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW2190` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW443` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW490` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW560` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW665` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW705` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW740` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW783` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW842` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW865` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `RW945` | Fully normalised water-leaving reflectance | — | `FLOAT32` | 0.0-1.0 | 1 | 0 |
| `TMEAN` | Mean turbidity | NTU | `FLOAT32` | 0.0-0.0 | 1 | 0 |
| `TOBS` | Age in days after the start of the observation period | — | `FLOAT32` | 0.0-0.0 | 1 | 0 |
| `TSI` | Trophic State Index | — | `FLOAT32` | 0.0-100.0 | 1 | 0 |
| `TSMMEAN` | Mean of total suspended matter | g/m³ | `FLOAT32` | 0.0-0.0 | 1 | 0 |

##### Lake Ice Extent 500m version 2

`clms_global_lie_500m_v2_daily_geotiff`  ·  BYOC `1a9d1719-03f8-47d6-911b-bc683d1268bd`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/water-bodies/river-and-lake-ice-extent/lie_global_500m_daily_v2.html)  
global · 500m · 2025 - present

> On a daily basis classifies pixels in Global freshwater bodies into 1) Snow-covered ice, 2) Partially snow-covered or snow-free ice, 3) Open water, and 4) Cloud. The data is updated in near-real time with the spatial resolution of 500 m and with a temporal extent from July 2025 to present

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `LIE` | A classification of lake ice state, with the following classes: Snow-covered ice, Partially snow-covered or snow-free ice, Open water, Cloud. | — | `UINT8` | 10.0-70.0 | 1 | 0 |
| `P` | GMM predicted posterior probability of the most likely class | % | `UINT8` | 0.0-100.0 | 1 | 0 |

##### Water Bodies 10-daily v1

`clms_global_wb_300m_v1_10daily_geotiff`  ·  BYOC `caae3fa1-7166-432b-8d9e-322ade546ade`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/water-bodies/water-bodies/wb_global_300m_10daily_v1.html)  
global · 300m · 2014 - 2020

> Detects the areas covered by inland water.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `WB` | Water Bodies detection layer | — | `UINT8` | 0.0-255.0 | 1 | 0 |
| `QUAL` | Water Bodies Occurrence information | — | `UINT8` | 0.0-255.0 | 1 | 0 |
| `WB` | Water Bodies detection layer | — | `UINT8` | 0.0-255.0 | 1 | 0 |
| `QUAL` | Water Bodies Occurrence information | — | `UINT8` | 0.0-255.0 | 1 | 0 |

##### Water Bodies 10-daily v2

`clms_global_wb_1km_v2_10daily_geotiff`  ·  BYOC `ba17bfe3-e702-47c6-b528-cf99256fbc30`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/water-bodies/water-bodies/wb_global_1km_10daily_v2.html)  
global · 1km · 1999 - 2020

> Detects the areas covered by inland water.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `WB` | Water Bodies detection layer | — | `UINT8` | 0.0-255.0 | 1 | 0 |
| `QUAL` | Water Bodies Occurrence information | — | `UINT8` | 0.0-255.0 | 1 | 0 |

##### Water Bodies monthly v1

`clms_global_wb_100m_v1_monthly_geotiff`  ·  BYOC `69577a6b-80e0-4507-8b99-57b5ef167d41`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/water-bodies/water-bodies/wb_global_100m_monthly_v1.html)  
global · 100m · 2020 - present

> Detects the areas covered by inland water

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `WB` | Water Bodies | — | `UINT8` | 0.0-255.0 | 1 | 0 |
| `QUAL` | Quality layer | — | `UINT8` | 0.0-255.0 | 1 | 0 |

##### Water Bodies monthly v2

`clms_global_wb_300m_v2_monthly_geotiff`  ·  BYOC `c19a3068-8be5-4077-8233-1dc54fbffe31`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/water-bodies/water-bodies/wb_global_300m_monthly_v2.html)  
global · 300m · 2020 - present

> Detects the areas covered by inland water

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `WB` | Water Bodies | — | `UINT8` | 0.0-255.0 | 1 | 0 |
| `QUAL` | Quality layer | — | `UINT8` | 0.0-255.0 | 1 | 0 |

#### Land cover & land use › Croplands

##### CPBSB 10m Yearly

`cpbsb_10m_yearly_v1`  ·  BYOC `3cfc6824-38a8-419c-8bd9-8dd05cd4a5be`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/croplands/cropping-patterns/bare-soil-before/clms_vlcc_bare-soil-before_europe_10m_yearly_v1.html)  
global · 10m · 2017 - present

> The High Resolution Layer Cropping Patterns - Bare Soil Before (CPBSB) raster product provides the bare soil period (in days) before the emergence of the main annual crop. Note that the bare soil period cannot transcend the calendar year for which the product is generated.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `Name` | Description | Units | `Source format` | Range | Scaling | Offset |
| `---------------` | -------------- | --------- | `----------------` | ------- | --------- | -------- |

##### CPFLD 10m Yearly

`cpfld_10m_yearly_v1`  ·  BYOC `f6489109-5511-4da4-9175-43f34c50f0db`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/croplands/cropping-patterns/fallow-land-duration/clms_vlcc_fallow-land-duration_europe_10m_yearly_v1.html)  
global · 10m · 2017 - present

> The High Resolution Layer Cropping Patterns - Fallow Land Duration (CPFLD) raster product provides information on the duration of fallow land periods, expressed in days, over a five-year period.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `CPFLD` | Fallow land duration (5-year period) | Number of days / 0: Flag for no fallow land | `UINT16` | 1.0-1826.0 | 1 | 0 |
| `Name` | Description | Units | `Source format` | Range | Scaling | Offset |
| `---------------` | -------------- | --------- | `----------------` | ------- | --------- | -------- |
| `CPFLDCL` | Confidence of fallow land duration | Number of days / 0: Flag for no fallow land / 65534: flag indicating that no confidence can be calculated | `UINT16` | 1.0-200.0 | 1 | 0 |

##### CPFLP 10m Yearly

`cpflp_10m_yearly_v1`  ·  BYOC `3dd04866-fe0a-48f2-a07b-033350949919`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/croplands/cropping-patterns/fallow-land-presence/clms_vlcc_fallow-land-presence_europe_10m_yearly_v1.html)  
global · 10m · 2017 - present

> The High Resolution Layer Cropping Patterns - Fallow Land Presence (CPFLP) raster product provides the yearly fallow land classification indicating if arable land has been left fallow in the respective calendar year. This dataset is provided annually starting in 2017 with 10 meter rasters (fully conformant with the EEA reference grid) in 100 x 100 km tiles covering the EEA38 countries. High Resolution Layer Croplands product is part of the European Union's Copernicus Land Monitoring Service. Confidence layer available for the dataset. This dataset includes data from the French Overseas Territories (DOMs)

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `CPFLP` | Annual fallow land presence | 0 = No fallow land, 1 = Fallow | `UINT16` | 0.0-1.0 | 1 | 0 |
| `Name` | Description | Units | `Source format` | Range | Scaling | Offset |
| `---------------` | -------------- | --------- | `----------------` | ------- | --------- | -------- |
| `CPFLPCL` | Confidence of fallow land presence | Confidence percentage (0-100%) | `UINT16` | 0.0-253.0 | 1 | 0 |

#### Land cover & land use › Global dynamic land cover

##### Land Cover Map at 10m - Annual V1

`lcm_global_10m_yearly_v1`  ·  BYOC `828f6b20-8ffd-48f8-a1da-fefd271456db`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/global-dynamic-land-cover/lcm_global_10m_yearly_v1.html)  
global · 10m · 2020 - 2026

> Provides at global level information on different types (classes) of physical coverage of the Earth's surface, e.g. tree cover, grasslands, croplands, permanent water bodies, wetlands at 10 m spatial resolution for the 2020 base year. The data are updated annually and will be available for the 2020-2026 years. This dataset builds upon initiatives like the 100 m Copernicus Global Land Cover layers (2015-2019) and offers enhanced spatial detail that facilitates more effective monitoring of global land cover changes, including deforestation, urbanization, and other environmental transformations. Please note: this version is still in beta status, as final validation is ongoing.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `LCM10` | Land Cover Map at 10m - Annual V1 | — | `UINT8` | 10.0-254.0 | 1 | 0 |

##### Land Cover yearly v3

`clms_global_lcc_100m_v3_yearly_geotiff`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/global-dynamic-land-cover/lc_global_100m_yearly_v3.html)  
global · 100m

> Provides at global level spatial information on different types (classes) of physical coverage of the Earth's surface, e.g. forests, grasslands, croplands, lakes, wetlands.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `LCM10` | Land Cover Map at 10m - Annual V1 | — | `UINT8` | 10.0-254.0 | 1 | 0 |

#### No documentation page

##### `lswt_offline_1km_10daily_v1`

`lswt_offline_1km_10daily_v1`  ·  BYOC `db5aea5e-a0d1-487f-adff-ad8831933208`  
global · 1km · 2002 - 2012

> ⚠️ **The id lies about cadence.** The Browser calls it `ndvi_global_300m_**daily**_v3`, but its BYOC id `6303088f-3c19-4967-9038-119267c6d090` is the collection on the docs page titled **"NDVI 300m 10-daily V3"** (`.../vegetation-indices/ndvi_global_300m_10daily_v3.qmd:2-3`). **It is 10-daily.** The id is not a reliable guide to cadence; the docs page is.
> ⚠️ No product page under this id in the documentation. Verify in the Browser before scripting against it.

##### `ndvi_global_300m_daily_v3`

`ndvi_global_300m_daily_v3`  ·  BYOC `6303088f-3c19-4967-9038-119267c6d090`  
global · 300m · 2014 - present

> ⚠️ **No product page in the documentation.** Verify in the Browser before scripting against this id.

### Northern hemisphere, 4 product families

#### Bio-geophysical parameters › Snow

##### SCE daily v1

`clms_nh_sce_1km_v1_daily_geotiff`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/snow/snow-cover-extent/sce_northernhemisphere_1km_daily_v1.html)  
N. hemisphere · 1km

> Fraction of snow cover on the ground

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `NDVI` | Normalized Difference Vegetation Index | — | `UINT8` | -0.08-0.92 | 1/250 | -2/25 |
| `UNC` | Uncertainty on NDVI | — | `INT16` | 0.0-1.0 | 1/1000 | 0 |
| `NOBS` | Number of clear-sky surface reflectance in the dekad time window | — | `UINT8` | 0.0-32.0 | 1 | 0 |
| `QFLAG` | Quality flag associated to NDVI | — | `UINT8` | — | 1 | 0 |

##### SWE daily v1

`clms_global_swe_5km_v1_daily_geotiff`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/snow/snow-water-equivalent/swe_northernhemisphere_5km_daily_v1.html)  
N. hemisphere · 5km

> ⚠️ **The id says `global` but the docs say N. hemisphere.** `clms_global_` is the CLMS *Global Land component* namespace, not a coverage claim.

> Provides for the Northern Hemisphere daily updates of the equivalent amount of liquid water stored in the snow pack.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `NDVI` | Normalized Difference Vegetation Index | — | `UINT8` | -0.08-0.92 | 1/250 | -2/25 |
| `UNC` | Uncertainty on NDVI | — | `INT16` | 0.0-1.0 | 1/1000 | 0 |
| `NOBS` | Number of clear-sky surface reflectance in the dekad time window | — | `UINT8` | 0.0-32.0 | 1 | 0 |
| `QFLAG` | Quality flag associated to NDVI | — | `UINT8` | — | 1 | 0 |

##### SWE daily v2

`clms_global_swe_5km_v2_daily_geotiff`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/snow/snow-water-equivalent/swe_northernhemisphere_5km_daily_v2.html)  
N. hemisphere · 5km

> ⚠️ **The id says `global` but the docs say N. hemisphere.** `clms_global_` is the CLMS *Global Land component* namespace, not a coverage claim.

> Provides for the Northern Hemisphere daily updates of the equivalent amount of liquid water stored in the snow pack.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `NDVI` | Normalized Difference Vegetation Index | — | `UINT8` | -0.08-0.92 | 1/250 | -2/25 |
| `UNC` | Uncertainty on NDVI | — | `INT16` | 0.0-1.0 | 1/1000 | 0 |
| `NOBS` | Number of clear-sky surface reflectance in the dekad time window | — | `UINT8` | 0.0-32.0 | 1 | 0 |
| `QFLAG` | Quality flag associated to NDVI | — | `UINT8` | — | 1 | 0 |

#### Bio-geophysical parameters › Water bodies

##### LIE daily v1

`clms_global_lie_500m_v1_daily_geotiff`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/water-bodies/river-and-lake-ice-extent/lie_northernhemisphere_500m_daily_v1.html)  
N. hemisphere · 500m

> ⚠️ **The id says `global` but the docs say N. hemisphere.** `clms_global_` is the CLMS *Global Land component* namespace, not a coverage claim.

> Classifies, in pixels, inland/freshwater bodies

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `NDVI` | Normalized Difference Vegetation Index | — | `UINT8` | -0.08-0.92 | 1/250 | -2/25 |
| `UNC` | Uncertainty on NDVI | — | `INT16` | 0.0-1.0 | 1/1000 | 0 |
| `NOBS` | Number of clear-sky surface reflectance in the dekad time window | — | `UINT8` | 0.0-32.0 | 1 | 0 |
| `QFLAG` | Quality flag associated to NDVI | — | `UINT8` | — | 1 | 0 |

### Baltic, 1 product family

#### Bio-geophysical parameters › Water bodies

##### LIE Baltic, daily v1

`lie_baltic_250m_daily_v1`  ·  BYOC `bfebf889-ca5c-4baa-abbc-04907f1e8de8`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/water-bodies/river-and-lake-ice-extent/lie_baltic_250m_daily_v1.html)  
Baltic · 250m · 2017 - 2024-06

> Classifies, in pixels, inland/freshwater bodies

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `LIE` | Classification of lake ice extent | — | `INT16` | 1.0-3.0 | 1 | 0 |

### Pantropical, 1 product family

#### Land cover & land use › Global dynamic land cover

##### Tree Cover Density at 10m - Annual V1

`tcd_pantropical_10m_yearly_v1`  ·  BYOC `8bd33a42-dce4-4554-9a1f-1bb248b4183d`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/global-dynamic-land-cover/tcd_pantropical_10m_yearly_v1.html)  
pantropical · 10m · 2020 - 2026

> Provides pantropical tree cover density as projective tree cover in percent per pixel at 10 m resolution for the 2020 base year. The data are updated annually and will be available for the 2020-2026 years. The product belongs to the Copernicus Global Land Cover and Tropical Forest Mapping and Monitoring Service (LCFM) and builds upon initiatives like the REDDCopernicus, EO4SD Forest Monitoring and pan-European Vegetated Land Cover Characteristics. It advances tropical forest monitoring capabilities, ensuring alignment with international sustainability initiatives and providing critical information for analysis and monitoring of deforestation and forest degradation. Please note: this version is still in beta status, as final validation is ongoing.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `TCD10` | Tree Cover Density Map at 10m - Annual V1 | % | `UINT8` | 0.0-100.0 | 1 | 0 |

### Europe-only, 44 product families

#### Bio-geophysical parameters › Auxiliary data

##### Sentinel-2 CC 20m Daily V1

`clms_wsi_cloud-classification_europe_utm_20m_daily_v1`  ·  BYOC `64d015da-e225-48d8-9643-30a453657beb`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/auxiliary-data/cloud-mask/clms_wsi_cloud-classification_europe_utm_20m_daily_v1.html)  
Europe · 20m · 2016 - present

> The Cloud Classification (CC) product provides information on the extent of clouds and cloud shadows derived from optical satellite data acquired by the **Sentinel-2** constellation. Cloud detection is performed at a **120m** spatial resolution using the MAJA software.<br><br>It is generated in near real-time at European scale, with a pixel spacing of 20 m x 20 m. It used to produce the CLMS High-Resolution Water, Snow and Ice datasets (HR-WSI), which rely on Sentinel-2 imagery.<br><br>**Data availability**: from 2016 to the present. No product is generated for a Sentinel-2 tile when cloud cover exceeds 90%.<br><br>More information in the products documentation here.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `CC` | Cloud and cloud shadow classification of the Sentinel-2 image | Cloud classification: 0=No Data, 1=Clear, 2=Cloud Shadow, 3=Cloud | `UINT8` | 0.0-3.0 | 1 | 0 |
| `CC_QA` | Quality layer for the cloud and cloud shadow classification (CC) layer | Quality assessment for CC layer. Indicators for defects such as missing pixels and cloudy data. | `UINT8` | 0.0-255.0 | 1 | 0 |
| `QAFLAGS` | Quality flags | Bitmask with quality flags. Bit 0: cloud detection using single-scene threshold approach. | `UINT8` | 0.0-255.0 | 1 | 0 |

#### Bio-geophysical parameters › Snow

##### FSC 20m Daily V2

`clms_wsi_fractional-snow-cover_europe_utm_20m_daily_v2`  ·  BYOC `2bb9974a-0eb8-484d-adf1-20cc307021b6`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/snow/snow-cover-extent/clms_wsi_fractional-snow-cover_europe_utm_20m_daily_v2.html)  
Europe · 20m · 2016 - present

> The **Fractional Snow Cover (FSC)** product provides the fraction of the surface covered by snow at the top of canopy (FSC-TOC) and on ground (FSC-OG) per pixel as a percentage (0% - 100%). Cloud detection in the Sentinel-2 imagery is performed using the MAJA software.<br><br>It is generated in near real-time at European scale based on optical satellite data from the **Sentinel-2** constellation, with a spatial resolution of **20 m x 20 m**.<br><br>**Data availability**: from 2016 to the present. No product is generated for a Sentinel-2 tile when cloud cover exceeds 90%.<br><br>More information here.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `FSCOG` | Snow fraction on-ground (%) | Fractional snow cover on ground (%): 0-100=snow fraction; 205=cloud or cloud shadow; 210=inland water | `UINT8` | 0.0-100.0 | 1 | 0 |
| `FSCOG_QA` | Quality layer for the on-ground snow fraction (FSC OG) layer | Quality assessment for FSCOG: 0=high quality; 1=medium quality; 2=low quality; 3=minimal quality; 205=cloud or cloud shadow; 210=inland water | `UINT8` | 0.0-3.0 | 1 | 0 |
| `FSCTOC` | Snow fraction on top of canopy (%) | Fractional snow cover top of canopy (%): 0-100=snow fraction; 205=cloud or cloud shadow; 210=inland water | `UINT8` | 0.0-100.0 | 1 | 0 |
| `FSCTOC_QA` | Quality layer for the Top-of-canopy snow fraction (FSC TOC) layer | Quality assessment for FSCTOC: 0=high quality; 1=medium quality; 2=low quality; 3=minimal quality; 205=cloud or cloud shadow; 210=inland water | `UINT8` | 0.0-3.0 | 1 | 0 |
| `QAFLAGS` | Quality flags | Bitmask with pixel quality flags. | `UINT8` | — | 1 | 0 |
| `CLD` | Cloud and cloud shadow mask | Bitmask with cloud and cloud shadow masks derived from MAJA Sentinel-2 Level-2A product. | `UINT8` | — | 1 | 0 |
| `NDSI` | Normalised Difference Snow Index (%) of detected snow areas | Normalised Difference Snow Index (%): 0-100=NDSI values for snow-covered pixels; 205=cloud or cloud shadow; 210=inland water | `UINT8` | 0.0-100.0 | 1 | 0 |

##### GFSC 60m Daily V1

`clms_wsi_gap-filled-fractional-snow-cover_europe_utm_60m_daily_v1`  ·  BYOC `0b5265f5-3664-44c2-96ab-e91aba67b0c3`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/snow/snow-cover-extent/clms_wsi_gap-filled-fractional-snow-cover_europe_utm_60m_daily_v1.html)  
Europe · 60m · 2016 - present

> The daily cumulative **Gap-filled Fractional Snow Cover (GFSC)** product provides pixel-wise snow cover extent as a percentage (0% - 100%). It is based on synthetic aperture radar (SAR) data from the **Sentinel-1** constellation and optical imagery from the **Sentinel-2** constellation. The product is generated by merging all available Sentinel-1 and Sentinel-2 observations acquired over the previous **seven days** to produce a spatially complete composite of snow conditions, thereby reducing data gaps caused by cloud cover and sensor coverage limitations. Snow information derived from Sentinel-1 is focused on the detection of wet snow in high-mountain areas.<br><br>It is generated on a daily basis at European scale, with a spatial resolution of **60 m x 60 m**.<br><br>**Data availability**: from 2016 to the present.<br><br>More information here.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `GF` | Snow fraction (%) | Snow fraction (%): 0-100=snow fraction; 205=cloud or cloud shadow; 210=inland water | `UINT8` | 0.0-100.0 | 1 | 0 |
| `GF_QA` | Quality layer for the snow fraction (GF) layer | Quality assessment for GF: 0=high quality; 1=medium quality; 2=low quality; 3=minimal quality; 205=cloud or cloud shadow; 210=inland water | `UINT8` | 0.0-3.0 | 1 | 0 |
| `QAFLAGS` | Quality flags | Bitmask with pixel quality flags | `UINT8` | — | 1 | 0 |

##### SCE daily v1

`clms_global_sce_500m_v1_daily_geotiff`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/snow/snow-cover-extent/sce_europe_500m_daily_v1.html)  
Europe · 500m

> ⚠️ **The id says `global` but the docs say Europe.** `clms_global_` is the CLMS *Global Land component* namespace, not a coverage claim.

> Fraction of snow cover on the ground

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `GF` | Snow fraction (%) | Snow fraction (%): 0-100=snow fraction; 205=cloud or cloud shadow; 210=inland water | `UINT8` | 0.0-100.0 | 1 | 0 |
| `GF_QA` | Quality layer for the snow fraction (GF) layer | Quality assessment for GF: 0=high quality; 1=medium quality; 2=low quality; 3=minimal quality; 205=cloud or cloud shadow; 210=inland water | `UINT8` | 0.0-3.0 | 1 | 0 |
| `QAFLAGS` | Quality flags | Bitmask with pixel quality flags | `UINT8` | — | 1 | 0 |

##### SP S1+S2 (high mountains) 60m Yearly V1

`clms_wsi_snow-phenology-s1-s2_europe_utm_60m_yearly_v1`  ·  BYOC `1896152f-75d8-4daf-9db9-987773559a2c`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/snow/snow-cover-extent/clms_wsi_snow-phenology-s1-s2_europe_utm_60m_yearly_v1.html)  
Europe · 60m · 2016 - present

> The Sentinel-1 & Sentinel-2 **Snow Phenology (SP S1+S2)** product characterizes the timing and duration of the snow season. For each pixel and for a given hydrological year, it provides the number of days with snow cover, as well as the first and last day of the longest continuous snow period. The hydrological year starts on 1 September.<br><br>The product is generated at the European scale with a spatial resolution of **60 m x 60 m**, consistent with the input snow cover maps derived from optical satellite data acquired by the Sentinel-2 constellation and from C-band Synthetic Aperture Radar satellite data acquired by the Sentinel-1 constellation (Gap-filled Fractional Snow Cover - GFSC).<br><br>**Data availability**: from 2016 to the present. The data can be downloaded in multiple projections and pixel spacings.<br><br>More information here.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `SCD` | Snow cover duration (in days) | Number of days of snow cover over the hydrological year | `UINT16` | 0.0-366.0 | 1 | 0 |
| `SCO` | Snow cover onset date defined as the first day of the longest snow cover period | Snow cover onset date, expressed as the number of days from the beginning of the hydrological year (1st September = day 0). Note that SCO is not given when the snow cover duration SCD is less than 60 days. | `UINT16` | 0.0-366.0 | 1 | 0 |
| `SCM` | Snow cover melt out date defined as the last day of the longest snow cover period | Snow cover melt out date, expressed as the number of days from the beginning of the hydrological year (1st September = day 0). Note that SCM is not given when the snow cover duration SCD is less than 60 days. | `UINT16` | 0.0-366.0 | 1 | 0 |
| `NCSO` | Number of days with clear sky observations within the hydrological year | Number of days with clear sky observations used in the interpolation of the snow cover time series within the hydrological year. | `UINT16` | 0.0-366.0 | 1 | 0 |
| `NWSO` | Number of days with Sentinel-1-based wet snow observations within the hydrological year | Number of days with Sentinel-1-based wet snow observations used in the interpolation of the snow cover time series within the hydrological year (used where Sentinel-2-based observations have gaps). | `UINT16` | 0.0-366.0 | 1 | 0 |
| `QAFLAGS` | Quality flags | Bitmask layer with pixel quality flags. The default visualisation displays areas where the snow cover duration is less than 60 days. These correspond to pixels where bit 4 is activated. Additional information can also be visualised by selecting other bits. | `UINT8` | — | 1 | 0 |
| `SCD_QA` | Quality layer for the snow cover duration (SCD) layer | Quality assessment for SCD: 0=high quality; 1=medium quality; 2=low quality; 3=minimal quality; 420=inland water | `UINT16` | 0.0-3.0 | 1 | 0 |
| `SCO_QA` | Quality layer for the snow cover onset date (SCO) layer | Number of days between the estimated snow onset date and the closest snow observation date. | `UINT16` | 0.0-365.0 | 1 | 0 |
| `SCM_QA` | Quality layer for the snow cover melt out date (SCM) layer | Number of days between the estimated snow melt out date and the closest snow observation date. | `UINT16` | 0.0-365.0 | 1 | 0 |

##### SP S2 20m Yearly V1

`clms_wsi_snow-phenology-s2_europe_utm_20m_yearly_v1`  ·  BYOC `0316f5d4-1320-41a1-994e-d756902efa9f`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/snow/snow-cover-extent/clms_wsi_snow-phenology-s2_europe_utm_20m_yearly_v1.html)  
Europe · 20m · 2016 - present

> The Sentinel-2 **Snow Phenology (SP S2)** product characterizes the timing and duration of the snow season. For each pixel and for a given hydrological year, it provides the number of days with snow cover, as well as the first and last day of the longest continuous snow period. The hydrological year starts on 1 September.<br><br>The product is generated at the European scale with a spatial resolution of **20 m x 20 m**, consistent with the input snow cover maps derived from optical satellite data acquired by the Sentinel-2 constellation (Fractional Snow Cover - FSC).<br><br>**Data availability**: from 2016 to the present. The data can be downloaded in multiple projections and pixel spacings.<br><br>More information here.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `SCD` | Snow cover duration (in days) | Number of days with snow cover over the hydrological year (1 September to 31 August) | `UINT16` | 0.0-365.0 | 1 | 0 |
| `SCO` | Snow cover onset date defined as the first day of the longest snow cover period | Snow cover onset date expressed as the number of days from 1 September (day 0). Not given when SCD < 60 days. | `UINT16` | 0.0-365.0 | 1 | 0 |
| `SCM` | Snow cover melt out date defined as the last day of the longest snow cover period | Snow cover melt out date expressed as the number of days from 1 September (day 0). Not given when SCD < 60 days. | `UINT16` | 0.0-365.0 | 1 | 0 |
| `NOBS` | Number of days with clear sky observations within the hydrological year | Number of days with clear sky observations used in the interpolation of the snow cover time series | `UINT16` | 0.0-365.0 | 1 | 0 |
| `QAFLAGS` | Quality flags | Bitmask with pixel quality flags | `UINT8` | — | 1 | 0 |
| `SCD_QA` | Quality layer for the snow cover duration (SCD) layer | Quality assessment for SCD: 0=high quality; 1=medium quality; 2=low quality; 3=minimal quality; 420=inland water | `UINT16` | 0.0-3.0 | 1 | 0 |
| `SCO_QA` | Quality layer for the snow cover onset date (SCO) layer | Number of days between the estimated snow cover onset date and the closest snow observation date | `UINT16` | 0.0-365.0 | 1 | 0 |
| `SCM_QA` | Quality layer for the snow cover melt out date (SCM) layer | Number of days between the estimated snow cover melt out date and the closest snow observation date | `UINT16` | 0.0-365.0 | 1 | 0 |

##### SWS (high mountains) 60m Daily V2

`clms_wsi_sar-wet-snow_europe_utm_60m_daily_v2`  ·  BYOC `41fc21f0-b657-4346-a4ab-aafc8cc636f2`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/snow/snow-state/clms_wsi_sar-wet-snow_europe_utm_60m_daily_v2.html)  
Europe · 60m · 2016 - present

> The **SAR Wet Snow (SWS)** product provides the wet snow extent for high mountain areas, based on C-band Synthetic Aperture Radar satellite data from the **Sentinel-1** constellation.<br><br>It is generated in near real-time for selected high mountain areas at European scale with a spatial resolution of **60 m x 60 m**.<br><br>**Data availability**: from 2016 to the present.<br><br>More information here.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `WSM` | Wet Snow classification in high Mountains areas | 110: wet snow, 125: dry snow or no snow or patchy snow, 200: radar shadow or layover or foreshortening, 210: water, 220: forest, 230: urban areas, 240: non-mountain areas | `UINT8` | 110.0-240.0 | 1 | 0 |
| `WSM_QA` | Quality layer for the wet snow classification (WSM) layer | 0: high quality, 1: medium quality, 2: low quality, 3: minimal quality, 250: masked | `UINT8` | 0.0-250.0 | 1 | 0 |

##### WDS 60m Daily V2

`clms_wsi_wet-dry-snow_europe_utm_60m_daily_v2`  ·  BYOC `e52773f2-d35d-492d-8144-371a9e741212`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/snow/snow-state/clms_wsi_wet-dry-snow_europe_utm_60m_daily_v2.html)  
Europe · 60m · 2016 - present

> The **Wet / Dry Snow (WDS)** product provides information on the snow state (wet or dry) by combining **Sentinel-1** radar-based wet snow maps within the snow cover extent derived from **Sentinel-2** optical data. Cloud detection in the Sentinel-2 imagery is performed using the MAJA software.<br><br>It is generated in near real-time at European scale, with a spatial resolution of **60 m x 60 m** in areas where Sentinel-1 and Sentinel-2 observation tracks overlap.<br><br>**Data availability**: from 2016 to the present. No product is generated for a Sentinel-2 tile when cloud cover exceeds 90%.<br><br>More information here.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `SSC` | Snow State Classification | wet snow / dry snow / snow free / patchy snow cover / radar shadow / layover / foreshortening / cloud / cloud shadow / water / forest / urban area | `UINT8` | 110.0-230.0 | 1 | 0 |
| `SSC_QA` | Quality layer for the snow state classification (SSC) layer | high quality / medium quality / low quality / minimal quality / masked | `UINT8` | 0.0-250.0 | 1 | 0 |

#### Bio-geophysical parameters › Soil moisture

##### SSM daily v1

`clms_global_ssm_1km_v1_daily_geotiff`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/soil-moisture/surface-soil-moisture/ssm_europe_1km_daily_v1.html)  
Europe · 1km

> ⚠️ **The id says `global` but the docs say Europe.** `clms_global_` is the CLMS *Global Land component* namespace, not a coverage claim.

> Provides information on the relative water content of the top few centimeters soil, describing how wet or dry the soil is in its topmost layer, expressed in percent saturation.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `SSC` | Snow State Classification | wet snow / dry snow / snow free / patchy snow cover / radar shadow / layover / foreshortening / cloud / cloud shadow / water / forest / urban area | `UINT8` | 110.0-230.0 | 1 | 0 |
| `SSC_QA` | Quality layer for the snow state classification (SSC) layer | high quality / medium quality / low quality / minimal quality / masked | `UINT8` | 0.0-250.0 | 1 | 0 |

##### SWI daily v1

`clms_europe_swi_1km_v1_daily_geotiff`  ·  BYOC `bd02588b-7236-4b1e-9480-aeae7dce3c7a`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/soil-moisture/soil-water-index/swi_europe_1km_daily_v1.html)  
Europe · 1km · 2015 - present

> Quantifies the moisture condition at various depths in the soil. Daily observations are available for the continental Europe in the spatial resolution of 1 km and with the temporal extent from January 2015 to present.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `QFLAG002` | Quality flag for different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `QFLAG005` | Quality flag for different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `QFLAG010` | Quality flag for different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `QFLAG015` | Quality flag for different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `QFLAG020` | Quality flag for different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `QFLAG040` | Quality flag for different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `QFLAG060` | Quality flag for different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `QFLAG100` | Quality flag for different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `SWI002` | Soil Water Index at different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `SWI005` | Soil Water Index at different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `SWI010` | Soil Water Index at different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `SWI015` | Soil Water Index at different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `SWI020` | Soil Water Index at different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `SWI040` | Soil Water Index at different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `SWI060` | Soil Water Index at different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `SWI100` | Soil Water Index at different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `SSF` | Surface State Flag | — | `UINT8` | 0.0-3.0 | 1 | 0 |

##### SWI daily v2

`swi_europe_1km_daily_v2_geotiff`  ·  BYOC `4bd995a1-dc49-4176-a285-b1d0084ba51a`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/soil-moisture/soil-water-index/swi_europe_1km_daily_v2.html)  
Europe · 1km · 2015 - present

> Quantifies the moisture condition at various depths in the soil. Daily observations are available for the continental Europe in the spatial resolution of 1 km and with the temporal extent from January 2015 to present.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `QFLAG002` | Quality flag for different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `QFLAG005` | Quality flag for different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `QFLAG010` | Quality flag for different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `QFLAG015` | Quality flag for different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `QFLAG020` | Quality flag for different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `QFLAG040` | Quality flag for different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `QFLAG060` | Quality flag for different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `QFLAG100` | Quality flag for different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `SWI002` | Soil Water Index at different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `SWI005` | Soil Water Index at different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `SWI010` | Soil Water Index at different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `SWI015` | Soil Water Index at different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `SWI020` | Soil Water Index at different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `SWI040` | Soil Water Index at different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `SWI060` | Soil Water Index at different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `SWI100` | Soil Water Index at different time lengths | % | `UINT8` | 0.0-100.0 | 1/2 | 0 |
| `SSF` | Surface State Flag | — | `UINT8` | 0.0-4.0 | 1 | 0 |

#### Bio-geophysical parameters › Water bodies

##### ICD 20m Yearly V1

`clms_wsi_ice-cover-duration_europe_utm_20m_yearly_v1`  ·  BYOC `11107497-588f-495b-911e-85a1614ebdb2`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/water-bodies/water-and-ice-cover/clms_wsi_ice-cover-duration_europe_utm_20m_yearly_v1.html)  
Europe · 20m · 2016 - present

> The **Ice Cover Duration (ICD)** product describes how long inland waters are covered by ice. For each pixel and for a given hydrological year, it provides the number of days with ice cover. The hydrological year starts on 1 September. It is based on ice cover maps derived from **Sentinel-2** optical data (Water/Ice Cover WIC S2) and **Sentinel-1** C-band Synthetic Aperture Radar data (Water/Ice Cover WIC S1).<br><br>The product is generated at the European scale with a spatial resolution of **20 m x 20 m**.<br><br>**Data availability**: from 2016 to the present. The data can be downloaded in multiple projections and pixel spacings.<br><br>More information here.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `ICD` | Ice cover duration (in days) | [days] | `UINT16` | 0.0-366.0 | 1 | 0 |
| `ICD_QA` | Quality layer for the ice cover duration (ICD) layer | 0=high quality; 1=medium quality; 2=low quality; 3=minimal quality | `UINT16` | 0.0-3.0 | 1 | 0 |
| `NOBS1` | Number of days with Sentinel-1 based observations during the hydrological year | [days] | `UINT16` | 0.0-366.0 | 1 | 0 |
| `NOBS2` | Number of days with Sentinel-2 based observations during the hydrological year | [days] | `UINT16` | 0.0-366.0 | 1 | 0 |

##### LIE daily v2

`clms_global_lie_250m_v2_daily_geotiff`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/water-bodies/river-and-lake-ice-extent/lie_europe_250m_daily_v2.html)  
Europe · 250m

> ⚠️ **The id says `global` but the docs say Europe.** `clms_global_` is the CLMS *Global Land component* namespace, not a coverage claim.

> Classifies, in pixels, inland/freshwater bodies

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `ICD` | Ice cover duration (in days) | [days] | `UINT16` | 0.0-366.0 | 1 | 0 |
| `ICD_QA` | Quality layer for the ice cover duration (ICD) layer | 0=high quality; 1=medium quality; 2=low quality; 3=minimal quality | `UINT16` | 0.0-3.0 | 1 | 0 |
| `NOBS1` | Number of days with Sentinel-1 based observations during the hydrological year | [days] | `UINT16` | 0.0-366.0 | 1 | 0 |
| `NOBS2` | Number of days with Sentinel-2 based observations during the hydrological year | [days] | `UINT16` | 0.0-366.0 | 1 | 0 |

##### WCD 10m Yearly V1

`clms_wsi_water-cover-duration_europe_utm_10m_yearly_v1`  ·  BYOC `6cbd4f0b-834d-4e91-aa56-8c347b9cf971`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/water-bodies/water-extent/clms_wsi_water-cover-duration_europe_utm_10m_yearly_v1.html)  
Europe · 10m · 2016 - present

> The **Water Cover Duration (WCD)** product estimates the number of days land is covered by water. For each pixel and for a given hydrological year, it indicates how frequently water is present. The hydrological year starts on 1 September.   It is based on water masks derived from **Sentinel-1** radar and **Sentinel-2** optical data, combined with Water/Ice Cover data from Sentinel-2 (WIC S2).<br><br>The product is generated at the European scale with a spatial resolution of **10 m x 10 m**.<br><br>**Data availability**: from 2016 to the present. The data can be downloaded in multiple projections and pixel spacings.<br><br>More information here.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `WCD` | Water presence frequency in a hydrological year (in days) | [days] | `UINT16` | 0.0-366.0 | 1 | 0 |
| `WCD_QA` | Quality layer for the water cover duration (WCD) layer | 0=high quality; 1=medium quality; 2=low quality; 3=minimal quality; 205=cloud or cloud shadow; 253=sea water | `UINT8` | 0.0-3.0 | 1 | 0 |

##### WIC S1 60m Daily V1

`clms_wsi_water-ice-cover-s1_europe_utm_60m_daily_v1`  ·  BYOC `a4ec97d7-243c-4af3-873e-dc486d4e4a37`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/water-bodies/water-and-ice-cover/clms_wsi_water-ice-cover-s1_europe_utm_60m_daily_v1.html)  
Europe · 60m · 2016 - present

> The **Water and Ice Cover by Sentinel-1 (WICS1)** product provides information about river and lake areas covered by snow-covered or snow-free ice. It is based on synthetic aperture radar data from the **Sentinel-1** constellation.<br><br>It is generated in near real-time at European scale, with a spatial resolution of **60 m x 60 m**.<br><br>**Data availability**: from 2016 to the present.<br><br>More information here.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `WIC` | Water/Ice Cover | 1=open water; 100=snow-covered or snow-free ice; 200=radar shadow/layover/foreshortening; 255=no data | `UINT8` | 1.0-200.0 | 1 | 0 |
| `WIC_QA` | Quality layer for the Water/Ice Cover (WIC) layer | 0=high quality; 1=medium quality; 2=low quality; 3=minimal quality; 200=radar shadow/layover/foreshortening; 255=no data | `UINT8` | 0.0-3.0 | 1 | 0 |
| `QAFLAGS` | Quality flags | Bitmask layer with pixel quality flags. Bit 15 activated indicates inland water surfaces over which classification is performed. | `UINT16` | — | 1 | 0 |

##### WIC S1+S2 20m Daily V1

`clms_wsi_water-ice-cover-s1-s2_europe_utm_20m_daily_v1`  ·  BYOC `a0596412-1e04-4530-9e3e-931cf4a3b52e`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/water-bodies/water-and-ice-cover/clms_wsi_water-ice-cover-s1-s2_europe_utm_20m_daily_v1.html)  
Europe · 20m · 2016 - present

> The **Water and Ice Cover by Sentinel-1 and Sentinel-2 (WIC S1+S2)** product shows which river and lake areas are covered by ice, with or without snow. It combines data from two types of instruments acquired on the same day to increase coverage and reduce missing information. It uses water/ice cover information derived from **Sentinel-2** optical images (WIC S2), and from **Sentinel-1** radar data (WIC S1).<br><br>The product is generated in near real-time at European scale, with a spatial resolution of **20 m x 20 m**.<br><br>**Data availability**: from 2016 to the present.<br><br>More information here.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `WIC` | Water/Ice Cover | Water/ice cover classes: 1=open water; 100=snow-covered or snow-free ice; 200=radar shadow/layover/foreshortening; 205=cloud or cloud shadow; 254=other features (land, vegetation, salt seas); 255=no data | `UINT8` | 1.0-254.0 | 1 | 0 |
| `WIC_QA` | Quality layer for the Water/Ice Cover (WIC) layer | Quality assessment for WIC: 0=high quality; 1=medium quality; 2=low quality; 3=minimal quality; 200=radar shadow/layover/foreshortening; 255=no data | `UINT8` | 0.0-200.0 | 1 | 0 |
| `QAFLAGS` | Quality flags | Bitmask with pixel quality flags. Bit 9: satellite sensor type (optical=0, radar=1). | `UINT16` | — | 1 | 0 |

##### WIC S2 20m Daily V1

`clms_wsi_water-ice-cover-s2_europe_utm_20m_daily_v1`  ·  BYOC `4c770f75-303d-4b8e-bf6d-9ca148b34cfb`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/bio-geophysical-parameters/water-bodies/water-and-ice-cover/clms_wsi_water-ice-cover-s2_europe_utm_20m_daily_v1.html)  
Europe · 20m · 2016 - present

> The **Water and Ice Cover by Sentinel-2 (WICS2)** product provides the water and ice extent over land. A water mask is used to differentiate between snow on ice-covered water areas and snow on land. Cloud detection in the Sentinel-2 imagery is performed using the MAJA software.<br><br>It is generated in near real-time at European scale based on optical satellite data from the Sentinel-2 constellation, with a spatial resolution of **20 m x 20 m**.<br><br>**Data availability**: from 2016 to the present. No product is generated for a Sentinel-2 tile when cloud cover exceeds 90%.<br><br>More information here.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `WIC` | Water/Ice Cover | 1=open water; 100=snow-covered or snow-free ice; 205=cloud or cloud shadow; 254=other (land/vegetation/sea); 255=no data | `UINT8` | 1.0-254.0 | 1 | 0 |
| `WIC_QA` | Quality layer for the Water/Ice Cover (WIC) layer | 0=high quality; 1=medium quality; 2=low quality; 3=minimal quality | `UINT8` | 0.0-3.0 | 1 | 0 |
| `QAFLAGS` | Quality flags | Bitmask layer with pixel quality flags. | `UINT8` | — | 1 | 0 |
| `PRB` | Probability of the class indicated by the Water/Ice Cover (WIC) layer | [%] | `UINT8` | 0.0-100.0 | 1 | 0 |

#### Land cover & land use › Clcplus lulucf instance

##### CLCplus LULUCF Instance 100m Yearly V1

`clms_clcplus_lulucf-instance_europe_100m_yearly_v1`  ·  BYOC `714b4c8d-2d89-4ed8-933c-f7c8bb7a1d4b`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/clcplus-lulucf-instance/clms_clcplus_lulucf-instance_europe_100m_yearly_v1.html)  
Europe · 100m · 2018 - present

> This metadata refers to the CORINE Land Cover Plus Land Use, Land-Use Change and Forestry Instance (CLCplus LULUCF Instance), an annually updated, pan-European, spatially consistent and seamless geospatial proxy for land use reporting under the LULUCF regulation. The product is delivered as a single raster layer with a spatial resolution of 100 m, derived from multiple pan-European Copernicus Land Monitoring Service (CLMS) high resolution input datasets. The LULUCF Instance is available for the reference years 2018, 2021, 2022 and 2023, with production moving to an annual update cycle starting from the 2021 product. Each raster cell represents a dominant LULUCF land-use class, assigned according to thematic and spatial rulesets implemented during the extraction process. While each pixel corresponds primarily to one of the six main LULUCF land use categories - forest land, grassland, cropland, settlements, wetlands, and other lands - the dataset further differentiates these categories into sub classes, resulting in a total of 27 classes. This classification structure supports greenhouse gas reporting and other applications within the LULUCF sector by providing a harmonised and policy relevant representation of land use across Europe. It is crucial to understand that this product is fundamentally different from other CLMS products, as it is not based directly on satellite image classification or visual interpretation. Instead, it is produced through the combination and integration of existing CLMS data layers. Consequently, the dataset does not introduce fundamentally new information; rather, its novelty lies in the expert driven integration of multiple sources to produce a LULUCF oriented land use representation. More information here.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `LULUCF_INSTANCE` | Pan-European annual raster LULUCF dataset | [classes] | `UINT8` | 11.0-254.0 | 1 | 0 |

#### Land cover & land use › Croplands

##### CPBSA 10m Yearly

`clms_vlcc_bare-soil-after_europe_10m_yearly_v1`  ·  BYOC `163c6d26-0b32-44b9-8552-7b38af71cff1`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/croplands/cropping-patterns/bare-soil-after/clms_vlcc_bare-soil-after_europe_10m_yearly_v1.html)  
Europe · 10m · 2017 - present

> The High Resolution Layer Cropping Patterns - Bare Soil After (CPBSA) raster product provides bare soil period (in days) after the harvest of the main annual crop. Note that the bare soil period cannot transcend the calendar year for which the product is generated.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `CPBSA` | Bare soil duration after main season | days / quality flags | `UINT16` | 0.0-65534.0 | 1 | 0 |
| `Name` | Description | Units | `Source format` | Range | Scaling | Offset |
| `---------------` | -------------- | --------- | `----------------` | ------- | --------- | -------- |
| `CPBSACL` | Confidence of bare soil after season | days / quality flags | `UINT16` | 0.0-65534.0 | 1 | 0 |

##### CPCST 10m Yearly

`clms_vlcc_cropping-seasons-types_europe_10m_yearly_v1`  ·  BYOC `c2483b33-1e6b-4e69-a07a-1d64ec438253`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/croplands/cropping-patterns/cropping-seasons-types/clms_vlcc_cropping-seasons-types_europe_10m_yearly_v1.html)  
Europe · 10m · 2017 - present

> The High Resolution Layer Cropping Patterns - Cropping Seasons Types (CPCSY) raster product provides the number of different crop types grown in a 3-year period [0-3] (excluding cover crops).

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `CPCST` | Crop type diversity over 3 years | 1 = 1 annual crop type over 3-years period, 2 = 2 annual crop types over 3-years period, 3 = 3 annual crop types over 3-years period, 65528 = 65528 | `UINT16` | 1.0-65528.0 | 1 | 0 |

##### CPCSY 10m Yearly

`clms_vlcc_cropping-seasons_europe_10m_yearly_v1`  ·  BYOC `93db885a-db11-4a7d-b035-bd6020a4447d`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/croplands/cropping-patterns/cropping-seasons/clms_vlcc_cropping-seasons_europe_10m_yearly_v1.html)  
Europe · 10m · 2017 - present

> The High Resolution Layer Cropping Patterns - Cropping Seasons Yearly (CPCSY) raster product provides number of growing seasons detected within 1 year (0/1/2).

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `CPCSY` | Number of growing seasons per year | 0 = No annual cropland, 1 = 1 growing season, 2 = 2 growing seasons, 65526 = 65526, 65527 = 65527, 65531 = 65531, 65532 = 65532, 65533 = 65533, 65535 = Outside area | `UINT16` | 0.0-65535.0 | 1 | 0 |

##### CPMCD 10m Yearly

`clms_vlcc_main-crop-duration_europe_10m_yearly_v1`  ·  BYOC `0c1cf3ba-b04b-48c1-982f-e5861c0fdbd1`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/croplands/cropping-patterns/main-crop-duration/clms_vlcc_main-crop-duration_europe_10m_yearly_v1.html)  
Europe · 10m · 2017 - present

> The High Resolution Layer Cropping Patterns - Main Crop Duration (CPMCD) raster product provides the duration (in days) of the growing season for the main (annual) crop.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `CPMCD` | Main crop growing season duration | days | `UINT16` | 0.0-365.0 | 1 | 0 |
| `Name` | Description | Units | `Source format` | Range | Scaling | Offset |
| `---------------` | -------------- | --------- | `----------------` | ------- | --------- | -------- |
| `CPMCDCL` | Confidence of main crop duration | confidence | `UINT16` | 0.0-100.0 | 1 | 0 |

##### CPMCE 10m Yearly

`clms_vlcc_main-crop-emergence_europe_10m_yearly_v1`  ·  BYOC `10c22197-036f-44d0-b09c-5864d811f154`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/croplands/cropping-patterns/main-crop-emergence/clms_vlcc_main-crop-emergence_europe_10m_yearly_v1.html)  
Europe · 10m · 2017 - present

> The High Resolution Layer Cropping Patterns - Main Crop Emergence (CPMCE) raster product provides the emergence date of the main (annual) crop expressed in DOY (day of year). YYDOY where YY = last 2 digits of the year (e.g. 19 for 2019) and DOY is the day of the year (1-365).

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `CPMCE` | Main crop emergence date | YYDOY where YY = last 2 digits of the year (e.g. 19 for 2019) and DOY is the day of the year (1-366) | `UINT16` | 16001.0-99366.0 | 1 | 0 |
| `Name` | Description | Units | `Source format` | Range | Scaling | Offset |
| `---------------` | -------------- | --------- | `----------------` | ------- | --------- | -------- |
| `CPMCECL` | Confidence of main crop emergence | Days | `UINT16` | 1.0-40.0 | 1 | 0 |

##### CPMCH 10m Yearly

`clms_vlcc_main-crop-harvest_europe_10m_yearly_v1`  ·  BYOC `78f39ff7-e8f3-4579-a2e4-c6a99cc6e49f`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/croplands/cropping-patterns/main-crop-harvest/clms_vlcc_main-crop-harvest_europe_10m_yearly_v1.html)  
Europe · 10m · 2017 - present

> The High Resolution Layer Cropping Patterns - Main Crop Harvest (CPMCH) raster product provides the harvest date of the main (annual) crop expressed in days of the year (DOY). The harvest is considered as the time of removal of most of the biomass. YYDOY where YY = last 2 digits of the year (e.g. 19 for 2019) and DOY is the day of the year (1-365)

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `CPMCH` | Main crop harvest date | YYDOY where YY = last 2 digits of the year (e.g. 19 for 2019) and DOY is the day of the year (1-366) | `UINT16` | 17001.0-99366.0 | 1 | 0 |
| `Name` | Description | Units | `Source format` | Range | Scaling | Offset |
| `---------------` | -------------- | --------- | `----------------` | ------- | --------- | -------- |
| `CPMCHCL` | Confidence of main crop harvest | Days | `UINT16` | 1.0-40.0 | 1 | 0 |

##### CPSCD 10m Yearly

`clms_vlcc_secondary-crop-duration_europe_10m_yearly_v1`  ·  BYOC `deada876-a483-4b45-baf2-85086860ab8b`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/croplands/cropping-patterns/secondary-crop-duration/clms_vlcc_secondary-crop-duration_europe_10m_yearly_v1.html)  
Europe · 10m · 2017 - present

> The High Resolution Layer Cropping Patterns - Secondary Crop Duration (CPSCD) raster product provides the duration (in days) of the cover crop season (can exceed the calendar year).

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `CPSCD` | Secondary crop season duration | days | `UINT16` | 0.0-365.0 | 1 | 0 |
| `Name` | Description | Units | `Source format` | Range | Scaling | Offset |
| `---------------` | -------------- | --------- | `----------------` | ------- | --------- | -------- |
| `CPSCDCL` | Confidence of secondary crop duration | confidence | `UINT16` | 0.0-100.0 | 1 | 0 |

##### CPSCE 10m Yearly

`clms_vlcc_secondary-crop-emergence_europe_10m_yearly_v1`  ·  BYOC `86a3ea15-e4b0-4aed-874e-492f0934e800`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/croplands/cropping-patterns/secondary-crop-emergence/clms_vlcc_secondary-crop-emergence_europe_10m_yearly_v1.html)  
Europe · 10m · 2017 - present

> The High Resolution Layer Cropping Patterns - Secondary Crop Emergence (CPSCE) raster product provides the date of emergence of the cover crop in days of the year (DOY). YYDOY where YY = last 2 digits of the year (e.g. 19 for 2019) and DOY is the day of the year (1-365) This dataset is provided annually starting in 2017 with 10 meter rasters (fully conformant with the EEA reference grid) in 100 x 100 km tiles covering the EEA38 countries. High Resolution Layer Croplands product is part of the European Union’s Copernicus Land Monitoring Service. Confidence layer available for the dataset. This dataset includes data from the French Overseas Territories (DOMs)

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `CPSCE` | Secondary crop emergence data | YYDOY where YY = last 2 digits of the year (e.g. 19 for 2019) and DOY is the day of the year (1-366) | `UINT16` | 19001.0-23366.0 | 1 | 0 |

##### CPSCT 10m Yearly

`clms_vlcc_secondary-crop-types_europe_10m_yearly_v1`  ·  BYOC `63d3bcc2-413c-43c1-bde4-d6252860b666`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/croplands/cropping-patterns/secondary-crop-types/clms_vlcc_secondary-crop-types_europe_10m_yearly_v1.html)  
Europe · 10m · 2017 - present

> The High Resolution Layer Cropping Patterns - Secondary Crop Type (CPSCT) raster product indicates if a cover crop was present within the respective calendar year and further segregates the types of cover crop into: short summer, long summer, short winter and long winter cover crop.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `CPSCT` | Classification of secondary crop type | 0 = No annual cropland, 1 = Short summer CC, 2 = Long summer CC, 3 = Short winter CC, 4 = Long winter CC, 65526 = 65526, 65527 = 65527, 65530 = 65530, 65531 = 65531, 65532 = 65532, 65533 = 65533, 65534 = 65534, 65535 = Outside area | `UINT16` | 0.0-65535.0 | 1 | 0 |

##### CTY 10m Yearly

`clms_vlcc_crop-types_europe_10m_yearly_v1`  ·  BYOC `4fa71893-371f-4440-97c4-917f569f67b2`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/croplands/crop-types/crop-types/clms_vlcc_crop-types_europe_10m_yearly_v1.html)  
Europe · 10m · 2017 - present

> The High Resolution Layer Crop Types (CTY) raster product provides high resolution crop type classification for 17 classes of both arable and permanent crops accross the EEA38 extent. Using both Sentinel-1 and Sentiel-2, the model is finetuned to first map the crop field boundaries, and then determine the main crop for each field.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `CTY` | Cropland crop type classification (19 types) | Categorical label on crop type | `UINT16` | 0.0-3200.0 | 1 | 0 |
| `Name` | Description | Units | `Source format` | Range | Scaling | Offset |
| `---------------` | -------------- | --------- | `----------------` | ------- | --------- | -------- |
| `CTYCL` | Confidence of crop type classification | Probability as obtained from the confidence of the selected crop type class | `UINT8` | 0.0-100.0 | 1 | 0 |

#### Land cover & land use › Grasslands

##### GRA 100m Yearly

`clms_vlcc_grassland_europe_100m_yearly_v1`  ·  BYOC `f99fe8ab-0c49-4c68-acd2-1687b0e04816`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/grasslands/grassland-and-herbaceous/grassland/clms_vlcc_grassland_europe_100m_yearly_v1.html)  
Europe · 100m · 2017 - present

> The High Resolution Layer Grassland (GRA) raster product provides a binary status layer of grassland/non-grassland mask. This grassy and non-woody vegetation baseline product includes all kinds of grasslands: managed grassland, semi-natural grassland and natural grassy vegetation. It does not include temporary grasslands, which are masked out using the corresponding Ploughing indicator (PLOUGH), indicating on the number of years since a pixel was last ploughed. In the 100 meter raster product, the number of Grassland pixels are counted and the percentages stored in each 100 meter cell. The class 255 = outside area is predefined by the 100m boundary layer and remains unchanged.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `GRA` | Grassland presence and percentage coverage | % of grassland density | `UINT8` | 0.0-100.0 | 1 | 0 |

##### GRA 10m Yearly

`clms_vlcc_grassland_europe_10m_yearly_v1`  ·  BYOC `74eeaebb-d8eb-4e7e-909c-ab55465a8791`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/grasslands/grassland-and-herbaceous/grassland/clms_vlcc_grassland_europe_10m_yearly_v1.html)  
Europe · 10m · 2017 - present

> The High Resolution Layer Grassland (GRA) raster product provides a binary status layer of grassland/non-grassland mask. This grassy and non-woody vegetation baseline product includes all kinds of grasslands: managed grassland, semi-natural grassland and natural grassy vegetation. It does not include temporary grasslands, which are masked out using the corresponding Ploughing indicator (PLOUGH), indicating on the number of years since a pixel was last ploughed.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `GRA` | Classification of grassland / non-grassland | 0: all non-grassland areas, 1: grassland, 255: outside area | `UINT8` | 0.0-255.0 | 1 | 0 |
| `Name` | Description | Units | `Source format` | Range | Scaling | Offset |
| `---------------` | -------------- | --------- | `----------------` | ------- | --------- | -------- |
| `GRACL` | Confidence of grassland classification | None | `UINT8` | 1.0-255.0 | 1 | 0 |

##### GRAMD 10m Yearly 4 Events

`clms_vlcc_grassland-mowing-dates_europe_10m_yearly_v1`  ·  BYOC `23039406-da63-45df-8766-ccb5afce75a5`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/grasslands/grassland-mowing-events/grassland-mowing-dates/clms_vlcc_grassland-mowing-dates_europe_10m_yearly_v1.html)  
Europe · 10m · 2017 - present

> The High Resolution Layer Grassland Mowing Dates (GRAMD) raster product provides at pan-European level in the spatial resolution of 10 m a basic land cover classification, flagging and mapping the start date (DOY) (GRAMD) within the detected Herbaceous cover layer (temporal and permanent grassland)) with a Minimum Mapping Unit (MMU) of 0.25 ha. The GRAMD product will flag and map the dates (Day of Year) of each mowing event on temporary or permanent grassland per year, resulting in a product split in four different rasters per year.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `GRAMD1` | Classification of grassland mowing dates | Day of Year (DOY) / 0: flag for no mowing detected; 65533: flag for non-herbaceous areas | `UINT16` | 1.0-366.0 | 0 | 1 |
| `GRAMD2` | Classification of grassland mowing dates | Day of Year (DOY) / 0: flag for no mowing detected; 65533: flag for non-herbaceous areas | `UINT16` | 1.0-366.0 | 0 | 1 |
| `GRAMD3` | Classification of grassland mowing dates | Day of Year (DOY) / 0: flag for no mowing detected; 65533: flag for non-herbaceous areas | `UINT16` | 1.0-366.0 | 0 | 1 |
| `GRAMD4` | Classification of grassland mowing dates | Day of Year (DOY) / 0: flag for no mowing detected; 65533: flag for non-herbaceous areas | `UINT16` | 1.0-366.0 | 0 | 1 |

##### GRAME 10m Yearly

`clms_vlcc_grassland-mowing-events_europe_10m_yearly_v1`  ·  BYOC `480a24cb-713c-4e72-bcf9-a4edba3f4341`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/grasslands/grassland-mowing-events/grassland-mowing-events/clms_vlcc_grassland-mowing-events_europe_10m_yearly_v1.html)  
Europe · 10m · 2017 - present

> The High Resolution Layer Grassland Mowing Events (GRAME) raster product provides a basic land cover classification containing respectively the number of grassland mowing events within the detected Herbaceous cover layer (temporal and permanent grassland)) with a Minimum Mapping Unit (MMU) of 0.25 ha. The GRAME product will flag and map the number of mowing events (1, 2, 3, or 4+) on temporary or permanent grassland detected per year.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `GRAME` | Count of grassland mowing events | Number of mowing events (1, 2, 3, or 4+). Flag for non-herbaceous area: 253. | `UINT8` | 1.0-253.0 | 1 | 0 |
| `Name` | Description | Units | `Source format` | Range | Scaling | Offset |
| `---------------` | -------------- | --------- | `----------------` | ------- | --------- | -------- |
| `GRAMECL` | Confidence of grassland mowing events | Confidence percentage (0-100%) | `UINT8` | 0.0-100.0 | 1 | 0 |

##### HER 10m Yearly

`clms_vlcc_herbaceous-cover_europe_10m_yearly_v1`  ·  BYOC `e2d6c154-b874-454e-9bb1-43d04b45a92d`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/grasslands/grassland-and-herbaceous/herbaceous-cover/clms_vlcc_herbaceous-cover_europe_10m_yearly_v1.html)  
Europe · 10m · 2017 - present

> The High Resolution Layer Herbaceous cover (HER) raster product provides a basic land cover classification with 2 thematic classes (temporal and permanent herbaceous / non-herbaceous). The production of the herbaceous layer is primarily based on the probability estimates obtained from the Base Vegetation Layer (BVL) which also serves to harmonize the different vegetated HRL products (Grasslands, Tree Cover and Forests, Croplands). HER is further used as input for the Grassland status layer (GRA) extracting the permanent herbaceous in combination with the Ploughing indicator (PLOUGH).

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `HER` | Classification of herbaceous / non-herbaceous | Non-grassland in reference year, Permanent and temporary grassland in reference year | `UINT8` | 0.0-1.0 | 1 | 0 |

##### PLOUGH 10m Yearly

`clms_vlcc_ploughing-indicator_europe_10m_yearly_v1`  ·  BYOC `c9750aed-88a5-4a0d-907a-1cc406052886`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/grasslands/grassland-and-herbaceous/ploughing-indicator/clms_vlcc_ploughing-indicator_europe_10m_yearly_v1.html)  
Europe · 10m · 2017 - present

> The High Resolution Layer Ploughing indicator (PLOUGH) raster product continues the 2015 and 2018 PLOUGH Layer following a rolling archive principle by adding current information and removing historic years. It indicates the number of years since the last indication of ploughing within the permanent grassland area. PLOUGH is derived by taking into account the series of binary HER layers, the BVL classifications and HR VPP PPI (Plant Phenology Index) quantiles. BVL classes 4 (crop) and 7 (overlaying layer between herbaceous and crop) indicate a ploughing event. Low HR VPP PPI quantiles indicate low vegetation at a certain time of the year. For years with missing information (2016 and earlier) the ploughing information from the historic PLOUGH product is considered which causes some issues.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `PLOUGH` | Years since last ploughing (herbaceous) | Years since last indication of ploughing/Change of herbaceous cover | `UINT8` | 0.0-100.0 | 1 | 0 |

#### Land cover & land use › Tree cover and forests

##### BCD 100m Yearly

`clms_vlcc_broadleaved-cover-density_europe_100m_yearly_v1`  ·  BYOC `a06a42ae-f899-4a07-a5cd-fb7fd920d6c1`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/tree-cover-and-forests/dominant-leaf-type/broadleaved-cover-density/clms_vlcc_broadleaved-cover-density_europe_100m_yearly_v1.html)  
Europe · 100m · 2018 - present

> The High Resolution Layer Broadleaved Density (BCD) dataset provides information on the percentage of broadleaved pixels at 100m spatial resolution, and is derived through aggregation of the 10m DLT for the respective reference year. Within each cell the number of broadleaved pixels are counted and the percentages stored into in the 100m pixel of the BCD. The class 255 = outside area is predefined by the 100m boundary layer and remains unchanged.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `BCD` | Broadleaved cover density (100 m) | % of broadleaved cover density | `UINT8` | 0.0-100.0 | 1 | 0 |

##### CCD 100m Yearly

`clms_vlcc_coniferous-cover-density_europe_100m_yearly_v1`  ·  BYOC `a0edd575-c763-4c4a-a910-631df3df4506`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/tree-cover-and-forests/dominant-leaf-type/coniferous-cover-density/clms_vlcc_coniferous-cover-density_europe_100m_yearly_v1.html)  
Europe · 100m · 2018 - present

> The High Resolution Layer Coniferous Cover Density (CCD) dataset provides information on the percentage of coniferous pixels at 100m spatial resolution, and is derived through aggregation of the 10m DLT for the respective reference year. Within each cell the number of coniferous pixels are counted and the percentages stored into in the 100m pixel of the CCD. The class 255 = outside area is predefined by the 100m boundary layer and remains unchanged.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `CCD` | Coniferous cover density (100 m) | % | `UINT8` | 0.0-100.0 | 1 | 0 |

##### DLT 10m Yearly

`clms_vlcc_dominant-leaf-type_europe_10m_yearly_v1`  ·  BYOC `42b2ef44-5983-4bd1-9e2f-52c093c08b3d`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/tree-cover-and-forests/dominant-leaf-type/dominant-leaf-type/clms_vlcc_dominant-leaf-type_europe_10m_yearly_v1.html)  
Europe · 10m · 2018 - present

> The High Resolution Dominant Leaf Type (DLT) raster product provides a basic land cover classification with 3 thematic classes (all non-tree covered areas, broadleaved and coniferous).

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `DLT` | Dominant leaf type classification | 0 = All non-tree covered areas, 1 = Broadleaved trees, 2 = Coniferous trees | `UINT8` | 0.0-2.0 | 1 | 0 |
| `Name` | Description | Units | `Source format` | Range | Scaling | Offset |
| `---------------` | -------------- | --------- | `----------------` | ------- | --------- | -------- |
| `DLTCL` | Confidence of dominant leaf type | Confidence percentage (0-100%) | `UINT8` | 0.0-253.0 | 1 | 0 |

##### DLTC 20m 3yearly

`clms_vlcc_dominant-leaf-type-change_europe_20m_3yearly_v1`  ·  BYOC `9bdecd15-4101-4859-8d00-b2f49c2c6876`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/tree-cover-and-forests/dominant-leaf-type/dominant-leaf-type-change/clms_vlcc_dominant-leaf-type-change_europe_20m_3yearly_v1.html)  
Europe · 20m · 2018 - 2021

> The High Resolution Layer Dominant Leaf Type Change (DLTC) 2018-2021 raster product provides information on the change between the reference years 2018 and 2021 and consists of 7 thematic classes (unchanged areas with no tree cover / new broadleaved cover / new coniferous cover / loss of broadleaved cover / loss of coniferous cover / unchanged areas with tree cover / potential change among dominant leaf types).

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `DLTC` | Tree cover change classification | 0 = unchanged areas with no tree cover, 1 = new broadleaved cover, 2 = new coniferous cover, 3 = loss of broadleaved cover, 4 = loss of coniferous cover, 10 = unchanged areas with tree cover, 255 = outside area | `UINT8` | 0.0-255.0 | 1 | 0 |

##### FADSL 10m 3-yearly

`clms_vlcc_forest-additional-support-layer_europe_10m_3yearly_v1`  ·  BYOC `912a6eb9-12f2-4cad-a821-2c5b03dfccbb`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/tree-cover-and-forests/forest-type/forest-additional-support-layer/clms_vlcc_forest-additional-support-layer_europe_10m_3yearly_v1.html)  
Europe · 10m · 2018 - 2021

> The High Resolution Layer Forest Additional Support Layer (FADSL) provides information on trees under agricultural use or in urban context to be excluded from the Forest Type (FTY) product and at 10m spatial resolution. The derivation of Forest Additional Support Layer (FADSL) is based on the spatial intersection of the 10m DLT and TCD layers with CORINE Land Cover (CLC) 2018 and HRL Imperviousness Degree 2018 with 10 m spatial resolution; TCD range of 10-100%; with a MMW of 10m and no MMU (pixel base). This dataset is provided on a 3-yearly frequency in 10 meter rasters (fully conformant with the EEA reference grid) in 100 x 100 km tiles covering the EEA38 countries. High Resolution Layer Tree Cover and Forest product is part of the European Union’s Copernicus Land Monitoring Service. This dataset includes data from the French Overseas Territories (DOMs)

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `FADSL` | Forest Additional Support Layer over 3 years | 3: trees predominantly used for agricultural practices - broadleaved (from CLC2018); 4: trees in urban context - broadleaved and coniferous (from IMD 2018); 5: trees in urban context - broadleaved and coniferous (from CLC 2018) | `UINT8` | 3.0-5.0 | 1 | 0 |

##### FTY 100m 3-yearly

`clms_vlcc_forest-type_europe_100m_3yearly_v1`  ·  BYOC `d267ca76-6afb-4992-99d6-67c67df4820c`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/tree-cover-and-forests/forest-type/forest-type/clms_vlcc_forest-type_europe_100m_3yearly_v1.html)  
Europe · 100m · 2018 - present

> The High Resolution Layer Forest Type (FTY) dataset provides the Forest Type estimation at 100 meter spatial resolution. The number of broadleaved and coniferous pixels are counted and the percentages stored in the 100m cell. The class 255 = outside area is predefined by the 100m boundary layer and remains unchanged.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `FTY` | Forest Type over 3 years (100m) | 1: broadleaved forest, 2: coniferous forest, 3: mixed zones | `UINT8` | 0.0-3.0 | 1 | 0 |

##### FTY 10m 3yearly

`clms_vlcc_forest-type_europe_10m_3yearly_v1`  ·  BYOC `4d1aad1a-f800-43c5-87d0-5565a9a31c12`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/tree-cover-and-forests/forest-type/forest-type/clms_vlcc_forest-type_europe_10m_3yearly_v1.html)  
Europe · 10m · 2018 - present

> The High Resolution Layer Forest Type (FTY) provides a forest classification with 3 thematic classes (all non-forest areas / broadleaved forest / coniferous forest) at 10m spatial resolution and with a Minimum Mapping Unit (MMU) of 0.5 ha. This raster layer is largely following the FAO (Food and Agriculture Organisation of the United Nations) forest definition with tree covered areas in agricultural and urban context excluded using the respective Forest Additional Support Layer (FADSL).

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `FTY` | Forest Type over 3 years (10m) | 1: broadleaved forest, 2: coniferous forest | `UINT8` | 0.0-2.0 | 1 | 0 |

##### TCD 100m Yearly

`clms_vlcc_tree-cover-density_europe_100m_yearly_v1`  ·  BYOC `edd3c5f5-da8e-463f-8c9a-712aa451d37e`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/tree-cover-and-forests/tree-cover-density/tree-cover-density/clms_vlcc_tree-cover-density_europe_100m_yearly_v1.html)  
Europe · 100m · 2018 - present

> The High Resolution Layer Tree Cover Density (TCD) dataset provides information on the proportional crown coverage per pixel at 100 meter spatial resolution and ranges from 0% (all non-tree covered areas) to 100%, whereby Tree Cover Density is defined as the "vertical projection of tree crowns to a horizontal earth’s surface“. This product is an aggregation of its corresponding high resolution dataset.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `TCD` | Tree cover density (100 m) | % | `UINT8` | 1.0-100.0 | 1 | 0 |

##### TCD 10m Yearly

`clms_vlcc_tree-cover-density_europe_10m_yearly_v1`  ·  BYOC `3751d55a-7370-4071-9543-493ec3341d16`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-land-use-mapping/tree-cover-and-forests/tree-cover-density/tree-cover-density/clms_vlcc_tree-cover-density_europe_10m_yearly_v1.html)  
Europe · 10m · 2018 - present

> The High Resolution Layer Tree Cover Density (TCD) dataset provides information on the proportional crown coverage per pixel at 10 meter spatial resolution and ranges from 0% (all non-tree covered areas) to 100%, whereby Tree Cover Density is defined as the "vertical projection of tree crowns to a horizontal earth’s surface“.

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `TCD` | Tree cover density (10 m) | % | `UINT8` | 0.0-96.0 | 1 | 0 |
| `Name` | Description | Units | `Source format` | Range | Scaling | Offset |
| `---------------` | -------------- | --------- | `----------------` | ------- | --------- | -------- |
| `TCDCL` | Confidence of tree cover density | None | `UINT8` | 4.0-255.0 | 1 | 0 |

#### Priority areas › Urban atlas

##### UA BBH 3-yearly 2021

`clms_ua_building-height_europe_10m_3yearly_v1_2021`  ·  BYOC `62887e25-816e-4f4e-be0e-5e0f5a6640c9`  ·  [docs](https://documentation.dataspace.copernicus.eu/APIs/SentinelHub/Data/clms/land-cover-and-use-in-priority-areas/urban-atlas/building-height/clms_ua_building-height_europe_10m_3yearly_v1.html)  
Europe · 10m · 2021 - 2021

> Urban Atlas Building Block Height 2021 is a 10 m high resolution raster layer containing height information generated for selected cities and urban areas as part of the Urban atlas suite of products. Height information is based on satellite information and derived datasets like the digital surface model, the digital terrain model and the normalized digital surface model (DSM).

| Band | Meaning | Units | Type | Raw range | Scaling | Offset |
|---|---|---|---|---|---|---|
| `BBH` | UA 2021 Building Height (10 m raster) | meters | `UINT16` | 0.0-368.0 | 1 | 0 |
