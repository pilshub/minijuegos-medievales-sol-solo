# Minijuegos Medievales (Sol & Sol)

Pack de **tres minijuegos de arcade artesanal** con estética de pergamino
ilustrado. Diseñado por **Sol**, ejecutado por **DeepSeek V4 Flash**.

Sin dependencias externas: sin frameworks, sin build, sin red, sin fuentes
remotas. Todo el arte (portadas, marcos, escenas) está dibujado en HTML/CSS
puro y canvas 2D.

## Cómo abrir (sin build)

Abre `index.html` directamente en un navegador moderno (doble clic) o sirve
la carpeta con un servidor estático simple:

```
python -m http.server 8000
# luego visita http://localhost:8000
```

No hay pasos de instalación ni compilación.

## Juegos y mecánicas

| Juego | Archivo | Mecánica |
|---|---|---|
| **Tras las Almenas** | `castillo.html` | Defensa táctica: asigna espadas, arqueros y reparaciones antes de cada una de las 5 oleadas (infantería, arietes, torres de asedio). |
| **La Fragua del Herrero** | `fragua.html` | Ritmo y precisión: golpea el hierro en la zona dorada (2 golpes útiles), templa con el agua en el momento justo y lima el patrón. 4 ciclos → calidad S–E. |
| **El Mensajero del Rey** | `heraldo.html` | Carrera de carriles al atardecer (rocas, acequias, atajos y un río) + puzle de memoria de púas y puñales ante la puerta del bosque. |

## Controles

Todos los juegos funcionan con **táctil** (botones grandes en pantalla) y con
**teclado** (los botones nunca se deshabilitan).

| Juego | Botones táctiles | Teclado |
|---|---|---|
| Castillo | Asignar · Flechas · Reparar · Oleada | `1`/`↑` asignar · `2` arqueros · `3`/`↓` reparar · `␣`/`→` oleada · `Enter` empezar |
| Fragua | Martillo · Templar · Agua · Entregar | `◀` martillo · `↑` templar · `↓` agua · `␣`/`→` acción de fase · `Enter` empezar |
| Heraldo (camino) | Izq · Saltar · Der · Entrega(señales) | `←`/`→` carril · `␣`/`↑` saltar · `E`/`Enter` señales |
| Heraldo (bosque) | Púa · Pista · Puñal · Confirmar | `←` púa · `→` puñal · `␣`/`↑` repetir exhibición · `E`/`Enter` confirmar |

Durante el juego, las flechas y la barra espaciadora **no desplazan la página**
(`preventDefault`).

## Persistencia (localStorage)

Cada juego guarda su récord en este dispositivo (espacio de nombres propio):

- `minijuegos-medievales.castillo.record` — mejor puntuación de victoria (número).
- `minijuegos-medievales.fragua.record` — mejor calidad de hoja lograda (número).
- `minijuegos-medievales.heraldo.record` — `{"mejorPuntos": N, "mejorTiempo": S}` (JSON).

Los datos corruptos se ignoran sin romper el juego (lectura protegida con
`try/catch`).

## Estructura

- `index.html` — menú con portadas de los tres juegos (escenas CSS puras).
- `style.css` — tokens, reset, pergamino, marcos heráldicos, HUD, shell de
  juego, barras, paneles, controles táctiles, estados comunes y modificadores
  por `body.castillo|fragua|heraldo`.
- `castillo.html`, `fragua.html`, `heraldo.html` — los tres juegos completos.
- `project_config.json` — configuración para el verificador automático.

## Verificación (gauntlet)

Para ejecutar el QA automatizado (sintaxis, HTTP, navegador y partida real):

```
python C:/Users/fermi/_active/gaming/gauntlet/gauntlet.py run --project .
```

Los checks (`SYNTAX`, `HTTP`, `BROWSER`, `PLAY`) validan: JS inline sin
errores, recursos servidos con HTTP 200, navegación móvil sin errores de
consola y transiciones observables al pulsar los botones de acción.
