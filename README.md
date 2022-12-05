# Optimización por enjambre de partículas (PSO)

*Integrantes*:
  - David Avila Garcia
  - Santiago Licea Becerril

### Contenido
- [Optimización por enjambre de partículas (PSO)](#particle-swarm-optimization-pso-paralell-implementation-using-julias-wraper-for-mpi)
    - [Contenido](#contenido)
    - [Objetivo:](#objetivo)
    - [Modelo Secuencial](#modelo-secuencial)
      - [Análisis de Tiempo](#análisis-de-tiempo)
      - [Análisis de Escalabilidad](#análisis-de-escalabilidad)
    - [Modelo Paralelizado con MPI](#modelo-paralelizado-con-mpi)
      - [Análisis de Tiempo](#análisis-de-tiempo-1)
      - [Análisis del Error](#análisis-del-error)
      - [Análisis de Escalabilidad](#análisis-de-escalabilidad-1)
    - [Conclusiones](#conclusiones)


### Objetivo:
- Implementar el algorítmo de optimización PSO de forma secuencial.
- Implementar el algorítmo de optimización PSO de forma paralela.
- Comparar el tiempo de ejecución de ambas implementaciones.
- Evaluar el error de nuestra implementación en paralelo.

Para más informción sobre el algorítmo consultar la carpeta *DOCS*, en ella se encuentra el modelo matemático y documentación del modelo.

### Modelo Secuencial
El modelo secuencial se encuentra implementado en la carpeta docs. 

#### Análisis de Tiempo
Se utilizó la libreria BenchmarkTools para mayor comodidad
El tiempo de ejecución de nuestro algorítmo secuencial fue de $10.463 \text{ms} \pm 671.737 \mu s$.

#### Análisis de Escalabilidad
El algorítmo puede trabajar con cualquier número de partículas deseadas, como con cualquier número de iteraciones, sin embargo, hay límites físicos, como la memoria de la computadora o el tiempo de ejecución que hay que tomar en cuenta.

Al utilizar una función que puede estar definida en cualquier dimensión y haber generalizado nuestro algorítmo de optimización para trabajar en cualquier dimensión, podemos encontrar cualquier mínimo global dentro de un rango. Sin embargo, si se aumenta la dimensionalidad, recomendamos aumentar el número de partículas y de iteraciones para tener una buena aproximación, lo que produce un costo computacional muy alto y a su vez tiempos de ejecución mucho más prolongados por cada dimensión aumentada.

Esto hace que el algorítmo sea escalable en el número de partículas e iteraciones, así como la dimensión con la que se quiera trabajar.

### Modelo Paralelizado con MPI
El modelo paralelizado se encuentra de igual forma en la carpeta docs
#### Análisis de Tiempo
Para compararlo con el secuencial, utilizaremos los mismos parámetros tomados en el secuencial, pero se calculará manual mente utilizandoel siguiente comando en la terminal para guardar el tiempo de ejecución
```bash
for run in {1..478}; do mpiexec -n 12 julia mpi.jl >> resultados_mpi.txt; done;
```

Ejecutará 478 veces el algorítmo paralelizado utilizando 12 procesadores donde se guardará en un archivo txt
para posteriormente sacar la media y la desviación estandar

El tiempo de ejecución de nuestro algorítmo secuencial es de $6939.83 \pm 2903.838 \text{ms}$, resultante del promedio con un error de 1.96 veces la desviación estándar.

#### Análisis del Error
También guardamos el valor encontrado en cada ejecución. y sabiendo que el resultado es [1,1]  podemos sacar un error absoluto real utilizando la norma de la diferencia entre el resultado encontrado y el resultado real. Es decir $\varepsilon_{abs} = \lVert(1,1) - X_{pred}\rVert$.

Donde obtuvimos que:
- Error promedio 0.07279
- Desviación estándar 0.0649

De manera general, estamos $0.07279 \pm 0.10384$ del valor real. Lo que resulta en una precisión confiable dependiendo del caso.

#### Análisis de Escalabilidad
Al poder manejar cualquier número de dimensiones, partículas, iteraciones y procesadores, la escalabilidad queda determinada únicamente a las limitantes físicas.

### Conclusiones
El  secuencial podrá ser ligeramente más rápido que el paralelo, sin embargo, el paralelo ofrece una mejor precisión, pues cuando tenemos un solo enjambre, este se ve influenciado por la mejor posición de una sola partícula. Si tenemos múltiples enjambres, la influencia de la mejor posición en un enjambre no influencia a los demás enjambres, por lo que cada uno puede encontrar un mínimo local de manera más eficiente y el maestro
