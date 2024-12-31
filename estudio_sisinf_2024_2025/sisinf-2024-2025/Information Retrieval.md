* **Objetivo de los sistemas de Recuperación de Información IR**
	* Dada una colección de documentos (corpus documental) y una necesidad de información de un determinado usuario expresada en forma de pregunta (query) recuperar (extraer o listar) los documentos para resolver la necesidad de información del usuario
		* ![[Pasted image 20241231060445.png]]
* **Componentes básicos de un RI**
	* Formalismo para representar los documentos
	* Formalismo para representar las consultas
	* Medida de similitud entre un documento y una consulta
* **Posible solución**
	* Dada una consulta se recorre secuencialmente el corpus comparando las palabras de la consulta con las de los documentos
	* Emparejamiento sintáctico de patrones (Matching sintáctico simple)
	* Solución eficiente para muy pocos documentos
* **Problemas del matching sintáctico simple**
	* Aunque aparezcan palabras de la consulta para un documento, puede ser este no relevante para la consulta
	* Lo mismo del revés, aunque no aparezcan, puede ser relevante igualmente
* **Problemas derivados del recorrido secuencial del corpus**
	* La búsqueda en un corpus documental grande de más de 200 MB es ineficiente si se realiza de forma secuencial, ya que requiere demasiado tiempo al recorrer todos los documentos. Para resolver este problema, se utiliza un **índice invertido**, una estructura que asocia cada término con una lista de documentos donde aparece, evitando el recorrido completo. Este índice consta de un **diccionario** con términos ordenados como claves y listas de identificadores de documentos como valores, permitiendo acceder rápidamente a la información relevante.
	* ![[Pasted image 20241231061319.png]]
* **Necesidad de una medida que evalúe la relevancia entre una consulta y un documento**
	* Ranking de documentos. Los mas relevantes en primer lugar.
	* Diferentes modelos de representación y medidas de similitud entre queries y documentos:
		* Booleano
		* Vectorial
		* Probabilístico
* **Evaluar un RI
	* Medidas estándar de efectividad
		* Precisión (P) 
			* docs relevantes recuperados/docs totales recuperados
		* Recall (R)
			* docs relevantes recuperados/total de docs relevantes
		* F-measurement
			* Media harmónica de P y R
				* Formula turbia
		* Corpus TREC
	* Medidas de eficiencia:
		* Menor cantidad de recursos empleados
* RI no solo modelos para representar docs y consultas
	* Métodos de:
		* almacenamiento de docs
		* Compresión de docs e índices
		* Indexación de docs
		* Presentación (Ranking)
	* Otros:
		* Clasificación de docs
		* Agrupamiento de docs similares

* ![[Pasted image 20241231064333.png]]
	* Módulo de gestión de documentos
		* Gestionar los documentos del corpus y los metadatos que tienen asociados
			* Insertar, actualizar, eliminar, parsear para extraer info de ellos, recuperar mediante id, consultar metadatos mediante id (fecha de modificación, autor...)...
	* Módulo de operaciones de texto
		* El módulo de operaciones de texto transforma documentos o consultas en una representación lógica como una secuencia de términos. Esto se logra eliminando palabras sin contenido semántico (**stopwords**) o reduciendo palabras a sus raíces (**lematización**, **stemming**). También se pueden usar técnicas avanzadas de procesamiento de lenguaje natural (**NLP**) para identificar nombres compuestos (como "bases de datos"), entidades (como "George Bush") y desambiguar palabras con múltiples significados.
		* Transformar el documento/consulta original en una representación del mismo/de la misma (vista lógica)
			* Secuencia de términos (vista lógica)
	* Módulo de indexación
		* Gestionar los índices sobre los documentos
	* Módulo de operaciones de consulta
		* Se usan recursos como Thesaurus (por ejemplo, WordNet) y ontologías para mejorar las consultas al añadir términos relacionados, como sinónimos o conceptos más amplios (hiperónimos). Por ejemplo, "coche" se expande a "coche, auto o carro". Además, se puede pedir retroalimentación al usuario para aclarar ambigüedades, como si "manzana" se refiere a la fruta o a una empresa tecnológica. Esto enriquece la representación lógica de la consulta y mejora los resultados.
	* Módulo de operaciones de búsqueda
		* Dada la representación lógica de una consulta realiza consultas en los índices para determinar cuales son los docs relevantes
	* Módulo de ranking
		* Ordena los documentos recuperados de acuerdo con la relevancia respecto a la consulta que se está resolviendo
			* Medida de similitud entre la consulta y los docs
				* Modelo booleano
				* Modelo vectorial
				* Modelo probabilístico
			* Otros aspectos:
				* Contexto del usuario
				* Preguntas anteriores del usuario
