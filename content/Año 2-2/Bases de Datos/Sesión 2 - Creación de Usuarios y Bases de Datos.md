
> **Asignatura:** Bases de Datos | **Prof.:** Jaime Álvarez Benayas  
> **Tipo:** Práctica  
> **Ver también:** [[Sesión 1 - Sistemas de Información]] | [[Sesión 0 - Indice]]

---

## 📌 Herramientas necesarias

- **XAMPP** → servidor local con Apache + MySQL + PHP
- **phpMyAdmin** → interfaz web para gestionar MySQL (acceso: `localhost/phpmyadmin`)
- **MySQL CLI** → consola de comandos de MySQL

> 💡 Instalación de XAMPP: ver manual `Instalación de servidor MySQL en Windows.pdf`

---

## Método 1 — phpMyAdmin (Interfaz Gráfica)

### Paso 1: Crear una Base de Datos

1. Acceder a `localhost/dashboard/` → clic en **phpMyAdmin**
2. Seleccionar la pestaña **Databases**
3. En el formulario **Create database**:
   - **Nombre:** `prueba1`
   - **Collation:** `utf8_general_ci`
4. Clic en **Create**

> ✅ La BD `prueba1` aparecerá en la columna izquierda, completamente vacía.

> 📝 **¿Qué es un Collation?**  
> Indica un conjunto de caracteres, su codificación y reglas de comparación.  
> **UTF-8** es una codificación de longitud variable para Unicode que incluye la mayoría de caracteres y símbolos de los lenguajes del mundo.

---

### Paso 2: Crear un Usuario

1. Ir a la pestaña **Users** → clic en **Add user**
2. Rellenar los datos:
   - **User name:** `up1`
   - **Host:** `Local` → `localhost`
   - **Password:** (introducir y repetir)
   - **Privilegios globales:** dejar todos **sin marcar** (se asignarán por BD)
3. Clic en **Go**

> ✅ El usuario `up1` aparecerá en la lista de usuarios con privilegios `USAGE`.

La sentencia SQL que genera:
```sql
CREATE USER 'up1'@'localhost' IDENTIFIED BY '***';
GRANT USAGE ON *.* TO 'up1'@'localhost' IDENTIFIED BY '***'
REQUIRE NONE WITH MAX_QUERIES_PER_HOUR 0 
MAX_CONNECTIONS_PER_HOUR 0 MAX_UPDATES_PER_HOUR 0 
MAX_USER_CONNECTIONS 0;
```

---

### Paso 3: Asignar Privilegios al Usuario sobre una BD

1. En la lista de usuarios, clic en **Edit Privileges** del usuario `up1`
2. Clic en la pestaña **Database**
3. En **Database-specific privileges**, seleccionar `prueba1` → clic en **Go**
4. Marcar **Check All** para seleccionar todos los permisos
5. Clic en **Go**

> ✅ Sentencia SQL generada:
```sql
GRANT ALL PRIVILEGES ON `prueba1`.* TO 'up1'@'localhost' WITH GRANT OPTION;
```

---

### Paso 4: Permitir login con otros usuarios

Para poder cerrar sesión y acceder con distintos usuarios, editar el archivo:

```
C:\xampp\phpMyAdmin\config.inc.php
```

Cambiar `auth_type` a `cookie`:

```php
$cfg['Servers'][$i]['auth_type'] = 'cookie';
```

> Ahora phpMyAdmin mostrará una pantalla de login al acceder.

---

### Verificación

Al entrar con `up1`:
- Solo aparece `prueba1` (y `information_schema`) en el panel izquierdo
- El usuario tiene todos los privilegios sobre `prueba1`

---

## Método 2 — SQL directo desde phpMyAdmin

1. Acceder como `root`
2. Ir a la pestaña **SQL**
3. Ejecutar las siguientes instrucciones:

```sql
-- Crear base de datos
CREATE DATABASE prueba2 
DEFAULT CHARACTER SET utf8 
COLLATE utf8_general_ci;

-- Crear usuario
CREATE USER 'up2'@'localhost' IDENTIFIED BY 'up2';

-- Asignar todos los privilegios
GRANT ALL PRIVILEGES ON `prueba2`.* TO 'up2'@'localhost';
```

4. Clic en **Go**

> ✅ Resultado: `# MySQL returned an empty result set (i.e. zero rows).`  
> Esto es normal en sentencias que no devuelven datos (DDL/DCL).

---

## Método 3 — MySQL en Línea de Comandos (CLI)

### Abrir consola

Buscar `cmd` en Windows → abrir **Símbolo del sistema**

### Conectarse a MySQL como root

```bash
C:\xampp\mysql\bin\mysql.exe -u root -p
```

Introducir la contraseña cuando se solicite.

### Crear BD, usuario y asignar privilegios

```sql
-- Crear base de datos
CREATE DATABASE prueba3 
DEFAULT CHARACTER SET utf8 
COLLATE utf8_general_ci;

-- Crear usuario
CREATE USER 'up3'@'localhost' IDENTIFIED BY 'up3';

-- Asignar todos los privilegios
GRANT ALL PRIVILEGES ON `prueba3`.* TO 'up3'@'localhost';
```

> ✅ Respuesta esperada:
> ```
> Query OK, 1 row affected (0.00 sec)
> Query OK, 0 rows affected (0.01 sec)
> Query OK, 0 rows affected (0.00 sec)
> ```

---

## 📊 Resumen Comparativo de Métodos

| Método | Herramienta | Ventajas | Nivel |
|--------|-------------|----------|-------|
| Interfaz gráfica | phpMyAdmin | Visual, intuitivo | Principiante |
| SQL en phpMyAdmin | phpMyAdmin | Rápido, reutilizable | Intermedio |
| CLI MySQL | Consola | Control total, sin interfaz | Avanzado |

---

## 📝 Comandos SQL Clave

```sql
-- Crear BD
CREATE DATABASE nombre DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;

-- Crear usuario
CREATE USER 'usuario'@'localhost' IDENTIFIED BY 'contraseña';

-- Asignar todos los privilegios sobre una BD
GRANT ALL PRIVILEGES ON `nombre_bd`.* TO 'usuario'@'localhost';

-- Asignar privilegios específicos
GRANT SELECT, INSERT, UPDATE, DELETE ON `nombre_bd`.* TO 'usuario'@'localhost';
```

---

## 🔗 Conexiones

- [[Sesión 1 - Sistemas de Información]] — El SGBD que estamos usando es MySQL, parte del concepto de [[Conceptos Clave#SGBD|SGBD]]
- [[Sesión 3 - Modelos de Datos]] — Antes de crear tablas, se diseña el modelo de datos
- [[Conceptos Clave#Collation|Collation y UTF-8]]

---

*Tags: #práctica #XAMPP #phpMyAdmin #MySQL #usuarios #bases-de-datos #SQL*
