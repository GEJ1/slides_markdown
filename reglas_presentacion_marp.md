# Guia de estilos y criterios para presentaciones (Marp)

Este documento recopila los criterios de diseno, contenido y redaccion para crear presentaciones en Markdown con Marp.

Uso principal: copiar el contenido de este archivo al inicio de una conversacion con una IA y pedirle que lo adopte antes de generar cualquier clase. Eso evita tener que corregir los mismos errores una y otra vez.

---

## 1. Diseno y estetica visual

- **Fondo:** Colores claros, preferentemente blanco o gris muy suave (`#f8f9fa`). No usar fondos oscuros.
- **Tipografia:** Fuentes sans-serif de Google Fonts. `Montserrat` para titulos, `Open Sans` para el cuerpo del texto.
- **Colores de acento:** Azules corporativos (`#1a365d` para h1/h3, `#2b6cb0` para h2) y rojo fuerte (`#c53030`) exclusivamente para el tag `strong`. No usar estos colores en otros elementos.
- **Margenes:** Padding amplio en todas las slides (`padding: 80px 120px`) para que el contenido no toque los bordes.
- **Tamano de fuente global:** `26px` en `section`. Es el tamano minimo para que se lea bien proyectado en una sala.
- **Alineacion vertical:** `display: flex; flex-direction: column; justify-content: center;` en `section` para centrar verticalmente el contenido en cada diapositiva.

---

## 2. Estructura del contenido

- **Densidad:** Maximo 3 a 5 viñetas por diapositiva. Si hay mas informacion, dividir en dos o tres slides consecutivas. Nunca achicar la fuente para que "entre todo".
- **Titulos:** Cortos y directos. El titulo dice de que trata la slide, no resume su contenido completo.
- **Flujo logico:** Intro -> Desarrollo -> Cierre. La ultima slide debe cerrar, no quedar colgada.
- **Tablas:** Deben ir en una slide aislada. Una tabla que no entra completa en pantalla es inutilizable durante una presentacion. No debe haber scroll.
- **Imagenes:** Siempre descargadas localmente en una carpeta `/static/`. Nunca usar URLs externas durante una presentacion. Sintaxis segun necesidad:
  - Lateral (foto): `![bg right:40%](../static/imagen.jpg)` — usa `object-fit: cover`, recorta la imagen para llenar el area.
  - Lateral (logo o icono cuadrado): `![bg right:40% fit](../static/logo.jpg)` — agregar `fit` para usar `object-fit: contain` y evitar que se corte. Solo funciona bien para imagenes cuadradas o de proporcion similar al area del panel.
  - Logo ancho (ej. 2:1 o mas): no usar `bg`. Usar imagen inline con tamano fijo: `![w:380px](../static/logo.jpg)`. Los logos muy anchos se recortan en el borde derecho del slide aunque se use `fit`.
  - Centrada con tamano fijo: `![w:600px](../static/imagen.jpg)`
  - Fondo completo: `![bg](../static/imagen.jpg)`
- **Texto sobre imagen de fondo (portada):** Cuando una slide tiene `![bg]`, el texto puede quedar ilegible. Agregar en el CSS de `section.portada` color blanco y sombra de texto:
  ```css
  section.portada h1 {
    color: white;
    text-shadow: 0 2px 8px rgba(0,0,0,0.8);
  }
  section.portada h2 {
    color: rgba(255,255,255,0.9);
    text-shadow: 0 1px 6px rgba(0,0,0,0.7);
  }
  ```
- **Bloques de codigo o prompts:** Usar la clase `.demo-box` con `.prompt-text` interno para aislar visualmente el texto con fuente monospace y fondo grisaceo. No poner prompts en viñetas normales.
- **Diagramas de flujo:** Para representar relaciones, pipelines o arquitecturas, usar HTML con las clases `.diagram`, `.box`, `.box.accent` y `.arrow`. No describir flujos con parrafos de texto cuando un diagrama es mas claro.

---

## 3. Idioma y tono

- **Variante:** Espanol rioplatense (argentino formal).
- **Tratamiento:** Voseo consistente. "Fijate", "hace", "necesitas" con acento correcto. Jamas usar "tu" o conjugaciones de "tuteo".
- **Vocabulario:** Evitar modismos del espanol neutro. "Heladera" no "refrigerador", "celular" no "movil", "auto" no "coche".
- **Tono:** Profesional y directo. Cercano sin ser coloquial. Evitar lunfardo extremo pero tampoco sonar neutro o corporativo impersonal.
- **Mayusculas:** Sentence case en titulos y viñetas. Solo mayuscula inicial y nombres propios. No usar Title Case anglosajón.
- **Em dash (—):** Prohibido. Reemplazarlo siempre por dos puntos (`:`), pipe (`|`), parentesis o coma segun el caso.

---

## 4. Organizacion de archivos

