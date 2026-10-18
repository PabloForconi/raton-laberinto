# Maze Mouse

![Maze Mouse](img/logo.png)

Prototipo de juego HTML: sos un ratoncito de laboratorio que tiene que escapar de un laberinto de cartón completamente a oscuras, con una linterna atada al lomo que apunta hacia adelante.

- Vista cenital: la cámara sigue al ratón.
- Oscuridad total: solo se ve lo que ilumina la linterna, y las paredes cortan el haz.
- Tiempo límite por nivel: si se acaba, repetís el mismo laberinto.
- En los últimos 10 segundos suena la sirena: todo se tiñe de rojo y un haz giratorio deja ver más allá de la linterna; cada vez que el haz pasa por encima de la rata suena un "Uuuuh".

## Modos

- **Historia:** niveles diseñados (siempre iguales), cada uno presenta una mecánica nueva. Se guardan los niveles desbloqueados y las estrellas (1 a 3). Por ahora hay 4 niveles de prueba:
  1. **La trampera:** trampas al fondo de los callejones sin salida; si tocás una, perdés.
  2. **Pegote:** bandejas con pegamento que te frenan y te dejan las patas pegajosas un rato.
  3. **Quesos:** hay 10 quesos dando vueltas; juntá 5 antes de salir (dan una estrella extra).
  4. **Puertas:** puertitas de un solo sentido. Del lado del agujero empujás la cortina de cartón y pasás; del otro lado, por más que empujes, no se abren.
- **Desafío:** laberintos al azar, infinitos, cada vez más grandes y con la cámara más cerca.
- **Monedas y ratitas:** juntá monedas en los laberintos (se guardan aunque pierdas). En la **Máquina** cada giro cuesta 10 monedas por ahora, para probar, y te da una de las 20 ratitas al azar (si sale repetida, te devuelve la mitad). Para ver las 20 juntas: `index.html?ratas`. En **Ratitas** elegís con cuál jugar.

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
