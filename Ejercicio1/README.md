# Ejercicio 1 

## Análisis del problema

El problema consiste en encontrar la ruta más corta (en términos de costo) entre dos ciudades del mapa de Rumania, usando el algoritmo de búsqueda informada A*, el cual tiene en cuenta tanto el costo real del camino recorrido como una estimación heurística del costo restante hasta el objetivo. El objetivo es ir desde la ciudad inicial (Arad) hasta la ciudad meta (Bucharest).

**Estados:** Cada estado es una ciudad del mapa.

**Acciones:** Las acciones son los movimientos posibles entre ciudades conectadas directamente.

**Costos:** Cada acción tiene un costo asociado, que representa la distancia entre las ciudades.

**Heurística:** Se utiliza la distancia en línea recta desde cada ciudad hasta Bucharest.
