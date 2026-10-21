# Plein Futé

Carte pour trouver la station-service la moins chère en France, avec les prix des carburants en temps réel **et** un vrai planificateur d'itinéraire.

Application 100% statique (un seul fichier `index.html`, aucun backend, aucune dépendance de build) — utilisable directement dans un navigateur, installable comme une app sur mobile (PWA), ou hébergée sur GitHub Pages.

## Fonctionnalités

### Langue
- **Interface disponible en français, anglais et espagnol** — détectée automatiquement à partir de la langue du navigateur au premier lancement, modifiable à tout moment dans Paramètres (⚙️) → Langue. Le choix est mémorisé et s'applique immédiatement, sans recharger la page.

### Données et prix
- **Prix en temps réel** — données issues de l'API officielle du gouvernement français (`data.economie.gouv.fr`, prix des carburants en flux instantané) : Gazole (sélectionné par défaut), SP95, SP98, E10, E85, GPLc.
- **Espagne** — détection automatique du pays via la position : en Espagne, les stations viennent de l'API officielle du MITECO (gouvernement espagnol). E10/E85 n'existent pas sur le marché espagnol et n'apparaissent donc pas pour ces stations.
- **Allemagne** — stations issues de [Tankerkönig](https://creativecommons.tankerkoenig.de/) (nécessite une clé API gratuite). SP98/E85/GPLc ne sont pas couverts par cette API et n'apparaissent donc pas pour ces stations.
- Le mode Itinéraire et les prix nationaux les moins chers restent pour l'instant limités à la France.
- **Prix les moins chers de France** — une rangée de pastilles affiche, pour chaque carburant, la fourchette de prix nationale (du moins cher au plus cher, ex. « 1,654–1,892 € ») ; cliquer sur l'une d'elles centre la carte sur la station la moins chère correspondante, où qu'elle soit en France.
- **Détection de marque** — reconnaissance automatique de l'enseigne (TotalEnergies, Leclerc, Intermarché, Carrefour, Shell, BP, etc.) à partir de l'adresse.

### Localisation et recherche
- **Géolocalisation transparente** : avant la toute première demande, une courte pop-up explique pourquoi l'app a besoin de la position (trouver les stations les moins chères autour de toi, jamais envoyée ailleurs ni conservée), pour ne pas surprendre quelqu'un qui découvre l'app. Si la position est déjà autorisée, elle est utilisée directement sans repasser par cette étape.
- **Interrupteur « Utiliser ma position »** dans Paramètres (⚙️) : active ou désactive à tout moment l'usage de la position par l'app, indépendamment de l'autorisation du navigateur. Une fois désactivé explicitement, l'app ne redemande plus toute seule — il suffit de rebasculer l'interrupteur pour réactiver.
- **Récupération après un refus** : si l'accès a été refusé par le navigateur, l'app reste pleinement utilisable (recherche de ville, prix les moins chers de France) au lieu de rester bloquée sans résultat. Les Paramètres expliquent comment réactiver l'accès dans les réglages du navigateur — la seule méthode possible une fois le refus mémorisé, le site ne pouvant pas rouvrir la demande automatiquement.
- **Rappel de confidentialité caché** : rester appuyé 5 secondes sur le bouton « Ma position » affiche un petit rappel — aucune donnée n'est conservée, aucun compte, aucun serveur ; la position ne sert qu'en local, dans le navigateur, pour calculer les distances.
- **Recherche de ville par préfixe** sur la base officielle des communes de France (`geo.api.gouv.fr`, Etalab) : couvre les ~35 000 communes, y compris les plus petits villages, avec Nominatim (OpenStreetMap) en repli automatique si besoin.

### Recherche « Autour de moi »
- **Actualisation automatique en se déplaçant sur la carte** : à partir d'un certain niveau de zoom (ville/quartier), déplacer ou zoomer la carte relance la recherche autour du nouveau centre visible, sans recentrer la carte ni interrompre une zone dessinée à la main. Un bouton « Rechercher ici » (façon Park4night) apparaît pendant le déplacement pour forcer la recherche immédiatement sans attendre.
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
- **Sélecteur de type de carte** (haut à droite) : style Minimum (moderne et épuré, noms de villages à tous les zooms, numéros d'autoroute/départementales) ou Satellite, mémorisé d'une visite à l'autre.
- **Bouton « Ma position »** placé en bas à droite, à l'emplacement désormais standard sur les applications de cartographie mobiles.
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

### Sécurité et transparence
- Échappement systématique des données externes avant affichage (protection XSS).
- Content-Security-Policy restreignant les scripts, styles, images et requêtes réseau aux seuls domaines utilisés par l'app.
- Liens externes en `rel="noopener noreferrer"`.
- Localisation : explication préalable avant la première demande d'accès, et app pleinement utilisable sans position (voir « Localisation et recherche » ci-dessus).

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
