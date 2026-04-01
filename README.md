# slides_markdown

Este repositorio documenta un workflow para crear presentaciones de diapositivas a partir de archivos Markdown, usando la herramienta **Marp**.

El objetivo es que cualquier persona pueda replicar este método: escribir las slides como texto plano, darle estilo con CSS embebido, y exportarlas a HTML o PDF listos para presentar.

---

## Que es Marp

Marp (Markdown Presentation Ecosystem) es una herramienta que convierte archivos `.md` en presentaciones de diapositivas. Cada diapositiva se separa con `---`. El estilo visual se define una sola vez en el encabezado del archivo, usando CSS dentro del bloque `style`.

Marp no necesita PowerPoint ni Google Slides. El resultado es un archivo HTML autónomo o un PDF, ambos portables y offline.

---

## Instalacion

Hay dos formas de usar Marp:

### Opcion 1: Extension de VS Code (recomendada para empezar)

1. Instalar [Visual Studio Code](https://code.visualstudio.com/).
2. Buscar e instalar la extension **"Marp for VS Code"** (autor: Marp team).
3. Abrir cualquier archivo `.md` con el bloque `marp: true` en el encabezado.
4. La extension muestra una preview en tiempo real y permite exportar a HTML o PDF desde el menu de comandos (`Ctrl+Shift+P` > "Marp: Export Slide Deck").

### Opcion 2: CLI (para automatizar o usar desde terminal)

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
  reglas_presentacion_marp.md   <- guia de criterios de diseno y redaccion
  ejemplo/
    ejemplo.md                  <- archivo fuente de la presentacion de ejemplo
    ejemplo.html                <- exportacion (generada por Marp, no editar a mano)
    static/
      imagen.jpg                <- imagenes descargadas localmente
```

La convencion es una carpeta por presentacion (por ejemplo `/clase1/`, `/clase2/`), con una subcarpeta `/static/` dentro o en el nivel superior del proyecto para los recursos visuales.

---

## El encabezado del archivo (frontmatter)

Todo archivo `.md` de Marp empieza con un bloque YAML delimitado por `---`. Este bloque define los parametros globales y el CSS de la presentacion:

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
- `paginate: true`: agrega numeros de pagina automaticamente.
- `size: 16:9`: formato widescreen, el mas comun para proyectores.
- `style`: bloque de CSS puro que se aplica a todas las diapositivas.

---

## Como se estructura una diapositiva

Cada diapositiva es una seccion de Markdown separada por `---`:

```markdown
## Titulo de la diapositiva

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

Las clases `lead` y `portada` (u otras que definas en el CSS) permiten darle un estilo diferente a slides especificas sin afectar al resto.

---

## Sintaxis de imagenes en Marp

Marp extiende la sintaxis estandar de Markdown para controlar la ubicacion y el tamano de las imagenes.

| Sintaxis | Resultado |
|----------|-----------|
| `![bg right:40%](ruta.jpg)` | Imagen lateral derecha, ocupa el 40% del ancho |
| `![bg left:35%](ruta.jpg)` | Imagen lateral izquierda |
| `![bg](ruta.jpg)` | Imagen de fondo completo |
| `![w:600px](ruta.jpg)` | Imagen centrada con ancho fijo |

Las rutas deben ser relativas al archivo `.md`. Siempre usar imagenes descargadas localmente, nunca URLs externas: durante una clase, la conexion puede fallar.

---

## HTML embebido para componentes visuales

Marp permite usar HTML dentro del Markdown. Esto habilita componentes que no tienen equivalente en Markdown puro.

### Caja de ejemplo o prompt

```html
<div class="demo-box">
  <p><strong>Texto introductorio:</strong></p>
  <span class="prompt-text">
Contenido en fuente monospace.
Preserva los saltos de linea.
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

Estos componentes requieren que las clases CSS correspondientes esten definidas en el bloque `style` del frontmatter.

---

## Criterios de diseno y redaccion

El archivo `reglas_presentacion_marp.md` en este repositorio funciona como guia de criterios. Cubre:

- Paleta de colores, tipografia y margenes
- Densidad de contenido por diapositiva
- Uso de tablas, imagenes y componentes HTML
- Tono y variante del idioma
- Organizacion de archivos

Ese archivo esta pensado para copiarse al inicio de una conversacion con una IA antes de pedirle que redacte una clase nueva. De esa manera, la IA adopta los criterios desde el primer intento sin necesidad de corregirla diapositiva por diapositiva.

---

## Workflow tipico

1. Definir el tema y la estructura de la clase (puede hacerse con una IA).
2. Pedirle a la IA que genere el archivo `.md` completo, pasandole primero el contenido de `reglas_presentacion_marp.md`.
3. Revisar y ajustar el `.md` en VS Code con la preview de Marp activa.
4. Descargar las imagenes necesarias a la carpeta `/static/` local.
5. Exportar a HTML con la extension de VS Code o con el CLI.
6. Presentar desde el HTML (no necesita internet ni software especial en el equipo donde se presenta).

---

## Ejemplo incluido

La carpeta `/ejemplo/` contiene una presentacion de muestra sobre un tema neutro. Muestra todas las funcionalidades: portada con imagen lateral, slides de viñetas, tabla, blockquote, caja de codigo, diagrama de flujo y slide de cierre.

Para verla: abrir `ejemplo/ejemplo.md` en VS Code con la extension Marp instalada, o exportarla a HTML con el CLI.
