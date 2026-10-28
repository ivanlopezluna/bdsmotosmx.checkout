# BDS Motos Checkout

Archivos de personalización de marca del checkout nativo de VTEX (checkout6) de la cuenta `bdsmotos`. No es una app VTEX IO: no hay manifest, builders ni deploy. Cada archivo se copia a mano en **Admin > Storefront > Checkout** y se guarda.

| Archivo | Campo en Admin > Storefront > Checkout |
|---|---|
| `checkout6-custom.css` | Pestaña **Código** > **CSS** (`checkout6-custom.css`) |
| `checkout-header.html` | Pestaña **Código** > **HTML** > `checkout-header` (encabezado con logo y "Cancelar y volver al catálogo") |
| `checkout-footer.html` | Pestaña **Código** > **HTML** > `checkout-footer` (pie de marca) |

`checkout6-custom.js` no se incluye porque la marca y la liga de regreso no lo necesitan; el campo JavaScript del Admin se deja como está.

## Notas

- La configuración es de toda la cuenta: aplica de inmediato al checkout usado desde el Deploy Preview y desde producción.
- Las fuentes (Inter y Montserrat) se cargan desde Google Fonts con `@import` en el CSS; el logo SVG va en línea dentro del encabezado, sin archivos externos.
- El HTML de `checkout-header` y `checkout-footer` se inyecta directo en `<body>` (sin `div.container` envolvente), por eso `.bds-header` y `.bds-footer` son las bandas de fondo y sus `__inner` limitan el ancho; el CSS y los dos HTML deben pegarse juntos, porque el CSS depende de esa estructura.
- No se oculta ni se mueve ningún campo nativo del checkout.
