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



### Estimación de Potencia

Cálculo de retardos de Elemore
