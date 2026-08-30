# Papers you could implement

A menu of **54 published methods** that work on data you can reach from a free CDSE account.
It exists for one moment in the workshop: *"implement a paper"* is one of the three ways into
Exercise 3, and staring at a blank page is where people stall.

## How to use it

Pick a row, follow the DOI, read the paper, and **write the equation down yourself before you
ask an AI for anything.** Then check what the AI gives you against what you wrote.

🔑 **The formulas are deliberately not in this file.** Deriving one from the paper is the
exercise; having it handed to you turns the exercise into transcription. Every row below is
open access, so the real thing is one click away.

## What has and has not been checked

- ✅ **The citations are verified.** Author, year, journal and DOI resolved via Crossref.
- ✅ **The formulas were read off the primary PDF** when this list was assembled, so the
  papers really do contain a closed-form, per-pixel method. You are not being sent on a
  wild goose chase.
- ⚠️ **Nobody has run these over your area.** Fit is the part you find out yourself, and a
  published threshold from one continent often needs moving on another.
- ⚠️ **A paper is not an oracle.** At least one entry here prints an equation that
  contradicts its own prose. If the result looks wrong, suspect the paper as readily as
  your code.

## Vegetation, soil and water

| Index | What it is for | Level | Paper |
|---|---|---|---|
| **kNDVI** | Vegetation, where plain NDVI saturates | EASY | Camps-Valls et al. 2021, *Science Advances* 7(9):eabc7447 · [10.1126/sciadv.abc7447](https://doi.org/10.1126/sciadv.abc7447) |
| **SVHI** | Chlorophyll + leaf-water + protein stress; designed to beat NDVI/NDMI on *early* water stress | — | Kumar et al. 2025, *Frontiers in Remote Sensing* 6:1581355 · [10.3389/frsen.2025.1581355](https://doi.org/10.3389/frsen.2025.1581355) |
| **SWI** | Open water including saline, sediment-laden and ice-bearing | — | Jiang et al. 2020, *ISPRS Annals* V-3-2020:33–38 · [10.5194/isprs-annals-v-3-2020-33-2020](https://doi.org/10.5194/isprs-annals-v-3-2020-33-2020) |
| **MBI** | Bare/fallow soil, separating it from built-up | — | Nguyen et al. 2021, *Land* 10(3):231 · [10.3390/land10030231](https://doi.org/10.3390/land10030231) |
| **NBR+** | Burned area with water and cloud suppression built in | — | Alcaras, Costantino, Guastaferro, Parente & Pepe 2022, *Remote Sensing* 14(7):1727 · [10.3390/rs14071727](https://doi.org/10.3390/rs14071727) |
| **CFI** | Flowering canola, separated from winter wheat — which NDVI cannot do | — | Tian et al. 2022, *Remote Sensing* 14(5):1113 · [10.3390/rs14051113](https://doi.org/10.3390/rs14051113) |
| **CSI** | Leaf chlorophyll concentration, via published per-biome regressions | — | Zhang, Hu et al. 2022, *Methods in Ecology and Evolution* 13(12):2771–2787 · [10.1111/2041-210X.13994](https://doi.org/10.1111/2041-210X.13994) |
| **FDI** | Floating plastic, Sargassum and foam, as a departure from a NIR baseline | — | Biermann, Clewley, Martinez-Vicente & Topouzelis 2020, *Sci Rep* 10:5364 · [10.1038/s41598-020-62298-z](https://doi.org/10.1038/s41598-020-62298-z) |
| **NDI(B08, B02)** | Marine debris salience. Beat FDI and the Plastic Index for visualisation at Accra, Durban and Mytilene | — | van Dalen, Asano & Russwurm 2025, IEEE GRSL · [10.1109/LGRS.2025.3572407](https://doi.org/10.1109/LGRS.2025.3572407) |
| **KDI** | Herbicide-resistant weed against cereal canopy. Fully closed-form, published fixed weights | — | Lotfi et al. 2026, *Machine Learning with Applications* · [10.1016/j.mlwa.2026.100914](https://doi.org/10.1016/j.mlwa.2026.100914) |
| **BSSI** | Bare soil, using the *shape* of the spectrum rather than a two-band contrast | EASY–MEDIUM | Zhang, Fan, Zhang & Jiao 2022 · [10.21203/rs.3.rs-1846168/v1](https://doi.org/10.21203/rs.3.rs-1846168/v1) |
| **SRVI** | — | — | Chrysostomou et al. 2026, *Scientific Reports* · [10.1038/s41598-025-34720-x](https://doi.org/10.1038/s41598-025-34720-x) |
| **ENDBSI** | — | — | Chen et al. 2026, *GIScience & Remote Sensing* · [10.1080/15481603.2026.2626630](https://doi.org/10.1080/15481603.2026.2626630) |
| **Balod soil-salinity index** | — | — | Deshpande et al. 2025, *J. Landscape Ecology* 18(2) · [10.2478/jlecol-2025-0013](https://doi.org/10.2478/jlecol-2025-0013) |

## Soil and agriculture

| Index | What it is for | Level | Paper |
|---|---|---|---|
| **EOMI1–4** | Compost and manure freshly spread on bare cropland. **EOMI2 is the best performer** | EASY | Dodin et al. 2021, *Remote Sensing* 13(9):1616 · [10.3390/rs13091616](https://doi.org/10.3390/rs13091616) |
| **MSI** | Manure and slurry freshly spread on bare ground | EASY | Dubbini et al. 2024, *Sensors* 24(14):4687 · [10.3390/s24144687](https://doi.org/10.3390/s24144687) |
| **NDTI** | Tillage and crop residue cover | EASY | Van Deventer 1997, printed verbatim as Eq. 2 in Hively et al. 2021 · [10.3390/rs13183718](https://doi.org/10.3390/rs13183718) |
| **DBSI** | Bare soil in arid and semi-arid cities | — | Rasul et al. 2018, *Land* 7(3):81 · [10.3390/land7030081](https://doi.org/10.3390/land7030081) |
| **OPTRAM** | **MEDIUM.** Contrast against MBI (self-contained) — a clean lesson in what "closed-form" does and does not buy you | — | Mohamadzadeh et al. 2025, *Frontiers in Remote Sensing* 6:1519420 · [10.3389/frsen.2025.1519420](https://doi.org/10.3389/frsen.2025.1519420) |

## Water quality and floating matter

| Index | What it is for | Level | Paper |
|---|---|---|---|
| **PI** | Floating plastic and debris on water | — | Themistocleous et al. 2020, *Remote Sensing* 12(16):2648 · [10.3390/rs12162648](https://doi.org/10.3390/rs12162648) |
| **WAI** | Water anomalies, with land masked out | EASY | Wei et al. 2024, *Int. J. Digital Earth* 17(1) · [10.1080/17538947.2024.2313695](https://doi.org/10.1080/17538947.2024.2313695) |
| **AWI + AWTI** | ~8 lines for both plus the two-step tree. **All three bands native 20 m** | EASY | Ma et al. 2025, *Int. J. Digital Earth* 18(1) · [10.1080/17538947.2025.2540078](https://doi.org/10.1080/17538947.2025.2540078) |
| **Hue angle → Forel-Ule index** | — | MEDIUM | Van der Woerd & Wernand 2018, *Remote Sensing* 10(2):180 · [10.3390/rs10020180](https://doi.org/10.3390/rs10020180) |
| **CI for OLCI** | ~5 lines. Validated against 599 Baltic in-situ stations | EASY | Konik et al. 2023, *Remote Sensing* 15(6):1601 · [10.3390/rs15061601](https://doi.org/10.3390/rs15061601) |

## Fire and burned area

| Index | What it is for | Level | Paper |
|---|---|---|---|
| **ABAI** | Burned area, with a threshold the paper publishes | EASY | Chen et al. 2022, *Forests* 13(11):1787 · [10.3390/f13111787](https://doi.org/10.3390/f13111787) |
| **AFD-S2** | Primary test **** on **TOA reflectance**, with per-biome | EASY | Hu, Ban & Nascetti 2021, *IJAEOG* 101:102347 · [10.1016/j.jag.2021.102347](https://doi.org/10.1016/j.jag.2021.102347) |
| **FACI** | Forest condition, returned as classes rather than a ramp | EASY | Forests 2025, 16(3):497 · [10.3390/f16030497](https://doi.org/10.3390/f16030497) |
| **NBRSWIR** | **EASY.** ⚠️ Constants assume **reflectance 0–1** — see the trap below | — | Liu et al. 2020, *Eur. J. Remote Sensing* 53(1):104–112 · [10.1080/22797254.2020.1738900](https://doi.org/10.1080/22797254.2020.1738900) |
| **BAIS2** | Burned area, the Sentinel-2 native baseline | — | Filipponi 2018, *Proceedings* 2(7):364 · [10.3390/ecrs-2-05177](https://doi.org/10.3390/ecrs-2-05177) |

## Urban, geology and change detection

| Index | What it is for | Level | Paper |
|---|---|---|---|
| **IFD** | Iron-oxide minerals on mine waste and tailings | — | Mielke et al. 2014, *Remote Sensing* 6(8):6790 · [10.3390/rs6086790](https://doi.org/10.3390/rs6086790) |
| **Iron mineral speciation from one ratio** | Pre-masks: keep , drop | — | Pereira, García-Meléndez, Ferrer-Julià & van der Werff 2026, *Remote Sensing* 18(13):2240 · [10.3390/rs18132240](https://doi.org/10.3390/rs18132240) |
| **Fit a parabola per pixel** | — | MEDIUM | Same paper §2.3.2, method after van der Werff & van der Meer 2015 (, gold OA) · [10.3390/rs71012635](https://doi.org/10.3390/rs71012635) |
| **KBRI** | — | — | Pei et al. 2018, *Remote Sensing* 10(9):1321 · [10.3390/rs10091321](https://doi.org/10.3390/rs10091321) |
| **Salinity family, with fixed-coefficient EC regressions** | — | — | Nguyen et al. 2020, *Prog. Earth Planet. Sci.* 7:1 · [10.1186/s40645-019-0311-0](https://doi.org/10.1186/s40645-019-0311-0) |
| **PISI, ABEI, SUI, ENDBSI** | — | EASY | **PISI** = , Tian et al. 2018, , gold OA. , one line · [10.3390/rs10101521](https://doi.org/10.3390/rs10101521) |
| **DBI** | — | — | Rasul et al. 2018 · [10.3390/land7030081](https://doi.org/10.3390/land7030081) |
| **RBR and RdNBR** | The exists only to keep the denominator non-zero; the authors tested larger offsets and got worse field agreement | EASY | Parks, Dillon & Miller 2014, *Remote Sensing* 6(3):1827 · [10.3390/rs6031827](https://doi.org/10.3390/rs6031827) |
| **AIX** | five differenced indices plus a vote, all one-pass arithmetic | MEDIUM |  · [10.3390/rs12111862](https://doi.org/10.3390/rs12111862) |
| **BCI** | Exposed coal | — | Li et al. 2024, *Remote Sensing* 16(24):4648 · [10.3390/rs16244648](https://doi.org/10.3390/rs16244648) |

## Snow, ice and glaciers

| Index | What it is for | Level | Paper |
|---|---|---|---|
| **I_B4** | Green snow algae | EASY | Gray et al. 2020, *Nature Communications* 11:2527 · [10.1038/s41467-020-16018-w](https://doi.org/10.1038/s41467-020-16018-w) |
| **Snow grain size + total ozone from three S2 bands** | — | MEDIUM | Kokhanovsky et al. 2021, *Remote Sensing* 13(21):4404 · [10.3390/rs13214404](https://doi.org/10.3390/rs13214404) |
| **OLCI snow grain diameter and specific surface area** | — | MEDIUM | Kokhanovsky et al. 2019, *Remote Sensing* 11(19):2280 · [10.3390/rs11192280](https://doi.org/10.3390/rs11192280) |
| **Glacier algae red-edge ratio** | ❗ **No printed regression coefficients** — relative abundance only. Gate it behind a bare-ice test | EASY | Di Mauro et al. 2020, *Scientific Reports* 10:4739 · [10.1038/s41598-020-61762-0](https://doi.org/10.1038/s41598-020-61762-0) |
| **Supraglacial lake depth, with a full published coefficient table** | ~8 lines: a log, a quadratic, a water mask. **Depth in metres** is a satisfying output | EASY | Pope et al. 2016, *The Cryosphere* 10:15–27 · [10.5194/tc-10-15-2016](https://doi.org/10.5194/tc-10-15-2016) |

## SAR and thermal

| Index | What it is for | Level | Paper |
|---|---|---|---|
| **Pseudo-polarimetric descriptors from GRD** | three lines on one ratio. , , and a guard on | EASY | Bhogapurapu et al. 2021, *ISPRS J. Photogramm.* 178:20–35 · [10.1016/j.isprsjprs.2021.05.013](https://doi.org/10.1016/j.isprsjprs.2021.05.013) |
| **Oil spill Index C and D** | **EASY.** 🎤 **Three ratios returned as — the natural shape of an evalscript, not a scalar squeezed into a colour ramp.** L1C | — | Zakzouk et al. 2023, *MethodsX* 12:102520 · [10.1016/j.mex.2023.102520](https://doi.org/10.1016/j.mex.2023.102520) |
| **SVIH** | Invasive submerged vegetation in shallow water | EASY | Malligai, Abd-Elrahman & Leary 2025, *Remote Sensing* 17(11):1894 · [10.3390/rs17111894](https://doi.org/10.3390/rs17111894) |
| **SDWI** | Open water through cloud, day or night | — | Guo et al. 2021, *IEEE JSTARS* 14:8761–8772 · [10.1109/JSTARS.2021.3107279](https://doi.org/10.1109/JSTARS.2021.3107279) |
| **Split-window LST** | Fixed emissivities (Table 3, TIRS-): cropland forest impervious water | EASY | Du et al. 2015, *Remote Sensing* 7(1):647–665 · [10.3390/rs70100647](https://doi.org/10.3390/rs70100647) |
| **Wet snow** | **Wet snow ⟺ Rc < −2 dB**, valid 15° ≤ θ ≤ 75° | — | Nagler et al. 2016, *Remote Sensing* 8(4):348 · [10.3390/rs8040348](https://doi.org/10.3390/rs8040348) |
| **Soil moisture** | **MULTI-DATE** over a stack — the natural demo of and looping the array | — | Bauer-Marschallinger et al. 2019, *IEEE TGRS* 57(1):520–539 · [10.1109/TGRS.2018.2858004](https://doi.org/10.1109/TGRS.2018.2858004) |
| **Sentinel-5P, two clean multi-date stories** | — | EASY | **Bauwens et al. 2020**, *GRL* 47:e2020GL087978 · [10.1029/2020GL087978](https://doi.org/10.1029/2020GL087978) |

## The index libraries are wrong too — and this is the best single story in the file

| Index | What it is for | Level | Paper |
|---|---|---|---|
| **AWEI** | Open water, including in shadow | — | Feyisa, Meilby, Fensholt & Proud 2014, *RSE* 140:23–35 · [10.1016/j.rse.2013.08.029](https://doi.org/10.1016/j.rse.2013.08.029) |
| **DpRVI** | Vegetation structure from dual-pol SAR | — | Mandal et al. 2020, *RSE* 247:111954 · [10.1016/j.rse.2020.111954](https://doi.org/10.1016/j.rse.2020.111954) |

## Two traps worth knowing before you start

**Scene-wide statistics are not per-pixel.** Several of these papers normalise by the minimum
and maximum of a whole scene. An evalscript sees one pixel at a time and cannot know either.
Where you meet that, substitute fixed constants and say that you did.

**Reflectance scale.** Most published constants assume reflectance in 0–1. Sentinel Hub gives
you 0–1 by default so this usually works out, but on digital numbers in the thousands every
additive constant in every one of these papers is wrong.

## If you would rather browse than choose

[awesome-spectral-indices](https://github.com/awesome-spectral-indices) lists 280 indices with
formulas, bands, platforms and DOIs. They are third-party transcriptions, so follow the DOI
when it matters.

