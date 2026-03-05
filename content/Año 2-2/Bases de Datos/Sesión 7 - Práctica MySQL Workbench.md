
> **Asignatura:** Bases de Datos · Grado en Ingeniería Informática
> **Profesor:** Jaime Álvarez Benayas · Universidad Nebrija
> **Tema:** Relaciones 1:N en MySQL Workbench — identificativas vs. no identificativas, cardinalidades y sincronización con la BD

---

##  Índice

1. [[#Relaciones 1:N en MySQL Workbench]]
2. [[#Relación no identificativa vs. identificativa]]
3. [[#Cardinalidad y obligatoriedad]]
4. [[#Conexión con los apuntes teóricos]]
5. [[#Sincronización con la base de datos]]
6. [[#Error VISIBLE / INVISIBLE]]
7. [[#Flujo de trabajo completo]]

---

## Relaciones 1:N en MySQL Workbench

En MySQL Workbench se crean relaciones 1:N entre tablas usando la barra de herramientas del **EER Diagram**. En el ejemplo de la práctica se relacionan las entidades `grupo` y `alumno`.

> Ver teoría: [[Sesión 6 - El Modelo Relacional (II)#Transformación de asociaciones 1:N]]

### Tablas del ejemplo

```sql
-- Tabla principal (lado 1)
CREATE TABLE grupo (
    idGrupo INT NOT NULL,
    grupoPracticas TINYINT NOT NULL,
    PRIMARY KEY (idGrupo)
);

-- Tabla secundaria (lado N)
CREATE TABLE alumno (
    idAlumno INT NOT NULL,
    DNI VARCHAR(10) NOT NULL,
    nombre VARCHAR(45) NOT NULL,
    dirección VARCHAR(45) NOT NULL,
    telefono VARCHAR(9) NOT NULL,
    email VARCHAR(20) NOT NULL,
    grupo_idGrupo INT NOT NULL,   -- FK (añadida por la relación)
    PRIMARY KEY (idAlumno)
);
```

---

## Relación no identificativa vs. identificativa

### Relación no identificativa (dashed line ‑ ‑ ‑)

La **PK de la entidad principal** se incluye en la entidad secundaria **pero NO como parte de la PK** de esa entidad secundaria.

```
alumno                          grupo
──────────────────────          ──────────────────────
idAlumno INT (PK)               idGrupo INT (PK)
DNI VARCHAR(10)      ←──────    grupoPracticas TINYINT
nombre VARCHAR(45)
dirección VARCHAR(45)
telefono VARCHAR(9)
email VARCHAR(20)
grupo_idGrupo INT (FK)   ← clave primaria de grupo, pero NO es PK de alumno
```

> En Workbench la línea es **discontinua** para relaciones no identificativas.

### Relación identificativa (solid line ───)

La **PK de la entidad principal** se incluye en la entidad secundaria **Y además forma parte de su PK**.

```
alumno                          grupo
──────────────────────          ──────────────────────
idAlumno INT (PK)               idGrupo INT (PK)
grupo_idGrupo INT (PK+FK) ←──  grupoPracticas TINYINT
DNI VARCHAR(10)
...
```

> En Workbench la línea es **continua** para relaciones identificativas.

| | No identificativa | Identificativa |
|---|---|---|
| FK en PK de la secundaria | ❌ No | ✅ Sí |
| Línea en Workbench | Discontinua (‑ ‑ ‑) | Continua (───) |
| Uso típico | La entidad secundaria existe independientemente | La entidad secundaria depende de la principal para identificarse |

---

## Cardinalidad y obligatoriedad

Al hacer doble clic sobre la línea de relación en Workbench se abre la ventana **Relationship**, con la pestaña `Relationship`:

```
┌─────────────────────────────────────────────────────────┐
│  Referencing Table        Cardinality      Referenced   │
│  alumno                  ○ One-to-One(1:1) Table        │
│  FK: fk_alumno_grupo     ● One-to-Many(1:n) grupo       │
│  grupo_idGrupo: INT                        idGrupo (PK) │
│                          [Invert Rel.]                  │
│  ☑ Mandatory             □ Identifying    ☑ Mandatory   │
│  [Edit Table...]         Relationship     [Edit Table…] │
└─────────────────────────────────────────────────────────┘
```

### Cardinalidad mínima (Mandatory)

| Casilla `Mandatory` | Significado | Equivalente en SQL |
|---|---|---|
| ✅ Activada | Cardinalidad mínima = 1 (obligatorio) | `NOT NULL` en la FK |
| ❌ Desactivada | Cardinalidad mínima = 0 (opcional) | `NULL` permitido en la FK |

**Símbolos en el diagrama:**
- **Rayita vertical** `|` → obligatoriedad (cardinalidad mínima 1)
- **Círculo vacío** `○` → opcionalidad (cardinalidad mínima 0)

### Relación identificativa

- Activar la casilla `Identifying Relationship` convierte la línea de discontinua a continua.
- La FK pasa a formar parte de la PK de la tabla referenciante.

> Ver teoría en: [[Sesión 6 - El Modelo Relacional (II)#Transformación de asociaciones 1:N]]

---

## Conexión con los apuntes teóricos

La relación 1:N en Workbench implementa directamente la **propagación de clave primaria del lado 1 al lado N**:

```
LIBRO(ISBN, Título, Autor, IdEditorial)
              ↓ BD/MC
EDITORIAL(IdEditorial, Nombre, Director)
```

Se coloca `IdGrupo` en `alumno` (y no `idAlumno` en `grupo`) porque:
- 1 grupo puede tener **varios alumnos** → si pusiéramos `idAlumno` en `grupo`, `idGrupo` podría repetirse → viola la PK de `grupo`.

> Principio exactamente igual que en el ejemplo LIBRO–EDITORIAL de [[Sesión 6 - El Modelo Relacional (II)#Opción A — Propagación de clave primaria (más habitual)]]

---

## Sincronización con la base de datos

Para llevar el modelo de Workbench a la base de datos real (en XAMPP/phpMyAdmin) se usa **Database → Synchronize Model**:

```
Pasos:
1. Database → Synchronize Model with Database
2. Connection Options  → seleccionar conexión (localhost)
3. Sync Options        → opciones de sincronización
4. Connect to DBMS     → conectar
5. Select Schemas      → elegir schema (e.g., mydb)
6. Retrieve Objects    → recuperar objetos existentes
7. Select Changes      → revisar cambios a aplicar
8. Review DB Changes   → previsualizar SQL generado  ← AQUÍ copiar el SQL
9. Synchronize Progress
```

> ⚠️ Antes de ejecutar, revisar el SQL en el paso **Review DB Changes** para detectar palabras problemáticas.

---

## Error VISIBLE / INVISIBLE

### Descripción del error

Al sincronizar con versiones de MySQL más antiguas (como la incluida en XAMPP), el SQL generado por Workbench puede contener la palabra clave `VISIBLE` (o `INVISIBLE`) en las definiciones de índices, lo cual no es compatible:

```sql
-- SQL generado por Workbench (con error)
UNIQUE INDEX `DNI_UNIQUE` (`DNI` ASC) VISIBLE,
INDEX `fk_alumno_grupo_idx` (`grupo_idGrupo` ASC) VISIBLE,
```

Esto provoca el mensaje de error al ejecutar:

```
SQL script execution finished: statements: 4 succeeded, 1 failed
```

### Solución

1. En el paso **Review DB Changes**, hacer clic en **Copy to Clipboard** (o **Save to File**)
2. Abrir **phpMyAdmin** → pestaña **SQL**
3. Pegar el script y **eliminar manualmente** todas las ocurrencias de `VISIBLE` e `INVISIBLE`
4. Ejecutar el script corregido

```sql
-- SQL corregido (sin VISIBLE)
UNIQUE INDEX `DNI_UNIQUE` (`DNI` ASC),
INDEX `fk_alumno_grupo_idx` (`grupo_idGrupo` ASC),
```

> Usa buscar y reemplazar (`Ctrl+H` en la mayoría de editores) para eliminar ` VISIBLE` y ` INVISIBLE` de forma rápida.

---

## Flujo de trabajo completo

```
┌─────────────────────────────────────────────────────────────┐
│  1. DISEÑO CONCEPTUAL (Draw.io)                             │
│     Diagrama E/R con entidades, atributos y relaciones      │
└───────────────────────┬─────────────────────────────────────┘
                        │
                        ▼
┌─────────────────────────────────────────────────────────────┐
│  2. DISEÑO LÓGICO (MySQL Workbench — EER Diagram)           │
│     - Crear tablas con columnas y tipos de datos            │
│     - Añadir relaciones 1:N / 1:1 / M:N                    │
│     - Configurar identificativa / no identificativa        │
│     - Ajustar Mandatory para cardinalidad mínima           │
└───────────────────────┬─────────────────────────────────────┘
                        │
                        ▼
┌─────────────────────────────────────────────────────────────┐
│  3. SINCRONIZACIÓN (Workbench → XAMPP/phpMyAdmin)           │
│     - Database → Synchronize Model                          │
│     - Copiar SQL generado                                   │
│     - Eliminar VISIBLE / INVISIBLE                          │
│     - Ejecutar en phpMyAdmin                               │
└─────────────────────────────────────────────────────────────┘
```

---

## 🔗 Conexiones

- [[Sesión 6 - El Modelo Relacional (II)]] — Teoría de relaciones 1:N, identificativas/no identificativas, cardinalidades
- [[Sesión 4 - Modelos de Datos]] — EER Diagram en Workbench
- [[Sesión 2 - Creación de Usuarios y Bases de Datos]] — phpMyAdmin y ejecución de SQL
- [[Sesión 5 - El Modelo Relacional (I)]] — Fundamentos: PK, FK, restricciones
- [[Conceptos Clave]] — Añadir términos de la tabla siguiente

---

## 📝 Nuevos términos para `Conceptos Clave.md`

| Término | Definición |
|---|---|
| Relación identificativa | Relación en la que la PK de la entidad principal forma parte de la PK de la entidad secundaria (línea continua en Workbench) |
| Relación no identificativa | Relación en la que la PK de la entidad principal se añade a la entidad secundaria pero NO forma parte de su PK (línea discontinua en Workbench) |
| Mandatory (Workbench) | Opción en la relación que controla la cardinalidad mínima: activada = NOT NULL (obligatorio), desactivada = permite NULL (opcional) |
| Synchronize Model | Función de MySQL Workbench que genera y ejecuta el SQL DDL para llevar el modelo lógico a la base de datos física |
| Error VISIBLE/INVISIBLE | Incompatibilidad del SQL generado por Workbench con versiones antiguas de MySQL que no soportan estas palabras clave en definiciones de índices |

---

#bases-de-datos #mysql-workbench #practica #relaciones #identificativa #no-identificativa #cardinalidad #sincronizacion #xampp #phpmyadmin #nebrija
