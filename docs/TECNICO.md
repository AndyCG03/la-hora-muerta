# Ficha técnica

Cómo está hecho **La Hora Muerta**. Esta documentación describe el juego; el código fuente no es público.

## Resumen

| | |
|---|---|
| Motor | Godot 4.7.2 (GDScript) |
| Renderizado | Forward+ en Windows (DirectX 12), Mobile en Android (Vulkan) |
| Física | Jolt Physics |
| Plataformas | Android 7.0+ (arm64) · Windows 10/11 (x86_64) |
| Tamaño | APK ≈ 56 MB · Windows ≈ 142 MB (un único ejecutable) |
| Idiomas | Español e inglés (textos); voces en inglés |
| Guardado | Automático, local, con dos copias y comprobación de integridad |

## Arquitectura

```
Guion (datos)  ──►  Director (intérprete)  ──►  Nivel (mundo)
   eventos, reglas,        ejecuta los pasos         casa, puertas, luz,
   disparadores            en orden                  mecanismos, la Sombra
        ▲                                                   │
        └──────── catálogos de texto (es / en) ◄────────────┘
                  y voces sincronizadas
```

- **Historia dirigida por datos.** Todo lo que ocurre (diálogos, objetivos, sustos guionizados, puertas que se abren, la Sombra que despierta) está descrito como **eventos**: listas de pasos con condiciones. Un intérprete, el *Director*, los ejecuta. Para cambiar la historia no hay que tocar la lógica del juego.
- **Textos separados del código.** Líneas, notas, objetivos y finales están en catálogos por idioma. Cada línea con voz tiene su duración registrada para sincronizar los subtítulos.
- **Casa construida por código.** Las tres plantas, sus paredes, escaleras y muebles se generan al cargar a partir de una descripción de estancias. Los muebles con contenido y los recursos se reparten al azar en cada partida.
- **Variantes por partida.** Algunas pistas y sus códigos cambian entre partidas, y con ellas el texto y la voz correspondientes.

## Sistemas

| Sistema | Descripción |
|---|---|
| **Pánico** | Valor de 0 a 100 que depende de la luz, la linterna, la Sombra y los sustos. Controla el latido, la respiración, la viñeta, el temblor de cámara, la saturación y las alucinaciones. |
| **Linterna** | Pila limitada, parpadeo por pila baja, pánico o la Sombra cerca, retardo del haz respecto a la cámara y comprobación de si ilumina un punto concreto (cono, distancia y oclusión). |
| **La Sombra** | Máquina de estados (dormida, esperando, cazando, atacando, desvaneciéndose). Atraviesa geometría, cambia de planta, reacciona al ruido y a la luz, busca en los escondites y tiene una persecución final. |
| **Ruido** | Correr, las puertas, los muebles y soltar el aire generan ruido con un radio; la Sombra acude o adelanta su aparición. |
| **Escondites** | Armarios y camas. Contener la respiración frente a la búsqueda de la Sombra, con tiempo de gracia y tiempo de búsqueda según la dificultad. |
| **Apariciones** | Programador de sustos que se intensifica con la historia (pasos, golpes, susurros, objetos que caen, puertas que se abren solas, figuras) y alucinaciones con pánico alto. |
| **Objetivos** | Seis capítulos con objetivos encadenados, puertas condicionadas por el progreso y registro de objetivos cumplidos. |
| **Mapa** | Plano dibujado por código con trazo de lápiz irregular, revelado por las estancias visitadas. |
| **Audio** | Buses separados (voces, música, efectos y ambiente), música dinámica que se mezcla según la tensión y la persecución, pasos según la superficie y cola de diálogo con prioridades y silencio mínimo entre líneas. |
| **Guardado** | Captura completa del estado (jugador, inventario, puertas, mecanismos, muebles abiertos, variantes y eventos vistos) y reconstrucción exacta al continuar. |

## Recursos

| Tipo | Cómo se ha creado |
|---|---|
| Modelos 3D | 58 modelos low-poly generados por script en **Blender 5.3** y exportados a glTF |
| Ilustraciones | Imágenes de la introducción, el epílogo y el menú creadas con IA y retocadas; los cuadros del juego son recortes de ellas sobre lienzos planos |
| Efectos de sonido | Síntesis procedural: resonadores de madera y metal, rozamiento de bisagras, gargantas sintéticas para la Sombra y reverberación |
| Música | Composición procedural: cuerdas frotadas, timbales y racimos disonantes en bucle |
| Voces | Síntesis de voz con **Kokoro-82M**, en local |

## Rendimiento

- Las luces apagadas se desactivan por completo y las sombras dinámicas se limitan a las fuentes principales.
- Tres niveles de calidad (sombras, SSAO, brillo y niebla volumétrica) y escala de renderizado ajustable.
- En móvil arranca en calidad **Media**, con texturas comprimidas ETC2/ASTC.
- Una **pantalla de carga** precarga modelos, sonidos e imágenes antes de entrar en la casa.

## Calidad

El juego incluye pruebas automáticas que recorren la historia completa de principio a fin (puzzles, puertas, la Sombra, escondites, desmayos, ritual, huida y finales), comprueban que cada objeto se puede señalar con la mira y validan la pantalla de carga. La versión 1.0.1 pasa las 94 comprobaciones del recorrido completo.
