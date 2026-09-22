# Universo de flores para Karen — experiencia cinematográfica (V3)

## Objetivo
Reescribir `index.html` como una experiencia web romántica y mágica de un solo archivo: entrada a un universo oscuro, viaje warp dorado, universo central con girasol-sol, constelación KAREN interactiva, planeta de flores, mensaje tranquilo, lluvia de flores delicada y final contemplativo eterno.

## Por qué
El usuario pidió explícitamente generar de cero el archivo completo con una estética espacio profundo + flores amarillas, sofisticada (no infantil), sin librerías, 100% offline.

## Alcance
- Único archivo: `Descargas/Karen/index.html` (ruta relativa al repo `dalan`).
- HTML, CSS inline, JS inline, SVG inline, un `<canvas>` para cosmos, sin frameworks/CDN/externos.
- Copy exacta definida por el usuario (español). KAREN como protagonista.
- Responsive (móvil vertical/horizontal, tablet, PC) + `prefers-reduced-motion`.

## Checklist
- [ ] T1 Base HTML + sprite SVG + canvas cosmos (estrellas, nebulosas, galaxia, polvo, parallax de cursor)
- [ ] T2 Pantalla de entrada (estrella dorada, textos con delays, botón) + transición warp (túnel dorado ~2.4s)
- [ ] T3 Universo central: girasol-sol con glow/pulso, órbitas múltiples de distintos radios/velocidades, textos "KAREN" y cita
- [ ] T4 Constelación KAREN (5 clusters K-A-R-E-N con líneas sutiles) + clic en estrellas → explosión dorada
- [ ] T5 Planeta de flores (gira, hover/touch → crece, brilla, libera pétalos) + pétalos orbitando
- [ ] T6 Sección mensaje (calma, flor central, 4 líneas con pausas) + lluvia de flores/pétalos/estrellas delicada
- [ ] T7 Final: oscurecimiento, flor reaparece, 5 líneas, "Fin del viaje", escena sigue indefinidamente
- [ ] T8 Validación: HTML balanceado (python html.parser), `node --check` del script extraído, presencia de toda la copy (texto normalizado)

## Checks aplicables
- `python3 - <<'PY' ... html.parser ... PY` sobre index.html (tags balanceados, sin unclosed)
- `node --check /tmp/opencode/karen_script_v3.js` (sintaxis JS del script extraído)
- Verificación de las 16+ cadenas de copy con texto normalizado (sin tags, unescape, whitespace colapsado)

## Progreso
- [x] Respaldo de V2 en /tmp/opencode/karen-v2-atardecer.html
- [x] T1 Base HTML + sprite SVG + canvas cosmos (estrellas, nebulosas, galaxia, polvo, parallax de cursor)
- [x] T2 Pantalla de entrada (estrella dorada, textos con delays, botón) + transición warp (túnel dorado ~2.4s)
- [x] T3 Universo central: girasol-sol con glow/pulso, órbitas múltiples de distintos radios/velocidades, textos "KAREN" y cita
- [x] T4 Constelación KAREN (5 clusters K-A-R-E-N con líneas sutiles) + clic en estrellas → explosión dorada
- [x] T5 Planeta de flores (gira, hover/touch → crece, brilla, libera pétalos) + pétalos orbitando
- [x] T6 Sección mensaje (calma, flor central, 4 líneas con pausas) + lluvia de flores/pétalos/estrellas delicada
- [x] T7 Final: oscurecimiento, flor reaparece, 5 líneas, "Fin del viaje", escena sigue indefinidamente
- [x] T8 Validación: HTML balanceado (0 errores), node --check OK, copy completa (17 cadenas, normalizada con <br>→espacio)

- [x] **Fix crítico móvil (reporte real del usuario)**: botón "Entrar" no respondía y scroll pegado.
  - Causa: `body{overflow:hidden}` hasta entrar + botón vinculado al FINAL del script → si cualquier init falla en móvil, muere el botón Y el scroll.
  - Fix: la página ahora scrollea SIEMPRE (sin overflow:hidden base); #entry es overlay fijo con overscroll-behavior:contain; el botón se vincula PRIMERO con pointerup+click (guard `entering`); body.warping congela scroll solo durante el warp; try/catch en frame/resize/ARRANQUE.
- [x] **V4 — navegación sin dependencia del scroll (segundo reporte del usuario)**: el botón "Entrar" ahora MANDA directo al primer apartado: oculta la entrada con fade de 0.45s, scrollTo(0,0), universo visible de inmediato; túnel warp reducido a adorno de 1.15s que nunca bloquea; listeners extra touchend; respaldo force-vis a los 7.2s (si el navegador pausa animaciones por modo ahorro, botón y textos aparecen igual); botón fijo `#nextBtn` (↓) para avanzar de sección en sección con un toque sin gesto de scroll, desaparece al final; IntersectionObserver protegido con try/catch + guard de soporte.

- [x] **V5 — soporte WhatsApp/Quick Look (iPhone + Safari en app)**: el usuario abre el HTML directamente desde WhatsApp → Quick Look NO ejecuta JavaScript (por eso el botón seguía muerto). Fix: el botón es ahora `<label for="enterToggle">` + checkbox oculto; CSS `#enterToggle:checked ~ #entry` retira la entrada SIN JavaScript (funciona en Quick Look); revela .reveal y muestra #nextBtn por CSS; el JS sigue igual para Safari normal (warp, parallax, lluvia). Ambas vías coexisten (label marca checkbox nativo + enterFlow sincroniza tg.checked).

## Siguiente paso
Prueba física: (1) abrir desde WhatsApp → botón debe funcionar por CSS; (2) "Abrir en Safari" para la experiencia completa (warp, lluvia, botón ↓).