- **Una carpeta por clase:** `/clase1/`, `/clase2/`, etc. Cada carpeta contiene el `.md` fuente y el `.html` exportado.
- **Imagenes offline:** Siempre en una subcarpeta `/static/` dentro del proyecto, referenciadas con rutas relativas (`../static/imagen.jpg`). Nunca dependencia de red para las imagenes durante la presentacion.
- **Exportacion:** El archivo `.html` que genera Marp es autocontenido. Se puede abrir en cualquier navegador sin necesidad de internet ni de tener Marp instalado en el equipo donde se presenta.

---

## 5. Referencia del CSS base

Este es el bloque `style` completo que se incluye en el frontmatter. Contiene todos los componentes usados habitualmente.

```css
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;700&family=Open+Sans:wght@400;600&display=swap');

section {
  background-color: #f8f9fa;
  font-family: 'Open Sans', sans-serif;
  font-size: 26px;
  color: #2d3748;
  padding: 80px 120px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

h1, h2, h3 {
  font-family: 'Montserrat', sans-serif;
  color: #1a365d;
}

h1 {
  font-size: 44px;
  border-bottom: 3px solid #2b6cb0;
  padding-bottom: 12px;
  margin-bottom: 24px;
}

h2 {
  font-size: 32px;
  color: #2b6cb0;
}

strong {
  color: #c53030;
}

blockquote {
  background-color: #e2e8f0;
  border-left: 4px solid #2b6cb0;
  border-radius: 4px;
  padding: 16px 24px;
  margin: 12px 0;
  font-family: 'Courier New', monospace;
  font-size: 22px;
  color: #2d3748;
}

blockquote p {
  margin: 0;
}

table {
  width: 100%;
  border-collapse: collapse;
  font-size: 24px;
}

th {
  background-color: #2b6cb0;
  color: white;
  padding: 12px 16px;
  text-align: left;
}

td {
  padding: 12px 16px;
  border-bottom: 1px solid #cbd5e0;
}

tr:nth-child(even) td {
  background-color: #edf2f7;
}

ul li {
  margin-bottom: 12px;
  line-height: 1.5;
}

/* Slide de portada: titulo abajo, imagen de fondo */
section.portada {
  justify-content: flex-end;
  padding-bottom: 100px;
}

section.portada h1 {
  font-size: 52px;
  border: none;
  color: white;
  text-shadow: 0 2px 8px rgba(0,0,0,0.8);
}

section.portada h2 {
  font-size: 30px;
  color: rgba(255,255,255,0.9);
  text-shadow: 0 1px 6px rgba(0,0,0,0.7);
}

/* Bloque para mostrar prompts o ejemplos de codigo */
.demo-box {
  background-color: #ffffff;
  border: 1px solid #cbd5e0;
  border-radius: 8px;
  padding: 14px 18px;
  margin-top: 14px;
  box-shadow: 0 4px 6px rgba(0,0,0,0.05);
}

.prompt-text {
  font-family: monospace;
  color: #1a202c;
  background-color: #e2e8f0;
  padding: 10px 12px;
  border-radius: 6px;
  display: block;
  margin-top: 8px;
  white-space: pre-wrap;
  font-size: 0.82em;
  line-height: 1.5;
}

/* Diagrama de flujo con cajas y flechas */
.diagram {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20px;
  margin: 32px 0;
}

.box {
  background-color: #edf2f7;
  border: 2px solid #2b6cb0;
  border-radius: 8px;
  padding: 20px 32px;
  text-align: center;
  font-family: 'Montserrat', sans-serif;
  font-size: 22px;
  color: #1a365d;
  line-height: 1.5;
}

.box strong {
  color: inherit;
}

.box.accent {
  background-color: #2b6cb0;
  color: white;
  border-color: #1a365d;
}

.box.accent strong {
  color: white;
}

.arrow {
  font-size: 36px;
  color: #2b6cb0;
  font-weight: bold;
  flex-shrink: 0;
}

/* Nota al pie opcional */
.footnote {
  position: absolute;
  bottom: 28px;
  left: 120px;
  right: 120px;
  font-size: 16px;
  color: #718096;
  border-top: 1px solid #cbd5e0;
  padding-top: 6px;
}

code {
  background-color: #e2e8f0;
  padding: 2px 6px;
  border-radius: 3px;
  font-size: 22px;
}

pre {
  background-color: #2d3748;
  color: #e2e8f0;
  padding: 24px;
  border-radius: 6px;
  font-size: 22px;
}

pre code {
  background: none;
  color: inherit;
  padding: 0;
}
```

---

*Para usar esta guia con una IA: seleccionar todo el texto de este archivo, copiarlo, y al iniciar una nueva conversacion pegar el contenido con la instruccion: "Leer estas reglas y adoptarlas antes de que te pida crear una presentacion."*
