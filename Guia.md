# Guía para explicar "Libro Mayor: El Duelo Contable"

Documento de apoyo para que tu cliente pueda presentar el proyecto y responder preguntas de su profesora de programación con seguridad.

---

## 1. ¿Qué es el juego? (resumen de 30 segundos)

> "Es un juego de cartas por turnos, inspirado en Balatro e Inscryption, donde cada carta representa una transacción contable real (ventas, pagos, préstamos, etc.). El jugador arma 'asientos contables' combinando cartas, y si el Debe cuadra con el Haber, gana el doble de puntos. Gana quien primero llegue a 1000 puntos. Se puede jugar contra otra persona en el mismo dispositivo o contra una IA."

Puntos clave a mencionar:
- **Género:** roguelike de cartas / card battler por turnos.
- **Tema:** procedimiento administrativo-contable (libro mayor, partida doble, Debe/Haber).
- **Objetivo pedagógico implícito:** refuerza de forma lúdica el principio de partida doble (Activo = Pasivo + Patrimonio, Debe = Haber).

---

## 2. Mecánicas del juego

| Elemento | Explicación simple |
|---|---|
| **Mano** | Cada turno recibes 7 cartas de transacciones al azar. |
| **Asiento** | Eliges entre 2 y 5 cartas de tu mano. |
| **Cuadre** | Si la suma del Debe de las cartas elegidas es igual a la suma del Haber, el asiento "cuadra". |
| **Puntaje** | Puntos = suma del valor de las cartas × 2 (si cuadra) o × 0.5 (si no cuadra). |
| **Redibujar** | Una vez por turno puedes descartar tu mano y pedir una nueva. |
| **Meta** | El primer jugador (o la IA) en llegar a 1000 puntos gana. |
| **Modos** | 1 jugador vs. IA ("El Auditor") o 2 jugadores en el mismo dispositivo (turnos alternos con pantalla de traspaso). |

---

## 3. ¿Cómo funciona la IA ("El Auditor")?

Explicación técnica sencilla:

- La IA **no usa aprendizaje automático ni redes neuronales** — usa **fuerza bruta controlada**: prueba todas las combinaciones posibles de su mano (de 2 a 5 cartas) y calcula el puntaje de cada una con la misma fórmula que usa el jugador.
- Con una mano de 7 cartas, el número total de combinaciones posibles es pequeño (112 combinaciones: C(7,2)+C(7,3)+C(7,4)+C(7,5)), así que la IA puede evaluarlas **todas** en milisegundos y elegir siempre la mejor jugada posible.
- Si su mejor jugada no logra un asiento cuadrado, usa su redibujo antes de decidir, igual que podría hacerlo un jugador humano.
- **Por qué esto es válido como respuesta técnica:** cuando el espacio de posibilidades es pequeño y conocido, la fuerza bruta *es* la solución óptima — no hace falta un algoritmo más complejo para que sea "una IA lo suficientemente buena".

---

## 4. Stack tecnológico y por qué se eligió

| Decisión | Justificación |
|---|---|
| **HTML + CSS + JavaScript puro** (sin frameworks como React o motores como Unity) | El juego corre en cualquier navegador sin instalar nada, sin proceso de compilación (build), y se puede subir a cualquier hosting estático (GitHub Pages, Netlify, Vercel) en minutos. |
| **Un solo archivo autocontenido** | Facilita la entrega, el hosting y la futura conversión a APK — no depende de un backend ni de una base de datos. |
| **Sprites en pixel art generados por código (SVG)** | En vez de usar imágenes descargadas, cada ícono se genera dibujando una cuadrícula de píxeles con código. Esto evita depender de archivos de imagen externos y mantiene el juego 100% liviano. |
| **Sin librerías externas de terceros** (solo tipografías de Google Fonts para el estilo visual) | Menos dependencias = menos puntos de falla = más fácil de mantener y de explicar línea por línea. |

**Cómo se convertiría en APK:** al ser HTML/CSS/JS estándar, se puede envolver con **Capacitor** o **Cordova** (herramientas que empaquetan una página web dentro de una app Android/iOS) sin reescribir el código del juego.

