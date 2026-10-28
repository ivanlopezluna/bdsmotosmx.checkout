# BDS Motos Checkout

Fuente versionada de la marca del checkout nativo de VTEX (checkout6) de la cuenta `bdsmotos`. No es una app VTEX IO: no hay manifest, builders ni deploy. El usuario copia cada archivo a mano en su destino y publica.

El CSS y los colores se publican en la app **Checkout UI Custom** (`vtex.checkout-ui-custom`, Admin > Store Settings > Storefront > Checkout UI Custom). El encabezado y el pie siguen en las plantillas HTML del Admin (Storefront > Checkout), fuera de la app.

## Destino de cada archivo

| Archivo | Destino |
|---|---|
| `checkout6-custom.css` | App Checkout UI Custom > pestaña **CSS** (activar el interruptor "Active" y publicar) |
| Sección **Colors** de este README | App Checkout UI Custom > pestaña **Colors** (un color por campo) |
| `checkout-header.html` | Admin > Storefront > Checkout > pestaña **Código** > **HTML** > `checkout-header` (trae el `<link>` de las fuentes Inter y Montserrat, el logo y "Cancelar y volver al catálogo") |
| `checkout-footer.html` | Admin > Storefront > Checkout > pestaña **Código** > **HTML** > `checkout-footer` (pie de marca) |
| Pestaña **Layout** | No se pega nada: solo se eligen las opciones de la sección **Layout** de este README, sin cambiar orden de pasos, campos ni número de pedido |
| Pestaña **JavaScript** | No se usa: no hay `checkout6-custom.js` |

## Layout

Opciones elegidas en la pestaña Layout de la app y comprobadas en el checkout publicado (clases que la app agrega al `<body>`):

| Opción | Valor publicado | Clase en el `<body>` |
|---|---|---|
| Payment option as accordion | Activada (Accordion) | `v-custom-paymentBuilder-accordion` |
| Hide email step | Activada (paso de correo oculto) | `js-vcustom-hideEmailStep` |
| Carrito vertical | No es una opción de la pestaña: la app agrega siempre la clase `body-cart-vertical` (no existe una variante horizontal en su CSS ni aparece en las 13 opciones de la pestaña) | `body-cart-vertical` |

El resto de las opciones de la pestaña (precio unitario, campo de notas, formulario de Google, tamaños y bordes) quedan como estaban; el campo de notas no está activo (el `<body>` no trae `js-vcustom-showNoteField`).

## Colors

Publicados el 2026-10-28 en la pestaña Colors de la app (los 20 valores de la tabla).

Valores de la pestaña Colors, tomados de UI Tokens. Son los 20 campos de la pestaña, con el uso que les da la app:

| Campo | Valor | Origen en UI Tokens | Dónde se ve |
|---|---|---|---|
| Base | `#F5F5F5` | PAL005, fondo de página | Fondo del checkout |
| Inverted base | `#FFFFFF` | PAL003, superficies | Sin uso visible hoy |
| Action primary | `#B70000` | PAL002, rojo de marca | Enlaces, bordes de botones, números de paso, total, radio y foco |
| Action primary darker | `#8A0000` | PAL002, variante oscura | Hover de acciones |
| Action secondary | `#F7E0E0` | Tinta del rojo (fila activa) | Fondo de selección y de botones secundarios |
| Emphasis | `#000000` | PAL001, negro corporativo | Texto del medio de pago activo |
| Disabled | `#EBEBEB` | PAL003, fondo atenuado | Sin uso visible hoy |
| Success | `#B70000` | PAL002 | Botones principales ("Proceder al pago", "Ir para el pago", "Comprar ahora"): la app los pinta con este color y la acción primaria de la marca es el rojo |
| Success darker | `#8A0000` | PAL002 | Hover de los botones principales |
| Success faded | `#D5F5E3` | PAL004 | Sin uso visible hoy |
| Danger | `#B70000` | PAL007, borde de error | Campos con error, quitar cupón |
| Danger faded | `#FBEAEB` | PAL007, fondo de error | Sin uso visible hoy |
| Warning | `#E8971D` | PAL008, acento | Avisos de envío y de cupón |
| Warning faded | `#FDEBD0` | PAL008, fondo | Fondo del aviso de cupón |
| Muted 1 | `#141414` | PAL003, texto principal | Textos y títulos |
| Muted 2 | `#5C5C5C` | PAL003, texto secundario | Textos secundarios |
| Muted 3 | `#5C5C5C` | PAL003, texto secundario | Etiquetas de campos y precios tachados |
| Muted 4 | `#DEDEDE` | PAL003, bordes | Bordes de campos y tarjetas |
| Muted 5 | `#EBEBEB` | PAL003, fondo atenuado | Líneas divisorias |
| Muted 6 | `#F5F5F5` | PAL005 | Fondos tenues |

## Notas

- Orden de carga: la app arma `checkout6-custom.css` con la salida de `vtex.email-checkout-conflict`, luego su plantilla (con los Colors y el Layout aplicados) y al final el CSS de la pestaña CSS. El CSS de este repo va al final y usa `html body` como prefijo en las reglas que pisan a la app; no usa `@import`, así que no depende de la posición.
- Las fuentes (Inter y Montserrat) se cargan con `<link>` desde Google Fonts en `checkout-header.html`. El campo "Font family" de la pestaña Layout puede quedarse como está: el CSS fija Inter y Montserrat por encima.
- El logo SVG va en línea dentro del encabezado, sin archivos externos.
- El HTML de `checkout-header` y `checkout-footer` se inyecta directo en `<body>` (sin `div.container` envolvente), por eso `.bds-header` y `.bds-footer` son las bandas de fondo y sus `__inner` limitan el ancho (980px, igual al ancho máximo del contenido de la app). El CSS y los dos HTML deben pegarse juntos, porque el CSS depende de esa estructura.
- La configuración es de toda la cuenta: cada publicación aplica de inmediato al checkout usado desde el Deploy Preview y desde producción.
- No se oculta ni se mueve ningún campo nativo del checkout.

## Observaciones conocidas

- El modal de conflicto de correo (`vtex.email-checkout-conflict`) usa el azul propio de la app (`#1a73e8`) y no sigue la paleta de la marca. Se decidió no sobrescribirlo.
- El botón azul flotante (vtex-cartman) en la esquina inferior derecha es propio de la plataforma y no se estiliza.
- En móvil (hasta 768px) el pie reserva 56px de espacio inferior para que la barra fija nativa ("Proceder al pago" en el carrito, "Comprar ahora" en el pago) no tape el texto del pie; en identificación y envío, que no tienen barra, ese espacio queda como franja negra extra.
