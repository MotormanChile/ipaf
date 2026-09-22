# SEO / GEO — Progreso ipaf.cl

Responsable: Bastián · Última actualización: 2026-09-21
Alcance de este repo: **solo ipaf.cl** (sitio de una página: `index.html` + `styles.css`).
Los otros sitios del ecosistema (motorman.cl, motormaq.cl, yanmaq.cl, motoreskubota.cl, mtq.cl) viven en otros repos; ver "Hallazgos del ecosistema" al final.

| # | Acción | Estado | Qué se hizo / qué falta |
|---|--------|--------|-------------------------|
| 1 | Dominio único 301 + canonical | ✅ en producción | `www.ipaf.cl` → `https://ipaf.cl` (301) ahora vía **Cloudflare Redirect Rule** (no `.htaccess`, ver Ronda 3). http→https vía "Always Use HTTPS" de Cloudflare. Canonical `https://ipaf.cl/`. Verificado: `www.ipaf.cl` redirige correctamente. |
| 2 | Meta description única ~155 | ✅ | 154 caracteres, con keyword + categorías + ubicación. Title, OG y Twitter actualizados. |
| 3 | JSON-LD LocalBusiness / Service / FAQPage | ✅ | `@graph` con `EducationalOrganization`+`LocalBusiness`, `Service` (con catálogo de ofertas), 4 `Course`, `WebSite`, `WebPage`. `FAQPage` ahora con las **6** preguntas visibles (antes 5). Se eliminó el Breadcrumb que apuntaba a otro dominio (inválido). No se usa `Product` porque ipaf vende cursos (Service/Course es lo correcto). |
| 4 | sitemap.xml + envío | ✅ en producción · ⏳ envío | `sitemap.xml` con imágenes, ya sirviendo en `https://ipaf.cl/sitemap.xml`. **Pendiente manual:** enviarlo en Google Search Console y Bing Webmaster Tools. |
| 5 | robots.txt con bots IA | ✅ en producción | Permite explícitamente OAI-SearchBot, ChatGPT-User, Claude-SearchBot, Claude-User, PerplexityBot, Perplexity-User. **Postura entrenamiento: PERMITIR** GPTBot, ClaudeBot, Google-Extended, Applebot-Extended, CCBot (queremos que los modelos conozcan la marca). Confirmar con jefatura; para bloquear, cambiar a `Disallow: /`. Codificación UTF-8 corregida (ver Ronda 3). |
| 6 | Perfil de Negocio de Google | ⏳ manual | No es código. Verificar ficha "Motorman — Centro de Formación IPAF": categoría "Centro de formación", dirección Río Palena 9686, tel. +56 9 6531 5200, web `https://ipaf.cl/`, horario L–V 9–18, fotos de plataformas/curso. NAP debe coincidir exactamente con el schema. |
| 7 | Core Web Vitals (webp, lazy) | ✅ en producción | Todas las imágenes a WebP: ~5,5 MB → ~0,4 MB (banner móvil 1,2 MB PNG → 46 KB; 3A/3B de 5000 px → 900 px). `width`/`height` en todas las `<img>` (evita CLS), `loading="lazy"` fuera del hero, `fetchpriority="high"` + preload WebP en hero (LCP), video `preload="none"`. Favicons 32/192 px (antes PNG de 2138 px). **Pendiente:** medir en PageSpeed Insights ahora que está en producción. |
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
1. ~~Subir cambios a producción~~ ✅ hecho (Ronda 3, 2026-09-21).
2. ~~Probar: `www.ipaf.cl` → `301` → `ipaf.cl`~~ ✅ verificado en vivo.
3. Search Console + Bing Webmaster: agregar propiedad, enviar `https://ipaf.cl/sitemap.xml`, pedir indexación.
4. Validar schema en https://search.google.com/test/rich-results y https://validator.schema.org.
5. Cloudflare: desactivar bloqueo de bots IA si está activo.
6. Perfil de Negocio de Google (punto 6).
7. El video `video/formacion-ipaf-plataforma-elevadora.mp4` sigue siendo un placeholder de 0 bytes. Mientras tanto la sección #why muestra una imagen (el `<video>` quedó comentado en `index.html` para restaurarlo).
8. Medir PageSpeed Insights / Core Web Vitals ahora que el sitio real está en producción.

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

