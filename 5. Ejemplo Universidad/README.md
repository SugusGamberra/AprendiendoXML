# 📚 XML y XSD

> Lo de hoy es un caso práctico previo a cerrar dar por **concluido** este repo de XML y XSD :P Mañana nos pondríamos ya con JS, en dicho repo ya pondré una carpeta que esté enfocada en la asignatura de Lenguaje de Marcados 🩵

---

## 📋 Conceptos clave

Recordemos par de cositas para tener claras:

1. **UTF-8**: En `.xml` es obligatorio ponerlo porque ahí es donde están los datos reales (nombres, tildes, etc). En el `.xsd` no suele ponerse porque solo definimos _las etiquetas_ (la estructura), _no el contenido_.
2. **Validación**: El XSD es como el "jefe" o el "plano", dice qué se puede poner o qué no en el XML.

---

## Desglose de [`universidad.xsd`](universidad.xsd)

Aquí empezamos definiendo las reglas, recordemos qué hace cada piecita del puzzle :P

### Tipos de elementos
- `xs:complexType`: Se usa cuando una etiqueta **contiene otras etiquetas dentro**. En este ejemplo `<Universidad>` es complejo porque dentro tiene estudiantes.
- `xs:simpleType`: Se usa cuando una etiqueta solo contiene **texto** o **numeros** (contenido directo) pero queremos ponerle reglas (como que el nombre tenga tantas letras).

### Restricciones y control
- `xs:sequence`: Sirve para obligar a que las etiquetas aparezcan en un **orden específico**.
- `maxOccurs="unbounded"`: Esto en concreto significa "infinito". Pero aquí podemos definir un número concreto, según necesidades.
- `minOccurs="0"`: Esto indica que el elemento es **opcional**, en nuestro ejemplo el correo no es obligatorio ponerlo. Si no ponemos nada el valor por defecto mínimo es 1.

### Validaciones de contenido (`xs:restriction`)
Para que los datos sean correctos usamos restricciones:
- `base="xs:string"` o `base="xs:integer"`: Define si lo que escribimos es texto o números enteros, por ejemplo.
- `minLength`/`maxLength`: Para que el nombre no sea de una sola letra o hagas copypaste de la biblia ahi xd
- `minInclusive`/`maxInclusive`: Controlar que un número vaya desde x a y, como en nuestro caso, la edad es de 18 a 100 años.
- `xs:pattern`: Es un **regex** (regular expression) que valida que un correo tenga su @, su .com, restringe o permite ciertos caracteres...

---

## Desglose de [`universidad.xml`](./universidad.xml)

Recordemos un poco el xml en base al que hemos hecho:

1. **Cabecera**: `<?xml version="1.0" encoding="UTF-8">`, es la primera línea obligatoria, le dice al sistema qué tipo de archivo es, la versión que usa y los caracteres que usa (en este caso pa que las tildes y ñ se vean bien)
2. **Elemento raíz**: El contenedor padre, en nuestro caso `<Universidad ...>` con su cierre. Recordemos que _solo hay 1 elemento raíz_, que envuelve a todo lo demás. Si pones otra etiqueta a su mismo nivel sencillamente te dará error.
3. **Conexión con XSD**: `xmlns:xsi` que es como importar una librería para que el XML entienda cómo validar esquemas. `xsi:noNamespaceSchemaLocation="universidad.xsd"` es lo que enlaza las reglas de validación del XML al arcivo xsd, sin esto iría por libre básicamente.
4. **Elementos hijos y atributos**: En nuestro ejemplo el _atributo_ es el `id`, que es info extra sobre la etiqueta, de ahí que en el XSD usemos `xs:ID` para que cada estudiante tenga su código _único_. Los _elementos_ serían `nombre` y `edad`, que son las etiquetas que contienen la info real.

> Para que lo visualices en tu mente:
> **Nivel 1**: Raíz `Universidad`
> **Nivel 2**: Se puede repetir, en este caso `Estudiante` (gracias al maxOccurs to las veces que queramos podemos meter un estudiante)
> **Nivel 3**: Datos como el `nombre`, `edad`, `programa` y `correo`.

Recordemos cerrar todas las etiquetas siempre! Este es **case sensitive** (vaya, que si pusiste edad en el xsd, en el xml tienes que usar edad, no Edad, EDAD, whatever, dependes de eso!!) y cuidaaaaao con la **anidación**, no cruces etiquetas (x ejemplo, `<a><b></a></b>` estaría mal, `<a><b></b></a>` estaría bien!)