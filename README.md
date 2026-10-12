# Coffea Landing

Landing page estática de la cafetería ficticia **Coffea**. HTML5 semántico + CSS3, sin JavaScript, frameworks ni preprocesadores.
TP4 de Diseño UX-UI (Lic. en Sistemas de Información, FCyT, 2026). Diseño de referencia: *Coffea, Free Responsive Coffee Shop Website Template* (Figma Community).

## Estructura

```
coffea-landing/
├── index.html
├── 404.html
├── netlify.toml
├── css/
│   ├── main.css        # orden de @layer + @import
│   ├── tokens.css      # custom properties (colores, fuentes, radios, espacios)
│   ├── base.css        # reset, tipografía base, :focus-visible
│   ├── layout.css      # .container, franjas (pendiente)
│   ├── components/     # header, hero, categories, product-card, carousel,
│   │                   # promo, testimonial-card, newsletter, footer (pendiente)
│   └── utilities.css   # .visually-hidden (pendiente)
└── assets/
    ├── img/            # fotos (AVIF/WebP + fallback JPG)
    ├── icons/          # SVG optimizados
    └── fonts/          # opcional
```

## Convenciones

- Nomenclatura BEM: `.product-card`, `.product-card__title`, `.product-card--featured`.
- Sin valores sueltos: color, fuente, radio y espaciado salen de `tokens.css`.
- Mobile-first: estilos base para 360 px y `@media (min-width: ...)` hacia arriba.
- Capas: `@layer tokens, base, layout, components, utilities`.
- Toda la interacción (hover, foco, carruseles, menú, favoritos) se resuelve solo con CSS.

## Levantar en local

No hay build. Abrí `index.html` en el navegador o serví la carpeta:

```bash
python3 -m http.server 8000
# http://localhost:8000
```

## Despliegue (Netlify)

- Repositorio conectado a Netlify; la rama `main` publica a producción.
- Cada Pull Request genera un Deploy Preview.
- Build command: vacío. Publish directory: `.`
- `netlify.toml` define headers de seguridad y caché.

> **Caché `immutable`:** `css/` y `assets/` se cachean un año. Si cambiás un archivo, renombralo con versión (por ejemplo `main.v2.css`) y actualizá la referencia, o el navegador no lo vuelve a descargar.

## Flujo de trabajo

1. Una rama por fase (`fase-2-header-hero`, `fase-3-responsive`, ...).
2. Pull Request hacia `main` y revisión en el Deploy Preview.
3. Merge a `main` cuando la fase cumple su criterio de salida.

## Pendientes

- [ ] Confirmar licencia de las fotos del template o reemplazarlas
- [ ] Confirmar idioma final (`lang`) y moneda
- [ ] Extraer `--color-star` del SVG de estrellas
- [ ] Fotos reales de postres