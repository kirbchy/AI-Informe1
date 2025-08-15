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

