# Resultados individuales: Monolito (Isabella)

Taller Evaluativo: Renderizado Paralelo de Fractales (Master-Worker)
Computación en Internet I, Universidad Icesi, 2026-2

## 1. Equipo utilizado

| Dato | Valor |
|------|-------|
| Equipo | PC de la sala de cómputo (Dell, host `206m17`) |
| Sistema operativo | Ubuntu 24.04 |
| Java | OpenJDK 17.0.20.1 |
| Procesador / núcleos / RAM | No se registraron |

El monolito es **secuencial (un solo hilo)**, así que el tiempo depende sobre todo de la velocidad de un núcleo y no de cuántos núcleos tiene el equipo.

## 2. Tabla de ejecuciones (rango pedido: 1 a 10 minutos)

Comando base:

```
./gradlew :monolith:runMonolith --args="<ancho> <alto> <maxIter> <preset> <salida.png>"
```

| # | Preset | Resolución | maxIter | T_sec (ms) | T_sec (s) | T_sec (min) | Imagen |
|---|--------|-----------|---------|-----------|-----------|-------------|--------|
| 1 | seahorse | 1920×1080 | 20000 | 77688 | 77,69 | 1,29 | `m1.png` |
| 2 | seahorse | 3840×2160 | 10000 | 156884 | 156,88 | 2,61 | `m2.png` |
| 3 | seahorse | 3840×2160 | 20000 | 311560 | 311,56 | 5,19 | `m3.png` |
| 4 | mini | 3840×2160 | 30000 | 115016 | 115,02 | 1,92 | `m4-1.png` |
| 5 | elephant | 3840×2160 | 30000 | 194185 | 194,19 | 3,24 | `m5.png` |

Comandos usados:

```
./gradlew :monolith:runMonolith --args="1920 1080 20000 seahorse output/m1.png"
./gradlew :monolith:runMonolith --args="3840 2160 10000 seahorse output/m2.png"
./gradlew :monolith:runMonolith --args="3840 2160 20000 seahorse output/m3.png"
./gradlew :monolith:runMonolith --args="3840 2160 30000 mini output/m4-1.png"
./gradlew :monolith:runMonolith --args="3840 2160 30000 elephant output/m5.png"
```

## 3. Evidencia

Las imágenes generadas por el monolito están en la carpeta `output/`: `m1.png`, `m2.png`, `m3.png`, `m4-1.png` y `m5.png`.

## 4. Observaciones

- **El tiempo crece de forma casi lineal con los píxeles.** Entre la corrida 1 (1920×1080) y la 3 (3840×2160), con las mismas 20000 iteraciones y el mismo preset, hay 4 veces más píxeles y el tiempo pasó de 77,69 s a 311,56 s, unas 4,01 veces más.
- **También crece de forma casi lineal con las iteraciones.** Entre la corrida 2 (10000) y la 3 (20000), con la misma resolución y preset, el tiempo pasó de 156,88 s a 311,56 s, unas 1,99 veces más.
- **El preset cambia mucho la carga.** A 3840×2160, `seahorse` con 20000 iteraciones tardó 311,56 s, mientras que `elephant` con 30000 iteraciones (más iteraciones) tardó 194,19 s. Esto es coherente con la carga heterogénea del conjunto de Mandelbrot: según la región, una proporción distinta de píxeles agota el máximo de iteraciones.
- Estos tiempos secuenciales (T_sec) son la línea base contra la que se calcularán el Speedup y la Eficiencia de la fase distribuida.