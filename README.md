# FunCars

Enseñar a leer a niños pequeños con el método Doman (palabra global, flashcards rápidas, 5 pases × 5 cards, 75 exposiciones). Gamificación mínima: cada sesión completada = 3 monedas = 3 vidas en el mini-juego.

## Estado

**Prototipo validación — Lote 1**. Un solo HTML, cero dependencias, Web Speech API para el sonido. Objetivo: probar la mecánica con un niño real antes de invertir en stack completo.

## Probar

```bash
python3 -m http.server 8000
```

Abre `http://localhost:8000` en Chrome, Safari o Firefox (móvil o escritorio). Pulsa **Empezar sesión** — el click también desbloquea el audio en iOS. Verás 5 pases × 5 cards del Lote 1 (`sol · agua · casa · pan · feliz`), ~30 segundos.

## Contenido

Los 10 lotes iniciales (50 palabras) viven en [`content/batches.json`](content/batches.json). El prototipo solo usa el Lote 1 hardcodeado por simplicidad.

## Siguiente paso

Si la mecánica funciona con un niño:

1. Las 2 rondas (texto + imagen) con imágenes libres (Openclipart, Pixabay).
2. Persistencia local de sesiones y monedas.
3. Mini-juego que consume monedas.
4. Stack completo (Next.js + Supabase) solo tras validar.
