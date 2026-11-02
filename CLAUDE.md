# Plantilla «Asesoría y gestoría» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **sobrio**
(verde bosque, arena y blanco; sans geométrica muy pesada; bandas a todo el ancho; rayado de libro de cuentas).
Brief de diseño en `DISEÑO.md`. Todo en castellano de España, frases cortas, sin jerga.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa (también las listas propias `cifras`, `servicios`, `planes` y `plazos`); no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario = verde bosque, acento = arena, fondo = blanco, texto). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…); `src/styles/global.css` saca de ellas los derivados (`--verde-hondo`, `--verde-suave`, `--arena-clara`, `--tinta-verde`, `--sobre-verde`, `--raya`) con `color-mix`.
- **Tipografías y aspecto general**: `src/styles/global.css` (sans geométrica del sistema en 800 para títulos, `system-ui` para el texto, bandas `.banda--blanco|arena|clara|verde|hondo`, rayado `.rayado`, botones en píldora `.btn`, `.btn-sec`, `.btn--verde`, fotos con esquina curva `.foto-curva` / `.foto-curva--izq`, cabecera `.cabecera--cuenta` y pie `.pie--cuenta`). Fuentes del sistema: no añadas fuentes externas.
- **Imágenes**: en `public/`. Las fotos van en `public/fotos/` (las genera el paso de fotos a partir de `fotos.json`); los SVG de respaldo en `public/placeholders/`. En `site.yaml` se referencian con ruta absoluta (`/fotos/hero.jpg`). Personas: `/placeholders/persona.svg` hasta que el cliente suba su foto.
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = inicial en una pestaña verde y el nombre en texto.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie` (true en plan gratis).

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`, en el orden de `site.yaml`. Todas pintan bien con listas y campos vacíos (sin cifras no hay fichas, sin precio no hay precio).
- `hero` → `hero.astro`: portada verde pleno con título enorme y dos botones; foto `imagen` a sangre a la derecha y `cifras` (titulo = cifra, texto = etiqueta; hasta 4) flotando en fichas.
- `servicios` → `servicios.astro`: lista propia `servicios` (titulo, texto, icono, para). Se agrupan en columnas por `para` («Autónomos», «Pymes», «Particulares»…); sin `para`, rejilla simple.
- `planes` → `planes.astro`: lista propia `planes` (nombre, precio como cadena, periodo, incluye con «;», destacado) y `nota`. «desde 160 €» pinta «desde» pequeño encima.
- `proceso` → `proceso.astro`: pasos (`items`: titulo, texto) con números perfilados y franja de fotos `galeria` de borde a borde.
- `plazos` → `plazos.astro`: calendario fiscal, lista propia `plazos` (fecha, titulo, texto) junto a la foto `imagen` a sangre. «20 de enero» se parte en día y mes.
- `equipo` → `equipo.astro`: `personas` (nombre, cargo, foto, texto).
- `cita` → `cita.astro`: banda arena «Primera consulta gratis» con `items` (formas de hacer la consulta: titulo, texto, icono), `cta`, `cta_secundario` y foto `imagen` a sangre.
- `opiniones` → `opiniones.astro`: `testimonios` (texto, autor); la primera, como cita enorme.
- `preguntas` → `preguntas.astro`: preguntas frecuentes en acordeón `details/summary` (sin preguntas no se pinta).
- `contacto` → `contacto.astro`: datos en columnas sobre verde y formulario `mailto` con «¿Para quién es la consulta?» (los `para` de los servicios), con la foto `imagen` a sangre.
- `texto` → `texto.astro`: diseño genérico para apartados nuevos (`tipo: texto`), con o sin foto.

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`.
3. **Cambiar textos, teléfonos, horarios, fotos, planes o fechas**: solo en `site.yaml`. Si un texto contiene comas o «: » dentro de `{ … }`, ponlo entre comillas. Precios siempre entre comillas. Listas planas (nada de listas dentro de un elemento de lista; lo que incluye un plan va en una cadena con «;»), máximo 24 elementos.
4. **Página nueva**: crea `src/pages/<slug>.astro` con `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>` (usa bandas `.banda .banda--verde` / `.banda--blanco`, como `aviso-legal.astro`); enlázala en `site.yaml → menu`.
5. **Sección nueva**: crea `src/components/secciones/<id>.astro` (estructura: `seccion(id)`, `Seccion` o un `<section>` a todo el ancho con `.contenedor` dentro) y añade `secciones.<id>` en `site.yaml`. `src/pages/index.astro` la recoge sola.
6. **No tocar** `src/layouts/Base.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio y de las preguntas, robots, sitemap y llms.txt), salen solos de `site.yaml` y el fichero es el mismo en todas las plantillas. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
7. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), sin JavaScript nuevo salvo necesidad real, bandas a todo el ancho con 16 px de margen lateral del texto (`.contenedor`), sin scroll horizontal en móvil, botones de 44 px o más. Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altFicha`, `altGaleria`, `altSeccion` de `src/lib/seo.ts`); las decorativas, `alt=""`.
8. El formulario no tiene servidor: abre el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

## Páginas propias (fichas por elemento)
- Listas con página propia (espejo de `fichas:` de template.yaml en `src/data/fichas.ts`): `secciones.servicios.servicios` → `/servicios/<slug>/` (servicio).
  **Solo los elementos con `detalle`** (texto largo, párrafos separados por una línea en blanco, ≤ 3000 caracteres, sin HTML) tienen página;
  los demás siguen como hasta ahora. Campos opcionales del elemento: `slug` (si falta, sale del nombre; no lo pongas sin motivo)
  e `imagenes` («/fotos/a.jpg; /fotos/b.jpg», galería de la ficha; la foto principal es `imagen` o, si no hay, la primera de `imagenes`).
  El resto de campos (precio, duración…) salen en la tabla de datos de la ficha.
- Una orden «añade una página para X» = escribir su `detalle` en site.yaml. Nunca crees a mano páginas en
  `src/pages/servicios/`: salen solas de `src/pages/[coleccion]/[slug].astro`.
- No tocar `src/lib/paginas.ts`, `src/lib/slug.ts` ni `src/lib/seo.ts` (comunes a todas las plantillas). Las páginas propias entran solas en
  `sitemap.xml` y `llms.txt`, con su JSON-LD (migas y servicio/producto con precio si lo hay).
