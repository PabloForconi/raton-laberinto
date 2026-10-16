# Ratón de Laboratorio

Prototipo de juego HTML: sos un ratoncito de laboratorio que tiene que escapar de un laberinto de cartón completamente a oscuras, con una linterna atada al lomo que apunta hacia adelante.

- Vista cenital: la cámara sigue al ratón.
- Oscuridad total: solo se ve lo que ilumina la linterna, y las paredes cortan el haz.
- Tiempo límite por nivel: si se acaba, repetís el mismo laberinto.
- Los laberintos crecen y la cámara se acerca a medida que avanzás de nivel.

## Jugar

**Online:** https://pabloforconi.github.io/raton-laberinto/

O abrí `index.html` en el navegador. No necesita instalación ni servidor.

| Tecla | Acción |
|---|---|
| ↑ / W | avanzar |
| ↓ / S | retroceder |
| ← → / A D | girar |
| P / Esc | pausa |
| M | sonido |
| R | reiniciar nivel |
| N | saltar nivel (debug) |

Los parámetros ajustables (velocidad, linterna, tamaños de nivel, zoom y tiempo) están al principio del script en `index.html`.

`concept/` tiene el arte conceptual de referencia.
