# Conceptos Clave — Bases de Datos

> Nota central de definiciones y términos importantes.  
> **Ver índice:** [[Sesión 0 - Indice]]

---

## Sistema de Información

> *"Cualquier herramienta o agrupación de ellas que permita almacenar y administrar los datos de interés para una determinada organización."*

- Almacena elementos **internos** (modelo de datos propio) y **externos** (interacciones con entidades externas)
- Debe garantizar: registro, acceso, modificación, eliminación y **seguridad** de la información
- Ver desarrollo completo: [[Sesión 1 - Sistemas de Información#1. Sistema de Información]]

---

## SGBD

**Sistema de Gestión de Base de Datos** (DBMS: *Data Base Management System*)

> *"Conjunto de programas, procedimientos y lenguajes que proporcionan a los diferentes tipos de usuarios las herramientas necesarias para describir y operar los datos almacenados, garantizando su coherencia, consistencia y seguridad."*

### Lenguajes del SGBD

| Sigla | Nombre completo | Función |
|-------|----------------|---------|
| **LDD** | Lenguaje de Definición de Datos | Define estructuras, entidades, relaciones, reglas de integridad |
| **LMD** | Lenguaje de Manipulación de Datos | Recuperación, inserción, borrado, modificación de datos |
| **SQL** | Structured Query Language | Lenguaje autocontenido, interactivo |

Ver contexto: [[Sesión 1 - Sistemas de Información#6. SGBD]]

---

## Niveles de Abstracción

Los tres niveles al diseñar una BD:

### Nivel Externo (de Usuario)
- Visión **individual** de cada usuario o aplicación
- Pueden existir tantos esquemas externos como usuarios
- Ver: [[Sesión 1 - Sistemas de Información#5.1 Nivel Externo o de Usuario]]

### Nivel Conceptual
- Descripción de **todos los datos** de la organización + relaciones + restricciones
- **Independiente** del sistema informático utilizado
- Ver: [[Sesión 1 - Sistemas de Información#5.2 Nivel Conceptual]]

### Nivel Interno
- Representa los datos desde el punto de vista **lógico y físico**
- Depende del SGBD utilizado
- Ver: [[Sesión 1 - Sistemas de Información#5.3 Nivel Interno]]

---

## Modelos de Datos

> *Herramienta de diseño y representación que ayuda a interpretar un determinado universo del discurso.*

Características de un buen modelo: completo, no redundante, estable, flexible, comunicativo, reusable, eficiente.

Ver desarrollo completo: [[Sesión 3 - Modelos de Datos]]

---

## Universo del Discurso

> Parcela del mundo real que se pretende modelar.

Es el punto de partida del diseño de cualquier base de datos.  
Ver: [[Sesión 3 - Modelos de Datos#3. Conceptos Clave del Modelado]]

---

## Abstracción

> Acción de reducir el nivel de detalle de los elementos a modelar para conseguir una representación lo más general posible.

Se realiza con ayuda del **Modelo de Datos Formal**.  
Ver: [[Sesión 3 - Modelos de Datos#3. Conceptos Clave del Modelado]]

---

## Base de Datos

> *"Colección o repositorio de datos con redundancia controlada y con una estructura que refleja las interrelaciones del mundo real."*

Características esenciales:
- **Independencia** respecto a las aplicaciones
- **Compartición y acceso concurrente controlado**
- **Semántica autocontenida** (guarda los datos y su significado)

Ver: [[Sesión 1 - Sistemas de Información#4. Concepto de Base de Datos]]

---

## Collation

> Indica un conjunto de caracteres, su codificación y unas reglas de comparación.

- **UTF-8:** codificación de longitud variable para Unicode, incluye la mayoría de caracteres del mundo
- En MySQL se usa habitualmente: `utf8_general_ci`

Ver contexto práctico: [[Sesión 2 - Creación de Usuarios y Bases de Datos#Paso 1 Crear una Base de Datos]]

---

## Redundancia de Datos

La **ausencia de redundancia** en los sistemas orientados a datos proporciona:
- Consistencia de la información
- Reducción del espacio de almacenamiento
- Encapsulación de la semántica de los datos
- Eficiencia en la recuperación

Ver: [[Sesión 1 - Sistemas de Información#3.2 Orientados a Datos]]

---

## Seguridad en BD

Tres pilares de la seguridad de la información:

| Pilar | Descripción |
|-------|-------------|
| **Confidencialidad** | Solo acceden quienes tienen permiso |
| **Integridad** | Imposibilidad de alteración no autorizada |
| **Disponibilidad** | Acceso cuando se necesita |

---

## SQL — Comandos Esenciales

```sql
-- Gestión de Bases de Datos
CREATE DATABASE nombre CHARACTER SET utf8 COLLATE utf8_general_ci;

-- Gestión de Usuarios
CREATE USER 'usuario'@'localhost' IDENTIFIED BY 'contraseña';
GRANT ALL PRIVILEGES ON `bd`.* TO 'usuario'@'localhost';
GRANT ALL PRIVILEGES ON `bd`.* TO 'usuario'@'localhost' WITH GRANT OPTION;

-- Operaciones CRUD (LMD)
SELECT * FROM tabla;           -- Read
INSERT INTO tabla VALUES (...); -- Create
UPDATE tabla SET col=val;       -- Update
DELETE FROM tabla WHERE ...;    -- Delete
```

Ver práctica completa: [[Sesión 2 - Creación de Usuarios y Bases de Datos]]

---

*Tags: #conceptos-clave #definiciones #glosario #bases-de-datos*
