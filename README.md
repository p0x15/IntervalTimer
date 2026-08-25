# Ring Timer

PWA de intervalos con dos modos: circuito 40/20 (guide de 12 semanas) y rounds de box.

## Publicar en GitHub Pages

1. Crea un repo nuevo y sube estos archivos a la raíz.
2. Settings > Pages > Source: `Deploy from a branch`, branch `main`, folder `/ (root)`.
3. Espera 1 o 2 minutos y abre la URL `https://<usuario>.github.io/<repo>/`.

Tiene que ser HTTPS: el service worker y el bloqueo de pantalla no funcionan sobre `file://` ni `http://`.

## Instalar en el teléfono

- iOS: abre la URL en Safari, botón compartir, "Agregar a inicio".
- Android: Chrome te ofrece "Instalar app", o menú > "Agregar a pantalla principal".

Una vez instalada corre sin conexión.

## Probar en local

```
python3 -m http.server 8000
```

Luego abre `http://localhost:8000`. En localhost sí aplican las APIs seguras.

## Notas

- El audio necesita un toque tuyo para arrancar; el botón de empezar cuenta.
- El bloqueo de pantalla usa Wake Lock (iOS 16.4+, Chrome Android). Si no está disponible, la app te lo avisa.
- Los ajustes se guardan solos en el dispositivo.
