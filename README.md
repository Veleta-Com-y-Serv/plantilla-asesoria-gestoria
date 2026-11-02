# Plantilla NoExpertise · Asesoría y gestoría

Web sobria para asesorías y gestorías, con servicios por tipo de cliente, planes de cuota y calendario fiscal.
A ancho completo: portada verde de color pleno con cifras flotando, bandas de borde a borde en verde bosque, arena y
blanco, sans geométrica muy pesada, rayado de libro de cuentas y fotos a sangre con una esquina muy curva.
Responsive de 375 px a pantallas anchas.

- Sectores: asesoria, gestoria, contable, fiscal, laboral, administrador-fincas. Estilo: sobrio. Plan mínimo: presencia.
- Secciones: hero, servicios, planes, proceso, plazos, equipo, cita, opiniones, preguntas, contacto (y `texto` para apartados nuevos).
- Ejemplo: Asesoría Onyar, Girona (negocio ficticio).
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio (`AccountingService`) y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Contenido editable en `site.yaml`; metadatos y guion del asistente en `template.yaml`; fotos a generar en `fotos.json`; reglas para el agente en `CLAUDE.md`; brief de diseño en `DISEÑO.md`.

## Campos propios

| Sección | Campo | Qué es |
|---|---|---|
| `hero` | `cifras` (titulo, texto) | Hasta 4 datos que flotan sobre la portada (titulo = cifra) |
| `servicios` | `servicios` (titulo, texto, icono, para) | Servicios agrupados en columnas por `para` |
| `planes` | `planes` (nombre, precio, periodo, incluye, destacado), `nota` | Cuotas; `incluye` separado por «;»; precio como cadena |
| `proceso` | `items` (titulo, texto), `galeria` | Alta en tres pasos y franja de fotos |
| `plazos` | `plazos` (fecha, titulo, texto), `imagen` | Calendario fiscal junto a una foto a sangre |
| `cita` | `items` (titulo, texto, icono), `cta`, `cta_secundario`, `imagen` | Banda «Primera consulta gratis» |
| `contacto` | `imagen` | Foto junto al formulario |

## Construir

```
npm ci
npm run build    # dist/
```
