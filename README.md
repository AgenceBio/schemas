# `schemas`

## RPG Bio

- **Package** : [`rpg-bio/datapackage.json`](rpg-bio/datapackage.json).
- **Champs de ressources** : [`rpg-bio/table.schema.json`](rpg-bio/table.schema.json).

### Pour mettre à jour le champ `resources`

Le champ `resources` se récupère au format JSON dans le presse-papier du système d'exploitation en lançant cette commande :

```sh
curl -sSL https://www.data.gouv.fr/api/1/datasets/616d6531c2951bbe8bd97771/ |
  jq -r '.resources | map({ name: .title, path: .latest, format: (if .format == "geojson.gz" then "geojson" elif .format == "shp.zip" then "shapefile" else null end), mediatype: (if .format == "geojson.gz" then "application/json" elif .format == "shp.zip" then "application/octet-stream" else .mime end), schema: "./table.schema.json" })' |
  pbcopy
```
