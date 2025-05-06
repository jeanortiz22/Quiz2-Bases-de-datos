summary: Bases de datos NoSQL orientada a grafos
id: bases-datos-nosql-grafos
categories: desarrollo
status: draft
authors: Equipo Quiz 2
environments: Web

# Quiz 2

## Bases de Datos NoSQL Orientadas a Grafos
Duration: 0:03:00  
Los grafos son una estructura de datos que permite modelar relaciones entre entidades mediante nodos y aristas. Se utilizan en bases de datos para representar redes sociales, rutas, recomendaciones, entre otros.

## Neo4j
Duration: 0:03:00  

### 1. ¿Qué es Neo4j?
**Neo4j** es una base de datos NoSQL orientada a grafos. Utiliza nodos, relaciones y propiedades para modelar datos de forma natural. Ideal para:

- Redes sociales
- Recomendaciones
- Rutas
- Web semántica

### 2. Instalación de Neo4j

#### Opción 1: Neo4j Desktop
- Descargar desde: [neo4j.com/download](https://neo4j.com/download)
- Crear un proyecto local y seleccionar una base de datos

#### Opción 2: Neo4j Aura (versión en la nube)
- Accede desde: [aura.neo4j.io](https://aura.neo4j.io)

#### Problemas comunes
- El puerto 7474 ya está en uso
- Java no instalado
- Problemas de permisos

### 3. Lenguaje Cypher

Cypher es el lenguaje de consulta utilizado en Neo4j, similar a SQL pero enfocado en grafos.

### 4. DDL: Definición de Estructuras

#### Crear nodos
```cypher
CREATE (:Persona {nombre: 'Ana', edad: 28});
```

#### Crear relaciones
```cypher
MATCH (a:Persona {nombre: 'Ana'}), (b:Persona {nombre: 'Luis'})
CREATE (a)-[:AMIGO_DE]->(b);
```

#### Crear índice
```cypher
CREATE INDEX FOR (p:Persona) ON (p.nombre);
```

#### Crear restricción
```cypher
CREATE CONSTRAINT FOR (e:Empresa) REQUIRE e.nombre IS UNIQUE;
```

### 5. DML: Manipulación de Datos

#### Insertar nodos
```cypher
CREATE (:Persona {nombre: 'Luis', edad: 32});
```

#### Crear relaciones
```cypher
MATCH (p:Persona {nombre: 'Ana'}), (e:Empresa {nombre: 'TechCorp'})
CREATE (p)-[:TRABAJA_EN]->(e);
```

#### Actualizar nodos
```cypher
MATCH (p:Persona {nombre: 'Luis'})
SET p.edad = 33;
```

#### Eliminar nodos y relaciones
```cypher
MATCH (p:Persona {nombre: 'Luis'})
DETACH DELETE p;
```

### 6. Demostración práctica: Mini Red Social

#### Paso 1: Crear nodos
```cypher
CREATE (:Persona {nombre: 'Ana', edad: 28});
CREATE (:Persona {nombre: 'Luis', edad: 32});
CREATE (:Empresa {nombre: 'TechCorp'});
```

#### Paso 2: Crear relaciones
```cypher
MATCH (a:Persona {nombre: 'Ana'}), (b:Persona {nombre: 'Luis'})
CREATE (a)-[:AMIGO_DE]->(b);

MATCH (a:Persona {nombre: 'Ana'}), (e:Empresa {nombre: 'TechCorp'})
CREATE (a)-[:TRABAJA_EN]->(e);
```

#### Paso 3: Consultar la red
```cypher
MATCH (p:Persona)-[:TRABAJA_EN]->(e:Empresa)
RETURN p.nombre, e.nombre;
```

### 7. Visualización esperada

```
(Ana)-[:AMIGO_DE]->(Luis)
(Ana)-[:TRABAJA_EN]->(TechCorp)
```

### 8. Conclusión

- Neo4j es potente para modelar relaciones.
- Cypher es intuitivo para leer y escribir.
- Las operaciones DDL y DML permiten construir y consultar estructuras fácilmente.

## AllegroGraph
Duration: 0:03:00  
Azure Cosmos DB es una base de datos NoSQL distribuida globalmente que admite múltiples modelos, incluyendo grafos mediante la API de Gremlin. Está optimizada para escalabilidad y baja latencia.

## Dgraph
Duration: 0:03:00  
Aerospike es una base de datos NoSQL orientada a alto rendimiento y baja latencia, comúnmente utilizada para aplicaciones en tiempo real. Aunque no es una base de datos de grafos, puede integrarse con ellas.

## Virtuoso
Duration: 0:03:00  
Virtuoso es una base de datos multi-modelo que permite almacenar datos relacionales y de grafos RDF. Es muy utilizada en aplicaciones semánticas y del web semántico, como Linked Open Data.

## Arango DB
Duration: 0:03:00  
ArangoDB es una base de datos NoSQL multi-modelo que permite trabajar con grafos, documentos y claves-valor. Su flexibilidad permite consultas complejas a través de AQL, su lenguaje de consulta.

## OrientDB
Duration: 0:03:00  
OrientDB combina características de bases de datos de grafos y documentos. Soporta relaciones complejas, ACID transactions y es útil para modelado de dominios complejos en tiempo real.
