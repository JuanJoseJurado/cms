# Mi CMS - Sistema de Gestión de Contenido

Un CMS moderno y potente para crear y gestionar sitios web estáticos con plantillas personalizables y secciones dinámicas.

## 🚀 Características

- ✅ **Editor de contenido visual** con TinyMCE
- ✅ **Gestión de páginas** (crear, editar, eliminar)
- ✅ **Sistema de plantillas** con Handlebars
- ✅ **Secciones dinámicas** - 14+ tipos de secciones predefinidas
- ✅ **Constructor visual** - Arrastra y suelta secciones
- ✅ **Navegación dinámica** configurable
- ✅ **Exportación de sitio estático** completo
- ✅ **Diseño responsive** con Bootstrap 5
- ✅ **Base de datos SQLite** integrada
- ✅ **Panel de administración** intuitivo
- ✅ **Plantilla profesional** basada en Visible Template

## 📋 Requisitos

- Node.js 16+ 
- npm o yarn

## 🛠️ Instalación

1. **Clonar o descargar el proyecto**
```bash
cd mycms
```

2. **Instalar dependencias**
```bash
npm install
```

3. **Insertar datos de ejemplo** (opcional)
```bash
npm run seed
```

4. **Iniciar el servidor**
```bash
npm start
```

5. **Acceder al panel de administración**
```
http://localhost:3000/admin
```

## 📖 Uso

### Panel de Administración

El panel de administración te permite:

1. **Configurar el sitio**:
   - Título del sitio
   - Navegación (agregar/eliminar enlaces)
   - Footer
   - Meta tags SEO
   - **Restablecer tema**: el botón “Restablecer” de Configuración restablece los colores del tema a valores por defecto y los guarda automáticamente.
   - Inicialización del Admin al cargar el DOM (para asegurar que se carguen datos y eventos):
     ```javascript
     // Initialize CMS Admin when DOM is loaded
     if (!window.cmsAdmin) {
       document.addEventListener('DOMContentLoaded', () => {
         window.cmsAdmin = new CMSAdmin();
       });
     }
     ```

2. **Gestionar páginas**:
   - Crear páginas con contenido estático
   - Añadir secciones dinámicas a cualquier página
   - Editor visual TinyMCE para contenido rico
   - Configurar meta tags por página

3. **Constructor de secciones dinámicas**:
   - **14+ tipos de secciones** predefinidas
   - **Arrastra y suelta** para reordenar
   - **Editor visual** para cada sección
   - **Vista previa en tiempo real**

4. **Exportar el sitio**:
   - Genera un sitio estático completo
   - Incluye todas las páginas y recursos
   - Combina contenido estático y secciones dinámicas
   - Listo para subir a cualquier hosting

### Tipos de Secciones Dinámicas

#### 🎨 **Secciones de Presentación**
- **Hero/Banner** - Sección principal con imagen, título y botones de acción
- **About** - Sección acerca de con imagen y texto descriptivo
- **Call to Action (CTA)** - Llamadas a la acción con botones destacados

#### 📊 **Secciones de Contenido**
- **Stats** - Estadísticas con contadores animados e iconos
- **Services** - Servicios con iconos, títulos y descripciones
- **Features Overview** - Características principales con logros y tarjetas de funcionalidades
- **Additional Features** - Características adicionales con tarjetas de estado
- **Features Alt** - Características con pestañas interactivas
- **Text** - Secciones de texto puro con formato rico
- **Image + Text** - Combinación de imagen y texto en columnas

#### 🖼️ **Secciones Multimedia**
- **Portfolio** - Galería de trabajos con filtros por categoría
- **Gallery** - Galería de imágenes con lightbox
- **Testimonials** - Testimonios de clientes con sistema de calificación
- **Clients** - Logos de clientes con nombre, URL y texto alternativo

#### 👥 **Secciones Sociales**
- **Team** - Equipo con fotos, nombres, cargos y redes sociales
- **Contact** - Información de contacto con mapa y formulario
- **Newsletter** - Captura de emails con título, subtítulo, placeholder, botón, texto legal y acción del formulario

Nota: El botón “Restablecer” en Configuración vuelve a los colores por defecto (accent, background, heading, default) y guarda automáticamente en la configuración del sitio.

### Cómo Usar las Secciones Dinámicas

1. **Crear/Editar una página** en el panel de administración
2. **Hacer clic en "Add Section"** para añadir una nueva sección
3. **Seleccionar el tipo** de sección deseada
4. **Configurar el contenido** usando el editor visual
5. **Reordenar secciones** arrastrando y soltando
6. **Vista previa** para ver el resultado
7. **Guardar** y **exportar** el sitio

