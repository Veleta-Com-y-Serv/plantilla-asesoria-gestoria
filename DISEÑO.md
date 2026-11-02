# Asesoría y gestoría: brief de diseño

Plantilla `asesoria-gestoria` creada el 02/11/2026 a partir de `abogados` (base de origen) con
`php artisan plantillas:nueva` y rediseñada entera a ancho completo: de la base solo queda la estructura técnica.
Este fichero se queda en el repo: es lo que lee quien (persona o agente) rediseñe la plantilla.

## Brief

- **Para quién**: asesorías y gestorías (fiscal, laboral, contable) y administradores de fincas que trabajan para
  autónomos, pymes y particulares. Quien entra quiere quitarse el papeleo de encima, saber cuánto le costará y no
  perderse ningún plazo.
- **Qué tiene que conseguir la web**: que pida la primera consulta gratis (formulario con «¿Para quién es la
  consulta?») o que llame. Secundario: ver servicios por tipo de cliente, planes de cuota y el calendario fiscal.
- **Tono y estilo** (`sobrio`): ordenado, claro, de confianza, pero actual y cercano. Sí: el orden de un libro de
  cuentas (rayado, cifras tabulares, columnas) con bandas de color pleno y títulos enormes. No: la solemnidad de
  `abogados` (serifa, dorado, filetes finos, esquinas rectas), ni la caja centrada con tarjetas blancas.
- **Paleta de ejemplo**: primario `#1f4d3a` (verde bosque), acento `#d8c3a0` (arena), fondo `#ffffff` (blanco),
  texto `#14231c`. Derivados con `color-mix` en `global.css`: `--verde-hondo` (bandas oscuras y pie),
  `--verde-suave`, `--arena-clara` (banda clara, fondos de iconos y preguntas), `--tinta-verde` (verde legible sobre
  arena), `--sobre-verde` (texto claro en bandas verdes), `--raya` / `--raya-clara` (rayado). Aguanta otros cuatro
  colores siempre que el primario sea oscuro y el acento y el fondo claros.
- **Tipografía**: sans geométrica del sistema (Avenir Next, Century Gothic, Futura, Segoe UI) en 800 con
  interletrado negativo, enorme (portada hasta 6,75 rem, «Primera consulta gratis» hasta 6,5 rem, títulos hasta
  4,75 rem); cifras con `tabular-nums`. Texto en `system-ui`. Antetítulos en mayúsculas con una barra gruesa
  redondeada delante. Botones en píldora, gruesos, sin mayúsculas.
- **Ritmo de bandas** (todas de borde a borde, contenido a `max-width: 90rem`):
  portada verde pleno rayada con foto a sangre y cifras flotando → servicios (blanco, columnas por destinatario) →
  planes (arena plena, columnas con reglas, destacado en verde) → proceso (verde hondo rayado, números perfilados y
  franja de 4 fotos a sangre) → calendario fiscal (blanco, 50/50 con foto a sangre a la izquierda) → equipo (arena
  clara) → «Primera consulta gratis» (50/50 arena plena + foto a sangre) → opiniones (verde pleno, cita enorme) →
  preguntas (blanco) → contacto (verde hondo con datos en columnas + 50/50 formulario y foto a sangre) → pie (verde
  hondo con franja arena).
- **Firma visual**: rayado horizontal de libro de cuentas en las bandas verdes; fichas de cifras escalonadas con una
  esquina recta; fotos con una esquina muy curva (`--curva`) siempre hacia el texto; hojas de calendario (día en
  verde, mes en arena); números de paso perfilados en arena; barras verdes gruesas bajo las cabeceras de columna.
- **Cabecera**: fija, a todo el ancho, siempre sólida y blanca (sombra al hacer scroll). Inicial en una pestaña
  verde con una esquina recta. Botón en píldora verde.

## Apartados

| id | Qué enseña | Lista propia |
|---|---|---|
| `hero` | Verde pleno rayado, título enorme, párrafo, dos botones; foto a sangre a la derecha con cifras flotando | `cifras` (titulo, texto) |
| `servicios` | Columnas por destinatario con su número de servicios y filas rayadas con icono | `servicios` (titulo, texto, icono, para) |
| `planes` | Planes en columnas con precio enorme; el destacado en verde con «El más elegido» | `planes` (nombre, precio, periodo, incluye, destacado), `nota` |
| `proceso` | Alta en tres pasos con números perfilados y franja de fotos a sangre | `items` (titulo, texto), `galeria` |
| `plazos` | Calendario fiscal en hojas de calendario junto a una foto a sangre | `plazos` (fecha, titulo, texto), `imagen` |
| `equipo` | Retratos 3:4 con esquina curva y velo verde | `personas` (nombre, cargo, foto, texto) |
| `cita` | «Primera consulta gratis»: formas de hacerla y dos botones junto a una foto a sangre | `items` (titulo, texto, icono), `imagen` |
| `opiniones` | Primera opinión como cita enorme; las demás en columnas | `testimonios` (texto, autor) |
| `preguntas` | Acordeón `details/summary` en bloques arena con botón redondo | `preguntas` (pregunta, respuesta) |
| `contacto` | Datos en columnas sobre verde; formulario con destinatario y foto a sangre | `imagen` |

## Fotos (`fotos.json`)

Asesoría en un edificio de piedra del Barri Vell de Girona: mesa de roble con carpetas verdes (portada, 3:4);
archivadores, calculadora con facturas, pasillo de piedra y casas del Onyar (franja, 3:4); calendario y agenda en
blanco (calendario fiscal, 3:4); sala de reuniones con sillas verdes (primera consulta, 4:3); portal de piedra con
puerta verde (contacto, 4:3). Sin personas, sin texto ni cifras legibles, sin logotipos ni placas.

## Qué no hacer

- Volver a la estética de `abogados` (serifa, dorado, filetes finos, esquinas rectas, portada con foto velada) ni a la
  caja centrada estrecha con tarjetas blancas.
- Sombras de tarjeta por todas partes, degradados vivos, iconos de colores.
- Poner precios, cifras u opiniones fijos en los componentes: todo sale de `site.yaml` y lo que está vacío no se pinta.

## Páginas propias (fichas)
Con la misma piel que la portada (banda verde rayada con título enorme y foto de esquina curva, cuerpo blanco con tabla de datos de barra verde gruesa y caja de consulta en arena, otros servicios en filas rayadas sobre arena clara): cabecera y pie de la plantilla, migas (Inicio › Sección › Elemento), hero con la foto del
elemento (sin foto, su icono), `detalle` en párrafos, tabla de datos, caja de contacto, galería (`imagenes`) y otros elementos
de la misma lista.

