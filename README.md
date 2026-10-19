# Maze Mouse

![Maze Mouse](img/logo.png)

Prototipo de juego HTML: sos un ratoncito de laboratorio que tiene que escapar de un laberinto de cartón completamente a oscuras, con una linterna atada al lomo que apunta hacia adelante.

- Vista cenital: la cámara sigue al ratón.
- Oscuridad total: solo se ve lo que ilumina la linterna, y las paredes cortan el haz.
- Tiempo límite por nivel: si se acaba, repetís el mismo laberinto.
- En los últimos 10 segundos suena la sirena: todo se tiñe de rojo y un haz giratorio deja ver más allá de la linterna; cada vez que el haz pasa por encima de la rata suena un "Uuuuh".

## Modos

- **Historia:** 40 niveles diseñados (siempre iguales). Se guardan los niveles desbloqueados, las estrellas (1 a 3) y tu mejor tiempo de cada nivel. Una estrella por escapar, dos por bajar de un tiempo y tres por bajar de un tiempo más exigente (con todos los quesos, si el nivel tiene). Cada estrella nueva da 5 monedas, y al terminar ves tu tiempo, tu récord y tu próximo objetivo. En el camino directo hay pocas monedas; los tesoros más grandes están en los desvíos y los callejones: juntarlos rinde más pero cuesta tiempo. Las mecánicas aparecen de a una y después se combinan, con laberintos cada vez más grandes:
  - **1–6, quesos:** juntalos antes de salir (los pide la tercera estrella); a veces hay más de los que hacen falta.
  - **7–12, pegote:** bandejas con pegamento que te frenan y te dejan las patas pegajosas un rato.
  - **13–20, trampas:** al fondo de los callejones sin salida; si tocás una, perdés.
  - **21–28, puertas:** puertitas de un solo sentido. Del lado de la cinta empujás la cortina de cartón y pasás; del otro lado, por más que empujes, no se abren.
  - **29–40:** todo junto.
- **Desafío:** laberintos al azar, infinitos, cada vez más grandes y con la cámara más cerca.
- **Monedas y ratitas:** juntá monedas en los laberintos (se guardan aunque pierdas). En la **Máquina** cada giro cuesta 2 monedas por ahora, para probar rápido, y te da una de las 20 ratitas al azar (si sale repetida, te devuelve la mitad). Para ver las 20 juntas: `index.html?ratas`. En **Ratitas** elegís con cuál jugar.

## Jugar

**Online:** https://pabloforconi.github.io/raton-laberinto/

O abrí `index.html` en el navegador. No necesita instalación ni servidor.

| Tecla | Acción |
|---|---|
| 1 / 2 (en la portada) | Historia / Desafío |
| ↑ ↓ ← → / W A S D | moverte en esa dirección (el ratón gira hacia donde apuntás; se pueden combinar para diagonales) |
| P / Esc | pausa |
| Q (en pausa) | salir al menú |
| M | música (on/off) |
| F | efectos de sonido (on/off) |
| R | reiniciar nivel |
| N | saltar nivel (debug) |

En el celular: apoyás el dedo en cualquier lugar y aparece un joystick; el ratón gira hacia donde apuntás y avanza según cuánto empujás. Los botones de pausa, música y efectos están arriba a la derecha, y la casita (volver al menú) arriba a la izquierda.

La música (`audio/laberinto-de-circuitos.mp3`) arranca con el primer toque o tecla y suena bajita para no tapar los efectos.

Los parámetros ajustables (velocidad, linterna, tamaños de nivel, zoom y tiempo) están al principio del script en `index.html`. Los niveles de Historia se definen en la tabla `LEVELS` (tamaño, semilla y cantidad de cada mecánica).

`concept/` tiene el arte conceptual de referencia.
