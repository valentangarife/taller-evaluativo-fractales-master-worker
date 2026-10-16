# Resultados individuales: Monolito (valentina)

Taller Evaluativo: Renderizado Paralelo de Fractales (Master-Worker)
Computación en Internet I, Universidad Icesi, 2026-2

## 1. Equipo utilizado

| Dato | Valor |
|------|-------|
| Equipo | MacBook Air M2, 2022 |
| Chip | Apple M2 |
| Memoria RAM | 24 GB |
| Sistema operativo | macOS Tahoe 26.6.2 |
| Procesador | Apple Silicon M2 |



## 2. Tabla de ejecuciones (rango pedido: 1 a 10 minutos)

Comando base:

```
./gradlew :monolith:runMonolith --args="<ancho> <alto> <maxIter> <preset> <salida.png>"

```

| # | Preset | Resolución | maxIter | T_sec (ms) | T_sec (s) | T_sec (min) | Imagen |
|---|--------|-----------|---------|-----------|-----------|-------------|--------|
| 1 | seahorse | 1920×1080 | 20000 | 86158 | 86.16 | 1.44 | `v1.png` |
| 2 | seahorse | 3840×2160 | 10000 | 171736 | 171.74 | 2.86 | `v2.png` |
| 3 | seahorse | 3840×2160 | 20000 | 343294 | 343.29 | 5.72 | `v3.png` |
| 4 | mini | 3840×2160 | 30000 | 142390 | 142.39 | 2.37 | `v4.png` |
| 5 | elephant | 3840×2160 | 30000 | 209335 | 209.34 | 3.49 | `v5.png` |

## 3. Comandos usados

```
./gradlew :monolith:runMonolith --args="1920 1080 20000 seahorse output/v1.png"
./gradlew :monolith:runMonolith --args="3840 2160 10000 seahorse output/v2.png"
./gradlew :monolith:runMonolith --args="3840 2160 20000 seahorse output/v3.png"
./gradlew :monolith:runMonolith --args="3840 2160 30000 mini output/v4.png"
./gradlew :monolith:runMonolith --args="3840 2160 30000 elephant output/v5.png"
```

## 4. Evidencia

Las imágenes generadas por el monolito están en la carpeta `monolith/output/`: `v1.png`, `v2.png`, `v3.png`, `v4.png` y `v5.png`.

## 5. Observaciones

- **El tiempo crece de forma casi lineal con los píxeles.** Entre la corrida 1 (1920×1080) y la 3 (3840×2160), con las mismas 20000 iteraciones, hay 4 veces más píxeles y el tiempo pasó de 86.16 s a 343.29 s.
- **También crece de forma casi lineal con las iteraciones.** Entre la corrida 2 (10000 iter) y la 3 (20000 iter), con la misma resolución y preset, el tiempo pasó de 171.74 s a 343.29 s.
- **El preset cambia mucho la carga.** A 3840×2160 con 30000 iteraciones, `elephant` tardó 209.34 s mientras que `mini` tardó 142.39 s. Esto refleja la heterogeneidad del conjunto de Mandelbrot según la región.
- Estos tiempos secuenciales (T_sec) servirán como línea base para comparar con los resultados distribuidos.
