<H1 align = "center">
	Metodología 
  <a href="#">
  </a>
</H1>

A continuación, se muestran el conjunto de métodos y técnicas que se realizaron a lo largo de la investigación, 
en este caso se dividió en actividades o tópicos clave y sus procedimientos para el desarrollo del sistema.


## Fingerprinting 
El método fingerprinting crea un mapa de radio de un área determinada basado en los índices de intensidad de señal recibida (RSSI),
de varias balizas y genera una distribución de probabilidad de los valores RSSI para una dada coordenada (x, y) .	El laboratorio mide 8.85
metros cuadrados y se dividió en 16 cuadros de 2 metros cuadrados los .85 cm restantes no se tomaron en cuenta ya que en esa zona se encuentran
escritorios y otros muebles.Los 5 dispositivos balizas se colocaron en cada una de las esquinas del área de pruebas, así como uno en el centro. 
En la Figura x se muestra con más detalle.
__Figura 3- fingerprinting aplicado al laboratorio
 
## Resta cuadrática 

Al realizar 5 escaneos con la app posteriormente se promedian los datos recabados y se obtiene el valor en vector en cada coordenada generada.
Tomemos por ejemplo el arreglo que representa a la coordenada (1,1): [-89,-85.6,-90.8,-90.8,-89.6], el primer elemento -89 representa el valor
de RSSI de la baliza 1 en dicha coordenada, 85.6 representa RSSI de la baliza 2 y así sucesivamente hasta llegar a la baliza 5.

__Tabla 1- vectores estáticos de RSSI por coordenada
Al tener esta matriz se continua con el método para obtener la ubicación. El experimento consiste en aplicar la fórmula de resta cuadrática en datos
“vivos” obtenidos con la aplicación móvil que nos proporciona su RSSI.
Índice Resta Cuadrática [N,M] = (RSSIvivo1 – RSSIestatico1[N,M])2 + (RSSIvivo2 – RSSIestatico2[N,M])2 +...+ (RSSIvivo5 – RSSIestatico5[N,M])2


Donde el RSSIvivo1 es el valor de RSSI de la baliza 1 que captura la app y el RSSIestático1 es el valor de RSSI de la baliza 1 que está guardado,
esta resta se eleva al cuadrado y se suma con cada resta cuadrática hasta obtener el índice de resta cuadrática de una coordenada.
Esta fórmula es aplicada a cada vector estático hasta obtener 64 índices de resta cuadrático.

__Tabla 2- índices de resta cuadrática por coordenada

## Gradiente 
Posteriormente al obtener la matriz de restas cuadráticas se grafica en 3 dimensiones para observar su comportamiento y verificar por medio de
una gradiente descendiente, el cual es un algoritmo de optimización iterativo de primer orden para encontrar el mínimo de una función y
por lo tanto la ubicación determinada por la app.

__ Figura 4- gradiente de tomada en la coordenada (3,2)
Cabe recalcar que la app no lanza la gráfica, para obtener la gráfica se exportan los datos recogidos por la app. La app muestra la siguiente pantalla:
__Figura 5- pantalla de app lanzando ubicación

##	Nivel de precisión del sistema 
Finalmente se realiza un procedimiento para determinar el nivel de confianza en el cual se toman 30 números aleatorios generados en la página
https://www.random.org/ con un rango del 1 al 16 (número de coordenadas distribuidas en el laboratorio). Se escanea en esos puntos, y se anota
en una tabla de Excel para comparar la posición verdadera con la que arrojaba la aplicación.
__ Tabla 3- pruebas de precisión

Esta tabla da un promedio de 1.8 m de precisión, desglosando el resultado en que 6 veces acertó la posición exacta del usuario, 21 veces marcó una
posición vecina equivalente a 2 metros, y solo 3 veces marcaba error de 4 metros, se puede concluir que es un sistema confiable, abarcando en un 90 % un resultado favorable.

__Figura 6-grafica de pastel del nivel de confianza de la app