### API Endpoints

#### Configuración del Sitio
- `GET /api/site` - Obtener configuración del sitio
- `PUT /api/site` - Actualizar configuración del sitio
- `POST /api/export` - Exportar sitio (también disponible como sección Exportar en el admin)

#### Gestión de Páginas
- `GET /api/pages` - Listar todas las páginas
- `POST /api/pages` - Crear nueva página
- `GET /api/pages/:id` - Obtener página específica
- `PUT /api/pages/:id` - Actualizar página
- `DELETE /api/pages/:id` - Eliminar página

#### Secciones Dinámicas
- `GET /api/pages/:id/sections` - Obtener secciones de una página
- `POST /api/pages/:id/sections` - Añadir nueva sección
- `PUT /api/pages/:id/sections/:sectionId` - Actualizar sección
- `DELETE /api/pages/:id/sections/:sectionId` - Eliminar sección
- `PUT /api/pages/:id/sections/reorder` - Reordenar secciones

#### Exportación
- `POST /api/export` - Exportar sitio completo con secciones dinámicas

## 🎨 Personalización

### Sistema de Plantillas

El CMS utiliza **Handlebars** como motor de plantillas con una arquitectura modular:

#### Plantillas Principales
- `base.hbs` - Plantilla base con HTML común, head, scripts
- `home.hbs` - Plantilla específica para la página de inicio
- `default.hbs` - Plantilla por defecto para páginas internas

#### Partials del Sistema
- `header.hbs` - Cabecera con navegación
- `footer.hbs` - Pie de página

#### Partials de Secciones Dinámicas
- `section-hero.hbs` - Sección hero/banner
- `section-about.hbs` - Sección acerca de
- `section-stats.hbs` - Sección de estadísticas
- `section-services.hbs` - Sección de servicios
- `section-features-overview.hbs` - Sección de características principales
- `section-additional-features.hbs` - Sección de características adicionales
- `section-features-alt.hbs` - Sección de características con pestañas
- `section-portfolio.hbs` - Sección de portafolio
- `section-team.hbs` - Sección de equipo
- `section-contact.hbs` - Sección de contacto
- `section-cta.hbs` - Sección call-to-action
- `section-pricing.hbs` - Sección de precios
- `section-faq.hbs` - Sección de preguntas frecuentes
- `section-text.hbs` - Sección de texto
- `section-image-text.hbs` - Sección imagen + texto
- `section-testimonials.hbs` - Sección de testimonios
- `section-gallery.hbs` - Sección de galería
- `section-clients.hbs` - Sección de clientes
- `section-newsletter.hbs` - Sección de newsletter

### Crear Nuevas Secciones

Para añadir un nuevo tipo de sección:

1. **Crear el partial** en `src/templates/partials/section-[nombre].hbs`
2. **Añadir el tipo** en las plantillas `home.hbs` y `default.hbs`:
   ```handlebars
   {{else if (eq type 'mi-seccion')}}
     {{> section-mi-seccion data=data}}
   ```
3. **Actualizar el admin** para incluir el nuevo tipo en el selector

### Estilos y Diseño

El CMS utiliza la plantilla **Visible** con:
- **Bootstrap 5** como framework CSS base
- **AOS (Animate On Scroll)** para animaciones
- **Swiper** para carruseles y sliders
- **GLightbox** para galerías de imágenes
- **PureCounter** para contadores animados
- **Isotope** para filtros de portafolio

#### Archivos de Estilos
- `public/assets/css/main.css` - Estilos principales de la plantilla
- `public/css/site.css` - Estilos personalizados del CMS

### Base de Datos

La base de datos SQLite se crea automáticamente en `data/cms.db` con las tablas:

#### Tabla `pages`
```sql
- id (INTEGER PRIMARY KEY)
- title (TEXT) - Título de la página
- slug (TEXT UNIQUE) - URL amigable
- content (TEXT) - Contenido HTML estático
- sections (TEXT) - JSON con secciones dinámicas
- meta_description (TEXT) - Meta descripción SEO
- meta_keywords (TEXT) - Meta keywords SEO
- created_at (DATETIME)
- updated_at (DATETIME)
```

#### Tabla `site_settings`
```sql
- key (TEXT PRIMARY KEY) - Clave de configuración
- value (TEXT) - Valor de configuración
```

#### Estructura de Secciones

Las secciones se almacenan como JSON en el campo `sections`:

