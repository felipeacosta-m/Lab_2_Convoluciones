# Lab_2_Convoluciones
Convolución, correlación y transformación 
## Descripción del proyecto
Este proyecto implementa un código para estudiar la convolución en señales y sistemas, y la correlación para medir su similitud. A partir de una señal electromiográfica (EMG) de Physionet, se aplica la Transformada de Fourier para analizar sus componentes en el dominio de la frecuencia.

## Convolución en señales y sistemas
Para la convolución primeramente el método enseñado en clase que consiste en ubicar h[n] y x[n] en una tabla multiplicando cada muestra de la fila con cada muestra de la columna, de esta manera completando una tabla y para hallar la señal y[n]. Se sumaban los valores en diagonales en orden, y con ello encontrábamos la señal resultante de la convolución a mano como se puede ver en la imagen. 

*Procedimiendo utilizado*

Con esto procedíamos a graficarlo ubicando en X las posiciones de las muestras y en Y el valor de cada uno de estas.

Después de esto procedió a volver a encontrar la señal 𝑦[𝑛] resultante de la convolución utilizando Python para ello se utiliza esta parte del código.  
Donde definiamos como arreglos el sistema h[n] y la señal x[n] para cada uno de los integrantes, para proceder a utilizar la función “convolve” que realiza la convolución. Y añadimos un print para comparar los resultados entre el manual y el digital.

![image](https://github.com/felipeacosta-m/Lab_2_Convoluciones/blob/eece1624e112bbb9cd459f4693033f065b5e444b/Correlaciones.jpg)

## Correlación entre señales 
Para la segunda parte del código, se evaluan la correlación de dos señales que en este caso son : 

•	x1[nTs]=cos(2π100nTs)

•	x2[nTs]=sin⁡(2π100nTs)

Ambas señales están definidas en el intervalo 0 ≤ n< 90 y tienen un período de muestreo Ts= 1.25ms. El objetivo es calcular la correlación entre ellas y analizar la representación gráfica de las señales y su correlación. 

### Señales y su Representación
Las señales x1[n] y x2[n] son funciones discretas en el tiempo, lo que significa que están definidas en instantes específicos nTs en lugar de un tiempo continuo. Dado que la función seno y coseno están desfasadas 90° en el dominio del tiempo, esperamos que sus valores no sean idénticos en los mismos puntos de muestreo. Como el muestreo se realiza con un intervalo fijo Ts, el tiempo efectivo para cada muestra es nTs, donde n varía de 0 a 8, lo que significa que estamos observando solo 9 muestras de la señal. Las funciones seno y coseno son funciones periódicas, lo que significa que repiten su comportamiento en intervalos regulares de tiempo.

### Correlación entre Señales
La correlación es una medida estadística que describe el grado en que dos señales o variables están relacionadas entre sí. En términos simples, nos dice qué tan similares son dos señales y cómo cambia esa similitud cuando una de ellas se desplaza en el tiempo. Matemáticamente, la correlación cruzada entre dos señales x1[n] y x2[n] se define como:

![image](https://github.com/felipeacosta-m/Lab_2_Convoluciones/blob/8e8fa8f5c380f4a935338473a87f88e7d06ed65a/Formula_lab2.png)

*Formula de correlación de señales*

(Si la correlación es alta en un valor de l, significa que una señal es similar a la otra cuando está desplazada en l. Si la correlación es baja o negativa, significa que las señales están desfasadas o son opuestas en ese desplazamiento.)

Existen diferentes tipos de correlación, dependiendo de cómo se analicen los datos:
+ Correlación cruzada: Cuando trabajamos con señales discretas o continuas en el tiempo, usamos la correlación cruzada para medir la similitud entre dos señales a lo largo del tiempo.
+ Correlación lineal: Se usa en estadística para medir la relación lineal entre dos variables. Se expresa mediante un número entre -1 y 1:


*Codigo para obtener la correlación de las señales*

En primer lugar se define el período de muestreo Ts=1.25ms=1.25×10−3sTs y posteriormente se crea el vector n, que representa los índices de muestreo desde 0 hasta 8, luego se definen las señales mencionadas anteriormente.  Estas son señales trigonométricas con una frecuencia de 100 Hz. La diferencia entre ellas es un desfase de 90°, ya que seno y coseno están desfasados por naturaleza.

Por otra parte, se utiliza la función de np.correlate para calcular la correlación cruzada entre ambas señales. La correlación mide la similitud entre las señales a medida que una se desplaza respecto a la otra y por ultimo, se normaliza dividiendo por el valor máximo absoluto de la correlación, para que sus valores queden en el rango de [−1,1].  Se crea un vector lag que representa los valores de desplazamiento entre las señales, desde −8 hasta +8. Luego se crea la interfaz para graficar las señales de seno, coseno y la correlación de ambas.

### Graficas obtenidas

![image](https://github.com/felipeacosta-m/Lab_2_Convoluciones/blob/8e8fa8f5c380f4a935338473a87f88e7d06ed65a/Correlaciones.jpg)

*Grafica de las señales coseno y seno*

La primera gráfica muestra la evolución de x1[n] y x2[n]en el dominio del tiempo. Se observa que ambas señales oscilan entre -1 y 1, como se espera de funciones trigonométricas. x1[n] (coseno) empieza en 1 cuando n=0, mientras que x2[n](seno) comienza en 0 y por ultimo podemos notar que hay un desfase de 90∘ entre las señales, lo que significa que cuando una señal alcanza su máximo, la otra se encuentra en un valor intermedio.

*Grafica de la correlación cruzada entre x1[n] y x2[n]*

De la grafica podemos identificar que La correlación no es máxima en k=0, lo que indica que las señales no están perfectamente alineadas, la correlación es máxima en un cierto valor de k, lo que confirma el desfase de 90∘ entre ellas y valores negativos de correlación indican que en esos desplazamientos, las señales están en oposición de fase. Por lo tanto, el patrón de la correlación coincide con lo esperado para señales senoidales desfasadas en 90∘. La simetría de la gráfica refleja que la correlación entre seno y coseno es periódica.

## Transformada de Fourier

Para finalizar el código presentado realiza el procesamiento de una señal adquirida de la base de datos PhysioNet, incluyendo caracterización temporal, análisis espectral y estadísticos descriptivos. Para un mayor entendimiento se explicará cada una de las etapas realizadas para el procesamiento de la señal. 
En primera medida, para la descarga de la señal el código hace uso de la librería wfdb para leer un registro de señal electrocardiográfica (ECG) de PhysioNet. La señal cargada proviene de un archivo .dat con su correspondiente encabezado. hea. Se extraen los siguientes datos: La freecuencia de muestreo(fs), y la señal correspondiente a una derivacion del ECG.

Luego de esto, para la caracterización de la señal ECG se calculan una serie de estadísticos descriptivos, los cuales son: 1). La duracion total, que se obtiene dividiendo la cantidad de muestras entre la frecuencia de muestreo. 2).Media y mediana, las cuales representan la tendencia central de la señal. 3).Desviacion estandar, mide la dispersión de la señal con respecto a la media y la 4). Desviación absoluta mediana (MAD): Representa la variabilidad de la señal de forma robusta ante valores atípicos. 

