<p align="right"><a href="methodology.md">English</a></p>

# Méthodologie — Nigeria (2014–2025)

## Données et nettoyage

VIIRS DNB mensuel (VCMSLCFG) et annuel VNL V2, DMSP–VIIRS harmonisé, Black Marble quotidien, GHSL/WorldPop, Sentinel-5P NO₂/SO₂, MODIS LST, Banque mondiale. Nettoyage : pixels valides si cf_cvg ≥ 2, unité-mois gardée si ≥ 80 % de pixels observés, pics remplacés, fond et torchères masqués.

## 📈 Cas d'usage 1 — Dynamiques temporelles

- **Question** — L'activité accélère-t-elle ou ralentit-elle, hors effet de saison ?
- **Données** — VIIRS VCMSLCFG (monthly), VIIRS VNL V2 (annual), Harmonised DMSP–VIIRS (Li et al., 2020)
- **Méthode** — STL robuste (période 12) sur log(somme des lumières) ; pente de Theil–Sen et test de Mann–Kendall sur les composites annuels ; détection d'anomalies et de ruptures.
- **Validation** — Significativité de la tendance (Mann–Kendall) et cohérence mensuel/annuel (**p-value = 0,0002**)
- **Incertitude** — IC 95 % de la croissance annuelle : +1,4 % à +4,3 %
- **Limites** — Couverture nuageuse et nuits courtes en été ; la lumière n'est pas la valeur ajoutée.
- **Statut** — `experimental` · Confiance: élevée
- **Références** — Cleveland et al. (1990) STL ; Sen (1968) ; Elvidge et al. (2017).
- **Page du tableau de bord** — [`#time`](https://Hemanwel.github.io/NTL_Nigeria_Project/fr/?country=NGA#time)

**Résultats de cette exécution**

- `F02` Entre 2014 et 2025, la lumière nocturne de Nigeria a évolué de +2,6 % par an (IC 95 % : +1,4 % à +4,3 %). Sur les 12 derniers mois, le niveau désaisonnalisé est +12,4 % par rapport aux 12 mois précédents. (confiance élevée : tendance significative (p < 0,01 ; n = 12))
- `F95` Validation : Significativité de la tendance (Mann–Kendall) et cohérence mensuel/annuel (p-value = 0,0002). Incertitude : IC 95 % de la croissance annuelle : +1,4 % à +4,3 % Limites : Couverture nuageuse et nuits courtes en été ; la lumière n'est pas la valeur ajoutée. Statut : statistique expérimentale ; confiance élevée.

## 🗺️ Cas d'usage 2 — Croissance régionale et convergence

- **Question** — Quelles régions décollent, lesquelles décrochent ?
- **Données** — VIIRS VNL V2, GHSL / WorldPop, Sentinel-5P NO₂
- **Méthode** — Croissance robuste par unité (Theil–Sen, Mann–Kendall), classes croissance/stagnation/déclin, β- et σ-convergence, indice de Herfindahl.
- **Validation** — Corrélation de rang avec le NO₂ troposphérique (source indépendante) (**Spearman ρ = 0,34**)
- **Incertitude** — Classe attribuée seulement si |pente| ≥ seuil et p < α ; IC de β (erreurs robustes).
- **Limites** — Petites unités : bruit et débordement de lumière (blooming) entre voisins.
- **Statut** — `experimental` · Confiance: moyenne
- **Références** — Barro et Sala-i-Martin (1992) convergence ; Henderson, Storeygard et Weil (2012).
- **Page du tableau de bord** — [`#regions`](https://Hemanwel.github.io/NTL_Nigeria_Project/fr/?country=NGA#regions)

**Résultats de cette exécution**

- `F03` Sur 774 unités ADM2, 251 sont en croissance significative, 422 stagnent et 78 déclinent. L'activité lumineuse reste concentrée : Lagos concentre 15 % de la lumière nationale. (confiance moyenne : classement sur 774 unités, seuil ±1 %/an et p < 0,10)
- `F04` Entre unités ADM2, la lumière par habitant converge : les unités les moins éclairées rattrapent leur retard. (confiance moyenne : β = −0,024 [−0,031 ; −0,017], n = 705)
- `F24` Lagos (ADM1, 2025) : part de la lumière nationale 14,6 %, croissance annuelle +5,0 % (IC +3,8 % à +6,4 %, classe Croissance), lumière par habitant 0,134, population 0,58 M, dans le noir 0 %, PIB estimé (expérimental) 82,23 Md USD.
- `F25` Rivers (ADM1, 2025) : part de la lumière nationale 10,8 %, croissance annuelle -1,7 % (IC -4,1 % à +2,5 %, classe Stagnation), lumière par habitant 0,120, population 0,48 M, dans le noir 29 %, PIB estimé (expérimental) 60,85 Md USD.

## 💹 Cas d'usage 3 — Relation lumières–PIB

- **Question** — Peut-on estimer la croissance avant sa publication, et le PIB régional ?
- **Données** — VIIRS, PIB réel (Banque mondiale, WDI)
- **Méthode** — log(lumière) ~ log(PIB) en niveaux et en croissance, MCO avec écarts-types HAC ; prévision hors échantillon ; PIB régional = PIB national réparti au prorata de la lumière.
- **Validation** — Suivi hors échantillon de la croissance officielle (**corrélation / EAM (points) = n.d. / n.d.**)
- **Incertitude** — IC 95 % de l'élasticité : 0,81 à 2,53 ; intervalles de prévision 80 % et 95 %.
- **Limites** — Échantillon annuel court ; le PIB régional est une statistique expérimentale à confronter aux comptes régionaux.
- **Statut** — `experimental` · Confiance: moyenne
- **Références** — Henderson et al. (2012) AER ; Chen et Nordhaus (2011) PNAS ; Gibson et al. (2021) JDE.
- **Page du tableau de bord** — [`#time`](https://Hemanwel.github.io/NTL_Nigeria_Project/fr/?country=NGA#time)

**Résultats de cette exécution**

- `F05` L'élasticité de la lumière au PIB réel est de 1,67 en niveaux (IC 95 % : 0,81 à 2,53, R² = 0,50, 12 années) et de 0,68 en taux de croissance (IC : −1,25 à 2,61). (confiance moyenne : n = 12, significatif mais IC large (1,72))
- `F64` Élasticité lumières–PIB réel en niveaux : β = 1,67 (IC 95 % 0,81 à 2,53, R² = 0,50, n = 12, confiance moyenne : n = 12, significatif mais IC large (1,72)). +1 % de PIB ↔ +β % de lumière.
- `F65` Élasticité lumières–PIB réel en taux de croissance : β = 0,68 (IC 95 % -1,25 à 2,61, R² = 0,04, n = 11, confiance faible : n = 11, non significatif (p = 0,49)). +1 % de PIB ↔ +β % de lumière.
- `F66` Élasticité lumières–PIB réel en série longue DMSP–VIIRS : β = -0,08 (IC 95 % -0,18 à 0,01, R² = 0,48, n = 30, confiance moyenne : n = 30, significatif mais IC large (0,19)). +1 % de PIB ↔ +β % de lumière.

## ⚡ Cas d'usage 4 — Chocs et résilience

- **Question** — Quelle a été la profondeur d'un choc, et la vitesse de récupération ?
- **Données** — VIIRS (monthly), Black Marble VNP46A2 (daily), catalogue d'événements
- **Méthode** — Écart au niveau d'avant-choc sur la série désaisonnalisée ; ruptures structurelles ; indice quotidien Black Marble.
- **Validation** — Le creux dépasse-t-il la variabilité ordinaire ? (**creux (choc principal) = -14,6 % — non**)
- **Incertitude** — Variabilité mensuelle d'avant-choc (écart-type robuste) ; ruptures inexpliquées signalées.
- **Limites** — Les chocs touchant des activités peu éclairées (agriculture, services de jour) sont sous-estimés.
- **Statut** — `experimental` · Confiance: faible
- **Références** — Román et al. (2018) ; Elvidge et al. (2020) lumières et confinements.
- **Page du tableau de bord** — [`#shocks`](https://Hemanwel.github.io/NTL_Nigeria_Project/fr/?country=NGA#shocks)

**Résultats de cette exécution**

- `F06` Le choc le plus marqué dans la série désaisonnalisée est « COVID-19 » : creux de -14,6 % (06/2020), retour au niveau d'avant-choc après 4 mois. (confiance faible : creux comparé à la variabilité mensuelle d'avant-choc)
- `F67` COVID-19 (2020-03-01 → 2021-06-30) : creux de -14,6 % le 2020-06-01, retour au niveau d'avant-choc après 4 mois. Distinct du bruit : non.
- `F68` Ruptures structurelles : 2016-02-01 (-24,7 %); 2017-08-01 (16,2 %); 2019-03-01 (-9,1 %); 2023-06-01 (-14,5 %). Sans événement connu à ±6 mois : 4.
- `F69` Régions les plus touchées (creux) : Bayelsa -47,6 % (covid19), Gombe -45,7 % (covid19), Borno -45,4 % (covid19), Bauchi -45,0 % (covid19), Kano -30,1 % (covid19).

## ⚖️ Cas d'usage 5 — Inégalités et électrification

- **Question** — Où vivent les populations privées d'électricité ?
- **Données** — VIIRS VNL V2, GHSL / WorldPop, GHSL SMOD, accès à l'électricité (WDI)
- **Méthode** — Gini et Theil pondérés par la population ; population des pixels habités sous le seuil de détection ; sensibilité à trois seuils ; IC bootstrap de la variation du Gini.
- **Validation** — Écart avec le taux d'accès à l'électricité de la Banque mondiale (**écart moyen (points) = -4,0**)
- **Incertitude** — Plage selon le seuil de radiance ; IC bootstrap du Gini.
- **Limites** — Proxy de l'éclairage extérieur, pas du raccordement : un foyer raccordé mais peu éclairé paraît « dans le noir ».
- **Statut** — `experimental` · Confiance: moyenne
- **Références** — Theil (1967) ; Falchetta et al. (2020) accès à l'électricité par les lumières.
- **Page du tableau de bord** — [`#inequality`](https://Hemanwel.github.io/NTL_Nigeria_Project/fr/?country=NGA#inequality)

**Résultats de cette exécution**

- `F07` Le Gini de la lumière par habitant (ADM2) vaut 0,69 en 2025 (évolution non significative depuis 2014). Environ 4,40 million(s) de personnes vivent dans des zones habitées sans lumière détectable (44 % de la population habitée). (confiance moyenne : sensible au seuil de radiance (de 4,31 à 5,25 M selon le seuil) ; proxy d'éclairage extérieur, pas de raccordement)
- `F70` Gini de la lumière par habitant (ADM2) : 0,705 en 2014 → 0,691 en 2025 (variation -0,014, IC bootstrap -0,033 à 0,010). Theil T 0,924 ; part entre régions 42 %.
- `F71` Habitants de zones habitées sans lumière détectable : 3,56 M (47 %) en 2014 → 4,40 M (44 %) en 2025. Rapport lumière/hab. urbain/rural 0,6. Proxy de l'accès à l'électricité, sensible au seuil.
- `F72` Écart moyen entre la part de la population en zone éclairée et le taux d'accès à l'électricité de la Banque mondiale : -4,0 points.

## 🏭 Cas d'usage 6 — Zones industrielles

- **Question** — Où est l'industrie, et son activité progresse-t-elle ?
- **Données** — VIIRS VNL V2, GHSL BUILT-S, Sentinel-5P NO₂/SO₂, MODIS MOD11A2, OpenStreetMap
- **Méthode** — Concordance de six signaux par pixel (≥ 3 dont la lumière), grappes 8-connexes, typologie et confiance.
- **Validation** — Comparaison avec la liste de référence (OpenStreetMap) (**précision / rappel / F1 = 59 % / 34 % / 0,43**)
- **Incertitude** — Confiance par grappe selon le nombre de signaux forts ; sites isolés à vérifier.
- **Limites** — Résolution de Sentinel-5P (≈ 5 km) et MODIS (1 km) : les signaux qualifient un voisinage.
- **Statut** — `experimental` · Confiance: faible
- **Références** — Elvidge et al. (2016) torchères ; Pesaresi et al. (2023) GHSL.
- **Page du tableau de bord** — [`#industry`](https://Hemanwel.github.io/NTL_Nigeria_Project/fr/?country=NGA#industry)

**Résultats de cette exécution**

- `F08` 174 grappes industrielles détectées par concordance de signaux satellitaires : 48 d'industrie lourde, 21 zones d'activités et de logistique, 44 sites d'hydrocarbures et 61 sites isolés à vérifier. Elles émettent 15,0 % de la lumière nationale (dernière année) ; leur lumière évolue de +2,3 % par an. Lagos concentre la plus forte activité industrielle. (confiance faible : précision 59 % et rappel 34 % face à la liste de référence)
- `F73` 174 grappes industrielles (≥ 3 signaux sur 6) : Site isolé à vérifier 61, Industrie lourde 48, Hydrocarbures et torchères 44, Zone d'activités et logistique 21. Part de la lumière nationale : 15,0 % ; croissance annuelle +2,3 %. Validation (OpenStreetMap) : précision 59 %, rappel 34 %.
- `F74` IND-001 — Industrie lourde à Municipal Area Council (Abuja Federal Capital Territory) (451.07 km², 3 signaux, confiance faible); IND-002 — Site isolé à vérifier à Eti Osa (Lagos) (325.94 km², 3 signaux, confiance faible); IND-004 — Site isolé à vérifier à Ikeja (Lagos) (141.04 km², 3 signaux, confiance faible); IND-147 — Hydrocarbures et torchères à Warri South-West (Delta) (0.86 km², 3 signaux, confiance faible); IND-151 — Hydrocarbures et torchères à Ogba/Egbema/Ndoni (Rivers) (0.86 km², 3 signaux, confiance faible); IND-005 — Industrie lourde à Nassarawa (Kano) (125.345 km², 3 signaux, confiance faible); IND-003 — Site isolé à vérifier à Ikorodu (Lagos) (227.9 km², 3 signaux, confiance faible); IND-142 — Hydrocarbures et torchères à Ikpoba-Okha (Edo) (0.86 km², 3 signaux, confiance faible); IND-148 — Hydrocarbures et torchères à Ohaji/Egbema (Imo) (0.86 km², 3 signaux, confiance faible); IND-033 — Hydrocarbures et torchères à Ibeno (Akwa Ibom) (4.3 km², 3 signaux, confiance faible)
- `F75` Lagos : 13 grappe(s) industrielle(s), 714,2 km², 51,6 % de la lumière de la région.

## 🏖️ Cas d'usage 7 — Tourisme saisonnier

- **Question** — Quelles zones vivent du tourisme, et comment évolue la saison ?
- **Données** — VIIRS (monthly), nuitées ou arrivées WDI
- **Méthode** — Surcroît estival net des unités comparables de même latitude ; test unilatéral ; indice de saison base 100 ; saisons recoupant le Ramadan signalées.
- **Validation** — Corrélation avec les nuitées (**r = non disponible**)
- **Incertitude** — p-valeur par unité ; années 2020–2021 exclues du classement.
- **Limites** — Toute activité estivale (diaspora, résidences secondaires, festivals) est captée, pas seulement le tourisme.
- **Statut** — `experimental` · Confiance: faible
- **Références** — Analyses saisonnières des lumières et du tourisme, par ex. Hu et al. (2021).
- **Page du tableau de bord** — [`#tourism`](https://Hemanwel.github.io/NTL_Nigeria_Project/fr/?country=NGA#tourism)

**Résultats de cette exécution**

- `F09` 216 unités sur 759 ont un surcroît de lumière estival net d'au moins 10 % : Nembe (Bayelsa), Degema (Rivers), Warri South-West (Delta), Ughelli South (Delta). Le surcroît net médian atteint +109 % dans la zone la plus touristique. L'indice de saison (base 100 = 2019) tombe à 12 en 2020 et vaut 68 en 2025. (confiance faible : aucune statistique de nuitées pour valider l'indicateur)
- `F88` 216 zone(s) touristique(s) sur 759 unités ADM2 (surcroît estival net ≥ 10 %, mois de pointe [7, 8]) : Nembe (Bayelsa) (+109 %, confiance élevée), Degema (Rivers) (+105 %, confiance élevée), Warri South-West (Delta) (+101 %, confiance élevée), Ughelli South (Delta) (+93 %, confiance élevée), Akuku Toru (Rivers) (+92 %, confiance élevée), Ahoada West (Rivers) (+89 %, confiance élevée), Anambra West (Anambra) (+88 %, confiance moyenne), Ekeremor (Bayelsa) (+83 %, confiance élevée), Ethiope West (Delta) (+81 %, confiance élevée), Isoko North (Delta) (+80 %, confiance moyenne).
- `F89` Indice de saison (base 100 = 2019) : 2014 : 105, 2015 : 97, 2016 : 149, 2017 : 68, 2018 : 95, 2019 : 100, 2020 : 12, 2021 : 55, 2022 : 61, 2023 : 28, 2024 : 77, 2025 : 68. Années avec Ramadan chevauchant la saison : 2014, 2015, 2018, 2019, 2020, 2021, 2022, 2023.
- `F101` Validation : Corrélation avec les nuitées (r = non disponible). Incertitude : p-valeur par unité ; années 2020–2021 exclues du classement. Limites : Toute activité estivale (diaspora, résidences secondaires, festivals) est captée, pas seulement le tourisme. Statut : statistique expérimentale ; confiance faible.

## 🏙️ Cas d'usage 8 — Signaux d'urbanisation

- **Question** — Où les villes s'étendent-elles, où les villages s'électrifient-ils, et où la population croît-elle sans lumière ?
- **Données** — VIIRS VNL V2, GHSL GHS-POP / WorldPop, GHSL GHS-BUILT-S R2023A, population urbaine (WDI)
- **Méthode** — Surface éclairée (pixels au-dessus du seuil) et population par unité ; croissances de Theil–Sen ; pixels nouvellement éclairés (sombres deux années de suite au début, éclairés deux années de suite à la fin), séparés entre électrification de zones habitées et nouvelles implantations ; typologie lumière/population.
- **Validation** — Corrélation de rang avec la croissance de la surface bâtie GHSL (source indépendante) (**Spearman ρ = 0,23**)
- **Incertitude** — Persistance exigée sur deux années pour limiter le bruit ; marge de ± 1 point entre croissances avant de classer.
- **Limites** — La lumière mesure l'éclairage extérieur, pas l'urbanisation au sens administratif ; le débordement (blooming) élargit les villes ; la population GHSL est interpolée entre époques.
- **Statut** — `experimental` · Confiance: faible
- **Références** — Zhou et al. (2015) étendue urbaine par les lumières ; Pesaresi et al. (2023) GHSL ; Min et al. (2013) électrification des villages.
- **Page du tableau de bord** — [`#urban`](https://Hemanwel.github.io/NTL_Nigeria_Project/fr/?country=NGA#urban)

**Résultats de cette exécution**

- `F90` Surface éclairée nationale : +2,8 % par an ; population : +2,5 % par an. Classes (ADM2) : Urbanisation électrifiée 399, Croissance non éclairée 271, Croissance équilibrée 64, Indéterminé 37, Stable ou en déclin 3.
- `F91` Entre 2014 et 2025 : 10 084 km² nouvellement éclairés, dont 1 878 km² de zones déjà habitées (électrification, ≈ 512 k habitants) et 8 205 km² de nouvelles implantations ; 3 513 km² ont perdu leur lumière.
- `F92` Plus forte extension de la surface éclairée : Eastern Obolo (Akwa Ibom) (+173,7 %/an), Irele (Ondo) (+137,0 %/an), Kaga (Borno) (+112,2 %/an), Monguno (Borno) (+87,1 %/an), Igbo-Eze North (Enugu) (+80,2 %/an), Ideato North (Imo) (+73,0 %/an). Croissance non éclairée (population plus rapide que la lumière) : Ekeremor (Bayelsa), Degema (Rivers), Akpabuyo (Cross River), Oron (Akwa Ibom), Calabar South (Cross River), Southern Ijaw (Bayelsa), Okrika (Rivers), Ibeno (Akwa Ibom).
- `F93` Corrélation de rang (Spearman) entre croissance de la surface éclairée et croissance du bâti GHSL : 0,23 (p = 0,000, 737 unités).

## Limites générales des lumières nocturnes

- **Ce que mesurent les lumières** — Radiance émise vers le haut vers 01 h 30 : l'agriculture, le commerce de jour, les services peu éclairés et l'économie informelle rurale sont mal captés.
- **Saturation et débordement** — DMSP sature au centre des villes (DN 63) et « déborde » (blooming) ; VIIRS est bien meilleur mais le débordement gonfle encore la surface éclairée des villes.
- **Torchères et sites isolés** — Le masque automatique peut retirer des mines, ports ou centrales isolés, et manquer de petites torchères ; les candidats sont exportés pour vérification.
- **Nuages, saisons, lune** — Les mois nuageux sont partiellement observés ; la STL retire la saisonnalité moyenne mais pas une saison anormale (neige, mousson tardive).
- **Ruptures de produit** — DMSP et VIIRS ne sont pas directement comparables : la série longue harmonisée (Li et al., 2020) est un produit modélisé, à lire en tendance seulement.
- **Élasticité NTL–PIB** — Estimée sur 10 à 30 points annuels : intervalles larges, instabilité possible, relation non causale et variable selon le niveau de développement.
- **Accès à l'électricité** — « Habité sans lumière » ≠ « non raccordé » : un foyer raccordé à faible consommation est invisible ; l'indicateur dépend fortement du seuil de radiance et de la population.
- **Limites administratives** — geoBoundaries/GAUL peuvent différer des limites officielles ; les petites unités ADM2 sont sensibles au débordement de la lumière des voisines.
- **Zones industrielles** — La détection repose sur des seuils : une centrale, un port ou un grand centre commercial peut cumuler les signaux ; une usine peu éclairée ou sans émissions visibles échappe à la détection. Sentinel-5P (≈ 5 km) et MODIS (1 km) sont plus grossiers que VIIRS : les signaux NO₂/SO₂/chaleur qualifient un voisinage, pas un bâtiment.
- **Tourisme estival** — Le surcroît estival mesure toute hausse de lumière en été (résidences secondaires, diaspora, fêtes, chantiers), pas seulement le tourisme ; aux hautes latitudes, les nuits d'été très courtes réduisent les observations VIIRS. Le Ramadan modifie l'activité nocturne : les étés concernés sont signalés.
- **Urbanisation** — La surface éclairée dépend du seuil de détection et du débordement de lumière (blooming) autour des villes ; un quartier raccordé mais peu éclairé reste invisible. La population (GHSL/WorldPop) est modélisée à partir des recensements : sa croissance n'est pas une observation indépendante, et les années entre deux millésimes sont interpolées.


---
<sub>Généré par le notebook le 2026-10-30 · version 2.1.0</sub>
