# SEO / GEO — Progreso ipaf.cl

Responsable: Bastián · Última actualización: 2026-09-21
Alcance de este repo: **solo ipaf.cl** (sitio de una página: `index.html` + `styles.css`).
Los otros sitios del ecosistema (motorman.cl, motormaq.cl, yanmaq.cl, motoreskubota.cl, mtq.cl) viven en otros repos; ver "Hallazgos del ecosistema" al final.

| # | Acción | Estado | Qué se hizo / qué falta |
|---|--------|--------|-------------------------|
| 1 | Dominio único 301 + canonical | ✅ código · ⏳ deploy | `.htaccess`: `www.ipaf.cl` → `https://ipaf.cl` (301), http→https, `/index.html` → `/`. Canonical `https://ipaf.cl/` (ya estaba). **Hoy en producción `https://www.ipaf.cl` responde 200 (duplicado)**: se corrige al subir `.htaccess`. |
| 2 | Meta description única ~155 | ✅ | 154 caracteres, con keyword + categorías + ubicación. Title, OG y Twitter actualizados. |
| 3 | JSON-LD LocalBusiness / Service / FAQPage | ✅ | `@graph` con `EducationalOrganization`+`LocalBusiness`, `Service` (con catálogo de ofertas), 4 `Course`, `WebSite`, `WebPage`. `FAQPage` ahora con las **6** preguntas visibles (antes 5). Se eliminó el Breadcrumb que apuntaba a otro dominio (inválido). No se usa `Product` porque ipaf vende cursos (Service/Course es lo correcto). |
| 4 | sitemap.xml + envío | ✅ archivo · ⏳ envío | `sitemap.xml` con imágenes. **Pendiente manual:** enviarlo en Google Search Console y Bing Webmaster Tools (hoy `/sitemap.xml` da 404 en producción). |
| 5 | robots.txt con bots IA | ✅ | Permite explícitamente OAI-SearchBot, ChatGPT-User, Claude-SearchBot, Claude-User, PerplexityBot, Perplexity-User. **Postura entrenamiento: PERMITIR** GPTBot, ClaudeBot, Google-Extended, Applebot-Extended, CCBot (queremos que los modelos conozcan la marca). Confirmar con jefatura; para bloquear, cambiar a `Disallow: /`. ⚠️ Revisar que en Cloudflare esté **desactivado** "Block AI bots / AI Scrapers", o anulará este robots.txt. |
| 6 | Perfil de Negocio de Google | ⏳ manual | No es código. Verificar ficha "Motorman — Centro de Formación IPAF": categoría "Centro de formación", dirección Río Palena 9686, tel. +56 9 6531 5200, web `https://ipaf.cl/`, horario L–V 9–18, fotos de plataformas/curso. NAP debe coincidir exactamente con el schema. |
| 7 | Core Web Vitals (webp, lazy) | ✅ | Todas las imágenes a WebP: ~5,5 MB → ~0,4 MB (banner móvil 1,2 MB PNG → 46 KB; 3A/3B de 5000 px → 900 px). `width`/`height` en todas las `<img>` (evita CLS), `loading="lazy"` fuera del hero, `fetchpriority="high"` + preload WebP en hero (LCP), video `preload="none"`, caché 1 año y gzip en `.htaccess`. Favicons 32/192 px (antes PNG de 2138 px). **Pendiente:** medir en PageSpeed Insights después del deploy. |
| 8 | Contenido / guías long-tail | 📝 evaluado | Propuesta abajo. Requiere redacción y decisión de negocio. |
| 9 | llms.txt | ✅ | `/llms.txt` con datos clave, cursos, secciones y ecosistema. Enlazado desde `<head>`. |
| 10 | Organization schema + sameAs | ✅ | `Organization` Motorman con logo, dirección, teléfono, email y `sameAs` a Facebook, Instagram, LinkedIn, TikTok (tomados de motorman.cl) + sitios hermanos. Además `subOrganization` describiendo cada marca. El centro IPAF enlaza a Motorman vía `parentOrganization`. Footer con enlaces visibles al ecosistema. |
| 11 | Jerarquía H1/H2/H3 | ✅ | 1 solo H1. H2 genéricos reemplazados: "Resolvemos tus dudas" → "Preguntas Frecuentes sobre Cursos IPAF", "Contáctanos" → "Contacto Centro IPAF Motorman", "Beneficios Exclusivos" → "Beneficios del Curso IPAF en Motorman", "Ofertas por Volumen" → "Descuentos por Grupo en Cursos IPAF", etc. H3 de cursos incluyen "Curso IPAF Categoría 1A…" (texto accesible). |
| 12 | URLs sin conectores | ✅ | Sitio de 1 URL (`/`). Se normalizaron rutas de recursos: sin espacios, minúsculas, descriptivas (`img/cursos/curso-ipaf-categoria-1a.webp`, `video/formacion-ipaf-plataforma-elevadora.mp4`…). Redirecciones 301 de rutas antiguas en `.htaccess`. |

Otros arreglos encontrados en el camino:
- `og:image` y el `logo` del schema apuntaban a archivos inexistentes → corregido (nueva imagen OG 1200×630).
- Enlaces de WhatsApp con espacios sin codificar → codificados, con `rel="noopener"`.
- Dirección del footer era `href="#"` → ahora abre Google Maps.

## Pendientes manuales (fuera del código)
1. Subir cambios a producción (incluye `.htaccess`, `robots.txt`, `sitemap.xml`, `llms.txt`, carpeta `img/` nueva).
2. Probar: `curl -I https://www.ipaf.cl` debe devolver `301` → `https://ipaf.cl/`.
3. Search Console + Bing Webmaster: agregar propiedad, enviar `https://ipaf.cl/sitemap.xml`, pedir indexación.
4. Validar schema en https://search.google.com/test/rich-results y https://validator.schema.org.
5. Cloudflare: desactivar bloqueo de bots IA si está activo.
6. Perfil de Negocio de Google (punto 6).
7. El video `video/formacion-ipaf-plataforma-elevadora.mp4` sigue siendo un placeholder de 0 bytes.

## Punto 8 — Propuesta de guías long-tail
Crear una sección `/guias/` con páginas cortas y concretas (URLs sin conectores):
- `/guias/tarjeta-pal-renovacion` — cómo y cuándo renovar la Tarjeta PAL.
- `/guias/categorias-ipaf-diferencias` — 1A vs 1B vs 3A vs 3B con tabla comparativa.
- `/guias/plataforma-tijera-vs-brazo-articulado` — cuál elegir según la obra.
- `/guias/requisitos-operador-plataforma-elevadora-chile` — normativa y requisitos en Chile.
- `/guias/app-epal` — uso de la licencia digital ePAL.
Cada una con H1 único, FAQPage propio, enlace a `/#cursos` y a Motorman. Requiere pasar el sitio de 1 página a varias (agregar al sitemap y a llms.txt).

## Hallazgos del ecosistema (revisado 2026-09-21)
| Sitio | Dominio canónico hoy | Problema |
|-------|----------------------|----------|
| motorman.cl | `https://www.motorman.cl` | OK (sin www → 301 a www) |
| motormaq.cl | `https://motormaq.cl` | OK (www → 301 a sin www) |
| yanmaq.cl | — | ❌ www y sin www responden 200 (duplicado) |
| motoreskubota.cl | — | ❌ www y sin www responden 200 (duplicado); el `<title>` dice "Motorman Chile" en vez de la marca |
| mtq.cl | — | ❌ no responde (timeout) |
| ipaf.cl | `https://ipaf.cl` | ❌ hoy duplicado → corregido con `.htaccess` (falta deploy) |
