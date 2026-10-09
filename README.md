# FunCards

Aprender a leer con el método Doman (palabra global, flashcards rápidas, 5 pases × 5 cards, 75 exposiciones por palabra) + mini-juegos para gastar monedas ganadas al leer.

**En vivo:** https://pvblorodri-collab.github.io/FunCars/

## Stack

- 1 HTML + 1 JSON + SVGs + service worker. Cero dependencias de build.
- Web Speech API para la voz (es-ES, sin archivos de audio).
- Web Audio API para SFX.
- PWA installable (manifest + SW cache-first).

## Probar en local

```bash
python3 -m http.server 8080
```

Abre `http://localhost:8080`. En móvil usa la IP del PC.

## Contenido

Los 10 lotes iniciales (50 palabras) viven en [`content/batches.json`](content/batches.json).

## Mecánica

- **1 sesión** = 5 cards × 5 pases alternados (texto · imagen · texto · imagen · texto).
- **1 sesión completada** = +3 monedas. **1 moneda** = 1 vida en el juego.
- **Cadencia**: cada lote tiene cooldown de 8h entre sesiones.
- **Mastery**: 15 sesiones por lote = 75 exposiciones por palabra, lote dominado.
- Máximo **2 lotes activos** simultáneamente.
- 3 mini-juegos: Runner (esquivar), Parking (memoria), Carrera (ritmo).
