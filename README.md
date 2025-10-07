# BaseDatosTest1
# 📚 Sistema de Gestión de Biblioteca – Base de Datos PostgreSQL

Este proyecto implementa la base de datos para un **sistema de gestión de biblioteca**, desarrollado en **PostgreSQL**.  
Permite administrar **usuarios, libros, editoriales, categorías, préstamos, reservas** y versiones **digitales y físicas** de cada libro.

---

## 🗂️ Estructura de la Base de Datos

La base de datos contiene las siguientes tablas principales:

| Tabla | Descripción |
|--------|--------------|
| **categorias** | Contiene las categorías o géneros de los libros (ej. Ciencia, Historia, Literatura). |
| **editorial** | Registra las editoriales que publican los libros. |
| **libro** | Contiene la información principal de los libros (título, autor, año, ISBN, precio, etc.). |
| **copia_fisica** | Registra las copias físicas disponibles en la biblioteca. |
| **version_digital** | Almacena las versiones digitales de los libros (URL, formato, tamaño). |
| **usuarios** | Guarda los datos de los usuarios (lectores, editores, administradores, etc.). |
| **prestamo** | Controla los préstamos de copias físicas a los usuarios. |
| **reserva** | Registra las reservas de libros realizadas por los usuarios. |

---

## 🧩 Diagrama Entidad–Relación (ER)

Las principales relaciones del sistema son:

- **Un libro** pertenece a una **categoría** y una **editorial**.  
- **Una categoría** puede tener **muchos libros**.  
- **Una editorial** puede tener **muchos libros**.  
- **Un libro** puede tener varias **copias físicas** y/o una **versión digital**.  
- **Un usuario** puede realizar varios **préstamos** y **reservas**.  
- **Un préstamo** está asociado a **una copia física**, **un libro** y **un usuario**.

---

## 🔑 Claves Primarias y Foráneas

### Claves Primarias
Cada tabla define una **clave primaria** única para identificar sus registros:
- `id_categoria` → **categorias**
- `id_editorial` → **editorial**
- `id_libro` → **libro**
- `id_copia_fisica` → **copia_fisica**
- `id_digital` → **version_digital**
- `id_usuario` → **usuarios**
- `id_prestamo` → **prestamo**
- `id_reserva` → **reserva**

### Claves Foráneas
Las relaciones están definidas mediante las siguientes **foreign keys**:

| Tabla | Columna FK | Referencia |
|--------|-------------|------------|
| `libro` | `id_editorial` | → `editorial.id_editorial` |
| `libro` | `id_categoria` | → `categorias.id_categoria` |
| `copia_fisica` | `id_libro` | → `libro.id_libro` |
| `version_digital` | `id_libro` | → `libro.id_libro` |
| `prestamo` | `id_usuario` | → `usuarios.id_usuario` |
| `prestamo` | `id_libro` | → `libro.id_libro` |
| `prestamo` | `id_copia_fisica` | → `copia_fisica.id_copia_fisica` |
| `reserva` | `id_usuario` | → `usuarios.id_usuario` |
| `reserva` | `id_libro` | → `libro.id_libro` |

---

## 🧠 Tipos de Datos Personalizados

- **tipo_usuario**: Tipo enumerado que define el rol del usuario dentro del sistema  
  *(ejemplo: `lector`, `editor`, `administrador`)*.

---

## 💾 Scripts Incluidos

El archivo SQL principal crea toda la estructura de la base de datos:

```sql
BEGIN;

-- Tablas principales
CREATE TABLE categorias (...);
CREATE TABLE editorial (...);
CREATE TABLE libro (...);
CREATE TABLE copia_fisica (...);
CREATE TABLE version_digital (...);
CREATE TABLE usuarios (...);
CREATE TABLE prestamo (...);
CREATE TABLE reserva (...);

-- Relaciones entre tablas
ALTER TABLE ... ADD CONSTRAINT fk_libro FOREIGN KEY ...;
ALTER TABLE ... ADD CONSTRAINT fk_usuario FOREIGN KEY ...;

END;

