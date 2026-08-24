# Minijuegos Medievales Nuevos — pack con Sol (diseño) + DeepSeek V4 (ejecución)

Construye el proyecto COMPLETO en el directorio actual
(C:\Users\fermi\_active\gaming\minijuegos-medievales-nuevo), repo git vacío
en rama `main`. No hagas commits.

## Estilo de trabajo (importante)

- **Sol (orquestador)** ha diseñado cada juego con criterio. Respeta ese diseño
  al pie de la letra: mecánica, ritmo, curva de dificultad, arte y paleta.
- **El ejecutor eres tú (DeepSeek V4 Flash)**: tu trabajo es convertir la
  especificación de diseño en HTML/CSS/JS impecable y jugable. No inventes
  mecánicas que contradigan el diseño; implementa lo que esté especificado.
- Código pulido: canvas 2D con devicePixelRatio, rAF con delta-time, pausa por
  visibilitychange, botones ≥48px, teclado como alternativa.

## Páginas

- `index.html` — menú medieval con portadas de los 3 juegos (tarjetas táctiles)
- `castillo.html` — «Tras las Almenas» (gestión/defensa táctica)
- `fragua.html` — «La Fragua del Herrero» (artesanía/rompecabezas)
- `heraldo.html` — «El Mensajero del Rey» (aventura + puzle)
- `style.css` — estética medieval coherente
- `README.md`

Sin dependencias externas (sin frameworks, build, red, fuentes remotas).

## Convención de IDs (obligatoria — la usa el verificador automático)

Cada juego de los 3 (NO el menú) debe tener:
- Pantalla de título: `<div class="overlay" id="mj-titulo">` con botón
  `<button id="btn-jugar">▶ JUGAR</button>` y texto de mecánica.
- Al pulsar JUGAR: overlay se oculta (`display:none`) y aparece HUD
  `<div id="mj-hud" class="hud">`.
- Botones táctiles con estos ids (mín 44px) + aria-label, sin `disabled`:
  - **castillo.html**: `#bt-asignar`, `#bt-reparar`, `#bt-flechas`, `#bt-oleada`
  - **fragua.html**: `#bt-martillo`, `#bt-templar`, `#bt-agua`, `#bt-entregar`
  - **heraldo.html**: `#bt-der`, `#bt-izq`, `#bt-saltar`, `#bt-interact`
- Los botones de acción DEBEN cambiar la pantalla de forma visible al tocarlos.
- `touch-action:none` en canvas, botones grandes, teclado flechas+espacio.
- Récord en localStorage namespaced.

## Juego 1 — «Tras las Almenas» (castillo.html) [DISEÑO SOL]

Gestión táctica de defensa de un castillo en vista de perfil.

- **Fases de oleada.** El jugador asigna recursos entre guarnición (espadas),
  arqueros y reparaciones ANTE de cada oleada; luego la oleada entra
  (infantería, arietes, torres de asedio) y atacan la muralla en tiempo real.
- Recursos: monedas (llegan al matar/en oleada), madera (aldeanos automáticos),
  piedra (reparar). Arqueros cuestan oro+tiempo.
- Enemigos con velocidad/vida distinta; ariete hace mucho daño a la puerta;
  reparar resta poco pero se suele hacer seguido.
- **Objetivo**: aguantar 5 oleadas escaladas sin que la muralla (% vida) caiga.
  Curva suave con picos en oleadas 3 y 5. Bonificación por reserva.
- HUD en tiempo real: vida de muralla, recursos, oleada, bajas.

## Juego 2 — «La Fragua del Herrero» (fragua.html) [DISEÑO SOL]

Rompecabezas de ritmo y precisión:

- Golpea el hierro al rojo cuando el marcador de calentamiento está en la ZONA
  DORADA (una barra sube y baja). Pocos golpes bien calibrados forjan mejor
  espada que muchos malos.
- Ciclos por espada: Forja (precisión del golpe) → Templado (enfriar al tocar
  el momento justo) → Pulido (lima con el patrón correcto). 3-4 ciclos hasta
  completar la espada final.
- Al final se muestra la calidad de la espada (S→E) y se guarda récord.
- Ritmo pausado pero con precisión. Feedback visual: chispas al calibrar bien,
  grietas al fallar. Barra de calidad con letra final.

## Juego 3 — «El Mensajero del Rey» (heraldo.html) [DISEÑO SOL]

Aventura de dos fases con narrativa ligera:

- **Fase 1 — Cabalgar por el camino real.** Esquiva rocas, acequias, atajos y
  un río; evita caer y no pierdas el pergamino. Controles: `#bt-der`/`#bt-izq`
  para moverse (o flechas), `#bt-saltar` para superar obstáculos; la velocidad
  sube de forma natural.
- **Fase 2 — En el bosque.** Puzle de memoria: orden de símbolos (púas/puñal)
  para desbloquear la aldea y entregar el mensaje con 1 de 3 esfuerzos
  (buena/media/mínima).
- Persistencia: puntos y rapidez. Arte de atardecer, paleta pergamino/tierra.

## Verificación automática (obligatoria al final)

- Ejecuta:
  `python C:/Users/fermi/_active/gaming/gauntlet/gauntlet.py run --project .`
  y corrige hasta que SYNTAX, HTTP, BROWSER y, si hay selectores, PLAY pasen.
- No dejes servidores activos; no hagas commits.

## Entrega

- Resumen: archivos, mecánica de cada juego, resultado real del gauntlet run.