---

## 5. Proceso de desarrollo (metodología)

Puedes describirlo como un mini-proceso iterativo, útil si preguntan "¿cómo lo desarrollaste?":

1. **Levantamiento de requisitos:** el cliente definió las condiciones obligatorias (puntos acumulativos con meta, multijugador local o IA, temática contable, accesibilidad vía web/APK).
2. **Diseño del concepto:** se tomó como referencia la estructura de juegos de cartas con multiplicadores (Balatro) y de duelo por turnos con un rival con personalidad (Inscryption), adaptando la mecánica central al dominio contable (el "cuadre" Debe = Haber como condición de bono).
3. **Prototipo funcional:** se construyó primero la lógica de juego (datos de cartas, cálculo de puntaje, turnos) y después la interfaz visual.
4. **Iteración con el cliente:** tras la primera versión, se simplificaron las reglas a 4 pasos claros, se añadieron los sprites en pixel art y un botón de salida al menú con confirmación, para mejorar la experiencia de uso.
5. **Verificación:** se validó la sintaxis del código y el comportamiento del juego (que la IA siempre calcule una jugada válida, que el marcador y las condiciones de victoria funcionen correctamente).

---

## 6. Preguntas frecuentes que podría hacer una profesora de programación (con respuesta corta)

**¿Qué lenguaje usaste y por qué no uno "más serio" como Java o C#?**
JavaScript porque el requisito era que fuera accesible desde cualquier navegador sin instalación; es la opción estándar para juegos web y no limita una futura conversión a app móvil.

**¿Cómo estructuraste el código?**
Separando tres responsabilidades: los *datos* (lista de cartas, categorías, íconos), la *lógica* (funciones puras como el cálculo de puntaje, que no dependen de la pantalla) y la *interfaz* (funciones que dibujan el estado actual en pantalla). El estado del juego completo vive en un solo objeto (`state`).

**¿Qué es una "función pura" en tu código y dónde la usaste?**
Es una función que, dado el mismo input, siempre da el mismo output y no modifica nada fuera de sí misma. La función que calcula el puntaje de un asiento es un ejemplo: solo recibe las cartas seleccionadas y devuelve el resultado, sin tocar el resto del juego.

**¿Cómo evitas que la IA haga trampa?**
Usa exactamente la misma función de puntaje, el mismo tamaño de mano y el mismo mazo de cartas que el jugador humano; no tiene información oculta ni ventajas.

**¿Qué complejidad tiene el algoritmo de la IA?**
Es acotada (el tamaño de la mano siempre es 7), así que aunque técnicamente es fuerza bruta exponencial en el caso general, aquí es constante en la práctica: siempre evalúa como máximo 112 combinaciones.

**¿Cómo probaste que el juego funciona sin errores?**
Se validó la sintaxis del JavaScript de forma automática y se revisó manualmente cada flujo: iniciar partida, seleccionar cartas, jugar un asiento, redibujar mano, cambiar de turno, ganar la partida y volver al menú principal.

**¿Qué mejorarías si tuvieras más tiempo?**
Guardar el progreso entre sesiones, agregar sonido y animaciones, sumar más tipos de transacciones/cartas especiales, y un modo multijugador en línea (no solo local).

**¿Por qué el juego usa pixel art y no gráficos más "realistas"?**
Es una decisión de estilo coherente con el género (roguelikes de cartas como Balatro/Inscryption suelen usar estética retro/pixel), y además los sprites pixel art se pueden generar con código simple (cuadrículas de colores), sin necesitar un diseñador gráfico ni imágenes externas.

---

## 7. Frase de cierre sugerida

> "El juego cumple los cinco requisitos originales: tiene un sistema de puntos acumulativos con una meta clara (1000 pts), ofrece tanto multijugador local como una IA competente, está completamente tematizado en el proceso contable de partida doble, es accesible desde cualquier navegador y puede convertirse en APK sin cambios de código, y fue construido priorizando la menor cantidad de dependencias posible para minimizar errores."
