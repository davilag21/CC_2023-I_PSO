# Contenido

Aqui se enuentran los tiempos de jecución del modelo secuencial utilizando BenchmarkTools, y los tiempos sacados manuelmente del modelo paralelizado

### Paralelizado con MPI
Comando utilizado para generar las primeras 24 líneas del documento:
```bash
for run in {1..483}; do mpiexec -n 12 julia pso_mpi.jl >> resultados_mpi.txt; done;
Solo mostraremos 10 resultados en esta tabla
```
| Iteración | Tiempo (ms) | Aproximación      | $\varepsilon_{abs}$ |
| --------- | ----------- | ----------------- | ------------------- |
| 1         | 5537        | [0.9485,  0.9031] | 0.1563              |
| 2         | 5658        | [0.9791,  0.9583] | 0.0045              |
| 3         | 5563        | [0.9799,  0.9589] | 0.03456             |
| 4         | 5658        | [1.0316,  1.0592] | 0.0047              |
| 5         | 5630        | [0.9936,  0.9876] | 0.0567              |
| 6         | 5592        | [1.0039,  1.0058] | 0.1453              |
| 7         | 5624        | [0.9664,  0.9328] | 0.1426              |
| 8         | 5573        | [1.0705,  1.1423] | 0.14448             |
| 9         | 5571        | [0.9862,  0.9418] | 0.0347              |
| 10        | 5574        | [0.9705,  0.9418] | 0.0414              |
| 11        | 5124        | [0.9868,  0.9754] | 0.0645              |
| 12        | 5426        | [0.9536,  0.9112] | 0.0996              |
|           |             |                   |                     |
| $\mu$     | 5600.66     | -                 | 0.0056             |
| $\sigma$  | 41.058224   | -                 | 0.0024             |

Por lo que podemos estimar tiempos de ejecución de: $5600.66 \pm 41.05 \text{ms}$ para el tiempo y un error absoluto de: $0.00279 \pm 0.10384$.
