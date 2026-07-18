# 📊 Libro Mayor: El Duelo Contable

Un videojuego web casual de cartas y estrategia con temática contable retro. ¡Cuadra tus asientos antes que tu rival, domina el Libro Diario y cierra el balance para ganar la auditoría!

---

## 🧐 ¿De qué trata el juego?

**Libro Mayor: El Duelo Contable** es un juego de mesa digital por turnos diseñado para 1 o 2 jugadores (en el mismo dispositivo). La mecánica principal emula la contabilidad por partida doble tradicional, transformándola en un rompecabezas táctico y competitivo:

1. **La Mano:** Cada turno recibes **7 cartas** de transacciones financieras (Caja, Banco, Mercancías, Gastos, Ingresos, etc.).
2. **El Asiento:** Debes seleccionar libremente entre **2 y 5 cartas** para estructurar un asiento contable.
3. **La Partida Doble:** Cada carta aporta puntos a la columna del **Debe** o del **Haber**, además de un valor intrínseco en puntos.
4. **El Multiplicador:** 
   - **¡Cuadrado! (✓)** Si la suma del *Debe* es exactamente igual a la del *Haber*, el asiento está balanceado y tus puntos acumulados en ese turno se **duplican (x2)**.
   - **¡Descuadrado! (✗)** Si los montos no coinciden, el asiento es inválido ante la ley de auditoría y solo conservas la **mitad de los puntos (x0.5)**.
5. **La Meta:** El primer contador en alcanzar **1,000 puntos** cierra el balance general y se corona como el **Contador Mayor**.

---

## 🛠️ Modalidades de Juego

*   **👤 1 Jugador vs CPU ("El Auditor"):** Enfréntate a una Inteligencia Artificial algorítmica local que analiza de forma exhaustiva las combinaciones posibles en su mano para registrar siempre el asiento más óptimo y balanceado.
*   **👥 2 Jugadores (Local / Pass & Play):** Compite contra un colega en el mismo dispositivo. El juego incluye un sistema de protección de pantalla (*Handoff Overlay*) para que tu oponente no pueda espiar tus cartas cuando sea tu turno.

---

## 🎨 Características Visuales y Estéticas

*   **Estilo "Paper & Ink":** Diseño minimalista inspirado en libros contables antiguos, hojas de balance amarillentas y tipografías mecánicas (*Special Elite* e *IBM Plex Mono*).
*   **Pixel Art Procedural Integrado:** Motor interno en JavaScript para renderizar iconos vectoriales tipo píxel (`<svg>`) sin dependencias de imágenes externas ni librerías pesadas.
*   **Adaptabilidad Móvil:** Interfaz completamente interactiva, responsiva y diseñada con consideraciones de reducción de movimiento (*prefers-reduced-motion*).

---

## ⚙️ Tecnologías Utilizadas

*   **HTML5** estructurado para semántica de juegos.
*   **CSS3** avanzado utilizando variables nativas, degradados lineales repetitivos para simular renglones de papel, y diseño flexible.
*   **Vanilla JavaScript (ES6+)** puro. Sin frameworks, empaquetadores ni librerías externas. Todo el estado del juego, la lógica de combinatoria matemática y la IA se ejecutan de manera local e instantánea en el cliente.

---

## 🚀 Cómo Ejecutar el Proyecto

Al ser un desarrollo basado puramente en tecnologías web nativas, no necesitas instalar entornos complicados ni servidores de backend:

1. **Clona este repositorio:**
   ```bash
   git clone https://github.com/tu-usuario/libro-mayor-duelo-contable.git
   ```
2. **Navega al directorio del proyecto:**
   ```bash
   cd libro-mayor-duelo-contable
   ```
3. **Abre el archivo `index.html` en tu navegador favorito:**
   - Simplemente haz doble clic sobre el archivo en tu explorador de archivos.
   - O ejecútalo desde la terminal si usas un servidor ligero (ej. `python -m http.server 8000` o la extensión *Live Server* de VS Code).

---

## 🧠 Lógica Detrás de la IA ("El Auditor")

La IA utiliza un enfoque de **fuerza bruta optimizada** a través de combinatoria indexada. En cada turno, calcula todas las combinaciones posibles de subconjuntos de tamaño 2 a 5 elementos a partir de sus 7 cartas disponibles (un total de $21 + 35 + 21 = 77$ combinaciones potenciales). 
Evalúa el puntaje final neto resultante aplicando las reglas del multiplicador, y prioriza la opción que maximice el rendimiento total de puntos. Si detecta que ninguna combinación inicial le permite cuadrar un balance, ejecuta estratégicamente la mecánica de redibujo de mano antes de tomar una decisión definitiva.
