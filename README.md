# Mi CMS - Sistema de Gestión de Contenido

Un CMS ligero para crear y gestionar sitios estáticos con plantillas Handlebars y secciones dinámicas.

## 🚀 Características

- ✅ **Panel de administración** en `/admin`
- ✅ **Páginas**: crear, editar, eliminar, estado (publicada/borrador)
- ✅ **Secciones dinámicas** (14+ tipos) y contenido HTML con TinyMCE
- ✅ **Plantillas Handlebars**: `home`, `default` y parciales reutilizables
- ✅ **Exportación a sitio estático** a `output/`
- ✅ **Base de datos SQLite** con `better-sqlite3`
- ✅ **Tema Visible** con Bootstrap 5 y librerías de la plantilla
- ⚠️ **Clientes/Marcas**: sección temporalmente deshabilitada en el admin

## 📋 Requisitos

- Node.js 18+ (recomendado LTS). Versiones menores pueden fallar con `better-sqlite3@12`.
- npm o yarn

## 🛠️ Instalación

1. Instalar dependencias
```bash
npm install
```
2. (Opcional) Insertar datos de ejemplo
```bash
npm run seed
```
3. Iniciar el servidor
```bash
npm start
```
4. Abrir el panel de administración
```
http://localhost:3000/admin
```

Para desarrollo con recarga en caliente puedes usar:
```bash
# requiere nodemon instalado (global o dev)
npm i -D nodemon
npm run dev
```

## 📖 Uso

### Panel de Administración
- **Páginas**: crea/edita con título, slug, plantilla (`home` o `default`), estado y contenido HTML (TinyMCE).
- **Secciones**: añade tipos predefinidos. Reordena con botones «subir/bajar». El tipo "clients" está deshabilitado por estabilidad.
- **Configuración**: título del sitio, navegación, footer, contacto, redes y variables de tema.
- **Exportar**: genera el sitio estático (POST `/api/export`).

### Tipos de Secciones Disponibles
- 🎯 hero
- ℹ️ about
- 📊 stats
- ⚙️ services
- ⭐ features / features-overview / features-alt / additional-features
- 🎨 portfolio
- 👥 team
- 💬 testimonials
- 🖼️ gallery
- 🎯 cta
- 💰 pricing
- ❓ faq
- 📝 text
- 🖼️ image-text
- 📧 newsletter
- 🏢 clients (deshabilitada temporalmente en el editor; export elimina entradas inválidas)

## 🔌 API

- `GET /api/pages` — Lista páginas
- `POST /api/pages` — Crea página
- `GET /api/pages/:id` — Obtiene página
- `PUT /api/pages/:id` — Actualiza página
- `DELETE /api/pages/:id` — Elimina página
- `GET /api/site` — Obtiene configuración
- `PUT /api/site` — Guarda configuración del sitio (incluye `theme.variables` y claves `seo.*` si se envían)
- `POST /api/export` — Exporta el sitio estático a `output/`

## 🗄️ Base de Datos

Tablas creadas automáticamente en `data/cms.db`:

### pages
```sql
id INTEGER PRIMARY KEY AUTOINCREMENT,
slug TEXT UNIQUE NOT NULL,
title TEXT NOT NULL,
content_html TEXT NOT NULL,
template TEXT DEFAULT 'default',
meta TEXT DEFAULT '{}',            -- JSON serializado
sections TEXT DEFAULT '[]',        -- JSON serializado (array de secciones)
status TEXT DEFAULT 'published',
created_at TEXT NOT NULL,
updated_at TEXT NOT NULL
```

### site_settings
```sql
key TEXT PRIMARY KEY,
value TEXT -- JSON serializado
```

Estructura típica del campo `sections`:
```json
[
  {
    "id": 1,
    "type": "hero",
    "data": { "title": "Título", "subtitle": "Subtítulo" }
  }
]
```

## 🧩 Plantillas y Tema

- Motor: **Handlebars** con `src/templates/base.hbs` como layout principal.
- Plantillas: `src/templates/home.hbs`, `src/templates/default.hbs`.
- Parciales: en `src/templates/partials` (header, footer y secciones `section-*.hbs`).
- Tema Visible: assets en `public/assets` (Bootstrap, AOS, Swiper, GLightbox, PureCounter, Isotope).

### Variables de Tema (dinámicas)
`theme.variables` permite inyectar estilos CSS (custom properties) durante la exportación:
```json
{
  "accentColor": "#1acc8d",
  "backgroundColor": "#ffffff",
  "headingColor": "#040677",
  "defaultColor": "#212529",
  "fontSizeBase": "16"
}
```
Estas variables se incrustan como `<style id="theme-vars">` en el HTML exportado. También puedes editar `public/assets/css/main.css` para estilos del tema base y `public/css/site.css` para estilos del CMS.

## 🧪 Scripts Disponibles

```bash
npm start        # Iniciar servidor (producción)
npm run dev      # Iniciar servidor con nodemon (si está instalado)
npm run export   # Exportar sitio estático a output/
npm run seed     # Insertar datos de ejemplo
```

Scripts utilitarios (directorio `scripts/`):
- `export-all.js`
- `seed-data.js`
- `check-images.js`, `check-pages.js`
- `cleanup-sections.js`, `migrate-sections.js`, `update-sections.js`

## 📁 Estructura del Proyecto (real)
```
mycms/
├── data/
│   └── cms.db
├── public/
│   ├── admin/
│   │   ├── index.html
│   │   ├── admin.js
│   │   └── admin.css
│   ├── assets/
│   │   ├── css/ (main.css)
│   │   ├── js/
│   │   ├── img/
│   │   └── vendor/ (bootstrap, aos, swiper, glightbox, isotope, purecounter)
│   └── css/
│       └── site.css
├── scripts/
│   ├── export-all.js
│   ├── seed-data.js
│   ├── check-images.js
│   ├── check-pages.js
│   ├── cleanup-sections.js
│   ├── migrate-sections.js
│   └── update-sections.js
├── src/
│   ├── routes/
│   │   ├── admin.js         # sirve /admin
│   │   ├── api.pages.js     # CRUD de páginas
│   │   └── api.site.js      # configuración del sitio
│   ├── templates/
│   │   ├── base.hbs
│   │   ├── home.hbs
│   │   ├── default.hbs
│   │   └── partials/ (header, footer, section-*.hbs)
│   ├── db.js                # SQLite (better-sqlite3)
│   └── exporter.js          # Exportador a HTML estático
├── output/                  # Sitio exportado (generado)
├── server.js                # Servidor Express (ESM)
├── package.json
└── README.md
```

## 🌐 Despliegue

### Sitio Estático
1. Ejecuta `npm run export`.
2. Sube el contenido de `output/` a tu hosting.

### CMS Completo
1. Sube todo el proyecto al servidor.
2. `npm install`
3. `npm start`

## ⚠️ Limitaciones y Notas de la Versión

- **Clientes/Marcas**: el tipo `clients` está deshabilitado en el panel; el exportador elimina secciones vacías de este tipo.
- **SEO**: el panel ya guarda SEO con `PUT /api/site`. Puedes enviar `seo.defaultTitle`, `seo.defaultDescription`, `seo.defaultKeywords`.
- **Restablecer tema**: el botón de "restablecer colores" está implementado; restablece los colores por defecto y guarda la configuración.
- **Arrastrar y soltar**: el reordenamiento de secciones se realiza con controles de subir/bajar, no con drag & drop.
