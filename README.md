# Developing Open, Interoperable Semantic Resources

## Grupo 2

### Miembros

| Nº | Nombre | Usuario GitHub |
|---|---|---|
| 1 | Manuel Bravo Roig | @Manuel8R |
| 2 | Pablo Calle Tercero | @pcalle23 |
| 3 | Alberto Buceta Coroba | @BuceGithub |
| 4 | Daniel Javier Flores Flores | @danielorse |

---

## Estructura del repositorio

```text
OpenResources/
|
|-- Dataset/
|   |-- pokemonDataSetOriginal.csv
|   |-- Kanto.csv
|   |-- Dataset_Pokedex.csv
|   |-- Dataset_AllPokemon.csv
|
|-- ontology/
|   |-- ontology_v2.ttl
|   |-- ontologySchema.drawio
|   |-- ontologySchema.xml
|
|-- SHACL/
|   |-- shapes.ttl
|   |-- datos.ttl
|   |-- reportShacl.ttl
|   |-- report.md
|
|-- OntologyRequirements.csv
|-- Casos de uso.pdf
|-- AtributosDescartados.pdf
|-- README.md
```

---

## Datasets utilizados

Los datasets que hemos usado están relacionados con Pokemon y vienen de las siguientes fuentes:

- `Dataset_Pokedex`: https://www.kaggle.com/datasets/takamasakato/pokemon-all-status-data
- `Dataset_AllPokemon`: https://www.kaggle.com/datasets/maca11/all-pokemon-dataset
- `PokemonDataSetOriginal`: https://www.kaggle.com/datasets/divyadeep/pokemon

---

## Recursos principales

- `OpenResources/OntologyRequirements.csv`:incluye requisitos del proyecto.
- `OpenResources/Casos de uso.pdf`: recopilación de casos de uso.
- `OpenResources/AtributosDescartados.pdf`: atributos descartados y justificación.
- `OpenResources/ontology/ontology_v2.ttl`: versión actual de la ontología en Turtle.
- `OpenResources/ontology/ontologySchema.drawio`: esquema conceptual de la ontología.
- `OpenResources/ontology/ontologySchema.xml`: exportación del esquema.
- `OpenResources/SHACL/`: restricciones de los datos, datos de muestra correctos e inválidos y un report de su funcionamiento.

---

## Uso de IA

Hemos utilizado la IA para:

- Pulir los casos de uso a partir de múltiples datasets, con el objetivo de reducir redundancias y mejorar su claridad.
- Corregir y refinar los requisitos de la ontología para hacerlos más consistentes y mejor alineados con el dominio modelado.
- Afinar y pulir formato del README.md
- Realizar cambios simples pero que supone una molestia (sustituir el prefijo pokemon: por poke:)

---

## Última actualización del README

08 mayo de 2026
