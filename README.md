# Informe Tarea2_VLSI
## Emanuel Cordero Fallas y Yerlyn Mora Artavia
## Introducción
En este repositorio se encuentran los archivos utilizados para la resolución de la tarea 2 del curso así como el presente informe de los resultados obtenidos.

## Problema
Se debe diseñar una compuerta CMOS que resuelva la operación Y=(A+B)(C+D), una de las soluciones debe ser por medio de una compuerta compleja y la otra debe ser utilizando varias etapas sencillas.

## Solución por compuerta compleja
Primeramente se plantea el circuito que representa la ecuación booleana, debido a que la lógica CMOS presenta una salida negada se añade un inversor al final. El esquemático final es el siguiente:

![Esquematico_compleja](figuras/Esquematico_compleja.jpeg)

Para el tamaño de los transistores se realizó el análisis de esfuerzo lógico, teniendo en cuenta los anchos máximos y la carga máxima estipulada se obtuvo que para la compuerta compleja los PMOS deben tener un tamaño de 20 transistores unitarios mientras que los NMOS un tamaño de 10 transistores unitarios. Para el caso del inversor el PMOS debe ser de tamaño 29 y el NMOS de tamaño 58.

![Tamaños compleja](figuras/Tamaños_compleja.png)

Luego de calcular los tamaños de cada uno de los transistores, se monta el esquemático en el simulador y se verifica su funcionalidad, contrastandolo con la tabla de verdad.

![Funcionamiento_compleja](figuras/Funcionamiento_compleja.jpeg)

### Estimación de Potencia
Para el cálculo de la potencia de la compuerta se utilizó la siguiente expresión:

$$P_{sw}= \alpha \cdot C \cdot V_{DD}^2 \cdot f_{sw}$$

El periodo de reloj maximo utilizado fue de 600ps lo que equivale a una frecuencia de 1.67 GHz, con este dato y asumiendo un factor de actividad de 0.5 para cada una de las entradas se tiene que la potencia dinámica de la compuerta es de:


$$P_{sw}= 0.5 \cdot 0.483fF \cdot 1.8^2 \cdot 1.67 GHz$$

Obteniendo que la potencia de la compuerta es de $$P_{sw}= 1.31 \mu W$$

### Cálculo de retardos de Elmore
Para los retardos de elmore primero se calcula el retardo de la carga y descarga del inversor para luego analizar la compuerta compleja sin el inversor y sumar ambos retardos.


* Tiempos de propagación: Para los tiempos de propagación se plantea el peor caso de carga y descarga en la compuerta. Para el cálculo de los retardos de propagación se utilizaron los siguientes casos:

![tpdr_compleja](figuras/tpdr_compleja.jpeg)
![tpdf_compleja](figuras/tpdf_compleja.jpeg)

  * tpdr: Para el tiempo de rise, se debe calcular cuando la compuerta compleja da un 0 como salida ya que el inversor se encargará de proporcionar el 1.
 
   

    $$t_{pdr} = \frac{R}{10} \cdot 20C + \frac{R}{5} \cdot 147C + \frac{R}{29} \cdot 587C$$
    $$t_{pdr} = 51,64RC$$

  * tpdf: Para el tiempo de fall, se debe calcular cuando la compuerta compleja da un 1 como salida ya que el inversor se encargará de proporcionar el 0.
 
    

    $$t_{pdf} = \frac{R}{10} \cdot 40C + \frac{R}{5} \cdot 147C + \frac{R}{58} \cdot 587C$$
    $$t_{pdr} = 43,52RC$$

* Tiempos de contaminación: Para estos tiempos se plantean los mejores casos que puede presentar la compuerta, es decir, cuando la capacitancia que se debe cargar o descargar es menor:
  
![tcdr_compleja](figuras/tcdr_compleja.jpeg)
![tcdf_compleja](figuras/tcdf_compleja.jpeg)
  
  * tcdr: Para el tiempo de rise, se debe calcular cuando todos los NMOS están encendidos y se asume que las capacitancias de los nodos inferiores en la compuerta ya han sido descargadas en el ciclo anterior, luego se suma el retardo del inversor.
 

    $$t_{cdr} = \frac{R}{10} \cdot 147C + \frac{R}{29} \cdot 587C$$
    $$t_{cdr} = 34,94RC$$

    * tcdf: Para el tiempo de fall, se debe calcular cuando todos los PMOS están encendidos luego se suma el retardo del inversor.
 


    $$t_{cdf} = \frac{R}{20} \cdot 40C + \frac{R}{10} \cdot 147C + \frac{R}{29} \cdot 587C$$
    $$t_{cdf} = 36,94RC$$

### Contraste con simulación
Para obtener los retardos exactos se sustituye los valores obtenidos en la tarea anterior, siendo así $$R=12,84 k \Omega$$ y $$ C=0,483 fF$$. Una vez obtenidos estos valores, se crean las condiciones necesarias para medir los retardos en el simulador de custom compiler obteniendo los siguientes resultados:


|     |  Teórico  |  Simulado  | Diferencia    |
|  :---           |  ---:   |  :---:  |  ---   |
|  $t_{cdr} (ps)$ |  229,09 |  346,13 | 117,04 |
|  $t_{cdf} (ps)$ |  216,69 |  190    | 26,69  |
|  $t_{pdr} (ps)$ |  333,9  |  232    | 101,9  |
|  $t_{pdf} (ps)$ |  269,9  |  149    | 120,9  |


Se observó que la diferencia entre los datos teóricos y simulados es muy poca, lo cual indica que los retardos teóricos son útiles para obtener una aproximación de la compuerta y determinar si se deben realizar modificaciones de algún tipo, pero siempre es importante obtener los datos simulados para una medición más precisa.

### Layout de la compuerta
Una vez contrastados los datos teóricos y simulados se procedió a trazar el diagrama de palitos y el layout de la misma:

![Diagrama_palitos](figuras/diagrama_palitos.png)
![Layout_Compleja](figuras/Layout_compleja.jpeg)

Así mismo, una vez trazado el layout se procedió a hacer la verificación DRC hasta corregir todos los errores y obtener el modelo final.

![DRC_compleja](figuras/DRC_compleja.jpeg)

## Solución por compuerta simple 
Al realizar el análisis por medio de etapas sencillas, en la siguiente figura se muestra lo obtenido.  
![WhatsApp Image 2024-04-29 at 10 17 53 PM](https://github.com/EmanuelCF/Tarea2_VLSI/assets/149116215/de4a703e-b3a5-4e4f-800d-b52bfc64b380)

A partir del esfuerzo lógico, se obtuvo el tamaño de los transistores PMOS y NMOS en cada una de las etapas. En la primera etapa, conformada por una compuerta NOR se tiene un tamaño igual a 6 para los PMOS y de 24 para los NMOS. En la segunda etapa, conformada por una compuerta NOR, se tiene un tamaño igual a 13 para los PMOS y de 52 para los NMOS. Mientras que en el inversor, a la salida, se tiene un PMOS con tamaño igual a 47 y un NMOS con un tamaño de 93. En la siguiente figura se muestra el esquemático con los tamaños requeridos. 

![image](https://github.com/EmanuelCF/Tarea2_VLSI/assets/149116215/fcf61d97-4dcc-4ab2-862a-0b29adb247d5)
