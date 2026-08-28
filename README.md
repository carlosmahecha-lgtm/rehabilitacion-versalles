# Centro de Rehabilitación Versalles — Landing page

Landing page estática: `index.html` contiene el marcado, los estilos y el JavaScript;
`images/` contiene las fotografías. No requiere build ni dependencias. La única petición
externa son las tipografías de Google Fonts (Newsreader y Archivo).

## El sitio en producción

| | |
| --- | --- |
| Dominio | **https://centroversalles.com** (y `www.centroversalles.com`) |
| Dirección de Vercel | https://versalles-web-rho.vercel.app |
| Proyecto en Vercel | `versalles-web`, en el equipo `cratch` (plan Hobby) |
| Registrador del dominio | Vercel · vence el 28 de agosto de 2027 · renovación automática activada |
| Repositorio | https://github.com/carlosmahecha-lgtm/rehabilitacion-versalles |

El hosting, el certificado HTTPS y la CDN están incluidos en el plan Hobby, sin costo.
El repositorio **no está conectado a Vercel**: sirve como historial, pero los despliegues
son manuales (ver abajo).

## Ver el sitio en local

Abre `index.html` en el navegador. No necesita servidor.

## Publicar cambios

Desde esta carpeta, con el CLI de Vercel ya instalado y con sesión iniciada:

```bash
vercel deploy --prod
```

Vercel lo detecta como sitio estático y sirve `index.html` en la raíz; no hace falta
`vercel.json`. Conviene además dejar el cambio versionado:

```bash
git add -A && git commit -m "descripción del cambio" && git push
```

Si más adelante quieres que cada `git push` despliegue solo, hay que instalar la
aplicación de Vercel en la cuenta de GitHub `carlosmahecha-lgtm` (donde vive el
repositorio) y enlazar el proyecto desde el panel de Vercel.

## Correo del dominio

Pendiente. El plan es **Zoho Mail** en su plan gratuito: un dominio, hasta 5 buzones de
5 GB, acceso por web y app móvil (sin IMAP/POP, así que no funciona con Outlook ni Apple
Mail; para eso hace falta Mail Lite, ~US$1 por buzón al mes).

