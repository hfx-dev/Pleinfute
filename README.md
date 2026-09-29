# Station Essence

Carte pour trouver la station-service la moins chère en France, avec les prix des carburants en temps réel **et** un vrai planificateur d'itinéraire. C'est la version la plus aboutie du projet StationFuel.

Application 100% statique (un seul fichier `index.html`, aucun backend, aucune dépendance de build) — utilisable directement dans un navigateur ou hébergée sur GitHub Pages.

## Fonctionnalités

### Données et prix
- **Prix en temps réel** — données issues de l'API officielle du gouvernement français (`data.economie.gouv.fr`, prix des carburants en flux instantané) : Gazole, SP95, SP98, E10, E85, GPLc.
- **Prix les moins chers de France** — une rangée de pastilles dans l'en-tête affiche le prix national le plus bas par carburant ; cliquer sur l'une d'elles centre la carte sur la station correspondante, où qu'elle soit en France.
- **Détection de marque** — reconnaissance automatique de l'enseigne (TotalEnergies, Leclerc, Intermarché, Carrefour, Shell, BP, etc.) à partir de l'adresse.

### Localisation
- **Géolocalisation automatique** au chargement de la page (pas de ville par défaut câblée en dur) : la position est demandée immédiatement, avec indicateur de précision (cercle sur la carte). Si elle est refusée ou indisponible, un message clair invite à cliquer sur « Ma position » ou à chercher une ville — jamais de blocage silencieux.
- **Recherche d'adresse/ville** avec autocomplétion (Nominatim / OpenStreetMap).

### Recherche « Autour de moi »
- Rayon de recherche réglable (5 / 10 / 25 km).
- **Zone dessinée à la main** directement sur la carte (cercle, rectangle ou polygone) comme alternative au rayon.
- Tri des résultats par prix, distance ou nom.
- Classement des stations par niveau de prix (pas cher / prix moyen / cher) avec code couleur, et badge « moins cher » sur la meilleure offre.

### Mode Itinéraire
- Planification d'un trajet avec **étapes multiples** (départ, arrivée, arrêts intermédiaires), avec autocomplétion d'adresse sur chaque étape.
- Calcul du trajet via **OSRM** (avec **Valhalla** en option), affichage de la distance et de la durée.
- **Options avancées** : éviter les péages, les autoroutes, les ferries ; consommation du véhicule personnalisable pour estimer le **coût carburant + péages** du trajet.
- Recherche automatique des **stations les moins chères sur le trajet** (couloir de ~10 km autour de l'itinéraire), triées dans l'ordre de passage du départ à l'arrivée.

### Sur chaque station
- Fiche détaillée : tous les prix des carburants disponibles, statut d'ouverture (ouvert / 24h24).
- Liens directs vers **Google Maps** et **Waze** pour lancer la navigation.
- **Partage** : copier un message prêt à envoyer, ou partager directement sur WhatsApp.

### Interface
- Carte interactive (Leaflet + fond de carte OpenStreetMap) avec regroupement des marqueurs (clustering) et popups détaillées.
- Thème clair/sombre.
- Interface responsive.

## Utiliser l'application en ligne

Aucune installation nécessaire : ouvrez `index.html` dans un navigateur, ou activez **GitHub Pages** sur ce dépôt (*Settings → Pages → Deploy from a branch → `main` → `/ (root)`*) pour obtenir une URL publique.

> Ce dépôt est actuellement **privé** : une URL GitHub Pages activée ici ne sera accessible qu'aux personnes ayant accès au dépôt (ou selon le plan GitHub, potentiellement en accès restreint). Passez le dépôt en public si vous voulez que n'importe qui puisse l'utiliser.

## Sources de données

- Prix des carburants : [API officielle data.economie.gouv.fr](https://data.economie.gouv.fr/explore/dataset/prix-des-carburants-en-france-flux-instantane-v2/)
- Fond de carte : OpenStreetMap (tuiles standard, aucune clé requise)
- Recherche d'adresses : Nominatim (OpenStreetMap)
- Calcul d'itinéraire : OSRM / Valhalla
