# Coffea | Landing Page

Landing page estática de una sola página para la cafetería ficticia **Coffea**, construida solo con **HTML5 semántico y CSS3** (sin JavaScript, frameworks ni preprocesadores).

**Trabajo Práctico 4 · Diseño UX-UI · Licenciatura en Sistemas de Información · FCyT, Sede Concepción del Uruguay · 2026**

| | |
|---|---|
| **Autor/a** | Sofia Orellana |
| **Repositorio** | https://github.com/sofia-orellana/coffea-landing |
| **Sitio en producción** | [(https://tp-uiux.netlify.app)](https://tp-uiux.netlify.app) |
| **Diseño de referencia** | *Coffea, Free Responsive Coffee Shop Website Template* (Figma Community) |
| **Documento de requisitos** | `TP4_PRD_Landing_Coffea.pdf` |

---

## 1. Descripción

La página reproduce el diseño de Figma (frame de 1920 px) y propone las versiones tablet y mobile, que el diseño original no incluye. Tiene 9 secciones:

1. Header / navegación
2. Hero
3. Categorías
4. Our Special Coffee (carrusel)
5. Our Special Dessert (carrusel)
6. CTA de granos de café
7. Testimonios
8. Newsletter
9. Footer

Toda la interacción (hover, foco, carruseles, menú mobile, favoritos y validación del formulario) se resuelve solo con CSS.

## 2. Estructura del proyecto

```
coffea-landing/
├── index.html
├── 404.html
├── netlify.toml
├── README.md
├── css/
│   ├── main.css            # orden de @layer + @import de las capas
│   ├── tokens.css          # design tokens (custom properties)
│   ├── base.css            # reset, tipografía base, :focus-visible, skip link
│   ├── layout.css          # .container, franjas, títulos de sección
│   ├── utilities.css       # .visually-hidden, hover compartido de botones
│   └── components/
│       ├── header.css
│       ├── hero.css
│       ├── categories.css
│       ├── product-card.css
│       ├── carousel.css
│       ├── promo.css
│       ├── testimonial-card.css
│       ├── newsletter.css
│       └── footer.css
└── assets/
    ├── img/                # fotos (hero, productos, promo, newsletter, avatares)
    └── icons/              # SVG (búsqueda, corazón, flechas, redes, etc.)
```

## 3. Convenciones

- **BEM:** `.product-card`, `.product-card__title`, `.product-card--featured`.
- **Sin valores sueltos:** color, fuente, radio y espaciado salen de `css/tokens.css`.
- **Mobile-first:** estilos base para 360 px y `@media (min-width: …)` hacia arriba.
- **Capas:** `@layer tokens, base, layout, components, utilities`, para controlar la cascada sin `!important`.
- **Unidades:** `rem` para tipografía y espacios; `clamp()` para títulos fluidos.
- **Layout:** Flexbox y Grid. `position: absolute` solo para superposiciones (header sobre el hero, corazón sobre la imagen, flechas del carrusel).

### Breakpoints

| Nombre | Rango | Contenedor |
|---|---|---|
| base | 360–767 px | 100 % − 2 × 16 px |
| md | ≥ 768 px | 100 % − 2 × 32 px |
| lg | ≥ 1024 px | 100 % − 2 × 48 px |
| xl | ≥ 1440 px | 1444 px centrado (diseño original) |

## 4. Cómo levantar el proyecto en local

No hay build ni dependencias. Opciones:

```bash
# 1. Clonar
git clone https://github.com/sofia-orellana/coffea-landing.git
cd coffea-landing

# 2. Servir la carpeta (cualquiera de las dos)
python3 -m http.server 8000      # luego abrir http://localhost:8000
npx serve .
```

También funciona con la extensión *Live Server* de VS Code.

## 5. Decisiones de implementación

| Tema | Decisión |
|---|---|
| **Menú mobile** | Se implementó con un checkbox oculto + `<label>` en lugar de `<details>`/`<summary>`. Un `<details>` cerrado oculta su contenido y no puede mostrarse como nav horizontal en desktop de forma compatible con Safari 16 y Firefox. Sigue siendo CSS puro y accesible por teclado. |
| **Carrusel sin JS** | `overflow-x` con `scroll-snap`. Las flechas (visibles desde 1024 px) son anclas a la primera y última card. En mobile y tablet se desliza con swipe nativo. |
| **Favoritos** | `<input type="checkbox">` + `<label>` con `:checked`. Es un estado solo visual, no se guarda. |
| **Hover de categorías** | Los íconos son `<img>`, por lo que no pueden cambiar de color. Cambia el color del texto y se oscurece el ícono con `filter`. |
| **Newsletter** | Validación nativa del navegador (`type="email" required`, `:user-invalid`). El `<form>` apunta a `action="#"`: no hay envío real. |
| **Typos del Figma** | Corregidos en el HTML ("get", "Our story", "INFORMATION", "Plans & pricing", etc.). La marca se escribe **Coffea** en header y footer. |
| **Contenido placeholder** | Los textos de las cards, los testimonios y el párrafo del hero son placeholders, igual que en el diseño. |
| **Idioma** | `lang="en"`, porque el copy del diseño está en inglés. |

## 6. Imágenes

- Las fotos se exportaron desde Figma y se redimensionaron y comprimieron para cumplir el límite de peso (≤ 1,5 MB en la primera carga).
- Las imágenes con transparencia (mano con granos, granos, avatares) están en WebP; el hero y las fotos de producto, en JPG.
- Las imágenes decorativas usan `alt=""`; las fotos de producto tienen `alt` descriptivo.
- El hero usa `fetchpriority="high"`; el resto, `loading="lazy"` y `decoding="async"`.
- **Licencia:** las fotos provienen de un template de Figma Community y algunas pueden ser de stock. Antes de un uso real hay que confirmar su licencia o reemplazarlas por imágenes propias.
- Las fotos de la sección *Dessert* son [temporales / copias de las de café: completar según corresponda].

## 7. Accesibilidad

- Skip link, landmarks (`header`, `nav`, `main`, `footer`) y un único `<h1>`.
- Foco visible en todo elemento interactivo (`:focus-visible`).
- Botones solo-ícono con nombre accesible (`aria-label`).
- Rating de testimonios con `role="img"` y `aria-label`.
- Áreas táctiles de al menos 44 × 44 px en mobile y tablet.
- `prefers-reduced-motion` respetado.

## 8. Despliegue (Netlify)

El sitio se publica como sitio estático con deploy continuo desde GitHub.

| Ajuste | Valor |
|---|---|
| Rama de producción | `main` |
| Build command | *(vacío)* |
| Publish directory | `.` |
| Deploy Previews | Uno por cada Pull Request |
| HTTPS | Automático (certificado de Netlify) |

`netlify.toml` define el directorio de publicación, los headers de seguridad (`X-Content-Type-Options`, `X-Frame-Options`, `Referrer-Policy`) y el caché de `css/` y `assets/`.

> **Caché `immutable`:** `css/` y `assets/` se cachean por un año. Si se modifica un archivo, hay que renombrarlo con versión (por ejemplo `main.v2.css`) y actualizar la referencia, o el navegador no lo vuelve a descargar.

## 9. Flujo de trabajo

1. Una rama por fase (`fase-3-responsive`, `fase-4-interacciones`, etc.).
2. Pull Request hacia `main` y revisión en el Deploy Preview.
3. Merge a `main` cuando la fase cumple su criterio de salida.

## 10. Resultados de calidad

Medidos sobre la URL de producción de Netlify.

| Métrica | Umbral | Resultado |
|---|---|---|
| Lighthouse Performance (mobile) | ≥ 90 | [completar] |
| Lighthouse Accessibility | ≥ 95 | [completar] |
| Lighthouse Best Practices | ≥ 95 | [completar] |
| Lighthouse SEO | ≥ 95 | [completar] |
| Validación HTML (W3C) | 0 errores | [completar] |
| Validación CSS (W3C) | 0 errores | [completar] |
| Peso total de la primera carga | ≤ 1,5 MB | [completar] |
| Scroll horizontal entre 360 y 1920 px | Ninguno | [completar] |

## 11. Definition of Done

- [ ] Las 9 secciones implementadas y revisadas contra el Figma
- [ ] 0 errores en los validadores HTML y CSS del W3C
- [ ] Lighthouse ≥ 90 en Performance y ≥ 95 en Accessibility, Best Practices y SEO
- [ ] Sin JavaScript en el proyecto
- [ ] Ningún valor de color, fuente o radio fuera de `tokens.css`
- [ ] Probado en Chrome, Firefox, Safari (macOS e iOS) y Samsung Internet
- [ ] README con estructura, convenciones y cómo levantar en local
- [ ] Sitio publicado en Netlify con deploy continuo desde `main`, HTTPS activo y Deploy Previews por PR

## 12. Créditos

- Diseño: *Coffea, Free Responsive Coffee Shop Website Template* (Figma Community).
- Tipografías: [Playfair Display](https://fonts.google.com/specimen/Playfair+Display), [Outfit](https://fonts.google.com/specimen/Outfit), [Poppins](https://fonts.google.com/specimen/Poppins) y [Reggae One](https://fonts.google.com/specimen/Reggae+One), vía Google Fonts.