De acuerdo a esto se grafica la señal en función del tiempo para asi observar su comportamiento. 

*Señal ECG obtenida.*

Esta señal parece ruidosa y con picos irregulares, lo que puede indicar:Presencia de ruido (interferencias externas o movimiento del paciente), un ritmo cardíaco irregular (arritmias posibles si los picos no siguen un patrón normal) y un ruido de alta frecuencia. 
La señal presenta altos niveles de ruido, evidenciados por picos bruscos y variaciones que no corresponden a una señal ECG limpia, addemas de eso, Se observa un patrón de variaciones alrededor de 0 mV, con picos esporádicos más elevados, lo que sugiere una captación inestable de la señal cardíaca.
Teniendo en cuenta que una señal ECG típica debe mostrar ondas P, QRS y T, que representan la despolarización y repolarización del corazón, en esta imagen, debido al ruido, no es posible distinguir claramente estas ondas, pero es probable que la señal requiera procesamiento digital, como filtrado de ruido y eliminación de artefactos, para extraer la información.

*Resultados estadísticos descriptivos en función del tiempo.*


Posterior a esto, para analizar la señal en el dominio de la frecuencia, se calcula la Transformada de Fourier (FFT) utilizando scipy.fftpack.fft. Se grafican el espectro de magnitud: Representa la amplitud de las componentes frecuenciales de la señal y la densidad espectral de potencia: Muestra la distribución de la energía en función de la frecuencia.

### Graficas obtenidas

![image](https://github.com/felipeacosta-m/Lab_2_Convoluciones/blob/8e8fa8f5c380f4a935338473a87f88e7d06ed65a/ECG%20lab2.jpg)

En esta grafica se puede visualizar el resultado obtenido de la señal ECG dada.

![image](https://github.com/felipeacosta-m/Lab_2_Convoluciones/blob/8e8fa8f5c380f4a935338473a87f88e7d06ed65a/Fourier%20lab2.jpg)

En esta grafica se visualiza el resultado de aplicar la transformada de Fourier a la señal.

*Gráficos de la transformada de Fourier y densidad espectral de potencia de la señal ECG.*

La primer grafica representa la Transformada de Fourier de la señal ECG donde se evidencia la magnitud de la señal en función de la frecuencia. Se observa un pico prominente en la zona cercana a 0 Hz, lo que indica que la señal tiene una componente de muy baja frecuencia dominante (posiblemente debido al componente DC o variaciones lentas). Después de este pico, hay pequeñas variaciones en el espectro hasta aproximadamente 125 Hz (la mitad de la frecuencia de muestreo, que es el límite del teorema de Nyquist).
La segunda grafica permite ver como se distribuye la potencia de la señal a cada frecuencia, se evidencia que la mayor parte de la energía esta en frecuencias bajas con concentración cerca de los 0Hz.











