
> **Curso:** Bases de Datos — Grado en Ingeniería Informática  
> **Profesor:** Jaime Álvarez Benayas — Universidad Nebrija  
> **Sesión:** 4 · Modelos de datos y entorno de prácticas (MySQL Workbench)

---

## 📚 Contenidos

1. [[#Tipos de modelos de datos]]
2. [[#Componentes del modelo de datos]]
   - [[#Componente Estática]]
   - [[#Componente Dinámica]]
3. [[#Resumen del flujo de diseño]]
4. [[#Entorno de prácticas — MySQL Workbench]]
   - [[#Conexión a un servidor de bases de datos]]
   - [[#Creación de un modelo lógico (EER Diagram)]]

---

## Tipos de modelos de datos

El proceso de diseño de una base de datos implica crear **distintos modelos de datos** que representen los objetos de información en cada [[Sesión 3 - Modelos de Datos#Niveles de abstracción|nivel de abstracción]], aumentando el nivel de detalle progresivamente.

| Nivel | Modelo resultante | Características | Ejemplo |
|---|---|---|---|
| Externo / Usuario | Requisitos de información | Visión particular de cada usuario | Formularios, informes |
| Conceptual | Modelo Conceptual | Independiente del SGBD | Modelo E/R ([[Sesión 3 - Modelos de Datos#Modelo Entidad-Relación|Draw.io]]) |
| Lógico | Modelo Lógico | Soportado por el SGBD | Modelo Relacional, Codasyl |
| Físico | Modelo Físico | Almacenamiento real | Ficheros, índices |

### Descripción de cada modelo

- **Modelo externo:** Visión que tiene de la información cada usuario particular. Refleja todos los datos y relaciones de interés para ese tipo de usuario.

- **Modelo / esquema conceptual:** Describe los elementos de interés para la organización, sus propiedades y relaciones. Integra todos los modelos externos y captura la semántica del [[Conceptos Clave#Universo del discurso|universo del discurso]].

- **Modelo / esquema lógico:** Traducción del modelo conceptual a estructuras lógicas concretas:
  - **Tablas y columnas** → Modelo Relacional
  - **Clases y objetos** → Programación Orientada a Objetos
  - **Etiquetas** → XML  
  Requiere el soporte de un [[Conceptos Clave#SGBD|SGBD]].

- **Modelo / esquema físico:** Gestiona el almacenamiento, distribución, organización, seguridad y acceso a los datos. La mayoría de las decisiones las toma el propio gestor de la BD.

---

## Componentes del modelo de datos

Todo modelo de datos presenta dos grandes componentes:

```
Modelo de datos
├── Componente Estática  → Lo que NO cambia (estructura)
└── Componente Dinámica  → Lo que SÍ cambia (valores y operaciones)
```

### Componente Estática

Corresponde a las propiedades **invariables** del universo del discurso. Se plasma en los **tipos de entidades** y su estructura organizativa.

Incluye:
- **Objetos de datos** consignados en el sistema (entidades, relaciones…)
- **Asociaciones** entre los objetos anteriores
- **Propiedades** de los objetos y asociaciones
- **Dominios** de los que las propiedades tomarán valor

La componente estática también refleja **situaciones que NO pueden darse** en el universo modelado.

#### Restricciones del modelo

Cada modelo formal impone sus propias condiciones, dando lugar a las **restricciones del modelo** que invalidan determinadas ocurrencias de la BD:

| Tipo de restricción | Descripción |
|---|---|
| **Inherentes** | Impuestas por la naturaleza propia del modelo |
| **De integridad / semánticas** | Se derivan del universo del discurso; representan la semántica lo más fielmente posible |

> 💡 Las restricciones de integridad son los elementos que el modelo formal ofrece para capturar la realidad del dominio modelado.

### Componente Dinámica

Corresponde a las propiedades **cambiantes** del modelo (datos concretos o valores).

#### Ocurrencia / Estado de la BD

Los valores que toman los elementos de la componente estática **en un momento determinado tᵢ** se denominan **ocurrencia** o **estado de la base de datos en tᵢ**.

```
Estado t₀ ──[operación de actualización]──> Estado t₁
Estado t₁ ──[operación de selección]──────> Estado t₁  (sin cambio)
```

#### Operaciones

Las operaciones se definen sobre los valores de la componente estática. Toda operación tiene **2 componentes**:

| Componente | Descripción |
|---|---|
| **Localización** | Selección del conjunto de elementos sobre los que actuar |
| **Acción** | Lo que se realiza sobre las ocurrencias seleccionadas |

**Efectos de las operaciones:**

- **Operaciones de actualización** (INSERT, UPDATE, DELETE) + alteraciones estructurales → **nuevo estado** de la BD
- **Operaciones de selección** (SELECT) → el estado de la BD **no cambia**

**Ejemplos:**

```sql
-- Localización + Acción de selección (no cambia estado)
SELECT * FROM Empleados;

-- Localización + Acción de actualización (genera nuevo estado)
UPDATE Empleados SET salario = salario * 1.07;
```

---

## Resumen del flujo de diseño

```
1. ANÁLISIS CONCEPTUAL
   └─> Esquema Conceptual (máximo contenido semántico, independiente del SGBD)
       Herramienta: Draw.io → Diagrama E/R
           ↓
2. DISEÑO LÓGICO
   └─> Esquema Lógico (usando estructuras del SGBD: tablas, columnas, claves)
       Herramienta: MySQL Workbench → EER Diagram
           ↓
3. DISEÑO FÍSICO
   └─> Esquema Físico (el SGBD gestiona el almacenamiento)
       El diseñador puede tomar algunas decisiones; la mayoría las toma el SGBD
```

> ⚠️ El diseñador tiene **mucho control** en el nivel conceptual y lógico, pero **poco control** en el nivel físico (lo gestiona el SGBD automáticamente).

---

## Entorno de prácticas — MySQL Workbench

[[Sesión 2 - Creación de Usuarios y Bases de Datos#MySQL Workbench|MySQL Workbench]] es la herramienta principal del entorno de prácticas. Permite tres tipos de actividades:

| Actividad | Descripción |
|---|---|
| **Diseño** | Crear diagramas lógicos (EER) y trasladarlos a la BD |
| **Desarrollo** | Crear y ejecutar consultas SQL, optimización |
| **Administración** | Controlar y manipular aspectos estructurales de la BD |

> 📖 Para la instalación, consultar el manual: *"Instalar y conectar MySQL Workbench con servidor MySQL en Windows.pdf"*

### Conexión a un servidor de bases de datos

**Pasos para conectarse:**

1. Abrir MySQL Workbench → aparece la pantalla de inicio (*home*)
2. Hacer clic en la conexión **MySQL Windows XAMPP**
3. Se abre una nueva pestaña con el entorno de trabajo

**Pantalla principal tras la conexión:**

- Panel izquierdo → **Navigator** con dos pestañas:
  - **Administration** → gestión del servidor (estado, usuarios, exportación…)
  - **Schemas** → lista de bases de datos disponibles
- Panel central → **Query Editor** para escribir y ejecutar SQL
- Panel derecho → **SQL Additions** (ayuda contextual y snippets)

**Establecer esquema por defecto:**

```
Click derecho sobre la BD → "Set as Default Schema"
→ Aparece en negrita en el panel Schemas
→ Se muestra en la barra inferior: Schema: <nombre>
```

Las bases de datos creadas en [[Sesión 2 - Creación de Usuarios y Bases de Datos|la Sesión 2]] (cdcol, phpmyadmin, prueba2, test, webauth) aparecen listadas en la pestaña Schemas.

### Creación de un modelo lógico (EER Diagram)

**Crear un nuevo modelo:**

1. Desde la pantalla de inicio → clic en **`+`** junto a **Models**
2. Se abre la ventana **MySQL Model** con:
   - **Add Diagram** → crea un EER Diagram (diagramador visual)
   - **Physical Schemas** → esquema físico `mydb` (BD destino)
   - **Modeling Additions** → plantillas predefinidas (timestamps, user, category…)

**Dentro del EER Diagram** se pueden:
- Añadir tablas visualmente
- Especificar relaciones entre ellas (1:1, 1:n, n:m)
- Una vez terminado el diseño, **implementarlo directamente** en el servidor de BD

**Elementos del panel de herramientas del EER Diagram:**

```
Cursor / Selección
Relación 1:1 identificante
Relación 1:n identificante
Relación 1:1 no identificante
Relación 1:n no identificante
Relación n:m
Nueva tabla
Nueva vista
Nota / comentario
```

---

## 🔗 Conexiones

- [[Sesión 3 - Modelos de Datos]] — Modelado conceptual, E/R, Draw.io (base conceptual de esta sesión)
- [[Sesión 2 - Creación de Usuarios y Bases de Datos]] — Instalación de XAMPP y MySQL; las BDs creadas allí aparecen en Workbench
- [[Sesión 1 - Sistemas de Información]] — Niveles de abstracción (externo, conceptual, lógico, físico)
- [[Conceptos Clave#SGBD|Conceptos Clave → SGBD]]
- [[Conceptos Clave#Universo del discurso|Conceptos Clave → Universo del discurso]]
- [[Sesión 0 - Indice]]

---

## 📝 Nuevos conceptos clave (añadir a [[Conceptos Clave]])

| Término | Definición |
|---|---|
| **Componente estática** | Parte invariable del modelo de datos; define la estructura (entidades, relaciones, dominios, restricciones) |
| **Componente dinámica** | Parte variable del modelo; incluye los valores actuales y las operaciones posibles |
| **Ocurrencia / Estado** | Conjunto de valores que toma la BD en un instante determinado tᵢ |
| **Restricción inherente** | Limitación impuesta por la naturaleza del propio modelo formal |
| **Restricción de integridad** | Limitación derivada de la semántica del universo del discurso modelado |
| **Esquema lógico** | Traducción del modelo conceptual a estructuras del SGBD (tablas, columnas, claves) |
| **EER Diagram** | Diagrama Entidad-Relación Extendido; herramienta visual de MySQL Workbench para diseño lógico |
| **Default Schema** | Base de datos activa sobre la que se ejecutan las consultas en MySQL Workbench |

---

#bases-de-datos #modelos-de-datos #mysql-workbench #diseño-bd #esquema-conceptual #esquema-logico #esquema-fisico #componente-estatica #componente-dinamica #nebrija #sesion-4
