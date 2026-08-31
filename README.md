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

## Registro de sesiones (opcional)

Apagado por default: si no lo enciendes, la app no guarda ni manda nada, igual que
siempre. Quien la use sin configurar esto no cambia en nada su experiencia.

Al encenderlo, cada sesión terminada (o abandonada a media) se guarda en el
teléfono: fecha, hora de inicio y fin, rondas planeadas contra completadas,
work/rest configurados y duración real.

### Subirlas a un repo privado

Con un token de GitHub, la app escribe cada sesión a
`health-tracker/logs/timer/YYYY-MM-DD.json` del repo que le indiques.

1. GitHub > Settings > Developer settings > **Fine-grained personal access tokens**
2. **Repository access:** solo el repo destino. Nunca "todos".
3. **Permissions > Contents: Read and write.** Nada más.
4. Pega el token y el repo (`usuario/repo`) en los ajustes de la app.

El token vive en el `localStorage` de ese teléfono y no se sincroniza a ningún
lado. Si el teléfono se pierde, revoca el token desde GitHub. Como el alcance es
un solo repo y solo contenidos, el daño posible está acotado a ese repo.

Si no hay red al terminar, la sesión queda pendiente y se reintenta sola la
próxima vez que abras la app. También hay un botón para copiar el resumen en
texto, por si prefieres pegarlo a mano.

## Notas

- El audio necesita un toque tuyo para arrancar; el botón de empezar cuenta.
- El bloqueo de pantalla usa Wake Lock (iOS 16.4+, Chrome Android). Si no está disponible, la app te lo avisa.
- Los ajustes se guardan solos en el dispositivo.
