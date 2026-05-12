---
title: "Índice de Bienestar Personal — Documentación Oficial"
subtitle: "IBP v5 · Ecosistema de Medicina Holística · Puerto Rico"
date: "Mayo 2026"
author: "Ecosistema de Medicina Holística"
---

# Índice de Bienestar Personal (IBP)
## Documentación Oficial · Versión 5

**Ecosistema de Medicina Holística · Puerto Rico**
**Versión:** IBP v5
**Formato:** Aplicación web de archivo único (Single-File Web App)
**Idioma:** Español

---

## Tabla de Contenidos

1. [Descripción General](#1-descripción-general)
2. [Fundamento Conceptual y Científico](#2-fundamento-conceptual-y-científico)
3. [Arquitectura Técnica](#3-arquitectura-técnica)
4. [Pantallas y Flujo de Navegación](#4-pantallas-y-flujo-de-navegación)
5. [Los 10 Pilares del Buen Vivir](#5-los-10-pilares-del-buen-vivir)
6. [Algoritmo de Cálculo del IBP](#6-algoritmo-de-cálculo-del-ibp)
7. [Panel de Resultados](#7-panel-de-resultados)
8. [Gestión del Historial](#8-gestión-del-historial)
9. [Esquema de Datos (localStorage)](#9-esquema-de-datos-localstorage)
10. [Funciones JavaScript](#10-funciones-javascript)
11. [Sistema de Diseño Visual](#11-sistema-de-diseño-visual)
12. [Accesibilidad y Teclado](#12-accesibilidad-y-teclado)
13. [Diseño Responsivo](#13-diseño-responsivo)
14. [Guía de Uso Paso a Paso](#14-guía-de-uso-paso-a-paso)
15. [El Efecto Orquesta](#15-el-efecto-orquesta)
16. [La Ruta Semanal](#16-la-ruta-semanal)
17. [Tres Reglas Éticas](#17-tres-reglas-éticas)
18. [Privacidad y Almacenamiento](#18-privacidad-y-almacenamiento)
19. [Despliegue y Compatibilidad](#19-despliegue-y-compatibilidad)
20. [Glosario](#20-glosario)

---

## 1. Descripción General

El **Índice de Bienestar Personal (IBP)** es una herramienta de autoobservación semanal desarrollada dentro del ecosistema de medicina holística. Permite al usuario evaluar su semana en diez dimensiones del bienestar humano y obtener una puntuación compuesta (0–100) que refleja el estado actual de su salud integral.

### Propósito

El IBP transforma la salud de un concepto estático a una **práctica científica personal y dinámica**. Su objetivo no es diagnosticar ni prescribir, sino ofrecer una fotografía honesta de la semana vivida que facilite:

- La detección temprana de patrones de desgaste.
- El reconocimiento de fortalezas sostenibles.
- La elección de un microcambio concreto y ejecutable.
- El seguimiento de la evolución del bienestar a lo largo del tiempo.

### Declaración de alcance

> Esta herramienta es orientativa y complementaria. No mide el valor personal del usuario ni sustituye la atención de profesionales de salud mental, médicos u otros especialistas.

### Características principales

| Característica | Detalle |
|---|---|
| Tipo de aplicación | Archivo HTML único (sin servidor, sin instalación) |
| Dependencias externas | Ninguna (solo Google Fonts vía CDN) |
| Almacenamiento de datos | `localStorage` del navegador |
| Compatibilidad offline | Total |
| Idioma | Español |
| Versión actual | IBP v5 |

---

## 2. Fundamento Conceptual y Científico

### Enfoque transdisciplinario

El IBP integra conocimientos de múltiples disciplinas:

- **Medicina funcional:** enfoque en la causa raíz de las disfunciones y en la interacción de los sistemas biológicos.
- **Psicología positiva:** identificación de fortalezas, bienestar subjetivo y florecimiento humano.
- **Neurociencia comportamental:** hábitos, neuroplasticidad y toma de decisiones.
- **Longevidad funcional:** estrategias de vida que extienden los años saludables, no solo los años vividos.
- **Medicina holística:** visión integral del ser humano (biológica, psicológica, social y ambiental).

### Modelo biopsicosocial ampliado

El IBP adopta una definición de bienestar que va más allá de la ausencia de enfermedad. El bienestar es entendido como el **equilibrio practicable** entre cuatro dimensiones:

1. **Biológica:** nutrición, sueño, movimiento y recuperación física.
2. **Psicológica:** emociones, estrés, aprendizaje y expresión.
3. **Social:** vínculos, comunidad y contribución.
4. **Ambiental/Ocupacional:** entorno de trabajo, ocio y condiciones de vida.

### Filosofía operativa

La filosofía del IBP se articula en tres principios:

1. **Lo sostenible vence a lo perfecto.** Un hábito mediocre mantenido durante seis meses genera más beneficios que un protocolo perfecto abandonado en dos semanas.
2. **Lo pequeño vence a lo épico.** Los microcambios acumulados producen transformaciones profundas que los grandes propósitos frecuentemente no logran.
3. **Se mide para aprender, no para castigarse.** Cada número es información, no un juicio de valor sobre la persona.

---

## 3. Arquitectura Técnica

### Tecnología

El IBP es una **aplicación web de archivo único (Single-File Web App)**. Todo el código — HTML estructural, CSS de estilos y JavaScript de lógica — reside en un único archivo `index.html`.

```
indice-bienestar-mvp-1/
├── index.html          ← Aplicación completa
└── README.md           ← Guía de inicio rápido
```

### Stack tecnológico

| Capa | Tecnología | Versión/Estándar |
|---|---|---|
| Marcado | HTML5 | Semántico, ARIA |
| Estilos | CSS3 | Variables CSS, Grid, Flexbox |
| Lógica | JavaScript ES2020 | Vanilla (sin frameworks) |
| Tipografía | Google Fonts | Crimson Pro, Lora, IBM Plex Mono |
| Persistencia | Web Storage API | `localStorage` |

### Estructura del archivo HTML

```
index.html
├── <head>
│   ├── meta (charset, viewport)
│   ├── link (Google Fonts)
│   └── <style> (Sistema de diseño completo)
│
└── <body>
    ├── #screen-intro        (Pantalla de entrada — visible al cargar)
    ├── #pillar-modal-overlay (Modal de hábitos)
    ├── #app-nav             (Barra de navegación sticky — oculta al inicio)
    ├── #screen-app          (Pantalla principal — oculta al inicio)
    ├── #toast               (Notificaciones flotantes)
    └── <script>             (Toda la lógica JavaScript)
```

### Ciclo de vida de la aplicación

```
Carga de página
    │
    ▼
renderPillarsIntro()    → Genera tarjetas de pilares en pantalla de entrada
    │
    ▼
Usuario hace clic en "Comenzar mi evaluación semanal"
    │
    ▼
launchApp()
    ├── Oculta #screen-intro
    ├── Muestra #screen-app y #app-nav
    ├── renderQuestions()   → Genera los 10 sliders
    ├── renderResults()     → Calcula y muestra IBP inicial (todos en 5)
    └── renderHistory()     → Carga y muestra historial desde localStorage
```

---

## 4. Pantallas y Flujo de Navegación

### 4.1 Pantalla de Entrada (`#screen-intro`)

La pantalla de entrada es una página informativa completa que prepara al usuario para la evaluación. Sus secciones son:

#### Cabecera
- **Breadcrumb:** "Ecosistema Holístico · Bienestar Personal"
- **Eyebrow:** "Instrumento de Observación Semanal"
- **Título principal:** "Índice de Bienestar Personal"
- **Lead:** descripción filosófica del enfoque transdisciplinario.
- **Cita filosófica:** *"La vida no se optimiza, se habita — con conciencia, con propósito y con pequeños ajustes sostenibles."*

#### Caja de explicación del IBP
Explica visualmente qué es el IBP, cómo se calcula y qué significan las cuatro categorías de puntuación, acompañada de un círculo de puntuación de ejemplo (72/100).

#### Sección de los 10 pilares (`#pillarsIntroGrid`)
Cuadrícula de 10 tarjetas interactivas. Cada tarjeta muestra:
- Icono emoji del pilar.
- Número de pilar (01–10).
- Nombre del pilar.
- Descripción introductoria breve.
- Indicador visual "Ver 5 hábitos clave".

Al hacer clic se abre el **modal de hábitos**.

#### Modal de hábitos (`#pillar-modal-overlay`)
Ventana emergente accesible que muestra:
- Icono, número y nombre del pilar.
- Descripción introductoria extendida.
- Lista numerada de los 5 hábitos clave.
- Navegación entre pilares (← Anterior / Siguiente →).
- Contador de posición (ej. "3 / 10").
- Botón de cierre (✕).

#### Sección "El Efecto Orquesta"
Explica la interdependencia entre los pilares. Incluye un diagrama de sinergias clave con cuatro relaciones:

| Pilar origen | Impacta positivamente en |
|---|---|
| Sueño | Emocional + Intelectual |
| Relajación | Sueño + Ocupacional |
| Actividad física | Estrés + Emocional |
| Comunitario | Emocional + Ocio |

#### Sección "La Ruta Semanal"
Los cinco pasos del ciclo semanal (ver sección 16 de este documento).

#### Llamada a la acción (CTA)
- Botón principal: **"Comenzar mi evaluación semanal"** (id: `#startBtn`).
- Nota: *"Toma aproximadamente 5 minutos · Tus datos se guardan solo en este navegador."*

---

### 4.2 Pantalla Principal (`#screen-app`)

Contiene tres secciones principales:

#### Barra de navegación sticky (`#app-nav`)
Siempre visible al desplazarse dentro de la app. Contiene:
- Logo: "IBP · Bienestar Personal".
- Dos botones de navegación: **Evaluación** y **Historial** (con scroll suave al hacer clic).
- El botón activo se actualiza automáticamente según la sección visible.

#### Sección Hero
Presenta un resumen visual de la Ruta Semanal (5 pasos) junto a la descripción de la herramienta.

#### Sección Evaluación (`#sec-evaluacion`)
Cuadrícula de dos columnas:
- **Columna izquierda (`#questionsContainer`):** los 10 controles deslizantes de evaluación.
- **Columna derecha (`.results`):** el panel de resultados en tiempo real.

#### Sección Historial (`#sec-historial`)
Cuadrícula de tarjetas con todas las evaluaciones guardadas. Incluye botones de gestión del historial.

---

## 5. Los 10 Pilares del Buen Vivir

Cada pilar representa una dimensión fundamental del bienestar. A continuación se documenta cada uno con todos sus atributos.

---

### Pilar 01 — 🥗 Nutrición

**Introducción:** Uso de alimentos como combustible y material de construcción del cuerpo.

**Pregunta de evaluación:** ¿Qué tan equilibrada, suficiente y saludable sentiste tu alimentación e hidratación esta semana?

**Pista de orientación:** Piensa en calidad general, regularidad y alimentos mayormente reales.

**5 Hábitos clave:**
1. Consumir mayormente alimentos reales — más ingredientes, menos productos procesados.
2. Seguir la regla de MiPlato: ½ vegetales/frutas, ¼ proteína, ¼ carbohidratos.
3. Mantener horarios regulares de comida para estabilizar la energía.
4. Asegurar una hidratación adecuada con agua durante el día.
5. Escuchar las señales de hambre y saciedad del propio cuerpo.

**Microcambios sugeridos:**
- Agregar 1 fruta o 1 vegetal al día.
- Tener agua visible durante el día.

---

### Pilar 02 — 🌙 Sueño y Descanso

**Introducción:** Proceso de reparación física y mental que sostiene todo lo demás.

**Pregunta de evaluación:** ¿Qué tan reparador y regular fue tu descanso esta semana?

**Pista de orientación:** Piensa en calidad del sueño, regularidad y sensación de descanso.

**5 Hábitos clave:**
1. Mantener un horario constante para dormir y despertar, incluso en fines de semana.
2. Realizar una rutina de bajada: luz tenue y lectura los últimos 30 minutos.
3. Eliminar pantallas al menos 20 minutos antes de acostarse.
4. Priorizar el ritual de sueño sobre la fuerza de voluntad.
5. Asegurar un ambiente de descanso de calidad: oscuridad, silencio y temperatura fresca.

**Microcambios sugeridos:**
- Pantalla fuera 20 minutos antes de dormir.
- Bajar la luz 15 minutos antes de acostarte.

---

### Pilar 03 — 🚶 Actividad Física

**Introducción:** Combinación de movimiento diario, fuerza y movilidad para una energía sostenida.

**Pregunta de evaluación:** ¿Qué tanto te moviste de forma que favoreciera tu energía, fuerza o movilidad esta semana?

**Pista de orientación:** Incluye caminatas, estiramiento, baile, escaleras o ejercicio.

**5 Hábitos clave:**
1. Realizar movimiento diario: caminar, subir escaleras, moverse entre tareas.
2. Entrenar fuerza 2 a 3 veces por semana con pesas, bandas o peso corporal.
3. Dedicar 5–10 minutos a movilidad suave para mantener el cuerpo ágil.
4. Practicar una caminata de 10 minutos después de comer.
5. Evitar el sedentarismo prolongado con pausas de postura y estiramiento.

**Microcambios sugeridos:**
- Caminata de 10 minutos después de comer.
- Hacer 5 minutos de movilidad suave.

---

### Pilar 04 — 💛 Bienestar Emocional

**Introducción:** Capacidad de reconocer y responder a las emociones con habilidad y conciencia.

**Pregunta de evaluación:** ¿Qué tan capaz fuiste de reconocer y manejar tus emociones con conciencia esta semana?

**Pista de orientación:** No se trata de sentirte siempre bien, sino de notar y responder mejor.

**5 Hábitos clave:**
1. Practicar el "nombro para domar": identificar la emoción presente en el momento.
2. Escribir un diario breve de tres líneas sobre lo sentido y lo necesitado.
3. Mantener al menos una conversación segura con alguien de confianza.
4. Desarrollar la resiliencia ante los desafíos cotidianos sin autoexigencia excesiva.
5. Ejercer la pausa consciente antes de una reacción automática.

**Microcambios sugeridos:**
- Nombrar la emoción 1 vez al día.
- Escribir 3 líneas sobre cómo te sentiste.

---

### Pilar 05 — 🌬️ Relajación y Estrés

**Introducción:** Acción intencional de bajar el "volumen interno" y recuperar calma.

**Pregunta de evaluación:** ¿Qué tan bien lograste reducir tensiones y hacer pausas reales esta semana?

**Pista de orientación:** Respiración, pausas, oración, caminatas cortas o microdescanso cuentan.

**5 Hábitos clave:**
1. Realizar micro-relajaciones diarias de 3 a 10 minutos: respiración o meditación.
2. Aplicar higiene de pausas entre tareas largas para evitar la acumulación.
3. Identificar y limitar los drenajes de energía: multitarea y exceso de pantallas.
4. Practicar respiración lenta al mediodía como ancla de calma.
5. Establecer límites claros en trabajo y relaciones para proteger la paz mental.

**Microcambios sugeridos:**
- Respirar 3 minutos al mediodía.
- Hacer una pausa breve entre tareas largas.

---

### Pilar 06 — 🎨 Ocio y Juego

**Introducción:** Recreación que repara la motivación, la creatividad y el sentido de disfrute.

**Pregunta de evaluación:** ¿Qué tanto tuviste espacios de disfrute o recreación que realmente te recargaran esta semana?

**Pista de orientación:** Piensa en hobbies, paseos, naturaleza o actividades que te dejaron mejor.

**5 Hábitos clave:**
1. Priorizar el ocio nutritivo — hobbies, naturaleza — sobre el ocio drenante.
2. Planificar un bloque semanal no negociable de disfrute sano.
3. Participar en actividades sociales y juegos grupales.
4. Buscar encuentros con la naturaleza para recargar energía de forma profunda.
5. Permitirse el juego sin juicio de resultados ni productividad.

**Microcambios sugeridos:**
- Reservar 1 hora semanal de hobby sin culpa.
- Hacer un paseo corto sin pantalla.

---

### Pilar 07 — 📚 Aprendizaje

**Introducción:** Curiosidad activa y crecimiento mental continuo como práctica de vida.

**Pregunta de evaluación:** ¿Qué tanto aprendiste o integraste algo nuevo y útil esta semana?

**Pista de orientación:** Puede ser una idea, habilidad, lectura o conversación que te expandió.

**5 Hábitos clave:**
1. Aprender una cosa nueva por semana, sin importar el tema.
2. Integrar conocimientos en modo explicable: resumirlo en 60 segundos.
3. Consumir material educativo y cultural regularmente.
4. Desafiar la mente con juegos mentales, acertijos o nuevas perspectivas.
5. Practicar el pensamiento crítico al evaluar información y fuentes.

**Microcambios sugeridos:**
- Aprender 1 concepto y explicarlo.
- Leer 10 minutos sobre algo que te interese.

---

### Pilar 08 — ✍️ Expresión Artística

**Introducción:** Creación y expresión personal sin presión evaluativa ni resultado esperado.

**Pregunta de evaluación:** ¿Qué tanto encontraste espacio para crear o expresarte esta semana?

**Pista de orientación:** Dibujo, música, escritura, fotografía, diseño o cualquier forma creativa.

**5 Hábitos clave:**
1. Dedicar 20 minutos creativos a la semana: dibujo, música, escritura o diseño.
2. Enfocarse en el proceso creativo, no en el resultado estético.
3. Practicar la creación libre y la improvisación sin censura.
4. Explorar nuevas formas de expresión artística cada cierto tiempo.
5. Usar el arte como herramienta de regulación emocional.

**Microcambios sugeridos:**
- 15 minutos de creación libre.
- Tomar una foto consciente de algo bello.

---

### Pilar 09 — ⚖️ Bienestar Ocupacional

**Introducción:** Calidad de la relación con el trabajo, estudio o vocación principal.

**Pregunta de evaluación:** ¿Qué tan sostenible, organizada y significativa sentiste tu ocupación principal esta semana?

**Pista de orientación:** Piensa en trabajo, estudio u oficio: carga, sentido y sensación de avance.

**5 Hábitos clave:**
1. Definir objetivos pequeños y semanales para visibilizar el progreso.
2. Mantener un ritmo sostenible con pausas programadas y respetadas.
3. Organizar el entorno físico para reducir la fricción al comenzar tareas.
4. Buscar el sentido de propósito en las tareas diarias, incluso las rutinarias.
5. Establecer un equilibrio saludable entre el trabajo y la vida personal.

**Microcambios sugeridos:**
- Lista de 3 tareas, no de 30.
- Preparar el entorno de trabajo la noche anterior.

---

### Pilar 10 — 🤝 Bienestar Comunitario

**Introducción:** Conexión, pertenencia y contribución social como base de la salud integral.

**Pregunta de evaluación:** ¿Qué tan conectado, acompañado o útil te sentiste en relación con otras personas esta semana?

**Pista de orientación:** Vínculos, apoyo, pertenencia y oportunidades de contribuir.

**5 Hábitos clave:**
1. Tener al menos un contacto intencional semanal: llamada, visita o mensaje.
2. Realizar actos de contribución o ayuda a otras personas.
3. Participar en grupos o comunidades de interés compartido.
4. Cuidar los espacios comunes y el entorno social inmediato.
5. Practicar la empatía y la escucha activa en las relaciones cotidianas.

**Microcambios sugeridos:**
- Tener 1 conversación significativa a la semana.
- Escribir o llamar a alguien importante.

---

## 6. Algoritmo de Cálculo del IBP

### 6.1 Puntuación base

Cada pilar recibe una puntuación entera de **0 a 10** mediante un control deslizante (`<input type="range">`). El estado inicial de todos los pilares es **5**.

### 6.2 Cálculo de la puntuación total

```
IBP = Σ (valor de cada pilar)  donde  0 ≤ valor ≤ 10
IBP ∈ [0, 100]
```

La función JavaScript responsable:

```javascript
function computeResult() {
  const entries = pillarOrder.map(id => ({
    id,
    name: pillars[id].name,
    value: Number(state.responses[id] || 0)
  }));
  const ibp = entries.reduce((s, e) => s + e.value, 0);
  // ...
}
```

### 6.3 Clasificación por categorías

| Puntuación | Categoría | Descripción |
|---|---|---|
| 85 – 100 | **Equilibrio robusto** | Tus bases están firmes. Mantén lo que funciona y afina con suavidad. |
| 70 – 84 | **Buen rumbo** | Vas por buen camino. Una mejora focalizada puede darte más estabilidad. |
| 50 – 69 | **Señales de desgaste** | Hay cierta carga acumulada. Un microcambio en el lugar correcto importa. |
| 0 – 49 | **Modo rescate** | Tu sistema pide alivio. Empieza pequeño y sé amable contigo. |

```javascript
function classifyIBP(v) {
  if (v >= 85) return 'Equilibrio robusto';
  if (v >= 70) return 'Buen rumbo';
  if (v >= 50) return 'Señales de desgaste';
  return 'Modo rescate';
}
```

### 6.4 Selección del pilar prioritario

El pilar prioritario es aquel con **la puntuación más baja**. Si hay empate, se aplica un **orden de prioridad clínica predefinido**:

```javascript
const basePriorityOrder = [
  'sueno',          // 1.º — impacto sistémico más alto
  'estres',         // 2.º
  'nutricion',      // 3.º
  'actividad_fisica',
  'emocional',
  'comunitario',
  'ocupacional',
  'ocio',
  'aprendizaje',
  'artistico'       // 10.º — menor urgencia clínica
];
```

**Lógica de selección:**

```javascript
const minVal = Math.min(...entries.map(e => e.value));
const lowestIds = entries.filter(e => e.value === minVal).map(e => e.id);
const priorityId = [...basePriorityOrder, ...pillarOrder]
  .find(id => lowestIds.includes(id)) || lows[0].id;
```

Este orden refleja el impacto clínico comprobado: el sueño y el manejo del estrés tienen el mayor efecto sistémico sobre los demás pilares.

### 6.5 Selección del microcambio

El microcambio sugerido es siempre el **primer microcambio** del pilar prioritario (índice `[0]`):

```javascript
const micro = pillars[priorityId].micro[0];
```

### 6.6 Clasificación de puntuación por color

Cada valor de pilar (0–10) se clasifica visualmente:

| Valor | Clase CSS | Color |
|---|---|---|
| 0 – 3 | `score-low` | Rojo |
| 4 – 6 | `score-mid` | Ámbar |
| 7 – 10 | `score-high` | Verde |

### 6.7 Fortalezas y áreas de cuidado

- **Fortalezas:** los 3 pilares con puntuación más alta (ordenados descendente).
- **Áreas de cuidado:** los 3 pilares con puntuación más baja (ordenados ascendente).

En caso de empate, el desempate secundario es alfabético por nombre.

---

## 7. Panel de Resultados

El panel de resultados se actualiza en **tiempo real** cada vez que el usuario mueve un control deslizante. Contiene los siguientes elementos:

### 7.1 Marcador principal

- Número grande con la puntuación IBP actual (ej. `67`).
- Denominador fijo `/100`.

### 7.2 Categoría y resumen

- Etiqueta de categoría coloreada según el rango.
- Texto de resumen personalizado que nombra el pilar prioritario:

| Categoría | Mensaje |
|---|---|
| Equilibrio robusto | "Tu bienestar semanal muestra buenas bases. Mantén lo que funciona y afina con suavidad **[pilar]**." |
| Buen rumbo | "Vas por buen rumbo. Una mejora focalizada en **[pilar]** puede darte más estabilidad." |
| Señales de desgaste | "Tu semana muestra cierta carga acumulada. Conviene priorizar **[pilar]** con un cambio pequeño y sostenible." |
| Modo rescate | "Tu sistema parece pedir alivio. Empieza por **[pilar]** y elige una meta mínima y realista." |

### 7.3 Gráfico de barras

Visualización horizontal de las 10 barras de progreso, una por pilar. Cada barra:
- Etiqueta con nombre del pilar.
- Valor numérico (ej. `7/10`).
- Barra de relleno con gradiente de color ocre → verde.

### 7.4 Chips de fortalezas y áreas de cuidado

Pastillas visuales con el nombre del pilar y su valor entre paréntesis:
- Verde para fortalezas.
- Ámbar para áreas de cuidado.

### 7.5 Tarjeta de prioridad

Sección inferior del panel con:
- **Prioridad sugerida:** nombre del pilar prioritario.
- **Microcambio sugerido:** acción mínima concreta del pilar prioritario.
- **Campo "Señal de éxito"** (`<textarea>`): espacio para que el usuario escriba cómo sabrá que avanzó.

---

## 8. Gestión del Historial

### 8.1 Guardar evaluación

**Botón:** "Guardar evaluación" (id: `#saveBtn`, duplicado en `#saveBtn` de la zona de acciones).

Al guardar:
1. Se llama a `computeResult()` para obtener los datos actuales.
2. Se recupera la fecha actual en formato `YYYY-MM-DD`.
3. Se lee el contenido del campo "Señal de éxito".
4. Se crea un registro con el esquema completo (ver sección 9).
5. Se añade al array del historial en `localStorage`.
6. Se re-renderiza el historial.
7. Se muestra un toast de confirmación verde: *"✓ Evaluación guardada correctamente"*.

### 8.2 Exportar historial

**Botón:** "Exportar historial" (disponible en la zona de evaluación y en la sección de historial).

Proceso:
1. Se serializa el array del historial como JSON con indentación de 2 espacios.
2. Se crea un `Blob` con tipo `application/json`.
3. Se genera una URL temporal y se dispara la descarga del archivo **`historial_ibp.json`**.
4. Se revoca la URL temporal.
5. Toast: *"Historial exportado"*.

### 8.3 Importar historial

**Input file:** (acepta solo `application/json`).

Proceso:
1. Se lee el archivo seleccionado con `FileReader`.
2. Se parsea el JSON.
3. Se valida que el resultado sea un array (`Array.isArray()`).
4. Si válido: reemplaza el historial en `localStorage` y re-renderiza.
5. Toast de éxito: *"✓ N evaluaciones importadas"*.
6. Si inválido: Toast de error: *"No pude importar ese archivo JSON"*.

> **Nota:** la importación reemplaza completamente el historial existente, no lo fusiona.

### 8.4 Borrar historial

**Botón:** "Borrar historial" (clase `danger`, disponible en dos zonas).

Proceso:
1. Se muestra un diálogo de confirmación nativo del navegador.
2. Si el usuario confirma: elimina la clave `ibp_historial_v2` de `localStorage`.
3. Re-renderiza el historial (muestra el mensaje "Todavía no hay evaluaciones").
4. Toast ámbar: *"Historial borrado"*.

### 8.5 Visualización del historial

Las tarjetas de historial se muestran **ordenadas por fecha descendente** (más reciente primero). Cada tarjeta muestra:
- Fecha formateada (ej. "12 may 2026").
- Categoría con color de fondo correspondiente.
- Puntuación IBP en grande, coloreada según rango.
- Pilar de prioridad de esa sesión.
- Microcambio de esa sesión.
- Señal de éxito (si fue registrada).

---

## 9. Esquema de Datos (localStorage)

### Clave de almacenamiento

```
ibp_historial_v2
```

### Tipo de valor

Array JSON de objetos de evaluación.

### Esquema completo de un registro

```json
{
  "fecha": "2026-05-12",
  "respuestas": {
    "nutricion": 7,
    "sueno": 4,
    "actividad_fisica": 6,
    "emocional": 5,
    "estres": 3,
    "ocio": 7,
    "aprendizaje": 8,
    "artistico": 5,
    "ocupacional": 6,
    "comunitario": 6
  },
  "ibp": 57,
  "categoria": "Señales de desgaste",
  "prioridad": "Relajación y estrés",
  "microcambio": "Respirar 3 minutos al mediodía",
  "senalExito": "Hacer al menos 2 pausas de respiración en el día."
}
```

### Descripción de campos

| Campo | Tipo | Descripción |
|---|---|---|
| `fecha` | `string` | Fecha ISO 8601 (YYYY-MM-DD) del momento del guardado |
| `respuestas` | `object` | Valores de los 10 pilares en el momento del guardado (0–10 cada uno) |
| `ibp` | `number` | Suma total de los 10 valores (0–100) |
| `categoria` | `string` | Clasificación textual del IBP |
| `prioridad` | `string` | Nombre del pilar prioritario |
| `microcambio` | `string` | Texto del microcambio sugerido |
| `senalExito` | `string` | Texto libre escrito por el usuario (puede estar vacío) |

### Claves válidas del objeto `respuestas`

```
nutricion, sueno, actividad_fisica, emocional, estres,
ocio, aprendizaje, artistico, ocupacional, comunitario
```

---

## 10. Funciones JavaScript

Documentación de todas las funciones públicas de la aplicación:

### Funciones de renderizado

| Función | Descripción |
|---|---|
| `renderPillarsIntro()` | Genera las 10 tarjetas de pilares en la pantalla de entrada y configura el modal |
| `openModal(index)` | Abre el modal de hábitos para el pilar en la posición `index` |
| `closeModal()` | Cierra el modal de hábitos |
| `renderQuestions()` | Genera los 10 controles deslizantes de evaluación con sus etiquetas |
| `renderResults()` | Calcula y renderiza el panel de resultados completo |
| `renderHistory()` | Carga el historial desde `localStorage` y renderiza las tarjetas |

### Funciones de lógica

| Función | Descripción |
|---|---|
| `computeResult()` | Ejecuta el algoritmo completo y retorna un objeto con IBP, categoría, fortalezas, áreas, prioridad, microcambio y resumen |
| `classifyIBP(v)` | Retorna la categoría textual para un valor numérico IBP |
| `makeSummary(cat, name)` | Genera el texto de resumen personalizado con el nombre del pilar prioritario |
| `scoreClass(v)` | Retorna la clase CSS según el valor del pilar (0–3 / 4–6 / 7–10) |

### Funciones de persistencia

| Función | Descripción |
|---|---|
| `getHistory()` | Lee y parsea el historial desde `localStorage`. Retorna array vacío en caso de error |
| `setHistory(h)` | Serializa y guarda el array del historial en `localStorage` |
| `saveEvaluation()` | Construye y guarda el registro de la evaluación actual |
| `exportHistory()` | Genera y descarga el archivo `historial_ibp.json` |
| `importHistory(file)` | Lee, valida e importa un archivo JSON de historial |
| `clearHistory()` | Solicita confirmación y elimina el historial completo |

### Funciones de navegación y utilidades

| Función | Descripción |
|---|---|
| `launchApp()` | Transiciona de la pantalla de entrada a la pantalla principal |
| `navScrollTo(id)` | Hace scroll suave a la sección especificada y actualiza el botón activo |
| `updateNavOnScroll()` | Actualiza el botón activo de navegación según la sección visible (listener de `scroll`) |
| `showToast(msg, type, duration)` | Muestra una notificación flotante temporal. Tipos: `success`, `error`, `warn` |
| `formatDate(iso)` | Convierte "2026-05-12" a "12 may 2026" |
| `catStyle(cat)` | Retorna estilos CSS inline de color para cada categoría |
| `scoreColor(ibp)` | Retorna variable CSS de color según la puntuación IBP |

---

## 11. Sistema de Diseño Visual

### 11.1 Paleta de colores

El sistema de diseño utiliza variables CSS definidas en `:root`:

| Variable | Valor | Uso |
|---|---|---|
| `--verde-bosque` | `#2D5016` | Color primario, pilares, bordes activos |
| `--verde-claro` | `#3d6b20` | Verde secundario |
| `--ocre-tierra` | `#C67F3E` | Acentos, hints, indicadores |
| `--ocre-suave` | `#e8a76a` | Ocre secundario |
| `--azul-medicina` | `#3B5A7D` | Categoría "Buen rumbo" |
| `--morado-ritual` | `#6B4E71` | Decorativo |
| `--amarillo-semilla` | `#E8B62E` | Decorativo |
| `--beige-papel` | `#F5F1E8` | Fondo principal |
| `--beige-claro` | `#FAF7F2` | Fondo secundario |
| `--beige-oscuro` | `#EDE8DC` | Barras de progreso vacías |
| `--negro-carbon` | `#2B2B2B` | Texto principal |
| `--gris-medio` | `#6B6B6B` | Texto secundario |
| `--gris-suave` | `#A0A0A0` | Texto terciario, placeholders |
| `--rojo-bajo` | `#8b2020` | Errores, categoría "Modo rescate" |

### 11.2 Tipografía

| Variable | Fuente | Uso |
|---|---|---|
| `--font-display` | Crimson Pro (serif) | Títulos, números grandes, elementos destacados |
| `--font-body` | Lora (serif) | Texto de cuerpo, párrafos, botones |
| `--font-mono` | IBM Plex Mono | Etiquetas técnicas, contadores, capsulas |

### 11.3 Espaciado

| Variable | Valor |
|---|---|
| `--sp-xs` | 0.5rem (8px) |
| `--sp-sm` | 1rem (16px) |
| `--sp-md` | 1.5rem (24px) |
| `--sp-lg` | 2rem (32px) |
| `--sp-xl` | 3rem (48px) |

### 11.4 Bordes y sombras

| Variable | Valor | Uso |
|---|---|---|
| `--radius-sm` | 8px | Inputs, elementos pequeños |
| `--radius-md` | 14px | Tarjetas medianas |
| `--radius-lg` | 20px | Tarjetas grandes, paneles |
| `--radius-full` | 999px | Chips, pills, botones redondos |
| `--shadow-sm` | `0 2px 8px rgba(43,43,43,0.06)` | Elevación baja |
| `--shadow-md` | `0 6px 24px rgba(43,43,43,0.09)` | Elevación media |
| `--shadow-lg` | `0 16px 48px rgba(43,43,43,0.14)` | Elevación alta (toast, modal) |

---

## 12. Accesibilidad y Teclado

La aplicación implementa las siguientes medidas de accesibilidad:

### Atributos ARIA

| Elemento | Atributos |
|---|---|
| Modal overlay | `role="dialog"`, `aria-modal="true"`, `aria-labelledby="modal-name-text"` |
| Tarjetas de pilares | `role="button"`, `tabindex="0"`, `aria-label="[nombre] — abrir detalles"` |
| Botón de cierre del modal | `aria-label="Cerrar"` |

### Navegación por teclado

| Tecla | Acción |
|---|---|
| `Tab` | Navegar entre tarjetas de pilares y controles interactivos |
| `Enter` / `Espacio` | Abrir modal de la tarjeta de pilar con foco |
| `Escape` | Cerrar el modal de hábitos |
| `→` (flecha derecha) | Ir al pilar siguiente dentro del modal |
| `←` (flecha izquierda) | Ir al pilar anterior dentro del modal |

### Comportamiento del scroll

Al abrir el modal, se aplica `overflow: hidden` al `<body>` para evitar desplazamiento del fondo. Se restaura al cerrar.

---

## 13. Diseño Responsivo

La aplicación adapta su layout mediante tres puntos de ruptura (`breakpoints`):

### Breakpoint 1 — 980px y menos

| Elemento | Cambio |
|---|---|
| Hero y cuadrícula principal | Pasa de 2 columnas a 1 columna |
| Panel de resultados | Deja de ser `sticky` |
| Hero-side | Bordes inferiores redondeados |
| Caja IBP intro | Pasa a 1 columna |
| Puntaje demo | Dirección `row` en lugar de `column` |
| Orquesta body | Pasa a 1 columna |
| Ruta semanal | Pasa a 2 columnas |

### Breakpoint 2 — 700px y menos

| Elemento | Cambio |
|---|---|
| Cuadrícula de pilares | 2 columnas |
| Resultado top | 1 columna, centrado |
| Navegación links | Ocultos (`display: none`) |
| Toast | Texto normal, ancho 80vw |
| Ruta semanal | 1 columna |

### Breakpoint 3 — 440px y menos

| Elemento | Cambio |
|---|---|
| Cuadrícula de pilares | 1 columna |

---

## 14. Guía de Uso Paso a Paso

### Primer uso

1. **Abrir la aplicación.** Haz doble clic sobre `index.html` o abre la URL donde esté publicada.

2. **Leer la pantalla de entrada.** La pantalla de entrada presenta el IBP, los 10 pilares y el método de la Ruta Semanal. Tómate 2 minutos para leerla.

3. **Explorar los pilares.** Haz clic en cualquier tarjeta de pilar para ver sus 5 hábitos clave. Usa las flechas del modal o las teclas `→` y `←` para navegar entre pilares.

4. **Iniciar la evaluación.** Haz clic en el botón **"Comenzar mi evaluación semanal"**.

### Completar la evaluación

5. **Puntuar cada pilar.** Para cada uno de los 10 pilares, desliza el control de `0` (muy bajo) a `10` (muy bueno) según tu experiencia **real** de la última semana. No evalúes lo que debería haber sido — evalúa lo que fue.

6. **Observar el resultado en tiempo real.** El panel derecho se actualiza automáticamente mostrando tu IBP, categoría, fortalezas, áreas de cuidado, pilar prioritario y microcambio sugerido.

7. **Anotar tu señal de éxito.** En el campo "Señal de éxito", escribe en una oración cómo sabrás que avanzaste en el pilar prioritario durante la próxima semana. Ejemplo: *"Despertaré sin alarma al menos 3 días"*.

8. **Guardar la evaluación.** Haz clic en **"Guardar evaluación"**. Aparecerá un toast verde de confirmación.

### Semanas siguientes

9. **Revisar el historial.** Desplázate hacia abajo hasta la sección "Historial local" para ver tus evaluaciones anteriores.

10. **Comparar semana a semana.** Observa si el IBP sube, baja o se estabiliza. Los patrones son más útiles que cualquier puntuación individual.

11. **Respaldar tu historial.** Usa el botón **"Exportar historial"** para descargar un archivo JSON. Guárdalo en un lugar seguro o en la nube.

### Gestión avanzada

12. **Migrar a otro dispositivo.** Exporta el historial desde el dispositivo de origen e impórtalo en el destino con el botón **"Importar historial"**.

13. **Borrar y empezar de cero.** El botón **"Borrar historial"** elimina todos los datos guardados. Solicita confirmación antes de ejecutarse.

---

## 15. El Efecto Orquesta

El IBP no trata los pilares como compartimentos independientes. Existe una sinergia profunda entre ellos: se sostienen y se amplifican mutuamente. Esta interdependencia se denomina **Efecto Orquesta**.

> "El bienestar funciona como una orquesta: si un instrumento se desafina, la música continúa, pero pierde su brillo y armonía."

### Principio de efecto cascada

Cuando un pilar mejora, tiende a arrastrar positivamente a los pilares relacionados. Cuando uno cae, los pilares fuertes actúan como red de contención.

### Sinergias documentadas en la aplicación

| Pilar detonante | Impacto positivo directo |
|---|---|
| **Sueño** | Mejora la regulación emocional y la capacidad de concentración y aprendizaje |
| **Relajación** | Mejora la calidad del sueño y la satisfacción en el trabajo o estudio |
| **Actividad física** | Regula el cortisol y mejora el estado de ánimo de forma directa y sostenida |
| **Comunitario** | Nutre el bienestar emocional y abre espacios naturales de juego y descanso |

### Implicación para el uso del IBP

Esta arquitectura interdependiente justifica la estrategia de **foco en un solo pilar**: un cambio pequeño en el lugar correcto genera ondas que se propagan por toda la orquesta. Por eso el IBP no recomienda trabajar todos los pilares simultáneamente.

---

## 16. La Ruta Semanal

La Ruta Semanal es el protocolo de uso recomendado del IBP. Está diseñada para completarse en **15 minutos por semana**.

| Paso | Verbo | Acción | Herramienta |
|---|---|---|---|
| 01 | **Medir** | Calcular el IBP puntuando cada pilar de 0 a 10 según la semana real vivida | Esta aplicación |
| 02 | **Reflexionar** | Escribir qué funcionó, qué falló y qué se necesita esta semana | Campo "Señal de éxito" |
| 03 | **Priorizar** | Elegir solo un pilar para enfocar los esfuerzos. Uno, no varios | Prioridad sugerida |
| 04 | **Diseñar** | Implementar un microcambio mínimo viable, pequeño y concreto | Microcambio sugerido |
| 05 | **Revisar** | Ejecutar por 7 días y regresar a medir. El ciclo se repite con lo aprendido | Historial local |

La Ruta Semanal transforma la salud de un rompecabezas peleado en un **sistema que aprende**, acumulando datos y decisiones semana tras semana.

---

## 17. Tres Reglas Éticas

Las siguientes tres reglas guían la filosofía de uso del IBP:

### Regla 1 — Lo sostenible vence a lo perfecto

No se busca el protocolo de salud ideal, sino el hábito que puede mantenerse. Un cambio pequeño ejecutado consistentemente durante meses tiene un impacto acumulado superior a cualquier protocolo intensivo abandonado por agotamiento.

### Regla 2 — Lo pequeño vence a lo épico

Los microcambios —acciones mínimas, concretas y de baja fricción— son el mecanismo de cambio real. No se trata de heroísmo sino de estrategia. El IBP sugiere siempre la acción más pequeña posible en el pilar correcto.

### Regla 3 — Se mide para aprender, no para castigarse

La puntuación del IBP no es un juicio moral. Una semana con IBP 42 no significa que el usuario haya fallado: significa que su sistema estaba bajo presión y que hay información útil para la semana siguiente. La herramienta es un espejo, no un tribunal.

---

## 18. Privacidad y Almacenamiento

### Modelo de privacidad

El IBP opera bajo un modelo de **privacidad total local**:

- Todos los datos del usuario se almacenan exclusivamente en el `localStorage` de su navegador.
- **No existe ningún servidor backend.**
- **No se envían datos a ningún tercero.**
- **No hay cuentas de usuario, autenticación ni registro.**
- **No hay analítica ni rastreo.**

### Persistencia y límites

| Aspecto | Detalle |
|---|---|
| Tecnología | `window.localStorage` (Web Storage API) |
| Clave de almacenamiento | `ibp_historial_v2` |
| Límite de almacenamiento | ~5–10 MB por origen (límite del navegador) |
| Persistencia | Los datos persisten hasta que se borren manualmente o se limpien los datos del navegador |
| Alcance | Dominio/origen de la página (no se comparte entre subdominios) |

### Consideraciones para el usuario

- Si el usuario borra las cookies o los datos del sitio en su navegador, el historial se perderá.
- Para respaldar el historial, se debe exportar regularmente usando la función de exportación.
- La importación en otro dispositivo o navegador requiere transferir el archivo JSON.

---

## 19. Despliegue y Compatibilidad

### Opciones de despliegue

| Método | Descripción |
|---|---|
| **Archivo local** | Abrir `index.html` directamente en el navegador. Sin servidor necesario. |
| **GitHub Pages** | Publicar el repositorio y activar GitHub Pages. Acceso por URL pública. |
| **Netlify / Vercel** | Arrastrar la carpeta al panel de control para obtener URL inmediata. |
| **Servidor web** | Copiar `index.html` a cualquier servidor estático (Apache, Nginx, S3, etc.). |
| **Intranet / local** | Disponible para redes internas sin conexión a internet (solo requiere Google Fonts si hay red). |

> **Nota sobre Google Fonts:** la aplicación carga las tipografías Crimson Pro, Lora e IBM Plex Mono desde Google Fonts. Sin conexión a internet, se mostrará con fuentes de reserva del sistema (Georgia, Courier New) sin impacto en la funcionalidad.

### Compatibilidad de navegadores

| Navegador | Versión mínima recomendada | Estado |
|---|---|---|
| Google Chrome | 90+ | ✅ Totalmente compatible |
| Mozilla Firefox | 90+ | ✅ Totalmente compatible |
| Safari | 14+ | ✅ Totalmente compatible |
| Microsoft Edge | 90+ | ✅ Totalmente compatible |
| Brave | Basado en Chromium | ✅ Totalmente compatible |
| Opera | 76+ | ✅ Totalmente compatible |

### Compatibilidad de dispositivos

| Dispositivo | Estado |
|---|---|
| Escritorio (1200px+) | ✅ Layout de 2 columnas completo |
| Laptop (980px–1199px) | ✅ Layout adaptado |
| Tablet (700px–979px) | ✅ Layout de 1 columna |
| Móvil (menos de 700px) | ✅ Layout mobile optimizado |

---

## 20. Glosario

| Término | Definición |
|---|---|
| **IBP** | Índice de Bienestar Personal. Puntuación compuesta de 0 a 100 que resulta de evaluar 10 pilares del bienestar. |
| **Pilar** | Cada una de las 10 dimensiones del bienestar evaluadas en el IBP. |
| **Microcambio** | Acción mínima, concreta y de baja fricción sugerida para mejorar el pilar prioritario. |
| **Pilar prioritario** | El pilar con la puntuación más baja, identificado como el de mayor impacto potencial al mejorar. |
| **Ruta Semanal** | El ciclo de 5 pasos (Medir → Reflexionar → Priorizar → Diseñar → Revisar) diseñado para completarse en 15 minutos por semana. |
| **Efecto Orquesta** | La interdependencia entre pilares: mejorar uno impacta positivamente a los demás. |
| **Señal de éxito** | Texto libre del usuario que describe cómo reconocerá el avance en el pilar prioritario durante la semana. |
| **localStorage** | Mecanismo de almacenamiento web del navegador donde se guardan los datos del historial IBP. |
| **Single-File Web App** | Arquitectura donde toda la aplicación — HTML, CSS y JavaScript — reside en un único archivo. |
| **Orden de prioridad clínica** | Jerarquía predefinida para desempatar pilares con igual puntuación, basada en el impacto sistémico de cada pilar (Sueño > Estrés > Nutrición > ...). |
| **Toast** | Notificación temporal flotante que aparece en la parte inferior de la pantalla para confirmar acciones del usuario. |
| **Breakpoint** | Punto de ruptura de ancho de pantalla donde el layout de la aplicación se adapta al dispositivo. |

---

*Ecosistema de Medicina Holística · IBP v5 · Puerto Rico*
*Documentación generada en Mayo 2026*
*"Un cambio pequeño en el pilar correcto resuena en toda la orquesta."*