```json
[
  {
    "id": 1,
    "type": "hero",
    "order": 0,
    "data": {
      "title": "Título del Hero",
      "subtitle": "Subtítulo",
      "description": "Descripción",
      "image": "ruta/imagen.jpg",
      "buttons": [...]
    }
  }
]
```

## 📝 Scripts Disponibles

```bash
npm start        # Iniciar servidor de producción
npm run dev      # Iniciar servidor de desarrollo (con nodemon)
npm run export   # Exportar sitio estático
npm run seed     # Insertar datos de ejemplo
```

## 📁 Estructura del Proyecto

```
mycms/
├── data/                    # Base de datos SQLite
│   └── cms.db              # Base de datos principal
├── public/                 # Archivos estáticos
│   ├── admin/             # Panel de administración
│   │   ├── admin.html     # Interfaz principal del admin
│   │   ├── admin.js       # Lógica del panel de administración
│   │   └── admin.css      # Estilos del admin
│   ├── assets/            # Recursos de la plantilla Visible
│   │   ├── css/          # Estilos de la plantilla
│   │   ├── js/           # Scripts de la plantilla
│   │   ├── img/          # Imágenes de la plantilla
│   │   └── vendor/       # Librerías externas
│   ├── admin/             # Panel de administración (servido en /admin)
│   │   ├── index.html     # Interfaz principal del admin
│   │   ├── admin.js       # Lógica del panel de administración
│   │   └── admin.css      # Estilos del admin
│   └── css/              # Estilos personalizados
│       └── site.css      # Estilos del CMS
├── scripts/               # Scripts de utilidad
│   └── seed.js           # Script para datos de ejemplo
├── src/                  # Código fuente del servidor
│   ├── routes/          # Rutas de la API
│   │   ├── pages.js     # API de páginas
│   │   ├── site.js      # API de configuración
│   │   └── export.js    # API de exportación
│   ├── templates/       # Sistema de plantillas Handlebars
│   │   ├── base.hbs     # Plantilla base
│   │   ├── home.hbs     # Plantilla de inicio
│   │   ├── default.hbs  # Plantilla por defecto
│   │   └── partials/    # Componentes reutilizables
│   │       ├── header.hbs           # Cabecera
│   │       ├── footer.hbs           # Pie de página
│   │       ├── section-hero.hbs     # Sección hero
│   │       ├── section-about.hbs    # Sección acerca de
│   │       ├── section-stats.hbs    # Sección estadísticas
│   │       ├── section-services.hbs # Sección servicios
│   │       ├── section-features-overview.hbs # Características principales
│   │       ├── section-additional-features.hbs # Características adicionales
│   │       ├── section-features-alt.hbs # Características con pestañas
│   │       ├── section-portfolio.hbs# Sección portafolio
│   │       ├── section-team.hbs     # Sección equipo
│   │       ├── section-contact.hbs  # Sección contacto
│   │       ├── section-cta.hbs      # Sección CTA
│   │       ├── section-pricing.hbs  # Sección precios
│   │       ├── section-faq.hbs      # Preguntas frecuentes
│   │       ├── section-text.hbs     # Sección texto
│   │       ├── section-image-text.hbs # Sección imagen+texto
│   │       ├── section-testimonials.hbs # Testimonios
│   │       └── section-gallery.hbs  # Galería
│   ├── db.js            # Configuración de base de datos
│   └── exporter.js      # Exportador de sitio estático
├── output/              # Sitio exportado (generado automáticamente)
├── package.json         # Dependencias y scripts
└── server.js           # Servidor principal Express
```

## 🌐 Despliegue

### Sitio Estático

1. Ejecutar `npm run export`
2. Subir el contenido de la carpeta `output/` a tu hosting
3. ¡Listo!

### CMS Completo

Para desplegar el CMS completo:

1. Subir todos los archivos a tu servidor
2. Instalar dependencias: `npm install`
3. Configurar variables de entorno si es necesario
4. Iniciar: `npm start`

## 🔧 Configuración Avanzada

### Variables de Entorno

```bash
PORT=3000                    # Puerto del servidor
NODE_ENV=production         # Entorno de ejecución
```

### Personalizar Colores y Estilos

La plantilla Visible utiliza variables CSS que puedes personalizar en `public/assets/css/main.css`:

