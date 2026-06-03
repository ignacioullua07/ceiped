# CEIPeD · Sitio web

Sitio del **Centro de Estudios Interdisciplinarios para el Desarrollo (CEIPeD)**.
Construido con [Eleventy](https://www.11ty.dev/) (generador estático) + [Decap CMS](https://decapcms.org/)
para que el equipo cargue contenido sin tocar código.

---

## Correr en tu computadora

Necesitás [Node.js](https://nodejs.org/) (versión 18 o superior).

```bash
npm install      # instala las dependencias (una sola vez)
npm start        # levanta el sitio en http://localhost:8080
```

Para generar la versión final (carpeta `_site/`):

```bash
npm run build
```

---

## Estructura del proyecto

```
ceiped-site/
├─ .eleventy.js            Configuración de Eleventy (no hace falta tocarla)
├─ src/
│  ├─ _data/site.js        Nombre, tagline, navegación del sitio
│  ├─ _includes/           Plantillas: base, masthead, footer, artículo,
│  │                        área, programa, perfil
│  ├─ assets/
│  │  ├─ styles.css        Todos los estilos
│  │  ├─ logo.png
│  │  └─ uploads/          Imágenes que sube el equipo desde el panel
│  ├─ admin/               Panel de contenidos (Decap CMS)
│  │  ├─ index.html
│  │  └─ config.yml        Modelo de contenido del panel
│  ├─ content/             ← EL CONTENIDO
│  │  ├─ publicaciones/    Artículos (.md)
│  │  ├─ equipo/           Personas (.md)
│  │  ├─ areas/            Áreas de investigación (.md)
│  │  └─ programas/        Programas (.md)
│  ├─ index.njk            Home
│  ├─ publicaciones.njk    Listado de publicaciones
│  ├─ equipo.njk           Equipo
│  └─ nosotros.njk         Nosotros
```

Cada artículo, persona, área y programa es un archivo en `src/content/`.
El panel `/admin` simplemente crea y edita esos archivos por vos.

---

## Publicar el sitio (de cero a online)

El flujo recomendado es **GitHub + Cloudflare Pages + DecapBridge** (todo gratis).

1. **Subí el proyecto a un repositorio de GitHub** (por ejemplo `tu-usuario/ceiped-web`).
2. **Conectá el repo a Cloudflare Pages** con esta configuración de build:
   - *Build command:* `npm run build`
   - *Output directory:* `_site`
3. **Activá el panel de edición (DecapBridge):** creá un sitio en
   [decapbridge.com](https://decapbridge.com), te da un `SITE-ID`, y completás
   los tres valores marcados en `src/admin/config.yml`:
   - `repo:` → tu repositorio (`tu-usuario/ceiped-web`)
   - `identity_url:` → la URL que te da DecapBridge
   - `gateway_url:` → la URL que te da DecapBridge
4. Listo: tu equipo entra a `tusitio.org/admin` con email y contraseña
   (no necesitan cuenta de GitHub) y publica desde ahí.

> La guía visual completa está en **`Guía CMS - CEIPeD.html`** (sección
> "De cero a publicando").

---

## Cargar contenido

- **Imágenes** (portadas, fotos del equipo): se suben desde el panel y quedan en
  `src/assets/uploads/`. Mientras no haya foto, el sitio muestra un placeholder
  con rayas — es esperado.
- **Áreas y autores se conectan por relación:** al crear una publicación elegís
  el área y el autor de una lista; el sitio arma solo los listados por área,
  las publicaciones de cada persona y los relacionados.
- **Destacar en el Home:** marcá `destacado` en una publicación para que ocupe
  el lugar principal.

---

## Lo que falta para salir a producción

Esto ya no es programación — son pasos de puesta en marcha y carga:

- [ ] Crear el repositorio en GitHub y subir `ceiped-site/`.
- [ ] Conectar Cloudflare Pages (build `npm run build`, salida `_site`).
- [ ] Crear el sitio en DecapBridge y completar los 3 valores de `config.yml`.
- [ ] Subir el logo definitivo y las fotos reales (portadas + equipo).
- [ ] Revisar/completar los textos de las publicaciones de ejemplo.
- [ ] Conectar el formulario de newsletter a un proveedor real (hoy es visual).
