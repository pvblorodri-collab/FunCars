# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Stack

Static HTML + JSON + SVG + vanilla JS. Zero build pipeline. PWA installable (manifest + service worker). Web Speech API para TTS; Web Audio API para SFX. Desplegado como GitHub Pages desde `main`. Elegido por el usuario para evitar sobreingeniería durante la validación.

## Users

- **Niño (2-7 años).** Usa la app directamente en una tablet/móvil con asistencia inicial del padre. No sabe leer todavía o está empezando. Toca con dedos imprecisos, se distrae rápido, necesita feedback inmediato visual + sonoro, no tolera texto denso ni esperas largas.
- **Padre/madre.** Instala la app en el dispositivo del hijo y le guía los primeros usos. Decide qué lotes activar. Observa el progreso para sentir que la inversión de tiempo da fruto.

## Product Purpose

Enseñar a leer a niños de 2 a 7 años con el método Doman (palabra global, flashcards rápidas, repetición espaciada, componente emocional) + gamificación mínima que respete el ritmo pedagógico. Éxito = el niño reconoce visualmente las palabras expuestas 75 veces, y el padre percibe progreso tangible semana a semana.

## Positioning

Fiel al método Doman real (3 sesiones/día por lote con cadencia de 8h, 5 cards × 5 pases por sesión, 75 exposiciones por palabra, lotes de 5), **pero con bucle de recompensa diseñado para que la pedagogía no se pueda saltar**: las monedas se ganan sólo leyendo, el techo de monedas lo impone el método (no la cartera), los juegos consumen esas monedas, no las generan.

Diferenciador frente a Leo con Grin y similares: **el ejercicio post-sesión** (une palabra con imagen) refuerza en el mismo flow los tres enlaces del método — sonido ↔ escritura ↔ imagen — sin convertirse en un test puntuado.

## Operating Context

Uso típico en casa, sofá o cama, con la tablet/móvil del padre. Sesiones muy cortas (≈30-45 s cada una, +15 s el ejercicio de refuerzo). El niño entra, lee, hace el ejercicio, juega un rato (1-3 vidas = 10-60 s por partida), y sale. El padre puede supervisar o dejar al niño libre con confianza porque la cadencia Doman y el tope de monedas limitan el abuso.

Instalable como PWA ("Añadir a inicio") en Chrome Android y Safari iOS. Funciona offline tras la primera carga.

## Capabilities and Constraints

**Capacidades confirmadas y funcionando:**
- 10 lotes neutros/universales × 5 cards cada uno (50 palabras + 50 emojis). Catálogo en `content/batches.json`.
- Sesión Doman con 5 pases alternados (texto · imagen · texto · imagen · texto), 1 s por card, voz TTS en español.
- Ejercicio post-sesión "une palabra con imagen": 5 rondas, 3 opciones por ronda.
- Cadencia de 8h por lote; máximo 2 lotes activos simultáneamente; 15 sesiones = lote dominado (libera slot).
- Economía: 1 sesión = +3 monedas; 1 moneda = 1 vida en el juego; monedas acumulables, sin tope ni reset.
- 3 mini-juegos: Runner (esquivar), Parking (memoria 2×2), Carrera (ritmo).
- Pestaña "Mis palabras" para refuerzo libre tap-to-hear.
- Persistencia en localStorage.
- SFX con Web Audio API + haptics con `navigator.vibrate`.
- Soporte `prefers-reduced-motion` y `:focus-visible`.

**Restricciones duras:**
- Cero backend. Cero cuentas de usuario. Cero IA.
- Cero imágenes/audio como archivos: TTS del navegador + emoji como placeholder visual.
- Un solo HTML (`index.html`) + un JSON de contenido + 3 SVG + 1 service worker.
- No añadir dependencias de build (npm, bundlers, frameworks) hasta validar con usuarios reales.

**Terminología del dominio:**
- *Lote*: conjunto de 5 cards sobre un tema (Mi mundo, Mi cuerpo, Animales, …).
- *Sesión*: una ronda completa de 5 pases × 5 cards (25 exposiciones).
- *Exposición*: una presentación individual de una card.
- *Mastery*: 15 sesiones = 75 exposiciones por card = lote dominado.

## Brand Commitments

- **Nombre:** FunCards (juego de palabras: *Fun* + *Cards* — cartas de aprendizaje). Nunca "FunCars" (el repo mantiene ese nombre por historia pero la app es FunCards).
- **Marca tipográfica:** Pixelify Sans para `.brand` (letras pixel modernas); Fredoka para cuerpo (redonda, legible para niños).
- **Rojo Doman:** `#E53935` como color de identidad y de todas las palabras visualmente centrales (fiel al método original de tarjetas de cartón con tinta roja gigante).
- **Voz:** cercana, directa, en segunda persona para el niño ("¡Lo has conseguido!"), observacional para el padre ("3 de 15 sesiones").

## Evidence on Hand

- `content/batches.json`: 10 lotes × 5 cards reales, en español neutro.
- `index.html`: implementación completa funcional.
- Desplegado en https://pvblorodri-collab.github.io/FunCars/
- Repositorio https://github.com/pvblorodri-collab/FunCars
- **Sin usuarios reales todavía.** Prototipo pendiente de probar con un niño.
- No existen testimonios, métricas de uso ni validación de retención.

## Product Principles

1. **La pedagogía no se puede saltar.** Toda decisión de gamificación debe respetar o reforzar el método Doman (3 sesiones/día por lote, 5 cards, 15 sesiones a mastery). Si una feature permite acelerar el loop por fuera del método, se descarta.
2. **El niño es el usuario, no el cliente.** Prioridad a la UX táctil, tiempos cortos, feedback inmediato, cero texto denso. El padre tiene su propia superficie (progreso visible), pero no debería mediar cada interacción.
3. **Validar antes de añadir.** Cada feature nueva se mide contra "¿la vas a probar con un niño esta semana?". Si no, se pospone.
4. **Un solo archivo mientras se pueda.** Zero-stack mientras no haya usuarios reales. El coste de reescritura a RN/stack real sólo se asume cuando la demanda está probada.
5. **Honestidad con el método.** El método Doman tiene controversia científica; evitar afirmaciones de resultados en el marketing. Vender lo que se ve: estructura, consistencia, hábito.

## Accessibility & Inclusion

- Target 2-7 años: tamaños de touch ≥44 px, texto cabecera ≥32 px, cero scroll obligatorio en flujos críticos.
- Soporte `prefers-reduced-motion` activado (animaciones no esenciales se detienen).
- `:focus-visible` con anillo rojo visible para navegación por teclado.
- Palabras y voz en es-ES; voz más usada que texto como anclaje para pre-lectores.
- Lotes neutros (sin género, cultura ni religión impuestos). Lote "Mi familia" personalizable está en roadmap para que cada hogar meta sus nombres reales.
