# slides_markdown

Este repositorio documenta un workflow para crear presentaciones de diapositivas a partir de archivos Markdown, usando la herramienta **Marp**.

El objetivo es que cualquier persona pueda replicar este método: escribir las slides como texto plano, darle estilo con CSS embebido, y exportarlas a HTML o PDF listos para presentar.

---

## Qué es Marp

Marp (Markdown Presentation Ecosystem) es una herramienta que convierte archivos `.md` en presentaciones de diapositivas. Cada diapositiva se separa con `---`. El estilo visual se define una sola vez en el encabezado del archivo, usando CSS dentro del bloque `style`.

Marp no necesita PowerPoint ni Google Slides. El resultado es un archivo HTML autónomo o un PDF, ambos portables y offline.

---

## Instalación

Hay dos formas de usar Marp:

### Opción 1: Extensión de VS Code (recomendada para empezar)

1. Instalar [Visual Studio Code](https://code.visualstudio.com/).
2. Buscar e instalar la extensión **"Marp for VS Code"** (autor: Marp team).
3. Abrir cualquier archivo `.md` con el bloque `marp: true` en el encabezado.
4. La extensión muestra una preview en tiempo real y permite exportar a HTML o PDF desde el menú de comandos (`Ctrl+Shift+P` > "Marp: Export Slide Deck").

### Opción 2: CLI (para automatizar o usar desde terminal)

```bash
npm install -g @marp-team/marp-cli
marp archivo.md --html    # exporta a HTML
marp archivo.md --pdf     # exporta a PDF
```

---

## Estructura del repositorio

```
slides_markdown/
  README.md                     <- este archivo
  reglas_presentacion_marp.md   <- guía de criterios de diseño y redacción
  ejemplo/
    ejemplo.md                  <- archivo fuente de la presentación de ejemplo
    ejemplo.html                <- exportación (generada por Marp, no editar a mano)
    static/
      imagen.jpg                <- imágenes descargadas localmente
```

La convención es una carpeta por presentación (por ejemplo `/clase1/`, `/clase2/`), con una subcarpeta `/static/` dentro o en el nivel superior del proyecto para los recursos visuales.

---

## El encabezado del archivo (frontmatter)

Todo archivo `.md` de Marp empieza con un bloque YAML delimitado por `---`. Este bloque define los parámetros globales y el CSS de la presentación:

```markdown
---
marp: true
theme: default
paginate: true
size: 16:9
style: |
  section {
    background-color: #f8f9fa;
    font-size: 26px;
    padding: 80px 120px;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
---
```

- `marp: true`: activa el procesador de Marp sobre este archivo.
- `theme: default`: usa el tema base de Marp (el CSS propio lo sobreescribe casi todo).
- `paginate: true`: agrega números de página automáticamente.
- `size: 16:9`: formato widescreen, el más común para proyectores.
- `style`: bloque de CSS puro que se aplica a todas las diapositivas.

---

## Cómo se estructura una diapositiva

Cada diapositiva es una sección de Markdown separada por `---`:

```markdown
## Título de la diapositiva

- Punto uno
- Punto dos
- Punto tres

![bg right:40%](static/imagen.jpg)
```

### Clases especiales

Para cambiar el comportamiento de una diapositiva en particular, se usa un comentario HTML antes del contenido:

```markdown
<!-- _class: lead -->
# Diapositiva de portada
```

Las clases `lead` y `portada` (u otras que definas en el CSS) permiten darle un estilo diferente a slides específicas sin afectar al resto.

---

## Sintaxis de imágenes en Marp

Marp extiende la sintaxis estándar de Markdown para controlar la ubicación y el tamaño de las imágenes.

| Sintaxis | Resultado |
|----------|-----------|
| `![bg right:40%](ruta.jpg)` | Imagen lateral derecha, ocupa el 40% del ancho |
| `![bg left:35%](ruta.jpg)` | Imagen lateral izquierda |
| `![bg](ruta.jpg)` | Imagen de fondo completo |
| `![w:600px](ruta.jpg)` | Imagen centrada con ancho fijo |

Las rutas deben ser relativas al archivo `.md`. Siempre usar imágenes descargadas localmente, nunca URLs externas: durante una clase, la conexión puede fallar.

### Imágenes en la exportación a PDF

Al exportar a PDF, Marp usa Chromium internamente y por defecto bloquea el acceso a archivos locales. Si el PDF se genera sin imágenes, hay que habilitar el acceso explícitamente:

**CLI:**
```bash
marp --pdf --allow-local-files archivo.md
```

**Extensión de VS Code:** agregar en `settings.json`:
```json
"marp.exportAllowLocalFiles": true
```

---

## HTML embebido para componentes visuales

Marp permite usar HTML dentro del Markdown. Esto habilita componentes que no tienen equivalente en Markdown puro.

### Caja de ejemplo o prompt

```html
<div class="demo-box">
  <p><strong>Texto introductorio:</strong></p>
  <span class="prompt-text">
Contenido en fuente monospace.
Preserva los saltos de línea.
  </span>
</div>
```

### Diagrama de flujo (cajas y flechas)

```html
<div class="diagram">
  <div class="box">Entrada</div>
  <div class="arrow">→</div>
  <div class="box accent">Proceso</div>
  <div class="arrow">→</div>
  <div class="box">Salida</div>
</div>
```

Estos componentes requieren que las clases CSS correspondientes estén definidas en el bloque `style` del frontmatter.

---

## Criterios de diseño y redacción

El archivo `reglas_presentacion_marp.md` en este repositorio funciona como guía de criterios. Cubre:

- Paleta de colores, tipografía y márgenes
- Densidad de contenido por diapositiva
- Uso de tablas, imágenes y componentes HTML
- Tono y variante del idioma
- Organización de archivos

Ese archivo está pensado para ser leído por un agente de IA como contexto antes de generar una presentación nueva. De esa manera, la IA adopta los criterios desde el primer intento sin necesidad de corregirla diapositiva por diapositiva.

---

## Workflow típico

1. Definir el tema y la estructura de la clase (puede hacerse con una IA).
2. Pedirle a la IA que genere el archivo `.md` completo, pasándole primero el contenido de `reglas_presentacion_marp.md`.
3. Revisar y ajustar el `.md` en VS Code con la preview de Marp activa.
4. Descargar las imágenes necesarias a la carpeta `/static/` local.
5. Exportar a HTML con la extensión de VS Code o con el CLI.
6. Presentar desde el HTML (no necesita internet ni software especial en el equipo donde se presenta).

---

## Ejemplo incluido

La carpeta `/ejemplo/` contiene una presentación de muestra sobre un tema neutro. Muestra todas las funcionalidades: portada con imagen lateral, slides de viñetas, tabla, blockquote, caja de código, diagrama de flujo y slide de cierre.

Para verla: abrir `ejemplo/ejemplo.md` en VS Code con la extensión Marp instalada, o exportarla a HTML con el CLI.
