# Shark_Project (work in progress)



Por cuestiones de estética y comodidad para el lector, además de sostenibilidad technologica, se hará un breve resumen del exhausto proceso de limpieza realizado en el documento de python adjunto.

## Objetivo

El principal objetivo de la tarea es limpiar y consolidar una base de datos de manera que me permita realizar un estudio a futuro sobre la distribución de ataques de tiburón por el mundo a lo largo del año.
Potencialmente, se podría descburir si hay ciclos geográficos de ataques de tiburón y si, por ejemplo, tiene correlación con la temperatura del agua en esa época del año. 
Por ese motivo, también se ha priorizado la hora del día en el que ocurrió el ataque, ya que la temperatura del agua varia según la hora del día que sea.
Además, se ha hecho especial incapié en limpiar la categoría de edades y especie de tiburón para categorizar de mayor medida nuestro analisis y determinar si distintos tiburones tienen preferencia por distintos grupos de edades.


##Limpieza de filas

Después de limpiar los títulos de las columnas, se identificó que un gran porcentaje de filas tenían por lo menos 21 de las 23 filas en nulo, por lo que se dropeo esas filas.

##Limpieza de columnas

### Case Number

He limpiado el dato nulo (revisando previamente las filas colindantes) y después he identificado esta columna como el índice de la tabla así que acabaré la limpieza convirtiendo esta columna en el index.

###Date

He usado regex para separar el año, el mes y el día de case_number y formar una nueva celda de fecha, además de limpiar la columna year, y crear dos columnas más de mes y día.
También se ha ejecutado considerable "limpieza de lupa" para maximizar la canidad de no-nulos en la tabla ya que nos interesa tener toda la columna de fecha con los máximos valores no nulos posibles.

### Country

También se limpió de manera minuciosa reescribiendo paises mal escritos y sacando los valores reales de agunos valores nulos mirando el Area y el Location.

### Type, Area, Location, Activity, Name, Sex

Por su dificultad de relleno de nulos, y su poca importancia para el análisis, se pudo generalizar con 'Unknown' para los valores nulos de estas categorías.

### Age

Complicada columna, pero con especial cuidado de quitar los caracteres que molestaban y encontrando secuencias repetidas (como 'numero' palabra 'numero), pude hacer medias y dejar la columna Age de manera ordenada.
Mención especial a la función 'take_age'.

### Fatal

Pude rellenar hasta un 20% de los nulos viendo a ver si podía determinar si había sido un ataque mortal, dependiendo de si aparecían ciertas palabras clave (como 'death, o 'letal') en la columna descriptiva de 'injury'.

### Time

Primero busqué ciertas palabras que tiene relacion con un rango de horas del día (como sunset) y le otrogué una hora aleatoria de ese rango.
Luego para quedarme unicamente con las horas, dividí las palabras por la letra h y me quede unicamente con los dos caracteres antes de la h que coincidían precisamente con la hora.

### Species 

Species tenía una alta cantidad de valores únicos y pude disminuirlos solamente quedandome con la palabra "shark" y la palabra previa a esa, que casi siempre era el tipo de tiburón que era o al menos su tamaño, que es descripción suficiente.

### Columnas restantes

Con el resto de columnas, pude acabar por simplemente rellenar los nulos con 'Unknown' ya que eran pocos y generalmente insignificantes.

## Dtypes

Para acabar, realicé el protocolo rutinario de convertir los valores objeto pertinentes en categorias, y "downcast" los floats e ints.
La tabla empezó pesando 23MB y acabó pesando 3MB

