
> **Asignatura:** Bases de Datos | **Prof.:** Jaime Álvarez Benayas  
> **Tipo:** Teoría + Introducción a MySQL Workbench  
> **Ver también:** [[Sesión 1 - Sistemas de Información]] | [[Sesión 0 - Indice]]

---

## 📌 Propósitos de la Unidad

1. Estudiar los **modelos de datos** obtenidos como resultado de aplicar los distintos niveles de abstracción
2. Introducir la herramienta **MySQL Workbench** y sus prestaciones en diseño y administración de BD

---

## 1. ¿Qué es un Modelo?

Construir un modelo consiste en:
- **Representar entidades**, situaciones o fenómenos del mundo real
- De forma que el **comportamiento del modelo se asemeje a la realidad**
- Para que los resultados y conclusiones extraídos se correspondan con los del universo real

---

## 2. Modelos de Datos

> *Herramienta de diseño y representación que ayuda a interpretar un determinado universo del discurso.*

Se persigue obtener una **abstracción del elemento real** en forma de estructuras de datos que constituyen un **esquema o modelo de datos**.

En relación a las BD, los modelos de datos se usan para:
- **Definir y describir** los datos de interés de una organización
- **Reflejar la organización** de esos datos conforme a las particularidades de su tratamiento

### Modelo de Datos Formal

> *Herramienta para realizar un proceso de abstracción obteniendo un esquema compuesto por un conjunto de estructuras de datos que representen un universo de discurso del mundo real.*

---

## 3. Conceptos Clave del Modelado

### Universo del Discurso
> Parcela del mundo real que se pretende modelar.

### Abstracción
> Acción de **reducir el nivel de detalle** de los elementos a modelar para conseguir una representación lo más general posible.

El proceso de abstracción se realiza con ayuda del **Modelo de Datos Formal**.

### Esquema de Base de Datos
> Conjunto de estructuras de datos para almacenar, lo más fielmente posible, la información relativa a la parcela del mundo real que se quiere modelar.

> ⚠️ El esquema **debe estar soportado por el SGBD** → ver [[Conceptos Clave#SGBD]]

---

## 4. El Modelado de Datos

> El modelado **no busca la solución correcta única**, sino obtener las **distintas posibilidades** y los beneficios de cada una.

### ¿Por qué es importante?

- Un buen modelado **facilita considerablemente la programación** de aplicaciones
- Cualquier **cambio posterior en el esquema** puede tener considerable repercusión al propagarse a los niveles superiores
- Permite mostrar en **un solo documento** todos los datos de importancia
- Evita revisar especificaciones funcionales para entender los requisitos de almacenamiento

---

## 5. Características del Modelo de Datos

Un buen modelo de datos debe ser:

| Característica | Descripción |
|----------------|-------------|
| **Completo** | Representa toda la información necesaria |
| **No redundante** | Sin repetición de datos |
| **Refuerza condiciones del universo del discurso** | Refleja las reglas del mundo real |
| **Reusable** | Puede aplicarse en distintos contextos |
| **Estable y flexible** | Adaptación sencilla a cambios |
| **Comunicativo** | Fácil de entender por todos los implicados |
| **Integrable** | Facilidad de integración con otros modelos |
| **Resolutivo** | Resuelve conflictos entre objetivos del modelo |
| **Eficiente** | Favorece el rendimiento |

---

## 6. Flujo de Trabajo en el Diseño de BD

```
Universo del Discurso (mundo real)
          │
          ▼ (abstracción)
    Modelo Conceptual ──────────── Draw.io (Diagrama E-R)
          │
          ▼ (implementación lógica)
    Modelo Lógico ───────────────── MySQL Workbench (diseño visual)
          │
          ▼ (implementación física)
    Base de Datos Física ─────────── XAMPP + MySQL
```

---

## 7. Herramientas del Curso

### MySQL Workbench
- Herramienta visual para **diseño y administración** de bases de datos
- Permite crear esquemas gráficamente
- Genera código SQL automáticamente
- Se conecta al servidor MySQL de XAMPP

### Draw.io
- Para crear **diagramas Entidad-Relación (E-R)**
- Fase de diseño conceptual
- Independiente del SGBD

### XAMPP
- Servidor local completo
- Incluye: **Apache + MySQL + PHP + Perl**
- Se accede a phpMyAdmin desde `localhost`

---

## 🔗 Conexiones

- [[Sesión 1 - Sistemas de Información]] — El nivel conceptual de abstracción es el punto de partida del modelado
- [[Sesión 2 - Creación de Usuarios y Bases de Datos]] — Implementación práctica en XAMPP tras el diseño
- [[Conceptos Clave#Universo del Discurso|Universo del Discurso]]
- [[Conceptos Clave#Abstracción|Abstracción]]
- [[Conceptos Clave#Modelos de Datos|Modelos de Datos]]

---

*Tags: #teoría #modelado #modelo-de-datos #abstracción #MySQL-Workbench #diseño-BD*