* Modelos: pertenecen específicamente al **módulo de ranking**, aunque también tienen relación con el **módulo de búsqueda** dependiendo de su implementación.
	* **Modelo booleano**
		* Cada doc se representa con una lista de bits indicando si en ese doc aparece un determinado término del vocabulario del corpus
		* ![[Pasted image 20241231223245.png]]
		* Sencillo y rápido de implementar
		* Difícil hacer ranking
			* Recupera o muy pocos o demasiados docs
			* Dificultad de los usuarios para expresar consultar booleanas
	* **Modelo booleano extendido**
		* En lugar de considerar sólo 0 y 1 en los vectores que constituyen las representaciones lógicas de los documentos, se considera el número de veces que aparece un término en un documento
		* Más fácil hacer un ranking de los docs recuperados
			* Mas apariciones antes de los de menos apariciones
	* **Modelo vectorial**
		* Las queries y los docs se representan mediante vectores
			* dimensión = cardinalidad del vocabulario (conjunto de términos considerados)
		* ![[Pasted image 20241231224122.png]]
			* Muchas variantes para determinar la similitud de los vectores...
				* La de la foto
				* Dice
				* Jaccard
				* ...
		* Ventajas
			* Sencillo de implementar
			* Poco coste computacional
			* Librerías proporcionadas
			* Alto rendimiento
		* Desventajas
			* Asume independencia de términos
			* No tiene en cuenta el tamaño de los doc
				* En documentos mas grandes mas sencillo encontrar términos
	* **Modelo probabilístico**
		* Estrategia adaptativa basada en probabilidades condicionadas y el teorema de Bayes

* **Diferencias entre Corpus y Web**
	* Un **corpus** es un conjunto controlado y finito de documentos con un propósito específico, mientras que la **web** es un espacio abierto, dinámico y descentralizado, diseñado para publicar y acceder a información globalmente.
	* Hay que localizar los docs
		* Localización manual (directorios de búsqueda)
		* automática (crawlers o arañas)
		* híbrida (arañas localizan usuarios clasifican)
	* **Directorios de búsqueda**
		* Organización manual de las páginas en categorías
			* Yahoo en sus inicios
		* Desventajas
			* Escalabilidad
			* Definición de la estructura
	* **Motores de búsqueda**
		* Adaptación de las técnicas de RI en grandes corpus a la Web mediante el uso de arañas (crawlers) generalmente con interfaces basadas en palabras clave
		* Construcción de un gran índice de palabras sobre todos los documentos del web estático.
		* Búsquedas por palabras clave sobre el índice, obteniendo granularidad de documento.
		* ![[Pasted image 20241231225655.png]]
		* * **Algoritmo Hits**
			* Relevancia basada en hiperenlaces
				* búsqueda sobre un índice
				* se itera sobre los enlaces entre docs
				* hubs páginas que enlazan muchas páginas buenas
				* autoridades son páginas buenas
				* la página autoridad debe estar contextualizada dentro del tema buscado y no simplemente recibir enlaces de cualquier tipo de página.
			* Procesamiento básico en HITS
				* motor de búsqueda tradicional
				* expanden resultados con páginas que apuntan a los resultados y con apuntadas por los resultados
				* cada página empieza con un peso de hub y un peso de autoridad
				* El peso de autoridad de un nodo se calcula como la suma de los pesos de hub de los nodos que lo enlazan en la iteración anterior.
				- El peso de hub de un nodo se calcula como la suma de los pesos de autoridad de los nodos a los que enlaza.
		* **Algoritmo Page-Rank
			* enlaces se consideran citas de otros doc
			* mas relevantes los doc más citados, también importa quién es el que te cita
			* página tiene pagerank alto si tiene muchas páginas que la apuntan, o la apuntan páginas con un pagerank alto (hubs)
			* El texto de los enlaces se asocia a la página
			* ![[Pasted image 20241231231636.png]]
			* ![[Pasted image 20241231232003.png]]		
### La web oculta
El contenido de la Web no indexado por los motores de búsqueda y por tanto difícilmente localizable a no ser que se conozca su existencia.

![[Pasted image 20241231232300.png]]
