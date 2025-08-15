## Ejercicio 1 

### Análisis del problema

El problema consiste en encontrar la ruta más corta (en términos de costo) entre dos ciudades del mapa de Rumania, usando el algoritmo de búsqueda informada A*, el cual tiene en cuenta tanto el costo real del camino recorrido como una estimación heurística del costo restante hasta el objetivo. El objetivo es ir desde la ciudad inicial (Arad) hasta la ciudad meta (Bucharest).

**Estados:** Cada estado es una ciudad del mapa.

**Acciones:** Las acciones son los movimientos posibles entre ciudades conectadas directamente.

**Costos:** Cada acción tiene un costo asociado, que representa la distancia entre las ciudades.

**Heurística:** Se utiliza la distancia en línea recta desde cada ciudad hasta Bucharest.

---

### Cómo se aplica A* 
Para encontrar la ruta más corta a nuestro objetivo implementamos el algoritmo A*, este algoritmo combina el costo acumulado desde el inicio con una heurística que estima lo que falta para llegar al destino. Esto le permite tomar decisiones más eficientes y precisas.

Para cada nodo usamos la función `f(node)` que se calcula como:

- f(n) = g(n) + h(n)

*g(n) es el costo real que se ha acumulado desde el estado inicial hasta el nodo actual `node.path_cost`.*

*h(n) es una estimación heurística de cuánto falta para llegar al objetivo `heuristic.get(node.state, float('inf'))`.*

También utilizamos una cola de prioridad (heapq) para guardar los nodos según su valor de f(n). Por lo que siempre expandimos primero el nodo que tenga el menor costo total estimado.
