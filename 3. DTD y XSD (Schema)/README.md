# 📌 DTD y XSD (Schema)

## 🧱 ¿Qué es un DTD?

Un **DTD (Document Type Definition)** define:

* Qué **elementos** y **atributos** existen
* La **estructura** del documento
* Las **restricciones** sobre el contenido

Es la forma clásica de definir la estructura de un XML.

---

## 🧩 ¿Qué es XSD (XML Schema)?

**XSD Schema** es la evolución del DTD y la forma **actual y recomendada**.

Permite:

* Definir **tipos de datos** (`string`, `int`, etc.)
* Controlar la **cardinalidad** (cuántas veces se repite un elemento)
* Validaciones más potentes y precisas

Ejemplos:

### 📄 XML: `biblioteca.xml`

Documento XML **bien formado** y preparado para validarse con un XSD:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<biblioteca 
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:noNamespaceSchemaLocation="biblioteca.xsd">

    <libro>
        <titulo>El Quijote</titulo>
        <autor>Cervantes</autor>
        <publicacion>1605</publicacion>
    </libro>

    <libro>
        <titulo>1984</titulo>
        <autor>Orson Welles</autor>
        <publicacion>1949</publicacion>
    </libro>

</biblioteca>
```

📌 **Notas importantes**:

* La cabecera XML está bien escrita (`version`, `encoding`)
* Se usa `xsi:noNamespaceSchemaLocation` para enlazar el XSD
* El XML no define tipos: **eso lo hace el Schema**

### 📐 XSD: `biblioteca.xsd`

Schema que define la estructura y validaciones del XML:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">

    <!-- Definición del tipo libro -->
    <xs:complexType name="libroType">
        <xs:sequence>
            <xs:element name="titulo" type="xs:string"/>
            <xs:element name="autor" type="xs:string"/>
            <xs:element name="publicacion" type="xs:int"/>
        </xs:sequence>
    </xs:complexType>

    <!-- Definición del elemento raíz -->
    <xs:element name="biblioteca">
        <xs:complexType>
            <xs:sequence>
                <xs:element 
                    name="libro" 
                    type="libroType"
                    minOccurs="0"
                    maxOccurs="unbounded"/>
            </xs:sequence>
        </xs:complexType>
    </xs:element>

</xs:schema>
```

📌 **Qué se está validando aquí**:

* `biblioteca` es el **elemento raíz**
* Puede haber **0 o más libros**
* Cada `libro` debe tener:

  * `titulo` → texto
  * `autor` → texto
  * `publicacion` → número entero

Si el XML no cumple esto, **no es válido**

---

### 🧠 Idea clave

* XML → contiene los **datos**
* XSD → define las **reglas**
* Si no cumple el XSD, el documento **falla**

---

> 🔜 **Mañana**: ventajas y desventajas de XML