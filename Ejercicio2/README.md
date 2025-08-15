## Ejercicio 2

### Resolver el ejercicio planteado. 

Hicimos lo siguiente:

- Definimos la clase **_Node_** para representar cada estado, incluyendo su posición, el nodo padre, el costo acumulado y la acción que nos llevó allí.

- Creamos la clase **_Problem_** para almacenar el estado inicial, el objetivo y las acciones posibles.

- Usamos un diccionario **_actions_** para asociar cada movimiento con su nombre (_Up_, _Down_, _Left_, _Right_).

- Implementamos **_heapq_**, donde la prioridad se basa en la distancia Manhattan al objetivo.

- Modificamos **_get_neighbors_** para devolver también la acción que lleva al vecino.

- En **_reconstruct_path_** devolvemos tanto la secuencia de posiciones como la lista de acciones.

---

### ¿Cómo cambia el comportamiento del algoritmo si cambiamos la  función de costo? 

En la prioridad solo usamos la distancia Manhatan, así: 

```python
heapq.heappush(frontier, (manhatan_distance(neighbor, goal), reached[neighbor])
```

Y siempre explora el nodo que parece más cercano a la meta según la heurística, sin considerar el costo recorrido.

Si cambiamos la función para que sea con el costo: 

```python
priority = new_cost + manhatan_distance(neighbor, goal)
```

El algoritmo se convierte en A*, porque: 

- Considera tanto la distancia recorrida como el cálculo de la meta.
- Garantiza que encuentra el camino más corto si la heurística es aceptable.

---

### ¿Qué sucede si hay múltiples salidas en el laberinto? ¿Cómo  podrías modificar el algoritmo para manejar esto? Plantea una  propuesta. 

Si hubiera varias salidas, el algoritmo no las consideraría, solo buscaría la primera meta fija, porque la variable goal es un solo punto.
Lo que proponemos para modificar el algoritmo es: 
- Guardar todas las salidas en una lista.
- Cambiar la condición de éxito.
- Usar una heurística que calcule la distancia al objetivo más cercano.
  
 ``` python
goals = [(1,6), (3,5), (2,7)]
```
``` python
if node.position in goals:
    return reconstruct_path(node)
```
``` python
def manhatan_distance_multi(pos, goals):
    return min(abs(pos[0] - g[0]) + abs(pos[1] - g[1]) for g in goals)
```

Esto haría que el algoritmo siempre se dirija a la salida más próxima.

--- 

 ### Modifica el laberinto por uno más grande y con otro tipo de obstáculo además de paredes. ¿Qué limitación encuentras en el  algoritmo? 

Cambiamos  el laberinto a un tamaño de 10x10 y pusimos un nuevo tipo de obstáculo "~" que representa agua. 
Este obstáculo es atravesable, pero en la vida real debería tener un costo mayor que caminar por un espacio libre " ", pero nos dimos cuenta de que el código actual no diferencia entre terrenos con distinto costo de movimiento:
- Siempre asume que moverse a cualquier celda libre cuesta lo mismo (+1), sin importar el tipo de camino. Esto hace que, si la ruta más corta en cantidad de pasos atraviesa varias casillas de agua, el algoritmo la elija, aunque en términos de “costo real” no sea la mejor opción
  
- _Limitación encontrada:_ el algoritmo no maneja costos variables por tipo de celda, por lo que no puede planificar rutas óptimas en mapas con terrenos de distinta dificultad
- _Posible solución:_ asignar un costo distinto a cada tipo de celda y modificar la forma en que se calcula el costo acumulado (new_cost), combinándolo con la heurística para implementar un algoritmo A*

``` python
# Nuevo laberinto 10x10
maze = [
    ["#", "#", "#", "#", "#", "#", "#", "#", "#", "#"],
    ["#", "S", " ", " ", "~", " ", " ", " ", " ", "#"],
    ["#", " ", "#", "#", "~", "#", "#", "#", " ", "#"],
    ["#", " ", "#", " ", "~", " ", " ", "#", " ", "#"],
    ["#", " ", "#", " ", "#", "#", " ", "#", " ", "#"],
    ["#", " ", " ", " ", "#", " ", " ", "#", " ", "#"],
    ["#", "#", "#", " ", "#", " ", "#", "#", " ", "#"],
    ["#", "E", "#", " ", "~", " ", " ", " ", " ", "#"],
    ["#", " ", " ", " ", "~", "#", "#", "#", " ", "#"],
    ["#", "#", "#", "#", "#", "#", "#", "#", "#", "#"]
]
```
``` python
    # Costos por tipo de celda
    terrain_cost = {
        " ": 1,  # camino normal
        "~": 3,  # agua, más costoso
        "S": 1,
        "E": 1
    }

```
``` python

priority = new_cost + manhatan_distance(neighbor, goal)
heapq.heappush(frontier, (priority, reached[neighbor]))
```