```css
:root {
  /* Colores principales */
  --default-color: #212529;
  --heading-color: #040677;
  --accent-color: #1acc8d;
  --surface-color: #ffffff;
  --contrast-color: #ffffff;

  /* Colores de navegación */
  --nav-color: rgba(255, 255, 255, 0.5);
  --nav-hover-color: #1acc8d;
  --nav-mobile-background-color: #ffffff;
  --nav-dropdown-background-color: #ffffff;
  --nav-dropdown-color: #212529;
  --nav-dropdown-hover-color: #1acc8d;

  /* Tipografía */
  --default-font: "Roboto", system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial, "Noto Sans", "Liberation Sans", sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "Noto Color Emoji";
  --heading-font: "Mukta", sans-serif;
  --nav-font: "Abel", sans-serif;
}
```

### Configuración de Secciones

Cada tipo de sección tiene su propia estructura de datos. Ejemplos:

#### Sección Hero
```json
{
  "type": "hero",
  "data": {
    "subtitle": "Bienvenido a",
    "title": "Mi Empresa",
    "description": "Descripción de la empresa",
    "image": "assets/img/hero-bg.jpg",
    "buttons": [
      {
        "text": "Ver Servicios",
        "url": "#services",
        "class": "primary-btn"
      }
    ]
  }
}
```

#### Sección Stats
```json
{
  "type": "stats",
  "data": {
    "items": [
      {
        "icon": "bi bi-emoji-smile",
        "number": "232",
        "label": "Clientes Felices"
      }
    ]
  }
}
```

#### Sección Team
```json
{
  "type": "team",
  "data": {
    "sectionTitle": "Equipo",
    "title": "Nuestro Equipo",
    "subtitle": "Conoce a nuestro equipo profesional",
    "members": [
      {
        "name": "Juan Pérez",
        "position": "CEO & Fundador",
        "image": "assets/img/team/team-1.jpg",
        "bio": "Descripción del miembro",
        "social": {
          "twitter": "https://twitter.com/",
          "facebook": "https://facebook.com/",
          "instagram": "https://instagram.com/",
          "linkedin": "https://linkedin.com/"
        }
      }
    ]
  }
}
```

#### Sección Features Overview
```json
{
  "type": "features-overview",
  "data": {
    "subtitle": "Características Avanzadas",
    "title": "Soluciones Integrales",
    "description": "Descubre todas las características que ofrecemos",
    "mainTitle": "Marco de Trabajo Integrado",
    "paragraphs": [
      "Aprovechando tecnología de vanguardia proporcionamos la base para la excelencia operacional.",
      "Nuestra arquitectura robusta integra sistemas diversos, optimizando flujos de trabajo."
    ],
    "achievements": [
      {
        "icon": "bi-shield-check",
        "value": "99%",
        "label": "Uptime Garantizado"
      }
    ],
    "features": [
      [
        {
          "icon": "bi-shield-lock",
          "title": "Seguridad Avanzada",
          "description": "Protege tu sitio web con las últimas tecnologías de seguridad.",
          "status": "active",
          "statusText": "Activo",
          "primary": true,
          "delay": "200"
        }
      ]
    ]
  }
}
```

#### Sección Additional Features
```json
{
  "type": "additional-features",
  "data": {
    "features": [
      {
        "icon": "bi-palette",
        "title": "Diseño Personalizado",
        "description": "Creamos diseños únicos que reflejan la identidad de tu marca.",
        "status": "active",
        "statusIcon": "bi-check-circle",
        "statusText": "Disponible",
        "delay": "200"
      }
    ]
  }
}
```

## 🐛 Solución de Problemas

### El servidor no inicia
- Verificar que Node.js 16+ esté instalado
- Ejecutar `npm install` para instalar dependencias
- Verificar que el puerto 3000 esté disponible
- Revisar los logs en la consola para errores específicos

### Error en la exportación
- Verificar que existan páginas en la base de datos
- Ejecutar `npm run seed` para crear datos de ejemplo
- Verificar permisos de escritura en la carpeta del proyecto
- Comprobar que las plantillas Handlebars estén correctas

### Problemas con secciones dinámicas
- Verificar que el JSON de las secciones sea válido
- Comprobar que los partials de sección existan en `src/templates/partials/`
- Revisar que los helpers de Handlebars estén registrados correctamente
- Verificar que las imágenes referenciadas existan en `public/assets/img/`

### Problemas con la base de datos
- La base de datos se crea automáticamente en `data/cms.db`
- Si hay problemas, eliminar `data/cms.db` y reiniciar el servidor
- Ejecutar `npm run seed` para recrear datos de ejemplo

### Errores de plantillas
- Verificar sintaxis de Handlebars en los archivos `.hbs`
- Comprobar que los partials estén registrados correctamente
- Revisar que las variables de contexto estén disponibles

