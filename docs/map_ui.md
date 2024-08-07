## map_ui() - Carte intéractive des stations

### Description

La fonction `map_ui` génère une carte intéractive en utilisant le package `leaflet`. Cette fonction mets en place les marqueurs représentant les stations données dans la liste `stations`, concernant les tuiles personnalisés, l'argument `site` permet de chercher dans le fichier `tiles_config.json` si une configuration pour ce site existe auquel cas il mettra les tuiles par défaut appartenant au `Orthophoto IGN`.

### Fonctionnalités

- Affichage des stations sur une carte avec des marqueurs

- Couleur des marqueurs en fonction de la dernière mise à jour de la station

- Intégration d'une configuration par site pour l'utilisation d'un géoserveur personnalisé

- Affichage d'information par station (Nom de la station, Site, Dernière mise à jour)

### Paquets nécessaires

Pour utiliser cette fonction, assurez-vous d'avoir ces paquets installés :

```R
install.packages(c("htmltools", "xts", "leaflet", "jsonlite"))
```

### Utilisation

#### 1. Paramètres (Optionnels)

- `stations` : Un data.frame contenant les informations des stations à afficher. Ce data.frame doit inclure les colonnes suivantes :
    - `date` : La date de la dernière mise à jour (format `Date`).
    - `lat` : La latitude de la station (numérique).
    - `lon` : La longitude de la station (numérique).
    - `sta_code` : Le code de la station (caractère).
    - `site_name` : Le nom du site où se trouve la station (caractère).

- `site` : Le nom du site pour laquel la configuration des tuiles doit être récupérée depuis un fichier JSON. Si non spécifié, la configuration par défaut est utilisée.

#### 2. Exemple d'utilisation

Voici un exemple d'utilisation de la fonction `map_ui`:

```R
ui <- fluidPage(
    mainPanel(
        leafletOutput("map", height = 600)
    )
)

server <- function(input, output, session) {
    stations <- data.frame(
    date = as.Date(c('2024-07-01', '2024-07-02')),
    lat = c(37.7749, 34.0522),
    lon = c(-122.4194, -118.2437),
    sta_code = c("SFO", "LAX"),
    site_name = c("San Francisco", "Los Angeles")
  )

  output$map <- renderLeaflet({
    map_ui(stations, site = "Viella")
  })
}
```

### Configuration

L'explication du fichier du configuration est dans le module de visualisation, le fichier est situé à `inst/app/www/tiles_config.json`.