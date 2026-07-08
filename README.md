# PageRank sobre la blogosfera política de EE.UU. (elecciones 2004)

Proyecto 2 **IMT2230 — Álgebra Lineal Avanzada y Modelamiento**. 

Se aplica el algoritmo PageRank, implementado mediante iteración de potencias sobre la Matriz de Google, a una red real de hipervínculos entre blogs políticos.

## Descripción de la red

Usamos la red **moreno_blogs** de [KONECT](http://konect.cc/networks/moreno_blogs/), recopilada originalmente por Adamic y Glance (2005). Cada **nodo** es un blog sobre las elecciones presidenciales de Estados Unidos de 2004 y cada **arista dirigida** u → v indica que el blog u contiene un hipervínculo hacia el blog v. Cada nodo tiene además una etiqueta de orientación política: *left-leaning* (demócrata) o *right-leaning* (republicano).

| Estadística | Valor |
|---|---|
| Nodos (n) | 1.224 |
| Aristas (m) | 19.025 |
| Grado de entrada/salida medio | 15,54 |
| Densidad m/(n(n−1)) | 0,0127 |
| Nodos colgantes (sin salidas) | 159 (12,99%) |

## Pregunta de investigación

**¿Los blogs con mayor PageRank pertenecen principalmente a una misma orientación política, o la influencia se distribuye entre blogs de izquierda y derecha?**

Hipótesis inicial: esperamos que la red presente concentración (pocos blogs con PageRank muy superior al resto, típico de redes de hipervínculos con páginas que actúan como centros de referencia), que el PageRank se correlacione con el grado de entrada —con posibles excepciones de blogs enlazados por páginas muy relevantes— y que los blogs de mayor PageRank tiendan a concentrarse en una orientación política.

## Estructura del repositorio

```
.
├── proyecto_2.ipynb        # notebook principal con todo el análisis
├── Datos_blogs/
│   ├── nodos_blogs.txt         # lista de aristas (origen destino)
│   └── orientacion_blogs.txt   # orientación política del nodo i (línea i)
├── figures/                # figuras generadas por el notebook (png)
├── resultados/             # tablas generadas por el notebook (csv)
└── README.md
```

Las carpetas `figures/` y `resultados/` se crean automáticamente al ejecutar el notebook; todas las figuras y tablas del informe se reproducen desde cero al correrlo.

## Requisitos

Python 3.10+ con las siguientes librerías:

```bash
pip install numpy scipy pandas networkx matplotlib jupyter
```

## Instrucciones de ejecución

1. Clonar el repositorio y verificar que la carpeta `Datos_blogs/` contiene los dos archivos de datos (incluidos en el repo; fuente original en [KONECT](http://konect.cc/networks/moreno_blogs/)).
2. Abrir el notebook y ejecutar todas las celdas en orden:

```bash
jupyter notebook proyecto_2.ipynb
```

o desde la terminal, sin abrir la interfaz:

```bash
jupyter nbconvert --to notebook --execute --inplace proyecto_2.ipynb
```

3. Las figuras quedan en `figures/` y las tablas en `resultados/`.

## Contenido del notebook

- **P1.** Carga de datos, construcción del grafo dirigido (NetworkX) y estadísticas básicas.
- **P3.** Análisis exploratorio: distribuciones de grado de entrada y salida, identificación de los 159 nodos colgantes y por qué son problemáticos para PageRank, top 10 de nodos por grado de entrada y de salida con su orientación política.
- **P4.** Construcción paso a paso de la matriz de hipervínculos H (dispersa, construcción vectorizada), la matriz columna-estocástica S (corrección de colgantes) y la Matriz de Google G con α = 0,85. G no se materializa: el producto G·r se calcula de forma factorizada en O(m + n) por iteración, con verificaciones de estocasticidad y positividad.

## Datos y referencias

- Dataset: [moreno_blogs — KONECT](http://konect.cc/networks/moreno_blogs/) (fuente original: [datasets de Moreno](http://moreno.ss.uci.edu/data.html#blogs)).
- L. A. Adamic y N. Glance. *The political blogosphere and the 2004 U.S. election: Divided they blog.* Proc. LinkKDD, 2005.
- S. Brin y L. Page. *The anatomy of a large-scale hypertextual Web search engine.* Computer Networks and ISDN Systems, 1998.

## Uso de herramientas de IA

Se utilizaron herramientas de IA como apoyo en el desarrollo del código y la mejoras de redacción conforme a lo permitido en el enunciado. Todo el contenido fue revisado, verificado y comprendido por los integrantes del grupo.
