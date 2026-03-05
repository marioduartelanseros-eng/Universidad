
> **Asignatura:** Bases de Datos | **Prof.:** Jaime Álvarez Benayas  
> **Tipo:** Teoría  
> **Ver también:** [[Sesión 3 - Modelos de Datos]] | [[Sesión 0 - Indice]]

---

## 📌 Introducción

Las **bases de datos** son:
- La principal herramienta para el **almacenamiento masivo de información**
- El soporte fundamental para la **persistencia de datos**
- Parte esencial de cualquier sistema de información moderno (presentes en la mayoría de aplicaciones y portales web)

---

## 1. Sistema de Información

> *"Cualquier herramienta o agrupación de ellas que permita almacenar y administrar los datos de interés para una determinada organización."*

Los datos bajo el control de un SI consisten en un **agregado ordenado de elementos de información relacionados entre sí**.

### Objetivo principal
Servir de soporte a la **operación cotidiana de la organización**. Para ello debe ofrecer mecanismos que permitan:

- ✅ **Registrar y guardar** información
- ✅ **Acceder / leer** información
- ✅ **Modificar / actualizar** información
- ✅ **Eliminar** información
- ✅ **Garantizar la seguridad** → confidencialidad, integridad y disponibilidad

### Elementos almacenados

| Tipo | Descripción |
|------|-------------|
| **Internos** | Modelo de datos propio (estructuras, restricciones de integridad, operaciones de administración) |
| **Externos** | Interacciones con entidades externas (pedidos a proveedores, facturación a clientes, etc.) |

---

## 2. Componentes de un Sistema de Información

Un SI se compone de:

### 🖥️ Hardware
Necesario para la **adquisición, procesado y presentación** de la información.

### 💾 Software
Se subdivide en:
- **Gestión del almacenamiento y acceso** → el programa de base de datos (SGBD)
- **Gestión de las comunicaciones** → para envío/recepción de información
- **Tratamiento de información** → aplicaciones para procesos específicos sobre los datos (lógica de negocio)

### 🗄️ Datos
Conjunto de datos almacenados, organizados según las estructuras lógicas del sistema.

---

## 3. Tipos de Sistemas de Información

### 3.1 Orientados a Proceso ❌ (enfoque antiguo)

> Sistema diseñado como un **conjunto de procesos independientes** usando archivos de datos separados.

**Problemas:**
- **Redundancia** de información → incoherencias e inconsistencias
- **Conflictos de acceso simultáneo** → inconsistencias
- **Desperdicio de espacio** al repetir información
- **Repetición de mecanismos de control** (uno por cada almacén)
- **Dependencia físico-lógica** entre datos y procesos

### 3.2 Orientados a Datos ✅ (enfoque moderno)

> El almacenamiento **no obedece a procesos concretos**, sino a todas las necesidades de información de la organización.

**Ventajas:**
- Repositorio/base de datos **único**
- **Independencia** entre datos y procesos → cambios en datos no afectan necesariamente a las aplicaciones
- **Sin redundancia** → consistencia de la información
- **Sin redundancia** → reducción del espacio de almacenamiento
- **Sin redundancia** → encapsulación de la semántica de los datos
- **Sin redundancia** → eficiencia en la recuperación de datos
- Repositorio único → **mayor disponibilidad** en entornos multiusuario

**Desventajas:**
- Instalación **costosa**
- Requiere **personal especializado**
- **Escasa estandarización**

---

## 4. Concepto de Base de Datos

> *"Colección o repositorio de datos con redundancia controlada y con una estructura que refleja las interrelaciones del mundo real."*

Características esenciales:
- **Independencia (desacoplamiento)** respecto a las aplicaciones que usen los datos
- **Posibilidad de compartición y acceso concurrente controlado**
- **Semántica autocontenida** → no solo se guardan datos, también su significado
- La definición y descripción de los datos es **única** y se almacena junto a ellos

---

## 5. Niveles de Abstracción

Al diseñar una BD se establecen **tres niveles de abstracción**:

```
┌─────────────────────────────────┐
│   NIVEL EXTERNO (de usuario)    │  ← Visión individual de cada usuario
├─────────────────────────────────┤
│      NIVEL CONCEPTUAL           │  ← Todos los datos de la organización
├─────────────────────────────────┤
│       NIVEL INTERNO             │  ← Representación física y lógica
└─────────────────────────────────┘
```

### 5.1 Nivel Externo o de Usuario
- Define las estructuras del **esquema externo**
- Corresponde a la **visión individual de cada usuario**
- Existirán **tantos esquemas externos como usuarios y aplicaciones**
- Dos o más usuarios pueden compartir el mismo esquema externo

### 5.2 Nivel Conceptual
- Incluye la descripción de **todos los datos** de la organización + relaciones + restricciones de seguridad
- Objetivo: obtener una representación **independiente de usuarios, aplicaciones y sistema informático**
- Ejemplo:

```
Tabla Pedidos:          Tabla Proveedores:       Tabla Productos:
- Id proveedor          - Id proveedor            - Id producto
- Id producto           - Nombre                  - Descripción
- Nº de productos       - Dirección               - Precio
- Fecha                 - Cuenta / NIF
```

### 5.3 Nivel Interno
- Describe cómo se **representan los datos lógicamente** y su organización para el **almacenamiento físico**
- Varía considerablemente según el **paquete informático** empleado
- Corresponde a la visión desde el punto de vista de los **programas de gestión**

---

## 6. SGBD — Sistema de Gestión de Base de Datos

> *"Conjunto de programas, procedimientos y lenguajes que proporcionan a los diferentes tipos de usuarios las herramientas necesarias para describir y operar los datos almacenados, garantizando su coherencia, consistencia y seguridad."*

Ver nota completa: [[Conceptos Clave#SGBD]]

### Definición/Descripción de elementos — LDD
El SGBD define:
- Las **entidades** de datos
- La **estructura** de las entidades
- Las **relaciones** entre entidades
- Las **reglas de integridad** referencial

### Manipulación de datos — LMD
Operaciones a **nivel de base de datos:**
- Creación de bases de datos
- Definición del esquema
- Consultas sobre el esquema

Operaciones a **nivel de objetos:**
- Recuperación (consulta selectiva)
- Inserción
- Borrado
- Modificación

### Lenguajes del SGBD

| Lenguaje | Función |
|----------|---------|
| **LDD** | Definición de estructuras a todos los niveles |
| **LMD** | Recuperación y actualización de datos |
| **Admin scripts** | Copias de seguridad, carga/descarga de datos |
| **SQL** | Lenguaje autocontenido, usado de forma interactiva |
| **L. anfitrión** | (ProC, Java...) con comandos SQL embebidos |
| **L. 4ª generación** | Sentencias SQL avanzadas |

---

## 🔗 Conexiones

- [[Sesión 3 - Modelos de Datos]] — El nivel conceptual da lugar al modelado de datos
- [[Sesión 2 - Creación de Usuarios y Bases de Datos]] — Implementación práctica con XAMPP
- [[Conceptos Clave]] — Resumen de todos los términos importantes

---

*Tags: #teoría #sistemas-de-información #SGBD #niveles-abstracción #bases-de-datos*