## Ronda 2 — mejoras tras auditoría (2026-09-21)
| Acción | Estado | Detalle |
|--------|--------|---------|
| Video vacío | ✅ | Reproductor roto reemplazado por imagen hasta tener el video real. |
| Keywords locales | ✅ | "alzahombre(s)" y "trabajo en altura" en hero, sección #why y FAQ. |
| FAQ | ✅ | Nueva pregunta "¿Qué es un alzahombre y qué curso IPAF necesito?" (visible + schema, 7/7 en sincronía). Nota: Google retiró los resultados enriquecidos FAQ (mayo 2026); se mantiene por contenido/IA. |
| "Tiempo limitado" | ✅ | Cambiado a "Ahorra en grupo" (no había fecha de vigencia). |
| Guías long-tail | ✅ 2 de 5 | `/guias/categorias-ipaf/` y `/guias/renovar-tarjeta-pal/` con Article + BreadcrumbList, enlazadas desde home (FAQ, #why, footer), sitemap y llms.txt. |
| Limpieza | ✅ | Eliminados `img/logo/experiencia.jpg.webp` (776 KB) y `Logo-ipaf-1.png` (sin uso). |
| Precios / duración / fechas | ⏳ negocio | Falta definir precio "desde", horas por categoría y calendario → luego agregar `offers` y `courseWorkload` al schema Course. |
| Testimonios / ID centro IPAF | ⏳ negocio | Falta material real (testimonios con empresa, logos, ID de centro). |
| Revisión experta de guías | ⏳ | Que Rodrigo Carreño revise las 2 guías; si aprueba, firmarlas con su nombre (autor Person en schema). |

## Ronda 3 — Deploy a producción (2026-09-21)

**Hallazgo clave:** `ipaf.cl` seguía sirviendo el sitio viejo desde un hosting cPanel (`190.196.219.30`), mientras el repo de GitHub ya se desplegaba automáticamente en cada push — pero a un dominio de Cloudflare Workers sin usar (`ipaf.motorman-online.workers.dev`), nunca conectado al dominio real. El `.htaccess` del repo asumía hosting Apache, que ya no es donde vive el sitio.

| Acción | Estado | Detalle |
|--------|--------|---------|
| Conectar dominio real | ✅ | `ipaf.cl` agregado como dominio personalizado del Worker de Cloudflare (`Workers y Pages → ipaf → Dominios`). Se eliminó el registro DNS `A` manual que apuntaba al hosting viejo. |
| Purgar caché | ✅ | Cloudflare tenía cacheado el HTML del sitio viejo (logo y textos de antes de esta ronda). Purgado completo en `Caching → Configuration → Purge Everything`. |
| Codificación UTF-8 | ✅ | `robots.txt` y `llms.txt` se veían con tildes rotas (mojibake) porque el Worker sirve `.txt` sin `charset`. Creada Transform Rule (`Reglas → Charset UTF-8 para .txt`) que fuerza `Content-Type: text/plain; charset=UTF-8`. |
| Redirect www → apex | ✅ | El `.htaccess` ya no se ejecuta (Cloudflare Workers no procesa Apache). Recreado como **Redirect Rule** nativa de Cloudflare (plantilla "Redirigir de WWW a raíz"). |
| http → https | ✅ | Ya estaba cubierto por "Always Use HTTPS" de Cloudflare a nivel de zona; no requirió cambio. |
| Redirects de rutas legacy | ✅ | 12 redirects 301 recreados como **Bulk Redirect List** (`ipaf_rutas_legacy`) + su regla: 6 rutas antiguas de imágenes/video (banner, categorías 1A/1B/3A/3B, instructor, video) con y sin `%20`, más `/index.html` → `/`. |
| Verificación en vivo | ✅ | Home, ambas guías, sitemap.xml, robots.txt, llms.txt, `www.ipaf.cl` y un redirect legacy probados directamente en `ipaf.cl` tras el deploy. |

**⚠️ Importante para el futuro:** el archivo `.htaccess` del repo **ya no tiene efecto en producción**. Cualquier regla nueva de redirect, headers o reescritura debe agregarse en el dashboard de Cloudflare (`Reglas` de la zona `ipaf.cl`), no en `.htaccess`. Vale la pena dejarlo documentado o eliminarlo para no confundir a futuros mantenedores.

**No se tocó:** correo (`mail`, `webmail`, `cpanel`, `ftp`, `imap`, `pop`, `smtp` de `ipaf.cl`) sigue apuntando al hosting original sin cambios. Nota aparte: el registro `MX` de `ipaf.cl` ya tenía una advertencia propia de Cloudflare por apuntar a un hostname proxied — preexistente, no relacionado a este deploy, pendiente de revisar con quien administra el correo.
