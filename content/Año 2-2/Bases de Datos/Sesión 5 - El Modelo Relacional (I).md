
> **Curso:** Bases de Datos — Grado en Ingeniería Informática  
> **Profesor:** Jaime Álvarez Benayas — Universidad Nebrija  
> **Sesión:** 5 · El modelo relacional — Conceptos fundamentales, relaciones y restricciones

---

## Contenidos

1. [[#Contexto y motivación]]
2. [[#Bases de datos relacionales]]
3. [[#Relaciones o tablas]]
   - [[#Intensión y extensión]]
   - [[#Tipos de relaciones]]
4. [[#Atributos clave de la relación]]
5. [[#Restricciones del modelo relacional]]
   - [[#Restricciones inherentes]]
   - [[#Grupos repetitivos (violaciones de 1FN)]]

---

## Contexto y motivación

El modelo relacional es un **modelo de datos lógico** que concreta el diseño realizado a través del [[Sesión 3 - Modelos de Datos#Modelo Entidad-Relación|modelo conceptual E/R]]. El flujo completo de diseño es:

```
Especificación        Modelo conceptual      Modelo lógico         Base de datos
de requisitos  ──►   (Diagrama E/R)   ──►  (Modelo relacional)  ──►  MySQL
```

**Problemática:** El modelo E/R (Extendido) captura toda la semántica del universo del discurso, pero **no es soportado directamente por ningún SGBD**.

**Solución:** Se desarrolla un **modelo lógico** que, usando estructuras de datos concretas, representa la misma información que el modelo conceptual y sí es soportado por el SGBD.

>  *¿Por qué no hacer el modelo relacional directamente desde la especificación de requisitos, saltándose el E/R?*  
> Porque el E/R permite capturar más semántica y detectar errores conceptuales antes de entrar en los detalles del SGBD. El objetivo es minimizar la **pérdida semántica** en la traducción.

En esta sesión se tratan en profundidad:
- El concepto algebraico de **relación** (fundamento de las BD relacionales)
- **Propiedades** de las relaciones y sus restricciones semánticas (integridad referencial)
- La **representación** de entidades y asociaciones mediante el grafo relacional
- Las técnicas de **transformación E/R → Modelo Relacional**

---

## Bases de datos relacionales

### Historia y fundamento

El modelo relacional fue propuesto por **E. F. Codd** a finales de los años 60 en su artículo *"A Relational Model for Large Shared Data Banks"*, basándose en:
- **Teoría de Conjuntos**
- **Álgebra relacional**

### El concepto de relación

Según la Teoría de Conjuntos, una **relación** viene dada por grupos de valores (**tuplas**) tomados de sus correspondientes **dominios**.

Ejemplo: la relación E/R *Trabajador → trabaja en → Departamento (N:1)* se traduce en dos tablas relacionadas:

| DNI | Nombre | IdDepartamento |
|---|---|---|
| 11111111 | José Pérez | Logística |
| 22222222 | María Rodríguez | Ventas |

| IdDepartamento | Ubicación |
|---|---|
| Logística | Sede Madrid |
| Ventas | Sede Sevilla |

El **dominio** es análogo al del [[Sesión 3 - Modelos de Datos#Atributos|modelo E/R]]: especifica una colección completa de posibles valores para un elemento. Ejemplos: números naturales, enteros, cadenas de longitud 6, etc.

Formalmente, cada tupla `t` de una relación `R` tiene la forma:

```
t₁(v₁₁ ∈ D₁,  v₁₂ ∈ D₂,  …,  v₁ₙ ∈ Dₙ)
t₂(v₂₁ ∈ D₁,  v₂₂ ∈ D₂,  …,  v₂ₙ ∈ Dₙ)
```

Todas las tuplas mantienen el **mismo número y orden** de valores, tomados siempre de los mismos dominios. El resultado visual es una **tabla** (matriz de valores).

### Objetivos del modelo relacional

| Objetivo | Descripción |
|---|---|
| **Independencia física** | La representación lógica permanece separada del almacenamiento físico |
| **Flexibilidad** | Permite recoger los esquemas de distintos perfiles de usuario |
| **Uniformidad** | Un único tipo de estructura (tabla) para entidades e interrelaciones |
| **Sencillez** | Fácil manejo y comprensión |

---

## Relaciones o tablas

### Estructura básica

| Atributo1 | Atributo2 | ... | AtributoN |
| --------- | --------- | --- | --------- |
| Valor₁₁   | Valor₁₂   | ... | Valor₁ₙ   |
| ValorN₁   | ValorN₂   | ... | ValorNN   |

Cada relación queda caracterizada por:

| Elemento | Descripción |
|---|---|
| **Nombre** | Identifica la relación |
| **Atributos** | Propiedades comunes de todos los elementos de la relación |
| **Tupla** | Conjunto de valores que toman los atributos para un elemento concreto |
| **Grado** | Número de atributos (columnas) |
| **Cardinalidad** | Número de tuplas (filas) |
| **Dominio** | Conjunto finito de valores homogéneos y atómicos asociado a cada atributo |

> ⚠️ Varios atributos pueden compartir un mismo dominio. Ejemplo: `nombre` y `apellidos` comparten el dominio de cadenas de caracteres.

**Ejemplo de relación `Empleado`:**

| IdEmpleado | Nombre | IdDepartamento |
|---|---|---|
| 1 | Juan Sánchez | 1 |
| 2 | Pedro López | 1 |
| 3 | Elena González | 2 |
| 4 | Judith Álvarez | 3 |

- **Grado:** 3 (tres atributos)
- **Cardinalidad:** 4 (cuatro tuplas)

### Intensión y extensión

| Concepto | También llamado | Descripción |
|---|---|---|
| **Intensión** | Esquema de relación | Parte **estática**: definición de la relación `R({Aᵢ:Dᵢ}ᵢ₌₁..ₙ)` |
| **Extensión** | Estado / Ocurrencia | Parte **dinámica**: conjunto de tuplas en un momento determinado |

Notación del esquema de relación:
```
R({Aᵢ : Dᵢ}ᵢ₌₁..ₙ)

Donde:
  R  = nombre de la relación
  Aᵢ = nombre del atributo i
  Dᵢ = dominio del atributo i
  {Aᵢ:Dᵢ} = cabecera de la relación
```

Esto conecta directamente con la [[Sesión 4 - Modelos de Datos#Componente Estática|componente estática]] (intensión) y la [[Sesión 4 - Modelos de Datos#Componente Dinámica|componente dinámica]] (extensión) del modelo de datos.

### Tipos de relaciones

```
  Relaciones
  ├── Básicas      → Independientes; corresponden a entidades/asociaciones del     Nivel conceptual
│                    Siempre tienen nombre y existencia física
  └── Derivadas    → Resultado de operaciones relacionales sobre otras relaciones
      ├── Vistas        → Nivel externo/usuario; virtuales; no almacenan datos   p   propios
    │                   Se definen como una consulta con nombre
    └── Instantáneas  → Nivel interno; reales; almacenan el resultado de una         consulta
                        Representan el estado de la BD en un instante
```

**Ejemplo de vista SQL:**
```sql
  CREATE VIEW resumen_productos AS
  SELECT p.nombre, p.precio, SUM(v.cantidad) AS ventas
  FROM productos p
  LEFT JOIN ventas v ON p.id_producto = v.id_producto
  GROUP BY p.id_producto;
```

---

## Atributos clave de la relación

### Clave candidata

Conjunto **no vacío** de atributos que identifica de forma **unívoca** cada tupla. Propiedades:
- No pueden existir dos tuplas con el mismo valor de clave candidata
- El conjunto de atributos debe ser **mínimo**: si se suprime cualquiera de ellos, deja de ser clave

### Tipos de claves

| Tipo | Definición |
|---|---|
| **Clave candidata** | Conjunto mínimo de atributos que identifica unívocamente cada tupla |
| **Clave primaria (PK)** | La clave candidata elegida para identificar las tuplas |
| **Clave alternativa** | Cualquier clave candidata no elegida como primaria |
| **Clave externa / ajena (FK)** | Atributo(s) de R2 que referencian una clave candidata de R1 |

### Clave externa (Foreign Key)

Una **clave externa** de R2 respecto de R1 es un conjunto de atributos de R2 cuyos valores deben ser:
- **Nulos** (NULL), o
- **Coincidir** con el valor de alguna clave candidata de R1

> El dominio de la clave externa **debe coincidir** con el dominio de la clave candidata referenciada.  
> Esto permite referenciar de forma unívoca una tupla de R1 desde R2.

```
R1   (tabla referenciada)          R2 (tabla que referencia)
  ┌──────────────────────┐         ┌──────────────────────────────┐
  │ PK_R1 │ Atrib...     │ ◄────── │ Atrib... │ FK→R1  │ Atrib... │
  └──────────────────────┘         └──────────────────────────────┘
```

---

## Restricciones del modelo relacional

La [[Sesión 4 - Modelos de Datos#Componente Estática|componente estática]] del modelo relacional incluye dos tipos de restricciones:

### Restricciones inherentes

Se derivan de la **definición matemática de relación**:

| Restricción | Descripción |
|---|---|
| **Sin tuplas duplicadas** | Implica la obligatoriedad de una clave primaria |
| **Orden de tuplas irrelevante** | Las filas no tienen posición significativa |
| **Orden de atributos irrelevante** | Las columnas no tienen posición significativa |
| **Integridad de entidad** | Ningún atributo de la PK puede ser NULL |
| **Atomicidad (1FN)** | Cada atributo solo puede tomar un valor de su dominio — no se permiten grupos repetitivos |

### Grupos repetitivos (violaciones de 1FN)

La **Primera Forma Normal (1FN)** exige que cada atributo sea atómico. Hay tres formas de violarla con el campo `Teléfono` como ejemplo:

**❌ Violación 1 — Múltiples valores en una celda:**

| ID Cliente | Nombre | Apellido | Teléfono |
|---|---|---|---|
| 123 | Rachel | Ingram | 555-861-2025 |
| 456 | James | Wright | 555-403-1659 / **555-776-4100** |
| 789 | Cesar | Dure | 555-808-9633 |

→ Un campo contiene más de un valor del dominio. Viola la atomicidad.

**❌ Violación 2 — Múltiples columnas del mismo dominio:**

| ID Cliente | Nombre | Apellido | Teléfono 1   | Teléfono 2   | Teléfono 3 |
| ---------- | ------ | -------- | ------------ | ------------ | ---------- |
| 123        | Rachel | Ingram   | 555-861-2025 |              |            |
| 456        | James  | Wright   | 555-403-1659 | 555-776-4100 |            |
|            |        |          |              |              |            |

→ Se generan valores NULL en la PK (violación de integridad de entidad) y columnas vacías innecesarias.

**❌ Violación 3 — Concatenación en un solo campo expandido:**

| ID Cliente | Nombre | Apellido | Teléfono |
|---|---|---|---|
| 456 | James | Wright | 555-403-1659, 555-776-4100 |

→ Error semántico: ¿el dominio es un teléfono o una lista? Imposible hacer consultas del tipo "clientes con el mismo teléfono".

**✅ Solución correcta:** Crear una tabla separada `Teléfonos(ID_Cliente FK, Teléfono)` con una tupla por número.

---

## Conexiones

- [[Sesión 4 - Modelos de Datos]] — Tipos de modelos, componente estática/dinámica, esquema lógico
- [[Sesión 3 - Modelos de Datos]] — Modelo E/R conceptual (punto de partida del modelo relacional)
- [[Sesión 1 - Sistemas de Información]] — Niveles de abstracción (el modelo relacional es el nivel lógico)
- [[Conceptos Clave#Dominio|Conceptos Clave → Dominio]]
- [[Conceptos Clave#SGBD|Conceptos Clave → SGBD]]
- [[Sesión 0 - Indice]]

---

## Nuevos conceptos clave (añadir a [[Conceptos Clave]])

| Término | Definición |
|---|---|
| **Modelo relacional** | Modelo lógico propuesto por E. F. Codd (1969) que estructura la información en tablas (relaciones) basándose en la Teoría de Conjuntos |
| **Relación / Tabla** | Estructura formada por un nombre, atributos y tuplas; unidad básica del modelo relacional |
| **Tupla** | Fila de una tabla; conjunto de valores para cada atributo de la relación |
| **Atributo** | Columna de una tabla; propiedad de todos los elementos de la relación |
| **Grado** | Número de atributos (columnas) de una relación |
| **Cardinalidad** | Número de tuplas (filas) de una relación en un momento dado |
| **Intensión / Esquema** | Parte estática de una relación: su definición (nombre + cabecera) |
| **Extensión / Ocurrencia** | Parte dinámica: conjunto de tuplas en un instante determinado |
| **Relación básica** | Tabla independiente que corresponde a una entidad o asociación conceptual |
| **Relación derivada** | Tabla obtenida por operaciones sobre otras relaciones; puede ser vista o instantánea |
| **Vista** | Relación derivada virtual definida como una consulta con nombre; no almacena datos propios |
| **Clave candidata** | Conjunto mínimo de atributos que identifica unívocamente cada tupla |
| **Clave primaria (PK)** | Clave candidata elegida para identificar las tuplas; no puede ser NULL |
| **Clave alternativa** | Clave candidata no elegida como primaria |
| **Clave externa / ajena (FK)** | Atributo(s) de una tabla que referencian la clave candidata de otra tabla |
| **Integridad de entidad** | Restricción: ningún atributo de la PK puede ser NULL |
| **Primera Forma Normal (1FN)** | Restricción: cada atributo debe ser atómico (un solo valor de su dominio por celda) |
| **Grupo repetitivo** | Violación de 1FN: múltiples valores en un mismo atributo o grupo de columnas del mismo dominio |

---

#bases-de-datos #modelo-relacional #relaciones #tablas #tuplas #clave-primaria #clave-externa #1FN #integridad-referencial #codd #nebrija #sesion-5
