# Plein Futé

Carte pour trouver la station-service la moins chère en France, avec les prix des carburants en temps réel **et** un vrai planificateur d'itinéraire.

Application 100% statique (un seul fichier `index.html`, aucun backend, aucune dépendance de build) — utilisable directement dans un navigateur, installable comme une app sur mobile (PWA), ou hébergée sur GitHub Pages.

## Fonctionnalités

### Données et prix
- **Prix en temps réel** — données issues de l'API officielle du gouvernement français (`data.economie.gouv.fr`, prix des carburants en flux instantané) : Gazole (sélectionné par défaut), SP95, SP98, E10, E85, GPLc.
- **Prix les moins chers de France** — une rangée de pastilles affiche le prix national le plus bas par carburant (dans l'en-tête sur desktop, dans la top bar sur mobile) ; cliquer sur l'une d'elles centre la carte sur la station correspondante, où qu'elle soit en France.
- **Détection de marque** — reconnaissance automatique de l'enseigne (TotalEnergies, Leclerc, Intermarché, Carrefour, Shell, BP, etc.) à partir de l'adresse.

### Localisation et recherche
- **Géolocalisation automatique** au chargement de la page (pas de ville par défaut câblée en dur) : la position est demandée immédiatement, avec indicateur de précision (cercle sur la carte). Si elle est refusée ou indisponible, un message clair invite à cliquer sur « Ma position » ou à chercher une ville — jamais de blocage silencieux.
- **Recherche de ville par préfixe** sur la base officielle des communes de France (`geo.api.gouv.fr`, Etalab) : couvre les ~35 000 communes, y compris les plus petits villages, avec Nominatim (OpenStreetMap) en repli automatique si besoin.

### Recherche « Autour de moi »
- Rayon de recherche réglable (5 / 10 / 25 km).
- **Zone dessinée à la main** sur la carte (cercle, rectangle ou polygone) comme alternative au rayon — disponible sur desktop.
- Tri des résultats par prix, distance ou nom.
- Classement des stations par niveau de prix (pas cher / prix moyen / cher) avec code couleur, et badge « moins cher » sur la meilleure offre.

### Mode Itinéraire
- Planification d'un trajet avec **étapes multiples** (départ, arrivée, arrêts intermédiaires), avec autocomplétion d'adresse sur chaque étape.
- Calcul du trajet via **OSRM** (avec **Valhalla** en option), affichage de la distance et de la durée.
- **Options avancées** : éviter les péages, les autoroutes, les ferries ; consommation du véhicule personnalisable pour estimer le **coût carburant + péages** du trajet.
- Recherche automatique des **stations les moins chères sur le trajet** (couloir de ~10 km autour de l'itinéraire), triées dans l'ordre de passage du départ à l'arrivée.

### Carte
- **Sélecteur de type de carte** : style Minimum (moderne et épuré, noms de villages à tous les zooms, numéros d'autoroute/départementales) ou Satellite, mémorisé d'une visite à l'autre.
- **Détails superposables** : calque feu de forêt (données satellite NASA GIBS/MODIS) et calque transport en commun (OpenRailwayMap), chacun activable/désactivable indépendamment.
- Carte interactive (Leaflet) avec regroupement des marqueurs (clustering) et popups détaillées.
- Thème clair/sombre.

### Sur chaque station
- Fiche détaillée : tous les prix des carburants disponibles, statut d'ouverture (ouvert / 24h24).
- Liens directs vers **Google Maps** et **Waze** pour lancer la navigation.
- **Partage** : copier un message prêt à envoyer, ou partager directement sur WhatsApp.

### Mobile
- Interface entièrement repensée façon Google Maps : barre de recherche flottante, recherche plein écran avec sélection instantanée, liste des stations en feuille coulissante (glisser au doigt pour l'agrandir/réduire librement).
- **Installable comme une vraie app** (PWA) : icône sur l'écran d'accueil, ouverture en plein écran sans barre de navigateur, fonctionne même hors ligne pour la coquille de l'app.
- Visite guidée interactive (bouton « ? ») qui explique chaque fonctionnalité.

### Sécurité
- Échappement systématique des données externes avant affichage (protection XSS).
- Content-Security-Policy restreignant les scripts, styles, images et requêtes réseau aux seuls domaines utilisés par l'app.
- Liens externes en `rel="noopener noreferrer"`.

## Utiliser l'application

- **En ligne** : [hfx-dev.github.io/Pleinfute](https://hfx-dev.github.io/Pleinfute/) — ouvrez le lien et, sur mobile, « Ajouter à l'écran d'accueil » pour l'installer comme une app.
- **En local** : ouvrez `index.html` via un serveur local (ex. `python3 -m http.server`) — l'ouverture directe du fichier (`file://`) empêche le bon fonctionnement de la carte.

## Sources de données

- Prix des carburants : [API officielle data.economie.gouv.fr](https://data.economie.gouv.fr/explore/dataset/prix-des-carburants-en-france-flux-instantane-v2/)
- Communes de France : [geo.api.gouv.fr](https://geo.api.gouv.fr/) (Etalab)
- Fond de carte : [Thunderforest](https://www.thunderforest.com/) (style Minimum) et [Esri](https://www.esri.com/) (satellite)
- Recherche d'adresses (repli) : Nominatim (OpenStreetMap)
- Calcul d'itinéraire : OSRM / Valhalla
- Feu de forêt : NASA GIBS / MODIS
- Transport en commun : OpenRailwayMap
