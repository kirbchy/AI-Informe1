## Ejercicio 3

### Análisis del problema

Se necesita encontrar la ruta más corta entre dos estaciones de un sistema de metro (estación A y estación J). El objetivo es utilizar los algoritmos de BFS e IDS para determinar la ruta más corta entre las dos estaciones y realizar la respectiva comparación entre los resultados.

---

### Diseño del grafo

- El grafo se representa como un diccionario donde cada estación tiene una lista de estaciones conectadas.

```python

graph = {
    'A': ['B','C'],
    'B': ['A','D','E'],   
    'C': ['A','F'], 
    'D': ['B','G'], 
    'E': ['B','H','I'], 
    'F': ['C','J'], 
    'G': ['D'],
    'H': ['E'], 
    'I': ['E','J'], 
    'J': ['F','I'],     
}
```

- *Implementado:* Todas las conexiones entre estaciones tienen costo 1.

---

### Implementación 
- **_Problem:_**
  
    Define el estado inicial, el estado objetivo y el grafo, también contiene métodos para obtener acciones y verificar si un estado es la meta.

- **_Node:_**
  
    Representa cada estado durante la búsqueda, guarda el padre (para reconstruir la ruta) y la profundidad alcanzada.

- **_Actions:_**
  
    En nuestra implementación se refiere a moverse de una estación a cualquiera de las conectadas directamente.

---

### Algoritmos

- **Breadth-First Search (BFS):**
   
    Búsqueda por anchura usando cola FIFO, explora nivel por nivel.
- **Iterative Deepening Search (IDS):**
  
    Búsqueda con profundización iterativa, combina DFS con límites crecientes.

---

### Comparación entre BFS e IDS

| Algoritmo | Número de acciones | Ruta encontrada | Tiempo de ejecución | Uso de memoria      |
|-----------|--------------------|-----------------|---------------------|---------------------|
| BFS       | 3                  | A → C → F → J   |0.000124             |5,420 bytes (5.29 KB)|
| IDS       | 3                  | A → C → F → J   |0.000235             |2,760 bytes (2.70 KB)|

**Rendimiento en Tiempo**

- BFS es más rápido en este caso porque explora directamente por niveles y encuentra la meta en la primera vez que la alcanza.

- IDS repite búsquedas desde la raíz para cada incremento de profundidad, lo que lo hace un poco más lento.

**Uso de Memoria**

- BFS consumió más memoria (5.29 KB) porque almacena en la cola todos los nodos de cada nivel.

- IDS mantiene solo la rama actual en cada iteración y por eso fue más eficiente en memoria (2.70 KB).

---

### Conclusión

En base a los resultados, para grafos pequeños y sin límites de memoria estrictos, BFS es más eficiente en tiempo. IDS es preferible cuando la memoria es limitada o la profundidad de la meta es desconocida y muy grande.