### Problemas de estilos
- Verificar que los archivos CSS estén en las rutas correctas
- Comprobar que Bootstrap 5 y las librerías de la plantilla se carguen
- Revisar la consola del navegador para errores de recursos

## 📄 Licencia

Este proyecto es de código abierto. Puedes usarlo y modificarlo libremente.

## 🚀 Características Técnicas

### Tecnologías Utilizadas

#### Backend
- **Node.js** - Entorno de ejecución
- **Express.js** - Framework web
- **SQLite** - Base de datos embebida
- **Handlebars** - Motor de plantillas

#### Frontend
- **Bootstrap 5** - Framework CSS
- **TinyMCE** - Editor WYSIWYG
- **AOS** - Animaciones on scroll
- **Swiper** - Carruseles y sliders
- **GLightbox** - Lightbox para imágenes
- **PureCounter** - Contadores animados
- **Isotope** - Filtros y layouts

#### Plantilla Base
- **Visible Template** - Plantilla profesional responsive
- **Bootstrap Icons** - Iconografía
- **Google Fonts** - Tipografías (Roboto, Mukta, Abel)

### Rendimiento y SEO

- ✅ **Sitios estáticos** generados para máximo rendimiento
- ✅ **Meta tags** configurables por página
- ✅ **URLs amigables** (slugs personalizables)
- ✅ **Responsive design** para todos los dispositivos
- ✅ **Optimización de imágenes** con lazy loading
- ✅ **Minificación** de CSS y JS en producción

### Seguridad

- ✅ **Sanitización** de contenido HTML
- ✅ **Validación** de datos de entrada
- ✅ **Protección CSRF** en formularios
- ✅ **Headers de seguridad** configurados

## 🆕 Nuevas Características Implementadas

### Secciones de Características Avanzadas

Se han implementado dos nuevas secciones especializadas para mostrar características y funcionalidades:

#### 🎯 **Features Overview**
- **Diseño dual**: Combina contenido textual con tarjetas de características
- **Badges de logros**: Muestra métricas importantes con iconos
- **Estados de funcionalidades**: Indica el estado de cada característica (activo, pendiente, programado)
- **Animaciones AOS**: Efectos de aparición suaves y escalonados
- **Layout responsivo**: Se adapta perfectamente a todos los dispositivos

#### 🔧 **Additional Features**
- **Tarjetas de características**: Diseño limpio con iconos, títulos y descripciones
- **Sistema de estados**: Tags de estado con colores diferenciados
- **Grid responsivo**: Layout de 3 columnas que se adapta a móviles
- **Efectos hover**: Animaciones suaves al pasar el cursor
- **Iconografía Bootstrap**: Amplia gama de iconos disponibles

### Mejoras en el Sistema

#### ✨ **Integración Completa**
- Las nuevas secciones se integran automáticamente en el panel de administración
- Soporte completo para exportación de sitios estáticos
- Compatibilidad con el sistema de plantillas Handlebars existente
- Estilos CSS optimizados que respetan el diseño original

#### 🎨 **Personalización Avanzada**
- Configuración flexible de contenido a través del admin
- Soporte para múltiples estados de características
- Personalización de iconos, colores y textos
- Animaciones configurables con delays personalizados

## 🤝 Contribuir

¡Las contribuciones son bienvenidas! Por favor:

1. **Fork** el proyecto
2. **Crea una rama** para tu feature (`git checkout -b feature/nueva-seccion`)
3. **Commit** tus cambios (`git commit -m 'Añadir nueva sección de testimonios'`)
4. **Push** a la rama (`git push origin feature/nueva-seccion`)
5. **Abre un Pull Request**

### Ideas para Contribuir

- 🎨 Nuevos tipos de secciones
- 🌐 Soporte para múltiples idiomas
- 📱 Mejoras en responsive design
- 🔧 Nuevas funcionalidades del admin
- 📚 Mejoras en documentación
- 🐛 Corrección de bugs

## 📞 Soporte

Si tienes problemas o preguntas:

1. **Revisa la documentación** completa
2. **Busca en Issues** existentes
3. **Crea un nuevo Issue** con detalles del problema
4. **Incluye logs** y pasos para reproducir el error

---

**¡Disfruta creando sitios web profesionales con tu CMS personalizado!** 🎉

### 🌟 ¿Te gusta el proyecto?

Si este CMS te ha sido útil, considera:
- ⭐ Darle una estrella al repositorio
- 🐛 Reportar bugs que encuentres
- 💡 Sugerir nuevas características
- 🤝 Contribuir con código
- 📢 Compartirlo con otros desarrolladores
