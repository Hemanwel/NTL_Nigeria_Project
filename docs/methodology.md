<p align="right"><a href="methodology.fr.md">Français</a></p>

# Methodology — Nigeria (2014–2025)

## Data and cleaning

VIIRS DNB monthly (VCMSLCFG) and annual VNL V2, harmonised DMSP–VIIRS, daily Black Marble, GHSL/WorldPop, Sentinel-5P NO₂/SO₂, MODIS LST, World Bank. Cleaning: pixels valid if cf_cvg ≥ 2, unit-month kept if ≥ 80% of pixels observed, spikes replaced, background and gas flares masked.

## 📈 Use case 1 — Time dynamics

- **Question** — Is activity accelerating or slowing down, net of seasonality?
- **Data** — VIIRS VCMSLCFG (monthly), VIIRS VNL V2 (annual), Harmonised DMSP–VIIRS (Li et al., 2020)
- **Method** — Robust STL (period 12) on log(sum of lights); Theil–Sen slope and Mann–Kendall test on annual composites; anomaly and break detection.
- **Validation** — Trend significance (Mann–Kendall) and monthly/annual consistency (**p-value = 0.0002**)
- **Uncertainty** — 95% CI of annual growth: +1.4% to +4.3%
- **Limits** — Cloud cover and short summer nights; light is not value added.
- **Status** — `experimental` · Confidence: high
- **References** — Cleveland et al. (1990) STL; Sen (1968); Elvidge et al. (2017).
- **Dashboard page** — [`#time`](https://Hemanwel.github.io/NTL_Nigeria_Project/?country=NGA#time)

**Results of this run**

- `F02` Between 2014 and 2025, night-time light in Nigeria changed by +2.6% per year (95% CI: +1.4% to +4.3%). Over the last 12 months, the seasonally adjusted level is +12.4% relative to the previous 12 months. (confidence high: significant trend (p < 0.01; n = 12))
- `F95` Validation: Trend significance (Mann–Kendall) and monthly/annual consistency (p-value = 0.0002). Uncertainty: 95% CI of annual growth: +1.4% to +4.3% Limitations: Cloud cover and short summer nights; light is not value added. Status: experimental statistic; confidence high.

## 🗺️ Use case 2 — Regional growth and convergence

- **Question** — Which regions take off, which fall behind?
- **Data** — VIIRS VNL V2, GHSL / WorldPop, Sentinel-5P NO₂
- **Method** — Robust growth per unit (Theil–Sen, Mann–Kendall), growth/stagnation/decline classes, β- and σ-convergence, Herfindahl index.
- **Validation** — Rank correlation with tropospheric NO₂ (independent source) (**Spearman ρ = 0.34**)
- **Uncertainty** — Class assigned only if |slope| ≥ threshold and p < α; CI of β (robust errors).
- **Limits** — Small units: noise and light blooming between neighbours.
- **Status** — `experimental` · Confidence: medium
- **References** — Barro & Sala-i-Martin (1992) convergence; Henderson, Storeygard & Weil (2012).
- **Dashboard page** — [`#regions`](https://Hemanwel.github.io/NTL_Nigeria_Project/?country=NGA#regions)

**Results of this run**

- `F03` Of 774 ADM2 units, 251 show significant growth, 422 are stagnating and 78 are declining. Light remains concentrated: Lagos accounts for 15% of national light. (confidence medium: classification of 774 units, threshold ±1%/yr and p < 0.10)
- `F04` Across ADM2 units, light per capita converges: the least-lit units are catching up. (confidence medium: β = −0.024 [−0.031; −0.017], n = 705)
- `F24` Lagos (ADM1, 2025): share of national light 14.6%, annual growth +5.0% (CI +3.8% to +6.4%, class Growth), light per capita 0.134, population 0.58 M, in the dark 0%, estimated GDP (experimental) 82.23 bn USD.
- `F25` Rivers (ADM1, 2025): share of national light 10.8%, annual growth -1.7% (CI -4.1% to +2.5%, class Stagnation), light per capita 0.120, population 0.48 M, in the dark 29%, estimated GDP (experimental) 60.85 bn USD.

## 💹 Use case 3 — Light–GDP relationship

- **Question** — Can growth be estimated before its release, and regional GDP?
- **Data** — VIIRS, Real GDP (World Bank, WDI)
- **Method** — log(light) ~ log(GDP) in levels and growth, OLS with HAC errors; out-of-sample nowcast; regional GDP = national GDP allocated pro rata of light.
- **Validation** — Out-of-sample tracking of official growth (**correlation / MAE (pp) = n/a / n/a**)
- **Uncertainty** — 95% CI of the elasticity: 0.81 to 2.53; 80% and 95% prediction intervals.
- **Limits** — Short annual sample; regional GDP is an experimental statistic to be checked against regional accounts.
- **Status** — `experimental` · Confidence: medium
- **References** — Henderson et al. (2012) AER; Chen & Nordhaus (2011) PNAS; Gibson et al. (2021) JDE.
- **Dashboard page** — [`#time`](https://Hemanwel.github.io/NTL_Nigeria_Project/?country=NGA#time)

**Results of this run**

- `F05` The elasticity of light with respect to real GDP is 1.67 in levels (95% CI: 0.81 to 2.53, R² = 0.50, 12 years) and 0.68 in growth rates (CI: −1.25 to 2.61). (confidence medium: n = 12, significant but wide CI (1.72))
- `F64` Light–real GDP elasticity in levels: β = 1.67 (95% CI 0.81 to 2.53, R² = 0.50, n = 12, confidence medium: n = 12, significant but wide CI (1.72)). +1% GDP ↔ +β% light.
- `F65` Light–real GDP elasticity in growth rates: β = 0.68 (95% CI -1.25 to 2.61, R² = 0.04, n = 11, confidence low: n = 11, not significant (p = 0.49)). +1% GDP ↔ +β% light.
- `F66` Light–real GDP elasticity in long DMSP–VIIRS series: β = -0.08 (95% CI -0.18 to 0.01, R² = 0.48, n = 30, confidence medium: n = 30, significant but wide CI (0.19)). +1% GDP ↔ +β% light.

## ⚡ Use case 4 — Shocks and resilience

- **Question** — How deep was a shock, and how fast the recovery?
- **Data** — VIIRS (monthly), Black Marble VNP46A2 (daily), event catalogue
- **Method** — Gap to the pre-shock level on the seasonally adjusted series; structural breaks; daily Black Marble index.
- **Validation** — Does the trough exceed ordinary variability? (**trough (main shock) = -14.6% — no**)
- **Uncertainty** — Pre-shock month-to-month variability (robust SD); unexplained breaks flagged.
- **Limits** — Shocks hitting poorly lit activities (agriculture, daytime services) are underestimated.
- **Status** — `experimental` · Confidence: low
- **References** — Román et al. (2018); Elvidge et al. (2020) COVID-19 lockdown lights.
- **Dashboard page** — [`#shocks`](https://Hemanwel.github.io/NTL_Nigeria_Project/?country=NGA#shocks)

**Results of this run**

- `F06` The most pronounced shock in the seasonally adjusted series is “COVID-19”: trough of -14.6% (06/2020), return to the pre-shock level after 4 months. (confidence low: trough compared with pre-shock month-to-month variability)
- `F67` COVID-19 (2020-03-01 → 2021-06-30): trough of -14.6% on 2020-06-01, back to the pre-shock level after 4 months. Distinguishable from noise: no.
- `F68` Structural breaks: 2016-02-01 (-24.7 %); 2017-08-01 (16.2 %); 2019-03-01 (-9.1 %); 2023-06-01 (-14.5 %). Without a known event within ±6 months: 4.
- `F69` Hardest-hit regions (trough): Bayelsa -47.6 % (covid19), Gombe -45.7 % (covid19), Borno -45.4 % (covid19), Bauchi -45.0 % (covid19), Kano -30.1 % (covid19).

## ⚖️ Use case 5 — Inequality and electrification

- **Question** — Where do people without electricity live?
- **Data** — VIIRS VNL V2, GHSL / WorldPop, GHSL SMOD, electricity access (WDI)
- **Method** — Population-weighted Gini and Theil; population of inhabited pixels below the detection threshold; sensitivity to three thresholds; bootstrap CI of the Gini change.
- **Validation** — Gap with the World Bank electricity-access rate (**mean gap (pp) = -4.0**)
- **Uncertainty** — Range across radiance thresholds; bootstrap CI of the Gini.
- **Limits** — Proxy of outdoor lighting, not of connection: a connected but dimly lit household looks “in the dark”.
- **Status** — `experimental` · Confidence: medium
- **References** — Theil (1967); Falchetta et al. (2020) electricity access from lights.
- **Dashboard page** — [`#inequality`](https://Hemanwel.github.io/NTL_Nigeria_Project/?country=NGA#inequality)

**Results of this run**

- `F07` The Gini coefficient of light per capita (ADM2) is 0.69 in 2025 (no significant change since 2014). About 4.40 million people live in inhabited areas with no detectable light (44% of the inhabited population). (confidence medium: sensitive to the radiance threshold (from 4.31 to 5.25 M depending on the threshold); a proxy for outdoor lighting, not for grid connection)
- `F70` Gini of light per capita (ADM2): 0.705 in 2014 → 0.691 in 2025 (change -0.014, bootstrap CI -0.033 to 0.010). Theil T 0.924; between-region share 42%.
- `F71` People in inhabited areas without detectable light: 3.56 M (47%) in 2014 → 4.40 M (44%) in 2025. Urban/rural light-per-capita ratio 0.6. Proxy of electricity access, sensitive to the threshold.
- `F72` Average gap between the share of people in lit areas and the World Bank electricity-access rate: -4.0 points.

## 🏭 Use case 6 — Industrial zones

- **Question** — Where is industry, and is its activity growing?
- **Data** — VIIRS VNL V2, GHSL BUILT-S, Sentinel-5P NO₂/SO₂, MODIS MOD11A2, OpenStreetMap
- **Method** — Concordance of six signals per pixel (≥ 3 including light), 8-connected clusters, typology and confidence.
- **Validation** — Comparison with the reference list (OpenStreetMap) (**precision / recall / F1 = 59% / 34% / 0.43**)
- **Uncertainty** — Per-cluster confidence from the number of strong signals; isolated sites to verify.
- **Limits** — Sentinel-5P (≈ 5 km) and MODIS (1 km) resolution: signals describe a neighbourhood.
- **Status** — `experimental` · Confidence: low
- **References** — Elvidge et al. (2016) gas flares; Pesaresi et al. (2023) GHSL.
- **Dashboard page** — [`#industry`](https://Hemanwel.github.io/NTL_Nigeria_Project/?country=NGA#industry)

**Results of this run**

- `F08` 174 industrial clusters detected from concordant satellite signals: 48 heavy industry, 21 business parks & logistics, 44 oil & gas sites and 61 isolated sites to verify. They emit 15.0% of national light (latest year); their light changes by +2.3% per year. Lagos has the most industrial activity. (confidence low: precision 59% and recall 34% against the reference list)
- `F73` 174 industrial clusters (≥ 3 of 6 signals): Isolated site to verify 61, Heavy industry 48, Oil, gas & flares 44, Business park & logistics 21. Share of national light: 15.0%; annual growth +2.3%. Validation (OpenStreetMap): precision 59%, recall 34%.
- `F74` IND-001 — Heavy industry in Municipal Area Council (Abuja Federal Capital Territory) (451.07 km², 3 signals, confidence low); IND-002 — Isolated site to verify in Eti Osa (Lagos) (325.94 km², 3 signals, confidence low); IND-004 — Isolated site to verify in Ikeja (Lagos) (141.04 km², 3 signals, confidence low); IND-147 — Oil, gas & flares in Warri South-West (Delta) (0.86 km², 3 signals, confidence low); IND-151 — Oil, gas & flares in Ogba/Egbema/Ndoni (Rivers) (0.86 km², 3 signals, confidence low); IND-005 — Heavy industry in Nassarawa (Kano) (125.345 km², 3 signals, confidence low); IND-003 — Isolated site to verify in Ikorodu (Lagos) (227.9 km², 3 signals, confidence low); IND-142 — Oil, gas & flares in Ikpoba-Okha (Edo) (0.86 km², 3 signals, confidence low); IND-148 — Oil, gas & flares in Ohaji/Egbema (Imo) (0.86 km², 3 signals, confidence low); IND-033 — Oil, gas & flares in Ibeno (Akwa Ibom) (4.3 km², 3 signals, confidence low)
- `F75` Lagos: 13 industrial cluster(s), 714.2 km², 51.6% of the region's light.

## 🏖️ Use case 7 — Seasonal tourism

- **Question** — Which areas live from tourism, and how does the season evolve?
- **Data** — VIIRS (monthly), hotel nights or WDI arrivals
- **Method** — Summer excess net of comparable units at the same latitude; one-sided test; season index base 100; seasons overlapping Ramadan flagged.
- **Validation** — Correlation with hotel nights (**r = not available**)
- **Uncertainty** — p-value per unit; 2020–2021 excluded from the classification.
- **Limits** — Any summer activity (diaspora, second homes, festivals) is captured, not only tourism.
- **Status** — `experimental` · Confidence: low
- **References** — Seasonal light analyses of tourism, e.g. Hu et al. (2021).
- **Dashboard page** — [`#tourism`](https://Hemanwel.github.io/NTL_Nigeria_Project/?country=NGA#tourism)

**Results of this run**

- `F09` 216 of 759 units show a net summer light excess of at least 10%: Nembe (Bayelsa), Degema (Rivers), Warri South-West (Delta), Ughelli South (Delta). The median net excess reaches +109% in the most touristic zone. The season index (base 100 = 2019) falls to 12 in 2020 and stands at 68 in 2025. (confidence low: no hotel-night statistics to validate the indicator)
- `F88` 216 tourist zone(s) out of 759 ADM2 units (net summer excess ≥ 10%, peak months [7, 8]): Nembe (Bayelsa) (+109%, confidence high), Degema (Rivers) (+105%, confidence high), Warri South-West (Delta) (+101%, confidence high), Ughelli South (Delta) (+93%, confidence high), Akuku Toru (Rivers) (+92%, confidence high), Ahoada West (Rivers) (+89%, confidence high), Anambra West (Anambra) (+88%, confidence medium), Ekeremor (Bayelsa) (+83%, confidence high), Ethiope West (Delta) (+81%, confidence high), Isoko North (Delta) (+80%, confidence medium).
- `F89` Season index (base 100 = 2019): 2014: 105, 2015: 97, 2016: 149, 2017: 68, 2018: 95, 2019: 100, 2020: 12, 2021: 55, 2022: 61, 2023: 28, 2024: 77, 2025: 68. Years when Ramadan overlaps the season: 2014, 2015, 2018, 2019, 2020, 2021, 2022, 2023.
- `F101` Validation: Correlation with hotel nights (r = not available). Uncertainty: p-value per unit; 2020–2021 excluded from the classification. Limitations: Any summer activity (diaspora, second homes, festivals) is captured, not only tourism. Status: experimental statistic; confidence low.

## 🏙️ Use case 8 — Urbanisation signals

- **Question** — Where do cities spread, where do villages get electrified, and where does population grow without light?
- **Data** — VIIRS VNL V2, GHSL GHS-POP / WorldPop, GHSL GHS-BUILT-S R2023A, urban population (WDI)
- **Method** — Lit area (pixels above the threshold) and population per unit; Theil–Sen growth rates; newly lit pixels (dark two years in a row at the start, lit two years in a row at the end), split between electrification of inhabited areas and new settlements; light/population typology.
- **Validation** — Rank correlation with GHSL built-up area growth (independent source) (**Spearman ρ = 0.23**)
- **Uncertainty** — Persistence required over two years to limit noise; ± 1 pp margin between growth rates before classifying.
- **Limits** — Light measures outdoor lighting, not urbanisation in the administrative sense; blooming widens cities; GHSL population is interpolated between epochs.
- **Status** — `experimental` · Confidence: low
- **References** — Zhou et al. (2015) urban extent from lights; Pesaresi et al. (2023) GHSL; Min et al. (2013) village electrification.
- **Dashboard page** — [`#urban`](https://Hemanwel.github.io/NTL_Nigeria_Project/?country=NGA#urban)

**Results of this run**

- `F90` National lit area: +2.8% per year; population: +2.5% per year. Classes (ADM2): Electrified urbanisation 399, Unlit growth 271, Balanced growth 64, Undetermined 37, Stable or declining 3.
- `F91` Between 2014 and 2025: 10,084 km² newly lit, of which 1,878 km² already inhabited (electrification, ≈ 512k people) and 8,205 km² of new settlements; 3,513 km² lost their light.
- `F92` Fastest lit-area expansion: Eastern Obolo (Akwa Ibom) (+173.7%/yr), Irele (Ondo) (+137.0%/yr), Kaga (Borno) (+112.2%/yr), Monguno (Borno) (+87.1%/yr), Igbo-Eze North (Enugu) (+80.2%/yr), Ideato North (Imo) (+73.0%/yr). Unlit growth (population faster than light): Ekeremor (Bayelsa), Degema (Rivers), Akpabuyo (Cross River), Oron (Akwa Ibom), Calabar South (Cross River), Southern Ijaw (Bayelsa), Okrika (Rivers), Ibeno (Akwa Ibom).
- `F93` Spearman rank correlation between lit-area growth and GHSL built-up growth: 0.23 (p = 0.000, 737 units).

## General limits of night-time lights

- **What lights measure** — Upward radiance emitted around 01:30: agriculture, daytime trade, poorly lit services and the rural informal economy are poorly captured.
- **Saturation and blooming** — DMSP saturates in city centres (DN 63) and “blooms” beyond lit areas; VIIRS is much better, but blooming still inflates the lit area of cities.
- **Gas flares and isolated sites** — The automatic mask may remove isolated mines, ports or power plants, and miss small flares; candidates are exported for verification.
- **Clouds, seasons, moon** — Cloudy months are only partially observed; STL removes average seasonality but not an abnormal season (snow, late monsoon).
- **Product breaks** — DMSP and VIIRS are not directly comparable: the harmonised long series (Li et al., 2020) is a modelled product, to be read for trends only.
- **NTL–GDP elasticity** — Estimated on 10 to 30 annual observations: wide intervals, possible instability, a non-causal relationship that varies with the level of development.
- **Access to electricity** — “Inhabited without light” ≠ “not connected”: a connected household with low consumption is invisible; the indicator depends strongly on the radiance threshold and the population data.
- **Administrative boundaries** — geoBoundaries/GAUL may differ from official boundaries; small ADM2 units are sensitive to light spilling over from neighbouring units.
- **Industrial zones** — Detection relies on thresholds: a power plant, a port or a large shopping centre can meet the signals; a dimly lit factory without visible emissions is missed. Sentinel-5P (≈ 5 km) and MODIS (1 km) are coarser than VIIRS: NO₂/SO₂/heat signals describe a neighbourhood, not a building.
- **Summer tourism** — The summer excess captures any rise in summer light (second homes, diaspora visits, festivals, construction), not only tourism; at high latitudes, very short summer nights reduce VIIRS observations. Ramadan changes night-time activity: the summers concerned are flagged.
- **Urbanisation** — The lit area depends on the detection threshold and on light blooming around cities; a connected but dimly lit neighbourhood stays invisible. Population (GHSL/WorldPop) is modelled from censuses: its growth is not an independent observation, and years between two epochs are interpolated.


---
<sub>Generated by the notebook on 2026-10-30 · version 2.1.0</sub>
