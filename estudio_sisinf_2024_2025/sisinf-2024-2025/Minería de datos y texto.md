* Extracción no trivial de información que reside de manera implícita en los datos
* Descubrir a partir de los datos, conocimiento
	* No trivial
	* Implícito
	* Previamente desconocido
	* Potencialmente útil
	* Interesante
* Según objetivo
	* Predictiva
	* Descriptiva
* **Pasos:**
	* Aprender sobre el dominio de la app
	* Seleccionar datos para analizar evitando sesgos y asegurando precisión
	* Preparar los datos (cleaning -> fiabilidad)
		* puede llegar al 60% del trabajo total
	* Reducir y transformar los datos
	* Escoger el objetivo de minería
	* Escoger algoritmo apropiado
	* Analizar los resultados
		* Utilizar herramientas de visualización de forma adecuada
		* ...
		* Correlación vs Causalidad
		* ...
	* Explotación del conocimiento descubierto
	* ![[Pasted image 20250101031850.png]]La correlación no implica causalidad. En este caso, sería absurdo concluir que la disminución de los piratas **causa** el aumento de la temperatura global o viceversa. La relación observada es una coincidencia, ya que no hay una conexión lógica o científica entre estas dos variables.

* Regresión
	* Vainas raras

* **Reglas de asociación**
	* ![[Pasted image 20250101032443.png]]
	* Tres medidas importantes
		* ![[Pasted image 20250101032657.png]]
		* Entenderlos para posibles test
			* ![[Pasted image 20250101032837.png]]
			* ![[Pasted image 20250101032915.png]]
			* ![[Pasted image 20250101033123.png]]
			* Sirven como criterio de calidad
				* Soporte lo mas alto posible
				* Confianza próxima a 1
				* Elevación > 1
			* Para filtrar y ordenar reglas de asociación
* **Agrupamiento (clustering)**
	* Objetos dentro del mismo grupo son similares
	* Objetos de distintos grupos son diferentes
	* Interesa
		* Maximizar la similitud dentro de la agrupación
		* Maximizar la diferencia entre agrupaciones
* **Clasificación**
	* Asociar cada elemento del conjunto de datos a una de una serie de categorías definidas previamente
	* Variables
		* Response
			* etiqueta cada instancia con la categoría correspondiente
			* resto son predictoras (independientes)
		* explicar la dependiente en términos de las independientes
	* Matrices de confusión
		* ![[Pasted image 20250101040644.png]]
		* ![[Pasted image 20250101040657.png]]
		* Precisión ¿Formulas?
			* Capacidad para no identificar incorrectamente
		* Recall ¿Formulas?
			* Capacidad para no dejarse instancias de una clase sin identificar correctamente
		* F-measure ¿Formulas?
			* Media armónica entre precisión y exhaustividad
		* Accuracy
			* Número de clasificaciones correctas / Número total de clasificaciones realizadas
		* ![[Pasted image 20250101041029.png]]
			* TPR
				* cuántos resultados positivos se detectan de entre todas las muestras positivas disponibles en el test
			* FPR
				* cuántos resultados positivos se detectan de forma incorrecta entre todas las muestras negativas disponibles en el test
	* **Evaluación**
		* datos entrenamiento
		* datos test (validación)
		* Nunca evaluar sobre los datos de entrenamiento
		* generalización vs over fitting
		* ![[Pasted image 20250101041646.png]]
* **Minería de textos**
	* Minería de datos textuales = Minería de datos no estructurados
	* ¿Importante?
	* Técnicas parecidas a IR primera prte