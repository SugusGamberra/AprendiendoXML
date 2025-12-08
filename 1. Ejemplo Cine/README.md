# 🎬 Ejemplo 1 — XML de un Cine  

> 🌈 Este es nuestro **primer XML real** del tema de lenguajes de marcado.  
> Aquí aprenderás cómo funciona la estructura, cómo usar atributos, cómo anidar datos y cómo representar información de forma jerárquica.

---

## 📄 ¿Qué estamos representando?

En este ejemplo creamos un **catálogo de salas de cine**, cada una con:

- 🏷️ Un **id**  
- ⭐ Un **tipo** (vip / normal)  
- 🏟️ Una **capacidad**  
- 🎞️ Una **película proyectada**  
- 🎟️ (Opcional) Una **reserva** con sus datos  

Todo está dentro del elemento raíz `<cine>`.

---

## 🧩 Estructura del documento

### ✔️ Declaración XML

Así indicamos **versión** y **codificación**. Da igual si el encoding no es _UTF-8_ porque aquí es solo decorativo, y para la actividad propuesta era necesario que fuera US-ASCII!

```xml
<?xml version="1.0" encoding="US-ASCII"?>
```

### ✔️ Elemento raíz

Todo el documento cuelga de:

```xml
<cine>
    ...
</cine>
```

Sin este "Padre de todo" el XML **NO FUNCIONA**!!

---

## 🏛️ Elementos principales del ejemplo

### 🟦 `<sala>`

Representa una sala de cine, tiene atributos `id="S01"` `tipo="vip"`, ejemplo:

```xml
<sala id="S01" tipo="vip">
    ...
</sala>
```

### 🟨 `<nombre>`

El nombre de la sala, contiene **entidades especiales** porque no podemos poner directamente caracteres conflictivos (tildes) por la codificación que le dimos!!

```xml
<nombre>Sala Ant&oacute;n &amp; &lt;G&oacute;mez&gt;</nombre>
```

Hemos usado:
- `&aacute;` → á
- `&amp;` → &
- `&lt;` → <
- `&gt;` → >

### 🟩 `<pelicula>`

Un nodo con info de la peli que se ve en cada sala, tiene un atributo `codigo`!

```xml
<pelicula codigo="P-1">
    <titulo>Your voice</titulo>
    <duracion>180 min</duracion>
</pelicula>
```

### 🟥 `<reserva>`

```xml
<reserva id_reserva="R-1">
    <cliente dni="12345678A">Juan P&eacute;rez</cliente>
    <fecha>2026-12-01</fecha>
    <asiento>Fila 5, Butaca 3</asiento>
</reserva>
```

Hemos usado:
- Atributos (`dni`)
- Texto con tilde codificada (`P&eacute;rez`)
- Datos reales (fecha, asientos...)

---

## 🧠 Mini teoría que debes recordar

### ✔️ XML es un lenguaje de marcado, no de programación

No ejecuta nada. Solo **describe** datos.

### ✔️ Si quieres mostrarlo bonito → XSLT

El XML contiene datos.
La plantilla XSLT decide cómo se ven esos datos:

**XML:**
```xml
<producto>
  <nombre>Zapatillas Nike</nombre>
  <precio>50.00</precio>
</producto>
```

**XSLT:**
```xslt
<h1><xsl:value-of select="producto/nombre" /></h1>
<p>Precio: <xsl:value-of select="producto/precio" /> €</p>
```

---

## 📚 Propósito y para qué se usa XML

- Intercambiar datos entre sistemas
- Estructurar info
- Ser estándar y legible para máquinas y humanos
- Usarse en APIs antiguas, configs, videojuegos, android, bbdd, servicios web...
- Ser jerárquico (estructura en árbol)
- Formato de texto plano fácil de transportar

---

## 🕰️ Historia

- Creado en **1990**
- Evolución simplificada del **SGML**
- Nació para manejar datos de webs
- Mucho más amigable que su antecesor (era infumable xd)

---

## 🧱 Reglas fundamentales

- Todas las etiquetas **abren y cierran**
- Es **sensible** a mayúsculas y minúsculas
- El anidamiento debe ser **correcto**
- Solo puede haber **UN elemento raíz**
- Los atributos **siempre** llevan comillas
- Puedes usar etiquetas **autocerrables**
- Caracteres especiales usan entidades especiales (`&amp;`,`&lt;`, etc)
- Comentarios usando `<!-- comentario -->`

---

## 🔒 CDATA

Cuando quieras meter código dentro como JS, HTML o texto raro sin romper el XML se hace así:

```xml
<![CDATA[
<script>
    alert("Hola mundo");
</script>
]]>
```

---

## 🧾 Conclusión

Este archivo del cine te sirve para practicar:

- Rutas jerárquicas
- Atributos
- Entidades especiales
- Comentarios
- Anidamiento correcto

➡️ Es la estructura real que usarán luego APIs, servicios, apps y sistemas para enviar datos.

---

> 🩵 Hecho con amorcito de los apuntes de clases y mi tarea de práctica uwu