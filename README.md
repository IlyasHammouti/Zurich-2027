# Carte web : se loger à Zurich (résidences WOKO, ETH Hönggerberg)

Carte interactive Leaflet, sans build ni serveur d'application : un `index.html` et des fichiers `data/*.js`.
Elle fonctionne en double-clic (le navigateur doit avoir accès à Internet pour les fonds de carte) et sur GitHub Pages.

## Ce que la carte montre

| Thème | Contenu |
|---|---|
| Trajet en TP | Isochrones porte à porte vers l'ETH Hönggerberg (marche + transports publics), résidences colorées par temps |
| Trajet à vélo | Même chose à vélo (relief ignoré) |
| Desserte TP | Lignes (épaisseur = passages un jour de semaine), gares, trams, bus (zoom 14 et plus) |
| À pied | Isochrones de 5, 10 et 15 min autour de chaque résidence (cliquer une résidence pour isoler la sienne) |
| Commerces | 6 857 commerces et services OSM, filtrables par catégorie |

Chaque résidence a une fiche : loyer WOKO, trajets, arrêt et lignes les plus proches, commerces à 500 m et à 10 min à pied, lien WOKO.
Adaptation mobile : panneau en feuille basculante, thèmes défilants, étiquettes masquées aux petits zooms.
L'adresse peut cibler un thème : `index.html#desserte`, `#velo`, `#marche`, `#services`, `#tp`.

## Mettre en ligne sur GitHub Pages

1. Créer un dépôt GitHub (public) et y copier le CONTENU de ce dossier (`index.html`, `data/`, `README.md`) à la racine.
2. Dépôt > Settings > Pages > Source : « Deploy from a branch », branche `main`, dossier `/ (root)`.
3. L'adresse sera `https://<compte>.github.io/<depot>/`.

Commandes (PowerShell, depuis ce dossier) :

```powershell
git init -b main
git add index.html data README.md
git commit -m "Carte web : se loger à Zurich"
git remote add origin https://github.com/<compte>/<depot>.git
git push -u origin main
```

Avant de publier, vérifier que la page ne contient rien que tu ne veux pas rendre public (elle ne contient que des données publiques : WOKO, OSM, OFT, horaire).

## Régénérer les données

Depuis la racine du projet (PowerShell) :

```powershell
.venv\Scripts\python carto\scripts\export_webmap.py
```

Les couches viennent de `carto/data/*.gpkg` (voir les scripts de `carto/scripts/`). Les `data/*.js` sont des fichiers générés.

## Aperçu local

```powershell
python -m http.server 8765 --bind 127.0.0.1
```

puis ouvrir http://127.0.0.1:8765/ .

## Sources et licences à conserver

- OpenStreetMap : © contributeurs OpenStreetMap, licence ODbL (extrait BBBike du 24/10/2026).
- Arrêts : OFT (data.geo.admin.ch). Horaire : opentransportdata.swiss (GTFS 2026). Limites de Kreise et quartiers : Ville de Zurich (open data).
- Fonds : swisstopo (carte, orthophoto, relief), Esri (fond clair), OpenStreetMap. Le fond Esri et les tuiles OSM sont soumis à leurs conditions d'usage : prévoir un trafic modeste.
- Loyers et résidences : WOKO, relevé du 27/10/2026, à vérifier sur woko.ch avant toute décision.
