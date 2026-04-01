---
marp: true
theme: default
paginate: true
size: 16:9
style: |
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

  section.portada {
    justify-content: flex-end;
    padding-bottom: 100px;
  }

  section.portada h1 {
    font-size: 52px;
    border: none;
  }

  section.portada h2 {
    font-size: 30px;
    color: #4a5568;
  }

  .demo-box {
    background-color: #ffffff;
    border: 1px solid #cbd5e0;
    border-radius: 8px;
    padding: 20px;
    margin-top: 20px;
    box-shadow: 0 4px 6px rgba(0,0,0,0.05);
  }

  .prompt-text {
    font-family: monospace;
    color: #1a202c;
    background-color: #e2e8f0;
    padding: 12px;
    border-radius: 6px;
    display: block;
    margin-top: 10px;
    white-space: pre-wrap;
    font-size: 1em;
  }

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
---

<!-- _class: portada -->

# Control de versiones con Git
## Conceptos fundamentales

![bg](static/portada.jpg)

---

# Que es el control de versiones

El control de versiones es un sistema que registra los cambios de un archivo o conjunto de archivos a lo largo del tiempo.

- Permite recuperar versiones anteriores de cualquier archivo
- Registra quien hizo cada cambio y cuando
- Facilita el trabajo en equipo sobre los mismos archivos
- Es la base del desarrollo de software colaborativo

---

## Por que usar Git

Git es el sistema de control de versiones mas usado en el mundo. Es local, rapido y no necesita conexion para la mayoria de las operaciones.

![bg right:40%](static/git_logo.jpg)

- Funciona offline: el historial vive en tu maquina
- Cada copia del repositorio es un backup completo
- Es el estandar de la industria desde hace mas de 15 anos

---

## Los tres estados de Git

Todo archivo en un repositorio Git puede estar en uno de estos tres estados:

- **Modificado:** el archivo cambio pero Git todavia no sabe nada al respecto
- **Preparado (staged):** marcaste el cambio para incluirlo en el proximo commit
- **Confirmado (committed):** el cambio quedo registrado en el historial local

---

## El flujo de trabajo basico

<div class="diagram">
  <div class="box">Modificar<br>archivos</div>
  <div class="arrow">→</div>
  <div class="box accent">git add<br>(staging)</div>
  <div class="arrow">→</div>
  <div class="box">git commit<br>(historial)</div>
  <div class="arrow">→</div>
  <div class="box">git push<br>(remoto)</div>
</div>

Cada `commit` es una fotografia del proyecto en un momento dado. El mensaje del commit describe que cambio y por que.

---

## Comandos esenciales

> git init

Inicializa un repositorio Git en la carpeta actual.

> git add nombre_archivo.txt

Agrega un archivo al area de staging.

> git commit -m "descripcion del cambio"

Confirma los cambios en el historial.

---

## Ramas (branches)

Una rama es una linea de desarrollo independiente. Permite trabajar en una nueva funcionalidad sin afectar el codigo principal.

- La rama principal se llama convencionalmente `main` o `master`
- Crear una rama: `git branch nombre-rama`
- Cambiar a una rama: `git checkout nombre-rama`
- Fusionar una rama en `main`: `git merge nombre-rama`

---

## Comparacion de flujos de trabajo

| Escenario | Sin control de versiones | Con Git |
|-----------|--------------------------|---------|
| Revertir un error | Imposible si no hay backup | `git revert` o `git checkout` |
| Trabajar en equipo | Archivos que se pisan entre si | Ramas y merges controlados |
| Auditar cambios | No hay registro | `git log` muestra el historial completo |
| Probar algo nuevo | Copiar carpeta manualmente | Crear una rama y experimentar |

---

## Como escribir un buen mensaje de commit

El mensaje de commit es el registro permanente de que cambio y por que. Un mensaje vago inutiliza el historial.

<div class="demo-box">
  <p><strong>Mensaje poco util:</strong></p>
  <span class="prompt-text">arreglos varios</span>
</div>

<div class="demo-box">
  <p><strong>Mensaje util:</strong></p>
  <span class="prompt-text">Corregir calculo de descuento para usuarios con membresia anual

El descuento se aplicaba sobre el precio sin impuestos en lugar
del precio final. Esto generaba un cobro incorrecto en checkout.</span>
</div>

---

## Repositorios remotos

Un repositorio remoto es una copia del proyecto alojada en un servidor (GitHub, GitLab, Bitbucket, etc.). Sirve como punto de sincronizacion entre varios colaboradores.

![bg left:35%](static/github.jpg)

- `git remote add origin URL`: conecta el repo local con el remoto
- `git push`: sube los commits locales al servidor
- `git pull`: baja y fusiona los cambios del servidor

---

<!-- _class: lead -->

# Proximos pasos

Practicar es la unica forma de internalizar estos comandos.

**Para empezar hoy:**
Instalar Git, crear una carpeta de prueba y hacer los primeros tres commits de cualquier proyecto propio.

### En la proxima clase:
- Resolucion de conflictos al fusionar ramas
- Uso de `.gitignore`
- Flujos de trabajo en equipo (pull requests)
