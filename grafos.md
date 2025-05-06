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

### 1. ¿Qué es AllegroGraph?
Esta base de datos es uno de los modelos más modernos en el mercado. Posee un manejo eficiente de la memoria y tiene gran capacidad de almacenamiento. No usa tablas ni columnas, sino que usa **RDF triplas**(sujeto, predicado, objeto).

Uno de los aspectos más destacados de AllegroGraph es que tiene un manejo eficiente de la memoria y una gran capacidad de almacenamiento, lo que lo hace muy útil en aplicaciones que requieren procesar muchos datos interrelacionados.


### 2. Lenguaje SPARQL

SPARQL (SPARQL Protocol and RDF Query Language) es el lenguaje estándar para consultar bases de datos RDF (datos en forma de tripletas: sujeto – predicado – objeto), y trabaja con grafos de conocimiento.


### 3. Lenguaje de definición de datos (DDL)

| Acción DDL (SQL)         | En AllegroGraph (RDF Triplestore)      |
|--------------------------|----------------------------------------|
| Crear tabla              | Crear clase (`rdf:type rdfs:Class`)    |
| Definir columnas         | Definir propiedades (`rdf:Property`)   |
| Crear relaciones         | Crear aristas                          |
| Definir claves únicas    | Usar URI único como sujeto             |

Veamos un ejemplo concreto:

```turtle
<http://miapp.com/Persona/1> <http://miapp.com/propiedad/nombre> "Juan" . 
```
✓ Sujeto: `http://miapp.com/Persona/1` → Persona con ID 1.

✓ Predicado: `http://miapp.com/propiedad/nombre` → propiedad nombre.

✓ Objeto: "Juan" → valor del nombre.

Teniendo en cuenta lo anterior, ahora procederemos a crear las clases y a definir sus propiedades, tal como se muestra en el siguiente ejemplo:

```turtle
# Creamos una clase llamada Persona
<http://miapp.com/Persona> rdf:type rdfs:Class .

# Creamos propiedades:

# Una propiedad "nombre" que es un texto
<http://miapp.com/propiedad/nombre> rdf:type rdf:Property ;
    rdfs:domain <http://miapp.com/Persona> ;
    rdfs:range xsd:string .

# Una propiedad "edad" que es un número
<http://miapp.com/propiedad/edad> rdf:type rdf:Property ;
    rdfs:domain <http://miapp.com/Persona> ;
    rdfs:range xsd:integer .

```


### 4. Lenguaje de Manipulación de datos (DML)

Las operaciones DML se realizan principalmente usando **SPARQL**, el lenguaje estándar para consultas y manipulación de datos **RDF** `{<sujeto> <predicado> <objeto>}`.

A continuación se describen las principales operaciones DML soportadas:

**▷ INSERT DATA**

Permite insertar nuevos nodos y relaciones en el grafo RDF. En AllegroGraph, esto se utiliza para agregar información como propiedades de recursos.

```turtle
PREFIX ex: <http://example.com/>

INSERT DATA {
  ex:libro1 ex:titulo "Libro Barato" .
  ex:libro1 ex:precio "30"^^xsd:integer .
}
```
Este ejemplo crea un nodo ex:libro1 con dos propiedades: titulo y precio.

**▷ SELECT**

Se utiliza para consultar nodos y relaciones dentro del grafo RDF. Puede incluir cláusulas opcionales y filtros.

```turtle
PREFIX ex: <http://example.com/>

SELECT ?titulo ?precio WHERE {
  ?x ex:titulo ?titulo .
  OPTIONAL {
    ?x ex:precio ?precio .
    FILTER ( ?precio < 40 )
  }
}
```
Esta consulta selecciona el título de los libros y, si está disponible, su precio, filtrando solo aquellos cuyo precio sea menor a 40.

**▷ DELETE DATA**

Permite eliminar nodos o relaciones específicas. En AllegroGraph se puede utilizar para borrar datos previamente insertados.

```turtle
DELETE DATA {
  ex:libro1 ex:precio "30"^^xsd:integer .
}
```
Este ejemplo elimina la relación precio del recurso ex:libro1.

**▷ UPDATE (Simulado)**

SPARQL no cuenta con una instrucción UPDATE directa como en SQL. Sin embargo, en AllegroGraph y otros sistemas que implementan SPARQL, esta operación puede simularse mediante una combinación de DELETE e INSERT. Primero se elimina la información antigua y luego se inserta la nueva.


### 5. Instalación AllegroGraph

Para trabajar con AllegroGraph de forma visual, se recomienda utilizar Gruff, una herramienta gráfica que permite explorar y gestionar datos RDF
Para instalar AllegroGraph, se recomienda ingresar al enlace oficial y descargar la versión correspondiente a tu sistema operativo. Sin embargo, durante la instalación pueden surgir algunos problemas:

**• Permisos de administrador:** en Windows, a veces se necesita ejecutar el instalador como administrador para evitar errores.

**• Antivirus:** algunos antivirus bloquean el ejecutable o impiden que se instale correctamente.

**• Versiones incompatibles:** hay que asegurarse de que la versión descargada sea compatible con el sistema operativo (por ejemplo, Windows 64 bits).

**• Conflictos de puerto:** AllegroGraph por defecto usa el puerto 10035. Si está ocupado, el servidor no arranca.

Una vez instalado, se puede abrir desde la carpeta de instalación y empezar a trabajar con la interfaz llamada Gruff.


### 6. Demostración practica: Sistema de Bibliotecas

**Paso 1: Crear nodos**
```turtle
INSERT DATA {
  :ElPrincipito rdf:type :Libro ;
                :titulo "El Principito" ;
                :escritoPor :SaintExupery ;
                :prestadoA :Maria .

  :SaintExupery rdf:type :Autor ;
                :nombre "Antoine de Saint-Exupéry" .

  :Maria rdf:type :Lector ;
         :nombre "Maria López" .
}
```
**Paso 2: Consultar libros prestados**
```turtle
PREFIX : <http://biblioteca.com/>

SELECT ?titulo ?lector
WHERE {
  ?libro :titulo ?titulo ;
         :prestadoA ?persona .
  ?persona :nombre ?lector .
}
```
**Paso 3: Visualización esperada**
```turtle
(El Principito) --[:prestadoA]--> (Maria López)
(El Principito) --[:escritoPor]--> (SaintExupery)
```


### 7. Conclusiones

• Los grafos RDF son una forma eficaz de modelar relaciones complejas entre entidades del mundo real.

• SPARQL es un lenguaje poderoso y expresivo, capaz de realizar consultas similares a SQL, pero adaptado a la web semántica y a grafos distribuidos.

• Aplicaciones como sistemas de bibliotecas, redes sociales o mapas de ciudades se benefician enormemente del enfoque en grafos para representar y analizar datos conectados.

• La estructura sujeto-predicado-objeto permite un modelo extensible, ideal para representar nuevas entidades y relaciones sin alterar la base de datos existente.

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