El procedimiento: crear la cuenta en Zoho con el dominio `centroversalles.com`, y luego
agregar en el DNS de Vercel (https://vercel.com/cratch/~/domains) los registros que Zoho
entregue: un **TXT** de verificación de propiedad, los **MX** de entrega, y los **TXT** de
SPF y DKIM para que el correo no caiga en spam.

## Estructura de la página

| Sección | Ancla | Contenido |
| --- | --- | --- |
| Barra superior | — | Dirección, horarios, teléfono y WhatsApp |
| Encabezado | — | Logo, navegación y botón de agendamiento (menú hamburguesa bajo 940 px) |
| Hero | `#inicio` | Titular, propuesta de valor, cifras y fotografía principal |
| Capacidades | — | Cuatro diferenciales del centro |
| Nosotros | `#nosotros` | Presentación, tres compromisos y cita de dirección médica |
| Servicios | `#servicios` | Nueve especialidades en tarjetas con iconos |
| Ruta de atención | `#ruta` | Proceso en cuatro pasos |
| Instalaciones | `#instalaciones` | Galería de seis fotografías en retícula asimétrica |
| Métricas | — | Franja oscura con contadores animados |
| Historias de éxito | `#historias` | Testimonio destacado y tres testimonios cortos |
| Preguntas frecuentes | `#preguntas` | Seis preguntas en acordeón (`<details>`) |
| Llamado a la acción | — | WhatsApp y teléfono |
| Contacto | `#contacto` | Formulario validado, datos de sede y mapa de Google |
| Pie de página | — | Navegación, contacto, redes y enlaces legales |

## Fotografías

Las nueve fotografías vienen de **Pexels**, con licencia libre para uso comercial y sin
atribución obligatoria (se permite usarlas y modificarlas; no se pueden revender sin
alterar ni usarlas para sugerir que las personas retratadas respaldan el centro).

| Archivo | Uso | Origen |
| --- | --- | --- |
| `hero-fisioterapia.jpg` | Hero | pexels.com/photo/6111585 |
| `acompanamiento.jpg` | Nosotros | pexels.com/photo/7551627 |
| `sala-fisioterapia.jpg` | Galería 01 | pexels.com/photo/20860622 |
| `terapia-de-mano.jpg` | Galería 02 | pexels.com/photo/30483047 |
| `electroterapia.jpg` | Galería 03 | pexels.com/photo/30483052 |
| `rehabilitacion-ortopedica.jpg` | Galería 04 | pexels.com/photo/20860588 |
| `equilibrio.jpg` | Galería 05 | pexels.com/photo/30483062 |
| `vida-diaria.jpg` | Galería 06 | pexels.com/photo/7495948 |
| `historia-destacada.jpg` | Historia destacada | pexels.com/photo/16852335 (retrato tomado en Cali) |

**Son fotografías de banco, no del centro.** En cuanto tengas fotos propias, reemplaza
los archivos conservando el nombre (o cambia el `src`) y **actualiza el `alt`** para que
describa la escena real. Recuerda la autorización de uso de imagen de pacientes y
profesionales.

Al cambiar una foto, revisa dos cosas:

1. Los atributos `width`/`height` del `<img>` deben ser los del archivo nuevo, para que el
   navegador reserve el espacio correcto y la página no salte al cargar.
2. El encuadre. Las fotos se recortan con `object-fit: cover`; cuando el motivo no queda
   centrado en el recorte, se ajusta con `object-position`. Dos tarjetas ya lo usan:
   `.tile__art--upper` (sube el encuadre) y `.tile__art--lower` (lo baja).

Los iconos de servicios, el logo y los avatares de testimonios siguen siendo SVG en línea,
dibujados a la medida.

## Mapa

La sección de contacto embebe un mapa de Google con la dirección real. No requiere API key:
basta el parámetro `output=embed` en la URL del `<iframe class="map__frame">`. Si cambias
de sede, actualiza el valor de `q=` (codificado en URL) y también el enlace
«Ver cómo llegar» que está justo debajo.

Dos consecuencias de embeber Google:

- El iframe carga recursos de Google y puede poner cookies. Si publicas un aviso de
  cookies, este es el elemento que debe quedar bajo consentimiento.
- La vista previa como Artifact bloquea dominios externos, así que ahí el mapa se
  reemplaza por una tarjeta estática con la dirección (`.map__static`). En el sitio
  publicado se ve el mapa real.

## Qué debes reemplazar antes de publicar

- **Datos de contacto**: el WhatsApp `318 555 0180` y el correo `citas@rehabversalles.co`
  son de ejemplo. Los enlaces de WhatsApp usan el formato `https://wa.me/57XXXXXXXXXX`.
  No hay teléfono fijo en la página: el único canal telefónico es WhatsApp. La dirección
  (`Av. 5 Nte. #37 A 120, Cali`) y los horarios (Lun a Vie 8:00 a.m. – 6:00 p.m. ·
  Sáb 8:00 a.m. – 12:00 m.) ya son los reales y aparecen en la barra superior, la sección
  de contacto y el pie de página.
- **Cifras**: los `data-count` de la franja de métricas y las tres cifras del hero
  (3 años, 2.400 pacientes, 9 especialidades) son estimaciones coherentes con los 3 años
  de operación. Ajústalas a los números reales, incluido el 92 % de adherencia y los
  24 profesionales.
- **Testimonios**: los cuatro testimonios son ficticios. Sustitúyelos por testimonios
  reales con autorización escrita del paciente. Ojo con la coherencia entre el testimonio
  destacado y su fotografía: hoy el texto (Rosa E., 71 años, reemplazo de cadera)
  corresponde a la mujer del retrato.
- **Preguntas frecuentes**: revisa que las respuestas coincidan con la operación real
  (convenios, telerehabilitación, duración de sesiones, parqueadero).
- **Convenios y credenciales**: verifica las menciones a EPS, ARL y medicina prepagada.
- **Enlaces legales**: `#politica`, `#habeas` y `#pqrs` apuntan a anclas vacías.
- **Redes sociales**: `#instagram` y `#facebook` en el pie de página.

## Formulario de contacto

Valida en el navegador (nombre, teléfono, correo opcional, motivo y autorización de
tratamiento de datos, Ley 1581 de 2012) y muestra una confirmación, pero **no envía nada
todavía**. Para recibir las solicitudes, conecta el `submit` —marcado con un comentario
dentro del `<script>`— a un endpoint: una función serverless en `/api/citas`, Formspree o
el servicio que uses.

## Sistema de diseño

- **Color**: petróleo `#0F5A55`, petróleo profundo `#0A403D`, agua `#7FC8BE`,
  arcilla `#BE5F3B` (solo acentos), papel `#F4F7F5`, tinta `#0E1F1C`.
  Todos son variables CSS en `:root`.
- **Tipografía**: `Newsreader` para titulares, `Archivo` para texto, datos y etiquetas.
- **Galería**: retícula de 6 columnas con filas de alto uniforme
  (`grid-auto-rows`); las fotos se recortan con `object-fit: cover`, así que puedes
  cambiarlas sin importar la proporción original.
- **Tema**: la página tiene una sola atmósfera clara, pintada explícitamente, para que no
  cambie con el modo oscuro del sistema.

## Accesibilidad

Enlace de salto al contenido, jerarquía de encabezados, foco visible, `aria-expanded` en
el menú, texto alternativo descriptivo en todas las fotografías, preguntas frecuentes con
`<details>` nativo, mensajes de error asociados por `aria-describedby`, confirmación con
`aria-live` y respeto por `prefers-reduced-motion`.
