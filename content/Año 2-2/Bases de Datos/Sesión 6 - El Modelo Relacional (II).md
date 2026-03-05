
> **Asignatura:** Bases de Datos · Grado en Ingeniería Informática
> **Profesor:** Jaime Álvarez Benayas · Universidad Nebrija
> **Tema:** Restricciones semánticas, integridad referencial y transformación E/R → Relacional

---

## 📋 Índice

1. [[#Restricciones semánticas del modelo relacional]]
2. [[#Integridad referencial]]
3. [[#El grafo relacional]]
4. [[#Reglas básicas de transformación E/R → Relacional]]
5. [[#Transformación de asociaciones M:N]]
6. [[#Transformación de asociaciones 1:N]]
7. [[#Transformación de asociaciones 1:1]]
8. [[#Transformación de asociaciones reflexivas]]
9. [[#Transformación de asociaciones ternarias]]
10. [[#Transformación de jerarquías]]
11. [[#Pérdidas semánticas]]

---

## Restricciones semánticas del modelo relacional

Las **restricciones semánticas** permiten expresar normas del Universo del Discurso para modelarlo con mayor fidelidad. Las principales son:

| Restricción | Cláusula SQL | Descripción |
|---|---|---|
| Clave primaria | `PRIMARY KEY` | Uno o varios atributos; sin duplicados y sin NULLs |
| Unicidad | `UNIQUE` | Sin valores duplicados; permite NULLs; define claves alternativas |
| Obligatoriedad | `NOT NULL` | El atributo no admite valores nulos |
| Integridad referencial | `FOREIGN KEY` | El valor debe coincidir con una tupla existente en la relación referenciada, o ser NULL |

> 💡 Ver también: [[Sesión 5 - El Modelo Relacional (I)#Tipos de claves]]

---

## Integridad referencial

### Concepto

Si en una relación **R2** existe un atributo (o conjunto) que constituye una **clave candidata** en otra relación **R1**, su valor debe:
- Coincidir con alguna tupla de R1 para ese atributo, **o bien**
- Ser `NULL`

```
R1 (relación referenciada) ←── FK ── R2 (relación que referencia)
```

### Ejemplo de violación

| Cliente | | | Teléfono del cliente | |
|---|---|---|---|---|
| **ID Cliente** | Nombre | Apellido | **ID Cliente** | Teléfono |
| 123 | Rachel | Ingram | 123 | 555-861-2025 |
| 789 | Cesar | Dure | **456** | 555-403-1659 ❌ |
| | | | 456 | 555-776-4100 ❌ |
| | | | 789 | 555-808-9633 |

El valor `456` en *Teléfono del cliente* no existe en *Cliente* → **violación de integridad referencial**.

### Reglas de integridad referencial

Cuando se intenta **eliminar o modificar** una tupla de R1 cuya clave candidata está referenciada desde R2:

| Operación | Comportamiento |
|---|---|
| `NO ACTION` (Restringida) | Solo permite borrar/modificar en R1 si **no existen** tuplas relacionadas en R2 |
| `CASCADE` (Cascada) | El borrado/modificación en R1 **propaga** automáticamente el cambio a R2 |
| `SET NULL` | Los atributos FK en R2 se ponen a `NULL` (si el atributo lo permite) |
| `SET DEFAULT` | Los atributos FK en R2 adoptan su valor por defecto |

### Restricción de rechazo

Basada en condiciones adicionales sobre atributos o tuplas:

- **`CHECK`**: Se evalúa en cada operación sobre ese elemento. Ejemplo: `edad > 18`
- **`ASSERTION`**: Similar a CHECK pero puede aplicarse a varios elementos o relaciones. Tiene nombre propio en la BD.
- **Triggers (disparadores)**: Reglas de tipo **Evento–Condición–Acción** que se ejecutan cuando ocurre un evento y se cumple una condición. Son **procedimentales** (código en lenguaje de programación).

---

## El grafo relacional

El **Grafo Relacional** representa gráficamente la estática del Modelo Relacional: relaciones, interrelaciones, tipos de claves y restricciones de integridad referencial.

### Notación

| Elemento | Representación |
|---|---|
| Nombre de relación | **MAYÚSCULAS** |
| Atributos | Entre paréntesis junto al nombre |
| Clave primaria | Subrayado continuo |
| Clave alternativa | Subrayado discontinuo |
| Clave externa (FK) | Flecha dirigida hacia la relación referenciada |
| Atributo NOT NULL | Asterisco `*` |

### Siglas para reglas de integridad referencial

**Borrado:**
- `BR` — Borrado Restringido
- `BC` — Borrado en Cascada
- `BN` — Borrado con SET NULL
- `BD` — Borrado con SET DEFAULT

**Modificación:**
- `MR` — Modificación Restringida
- `MC` — Modificación en Cascada
- `MN` — Modificación con SET NULL
- `MD` — Modificación con SET DEFAULT

---

## Reglas básicas de transformación E/R → Relacional

La obtención del diagrama relacional corresponde al **modelado lógico**: determina las estructuras de datos soportadas por el SGBD.

| Elemento E/R | Transformación al modelo relacional |
|---|---|
| Entidad | → Una relación (tabla) |
| Atributo Identificador Principal (AIP) | → Clave primaria (`PRIMARY KEY`) |
| Atributos Identificadores Alternativos | → `UNIQUE` (subrayado discontinuo) |
| Atributos univaluados | → Se mantienen como atributos |
| Atributos multivaluados | → Nueva relación (PK = PK original + propio atributo) |
| Atributos obligatorios | → `NOT NULL` (marcados con `*`) |
| Atributos compuestos | → Se descomponen en sus atributos simples |
| Asociación M:N | → Nueva relación intermedia |
| Asociación 1:N | → Propagación de clave o nueva relación |
| Asociación 1:1 | → Nueva relación o propagación de clave |

---

## Transformación de asociaciones M:N

Cada asociación **Muchos a Muchos** genera una **nueva relación** cuya clave primaria es la **concatenación** de las PK de las dos entidades involucradas.

- Cada PK de las entidades actúa también como **clave externa (FK)** en la nueva relación.
- Si la asociación tiene **atributos multivaluados**, estos pasan a formar parte de la PK de la nueva relación.
- Los atributos **univaluados** de la asociación no necesitan integrarse en la PK.

### Ejemplo: SOCIO – Alquila – PELÍCULA

```
SOCIO(IdSocio, Apellidos, Nombre)
                  ↑ BC/MC          ↑ BC/MC
ALQUILER(IdSocio, IdPelicula, FecAlquiler)
                  
PELICULA(IdPelicula, Título, Director)
```

> ⚠️ `FecAlquiler` forma parte de la PK porque un socio puede alquilar la misma película en varias fechas distintas.

---

## Transformación de asociaciones 1:N

Existen **dos posibilidades**:

### Opción A — Propagación de clave primaria (más habitual)

La PK de la entidad del **lado 1** se añade como **FK** en la entidad del **lado N**.

```
LIBRO(ISBN, Título, Autor, IdEditorial*)
              ↓ BD/MC
EDITORIAL(IdEditorial, Nombre, Director)
```

**¿Por qué no al revés?** Porque 1 `IdEditorial` puede tener varios libros → `IdEditorial` se repetiría en EDITORIAL, violando la unicidad de PK.

#### Efecto de la cardinalidad mínima

| Cardinalidad mínima en el lado 1 | Efecto en la FK del lado N |
|---|---|
| `(1,1)` — obligatorio | FK → `NOT NULL` (marcada con `*`) |
| `(0,1)` — opcional | FK → puede ser `NULL` |

> ⚠️ **Pérdida semántica:** Si la cardinalidad mínima del **lado N** es 1 (obligatoriedad), el diagrama relacional no puede expresar que todos los elementos del lado 1 deben estar referenciados desde el lado N. Esto es una **pérdida semántica** inevitable.

### Opción B — Nueva relación

Se crea una nueva relación cuya PK es **solo la PK de la entidad del lado N**.

Se usa cuando:
- La asociación tiene **atributos propios** (e.g., `FecEdición`, `NumEjemplares`)
- La propagación generaría **gran cantidad de NULLs**

```
LIBRO(ISBN, Título, Autor)
              ↑ BD/MC
EDITORIAL(IdEditorial, Nombre, Director)
              ↑ BD/MC
EDICION(ISBN, IdEditorial*, FecEdición, NumEjemplares)
```

> `IdEditorial` es `NOT NULL` en EDICION por la cardinalidad mínima 1 del lado editorial.

---

## Transformación de asociaciones 1:1

### Opción A — Nueva relación intermedia

Se crea una relación con:
- PK = clave primaria de una de las entidades
- Clave alternativa = clave primaria de la otra entidad
- Ambas actúan como FK hacia sus respectivas relaciones

```
GERENTE(IdEmpleado, Nombre, Apellidos)
DIRECCIÓN(IdEmpleado, IdDepartamento)   ← Clave alternativa en IdDepartamento
DEPARTAMENTO(IdDepartamento, Nombre)
```

### Opción B — Propagación de clave (más eficiente)

La PK de una relación se incluye como FK en la otra. La elección depende de la cardinalidad mínima:

- Si ambos lados tienen cardinalidad mínima **1** → indiferente cuál propaga
- Si un lado tiene cardinalidad mínima **0** → la entidad con cardinalidad 0 recibe la FK de la otra

```
GERENTE(IdEmpleado, Nombre, Apellidos, Departamento)
                                            ↓ BD/MC
DEPARTAMENTO(IdDepartamento, Nombre)
```

> `Departamento` actúa como **clave candidata** en GERENTE (por naturaleza 1:1, no puede repetirse).

#### Pérdida semántica en 1:1

Si ambas cardinalidades mínimas son 1 → el grafo relacional **no puede expresar** que todos los elementos de DEPARTAMENTO deben ser referenciados desde GERENTE. Pérdida semántica inevitable.

Si una cardinalidad mínima es 0 → **no hay pérdida semántica**: la relación con cardinalidad 0 puede tener tuplas sin referenciar.

---

## Transformación de asociaciones reflexivas

### Reflexiva 1:1

La PK de la entidad aparece dos veces en la misma relación: una como PK y otra con un nombre diferente para indicar la ocurrencia con la que se asocia.

```
ALUMNO(IdAlumno, Nombre, Apellidos, Compañero)
    ↑ BC/MC ────────────────────────────────┘
```

- `Compañero` es FK hacia `IdAlumno` en la misma tabla
- Si la participación es `(1,1)`, `Compañero` es **clave alternativa**

### Reflexiva M:N

Se crea una nueva relación igual que en las asociaciones binarias M:N:

```
ALUMNO(IdAlumno, Nombre, Apellidos)
    ↑ BC/MC   ↑ BC/MC
COMPAÑEROS(IdAlumno, IdCompañero)
```

> La PK de COMPAÑEROS es la **combinación** de ambos atributos porque un alumno puede tener muchos compañeros y un compañero puede serlo de muchos alumnos.

---

## Transformación de asociaciones ternarias

Las asociaciones que involucran 3 o más entidades se transforman en:
- Una relación por cada entidad participante
- Una nueva relación para la asociación, con sus atributos propios

```
MEDICO(IdMedico, Nombre, Apellidos)
PACIENTE(IdPaciente, Nombre, Apellidos)
MEDICAMENTO(IdMedicamento, Nombre)
RECETA(IdMedico, IdPaciente, IdMedicamento)
```

> La PK de RECETA son las **tres claves** porque la relación es M:N:P.

---

## Transformación de jerarquías

### Opción 1 — Una sola relación (todo en una tabla)

Se incluyen todos los atributos del supertipo y de los subtipos, añadiendo un atributo **discriminante** (e.g., `Tipo`).

```
PUBLICACION(IDPublicacion, Título, Tipo, Páginas, Editorial, Periodicidad, Número)
```

✅ Ventaja: Eficiencia (una sola tabla)
❌ Inconveniente: Gran cantidad de **valores NULLs** (especialmente en jerarquías exclusivas)

### Opción 2 — Relación por supertipo + relaciones por subtipo

```
PUBLICACION(IDPublicacion, Título)
LIBRO(IDPublicacion, Páginas, Editorial)        ← IDPublicacion es FK → PUBLICACION
REVISTA(IDPublicacion, Periodicidad, Número)    ← IDPublicacion es FK → PUBLICACION
```

✅ Ventaja: Refleja fielmente la **semántica** de la jerarquía
❌ Inconveniente: Necesitas hacer JOINs para obtener datos completos

### Opción 3 — Una relación por subtipo (con atributos del supertipo incluidos)

```
LIBRO(IDPublicacion, Título, Páginas, Editorial)
REVISTA(IDPublicacion, Título, Periodicidad, Número)
```

✅ Ventaja: Útil cuando hay muchos atributos distintos en los subtipos
❌ Inconveniente: Duplicación del atributo `Título` (del supertipo)

---

## Pérdidas semánticas

Las **pérdidas semánticas** ocurren cuando algún detalle del modelo E/R **no puede representarse** en el modelo relacional.

| Situación | ¿Pérdida semántica? |
|---|---|
| Cardinalidad mínima 1 en el lado N de una 1:N | ✅ Sí — el relacional no puede obligar a que todos los del lado 1 sean referenciados |
| Cardinalidad mínima 0 en el lado N de una 1:N | ❌ No |
| Cardinalidad mínima 1 en ambos extremos de 1:1 | ✅ Sí |
| Cardinalidad mínima 0 en uno de los extremos de 1:1 | ❌ No |

---

## 🔗 Conexiones

- [[Sesión 5 - El Modelo Relacional (I)]] — Fundamentos: tuplas, dominios, claves, 1FN
- [[Sesión 7 - Práctica MySQL Workbench]] — Implementación de relaciones 1:N en MySQL Workbench
- [[Conceptos Clave]] — Añadir términos de la tabla siguiente

---

## 📝 Nuevos términos para `Conceptos Clave.md`

| Término | Definición |
|---|---|
| Restricción semántica | Norma del Universo del Discurso expresada formalmente en el modelo relacional (PK, UNIQUE, NOT NULL, FK) |
| Integridad referencial | Garantía de que todo valor de una FK existe como clave candidata en la relación referenciada, o es NULL |
| Relación referenciada (R1) | Relación que contiene la clave candidata apuntada por la FK |
| Relación que referencia (R2) | Relación que contiene la FK |
| NO ACTION | Regla de integridad: solo permite borrar/modificar en R1 si no hay tuplas dependientes en R2 |
| CASCADE | Regla de integridad: el cambio en R1 se propaga automáticamente a R2 |
| SET NULL | Regla de integridad: al borrar/modificar en R1, la FK en R2 pasa a NULL |
| CHECK | Restricción de rechazo evaluada en cada operación sobre un elemento |
| ASSERTION | Restricción de rechazo aplicable a varios elementos; tiene nombre propio en la BD |
| Trigger | Regla Evento-Condición-Acción; procedimental; se dispara ante operaciones DML |
| Grafo relacional | Representación gráfica de relaciones, claves y restricciones de integridad en el modelo relacional |
| Atributo discriminante | Atributo añadido al supertipo en la opción 1 de transformación de jerarquías para identificar el subtipo |
| Pérdida semántica | Incapacidad del modelo relacional para expresar ciertas restricciones presentes en el modelo E/R |
| Propagación de clave | Técnica para transformar 1:N añadiendo la PK del lado 1 como FK en el lado N |

---

#bases-de-datos #modelo-relacional #integridad-referencial #transformacion-ER #grafo-relacional #jerarquias #clave-externa #nebrija
