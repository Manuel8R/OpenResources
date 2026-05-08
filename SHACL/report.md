# Informe de Validación SHACL

## Grupo 2 - DOISR 2025-2026

Este documento recoge los resultados obtenidos tras la validación SHACL de la ontología Pokémon desarrollada en esta práctica.

La validación se ha realizado utilizando la herramienta **SHACL Playground**  
(<https://shacl.org/playground/>) a partir de los siguientes ficheros:

- **Grafo de shapes:** `shapes.ttl`  
- **Grafo de datos:** `datos.ttl`

Tras cargar ambos ficheros, la herramienta generó automáticamente un informe de validación (almacenado como `reportShacl.ttl`).

---

## 1. Descripción de los SHACL shapes

El fichero `shapes.ttl` contiene **8 shapes de validación**, diseñados para garantizar la coherencia estructural y semántica de los datos Pokémon.

### 1. `poke:PokemonFinalEvolutionShape`
Evita que un Pokémon marcado como evolución final (`esEvolucionFinal = true`) tenga evoluciones posteriores mediante `poke:evolucionaA`.

### 2. `poke:PokemonMovementClassShape`
Restringe `poke:tieneMovimiento` a instancias de la clase `poke:Movimiento`.

### 3. `poke:PokemonDistinctTypeShape`
Impide que un Pokémon tenga el mismo tipo como primario y secundario.

### 4. `poke:PokemonAllowedTypesShape`
Limita los tipos Pokémon a un conjunto cerrado de valores válidos predefinidos (Grass, Fire, Water, Electric, etc.).

### 5. `poke:PokemonSingleGenerationShape`
Garantiza que cada Pokémon pertenece a una única generación.

### 6. `poke:PokemonSingleFormShape`
Restringe a un máximo de una forma simultanea regional por Pokémon.

### 7. `poke:PokemonExpShape`
Obliga a que la experiencia necesaria para llegar al nivel 100 sea un entero mayor o igual a 1.

### 8. `poke:PokemonBaseStatsPositiveShape`
Verifica que todas las estadísticas base (HP, Attack, Defense, Sp. Attack, Sp. Defense, Speed) sean valores enteros positivos.

En conjunto, estas restricciones utilizan mecanismos como cardinalidad, tipos de datos, clases, listas cerradas y restricciones lógicas.

---

## 2. Resultado global de la validación

El resultado obtenido en la validación fue:

```ttl
sh:conforms false
```

Esto indica que el conjunto de datos no cumple completamente las restricciones definidas en los shapes.

Este resultado es esperado, ya que el fichero datos.ttl contiene instancias con errores intencionados para comprobar el comportamiento del sistema de validación.

Se han detectado múltiples violaciones distribuidas en distintos recursos del grafo de datos.

---

## 3. Análisis de errores detectados

A continuación se detallan los principales errores encontrados en el grafo de datos, agrupados por tipo de restricción SHACL afectada.

---

### 3.1 Errores en evolución de Pokémon

#### `poke:Bad_EvolucionFinalNoBooleana`

Se detecta un problema en el valor del atributo `esEvolucionFinal`, que no cumple con el tipo de dato esperado.

| Problema | Restricción incumplida | Corrección |
|----------|------------------------|------------|
| Valor no booleano | `xsd:boolean` | Usar `true` o `false` |

Ejemplo de corrección:

```ttl
poke:esEvolucionFinal false .
```

---
#### `poke:Bad_EvolucionaALiteral`
En este caso, el problema está en el uso de un literal en lugar de un recurso.

| Problema | Restricción incumplida | Corrección |
|----------|------------------------|------------|
| Evolución como literal | Se requiere IRI | Usar recurso `poke:Wartortle` |

Ejemplo de corrección:

```ttl
poke:evolucionaA poke:Wartortle .
```

---
#### `poke:Bad_EvolucionFinalConEvolucion`

Este caso comprueba la regla semántica principal de la shape: un Pokémon marcado como evolución final no puede tener una evolución posterior mediante `poke:evolucionaA`.

| Problema | Restricción incumplida | Corrección |
|----------|------------------------|------------|
| Evolución final con evolución posterior | `sh:not` | Eliminar `poke:evolucionaA` o marcar `esEvolucionFinal` como `false` |

Ejemplo de corrección:

```ttl
poke:esEvolucionFinal true .
```

---

### 3.2 Errores en movimientos


#### `poke:Bad_MovimientoNoEsMovimiento`
El valor asignado a `poke:tieneMovimiento` no pertenece a la clase esperada.

| Problema | Restricción incumplida | Corrección |
|----------|------------------------|------------|
| No es instancia de `poke:Movimiento` | `sh:class poke:Movimiento` | Usar un movimiento válido |

Ejemplo de corrección:

```ttl
poke:tieneMovimiento poke:Ember .
```

---

### 3.3 Errores en tipos de Pokémon


#### `poke:Bad_TiposIguales`
Se detecta incoherencia al asignar el mismo tipo como primario y secundario.

| Problema | Restricción incumplida | Corrección |
|----------|------------------------|------------|
| Tipos iguales | restricción de disyunción | Usar tipos diferentes |

Ejemplo correcto:

```ttl
poke:tieneTipoPrimario poke:Fire ;
poke:tieneTipoSecundario poke:Water .
```

---

### 3.4 Valores de tipo no válidos

Algunas instancias del dataset utilizan valores que no pertenecen al conjunto cerrado de tipos definido en la restricción `sh:in` del shape `poke:PokemonAllowedTypesShape`.

Esto provoca violaciones porque el modelo solo permite un conjunto limitado de tipos de Pokémon (como Grass, Fire, Water, Electric, etc.), y cualquier valor fuera de esa lista se considera inválido.

| Problema | Restricción incumplida | Corrección |
|----------|------------------------|------------|
| Tipo no incluido en la lista permitida | `sh:in` (conjunto cerrado de tipos) | Usar únicamente tipos definidos en la ontología |

En estos casos, el error no depende de la estructura del dato, sino del uso de un valor no autorizado dentro del vocabulario controlado. Por tanto, la solución consiste en sustituir el tipo incorrecto por uno de los tipos válidos definidos en el sistema.

Ejemplo de corrección:

```ttl
poke:tieneTipoPrimario poke:Fire .
```

---
### 3.5 Errores en generación y forma

En este apartado se agrupan los errores relacionados con la asignación de generación y formas regionales en los Pokémon.

Se han detectado incumplimientos de las restricciones de cardinalidad definidas en los shapes, lo que afecta a la consistencia global del modelo.

| Problema | Restricción incumplida | Corrección |
|----------|------------------------|------------|
| Falta de generación o múltiples valores asignados | `sh:minCount 1 / sh:maxCount 1` | Asignar exactamente una única generación |
| Más de una forma regional asociada a un Pokémon | `sh:maxCount 1` | Mantener solo una forma regional válida |

---

#### Ejemplo de corrección

Asignación correcta de generación:

```ttl
poke:tieneGeneracion poke:Gen1 .
```
En el caso de formas regionales, debe garantizarse que cada Pokémon tenga como máximo una única instancia asociada mediante poke:tieneFormaRegional. Si existe más de una, se debe eliminar la redundante o redefinir el modelado para evitar ambigüedad.

---
### 3.6 Errores en experiencia

Se han detectado instancias de Pokémon que no cumplen la restricción establecida sobre la experiencia necesaria para alcanzar el nivel 100.

Esta restricción exige que el valor sea un número entero y que sea mayor o igual a 1 (`sh:minInclusive 1`), además de que el dato esté presente.

| Problema | Restricción incumplida | Corrección |
|----------|------------------------|------------|
| Valor ausente o no válido en experiencia | `sh:minInclusive 1` / `xsd:integer` | Usar un entero ≥ 1 |

En los casos detectados, el error se produce cuando el valor de `poke:hasExpToLvl100` no respeta el tipo de dato esperado o no cumple el valor mínimo permitido.

Ejemplo de corrección:

```ttl
poke:hasExpToLvl100 1059860 .
```
Esta validación asegura que todos los Pokémon tengan un valor coherente de experiencia asociado a su progresión hasta nivel 100, evitando inconsistencias en el modelo de crecimiento.


---
### 3.7 Errores en estadísticas base

Se han detectado varias inconsistencias en las estadísticas base de algunos Pokémon. Estas restricciones aseguran que todas las estadísticas tengan valores válidos y coherentes dentro del modelo.

| Problema | Restricción incumplida | Corrección |
|----------|------------------------|------------|
| Valor de estadística ≤ 0 o ausente | `sh:minInclusive 1` | Todas las estadísticas deben ser enteros positivos |

Este tipo de error afecta a cualquier propiedad de estadísticas base como HP, ataque, defensa, ataque especial, defensa especial o velocidad, ya que todas comparten la misma restricción de positividad.

Ejemplo de corrección:

```ttl
poke:hasHP 45 ;
poke:hasAttack 49 ;
poke:hasDefense 49 ;
poke:hasSpAttack 65 ;
poke:hasSpDefense 65 ;
poke:hasSpeed 45 .
```

## 4. Evaluación del modelo SHACL

La validación realizada sobre el conjunto de datos demuestra que el modelo SHACL definido en `shapes.ttl` cumple correctamente su función de control de calidad y consistencia sobre la ontología Pokémon.

En términos generales, los resultados obtenidos confirman que las restricciones diseñadas son efectivas para detectar incoherencias estructurales, semánticas y de tipo en los datos.

### 4.1 Correcto funcionamiento de las restricciones

Se ha comprobado que:

- Las restricciones de **tipo de dato** (boolean, integer, IRI) detectan valores incorrectos de forma precisa.
- Las restricciones de **cardinalidad** (`minCount`, `maxCount`) aseguran la completitud de la información obligatoria.
- Las restricciones de **valores permitidos** (`sh:in`) evitan el uso de tipos no contemplados en la ontología.
- Las restricciones lógicas (como `sh:disjoint`) identifican inconsistencias semánticas relevantes.
- Las restricciones estructurales garantizan que las relaciones entre recursos sean coherentes.

---

### 4.2 Calidad del diseño de los shapes

El conjunto de shapes presenta una buena cobertura del dominio modelado, ya que:

- Se incluyen restricciones tanto a nivel de clase (`Pokemon`) como de propiedades.
- Se combinan validaciones de integridad estructural y semántica.
- Se evita la ambigüedad en la interpretación de relaciones críticas como evoluciones y tipos.

---

### 4.3 Conclusión general

Durante la revisión se detectó que `poke:PokemonFinalEvolutionShape` no cubría correctamente todos los casos negativos documentados. Por ello, se ajustó la shape para validar explícitamente que `poke:esEvolucionFinal` sea booleano, que `poke:evolucionaA` apunte a un IRI y que un Pokémon marcado como evolución final no tenga evolución posterior.

También se añadió el caso negativo `poke:Bad_EvolucionFinalConEvolucion` para comprobar directamente la restricción lógica de evolución final.

Por tanto, se puede concluir que:

- El modelo SHACL es coherente y completo para el dominio definido.
- Las restricciones son lo suficientemente estrictas para detectar errores relevantes.
- La ontología validada presenta un comportamiento consistente bajo el sistema de validación SHACL.

En conjunto, la validación confirma la correcta definición y funcionamiento del modelo de restricciones.
