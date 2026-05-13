# Developing Open, Interoperable Semantic Resources

## Grupo 2

### Miembros

| Nº | Nombre | Usuario GitHub |
|---|---|---|
| 1 | Manuel Bravo Roig | @Manuel8R |
| 2 | Pablo Calle Tercero | @pcalle23 |
| 3 | Daniel Javier Flores Flores | @danielorse |

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
|-- release/
|   |-1.0.0/
|   |  |-- ontology_v2.ttl
|   |  |-- ontologySchema.drawio
|   |  |-- ontologySchema.xml
|   |
|   |-2.0.0/
|   |  |-- ontology.ttl
|   |  |-- 406.html
|   |  |-- index-en.html
|   |
|   |-2.1.0/
|     |-- ontology.ttl
|     |-- 406.html
|     |-- index-en.html
|
|-- SHACL/
|   |-1.0.0/
|   |  |-- report.md
|   |  |-- reportShacl.ttl
|   |  |-- datos.ttl
|   |  |-- shapes.ttl
|   |
|   |-2.0.0/
|   |  |-- reportShacl.ttl
|   |  |-- datos.ttl
|   |  |-- shapes.ttl
|   |
|   |-2.1.0/
|   |  |-- reportShacl.ttl
|   |  |-- datos.ttl
|   |  |-- shapes.ttl
|   |  ...
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

13 mayo de 2026
