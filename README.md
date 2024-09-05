# Laboratorio 2 de señales (problema de la fiesta de cóctel)

El efecto cóctel consiste en enfocar la audición en una sola voz dentro de una habitación llena de personas. La solución de este problema a nivel computacional requiere diferentes mecanismos, como la transformada rápida de Fourier para el análisis en frecuencia de las señales y métodos de separación de fuentes.

Para este propósito, se grabaron dos audios en una sala insonorizada (ruido ambiental y voces), teniendo en cuenta que se utilizaron tres fuentes diferentes, así como tres micrófonos con un sistema de adquisición de señales.

La configuración de la captación de audio se muestra en la siguiente imagen. En este ejercicio, cada fuente dijo una frase diferente al mismo tiempo de grabación.

[imagen]

Los micrófonos se ubicaron a una distancia de 0.5 metros frente a cada fuente y a 1 metro de distancia entre las fuentes, como se muestra en la imagen anterior.

Para la adquisición de la señal, se utilizó el sistema de adquisición de datos llamado Recforge, que es una aplicación móvil para celulares. Esta aplicación permite garantizar la frecuencia de muestreo, el nivel de cuantización y el tiempo de grabación. Para este ejercicio, se utilizó una frecuencia de muestreo de 44 kHz, un nivel de cuantificación de 160 Kbps (kilobits por segundo) y un tiempo de grabación de 5.1 segundos. Estos valores aseguran una buena precisión de la señal digitalizada con respecto a la análoga, lo que permite un análisis más completo y preciso de las señales tanto en el dominio del tiempo como en el de frecuencia.

Continuando de esta manera, con la ayuda de la librería librosa, se subieron los audios a Colab, y con la librería matplotlib, se graficaron cada señal. Estas se pueden observar a continuación.





