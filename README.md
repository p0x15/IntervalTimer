# Ring Timer

PWA de intervalos con dos modos: circuito 40/20 (guide de 12 semanas) y rounds de box.

La pantalla principal deja solo lo que cambia sesión a sesión — día, peso y
rondas. Todo lo que se configura una vez (tiempos, volumen, pantalla, registro)
vive detrás del botón de ajustes, arriba a la derecha. El botón se bloquea
mientras el timer corre, para no esconder el reloj a media serie.

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
work/rest configurados, **peso del kettlebell** y duración real.

El peso se ajusta de medio en medio kilo y muestra la equivalencia en libras,
que es como suelen venir marcados los kettlebells prestados. En 0 queda como
"sin peso", para el circuito hecho solo con el movimiento.

### Subirlas a un repo privado

Con un token de GitHub, la app escribe cada sesión a
`sessions/YYYY-MM-DD.json` del repo que le indiques.

1. Crea un repo **privado y dedicado** solo a estos logs (por ejemplo `timer-logs`).
2. GitHub > Settings > Developer settings > **Fine-grained personal access tokens**
3. **Repository access:** solo ese repo. Nunca "todos", nunca un repo con otras cosas.
4. **Permissions > Contents: Read and write.** Nada más.
5. **Expiración:** 90 días. Renovarlo es un minuto.
6. Pega el token y el repo (`usuario/repo`) en los ajustes de la app.

#### Por qué un repo dedicado y no tu vault

El token se guarda en el `localStorage` del teléfono, y en GitHub Pages ese
almacenamiento **se comparte entre todos los sitios del mismo usuario**
(`usuario.github.io/proyecto-a` y `.../proyecto-b` son el mismo origen). Si
tienes varios repos publicados en Pages, cualquiera de ellos puede leer el
token de los demás.

Por eso el alcance importa más que el secreto: si el token solo puede escribir
en un repo que contiene JSONs de rondas de ejercicio, filtrarlo es irrelevante.
Si puede escribir en tu vault personal, no lo es.

Si pierdes el teléfono, revoca el token desde GitHub.

Si no hay red al terminar, la sesión queda pendiente y se reintenta sola la
próxima vez que abras la app. También hay un botón para copiar el resumen en
texto, por si prefieres pegarlo a mano.

## Notas

- El audio necesita un toque tuyo para arrancar; el botón de empezar cuenta.
- El bloqueo de pantalla usa Wake Lock (iOS 16.4+, Chrome Android). Si no está disponible, la app te lo avisa.
- Los ajustes se guardan solos en el dispositivo.
