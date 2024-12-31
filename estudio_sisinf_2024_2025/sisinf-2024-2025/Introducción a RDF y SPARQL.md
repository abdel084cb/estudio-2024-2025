* RDF es un modelo simple para describir recursos
	* Modo natural para humanos
	* Entendible por máquinas
* RDFS permite definir de forma sencilla vocabularios
* SPARQL leguaje declarativo basado en patrones
### RDF
* RDF: Resource Description Framework
* RDF es un modelo estándar para intercambiar datos en la web de forma que las computadoras puedan entenderlos. Describe relaciones entre recursos usando una estructura basada en grafos.
	* Nodos en grafo representan recursos
	* Aristas las relaciones entre los recursos
* RDFS (RDF Schema)
	* Lenguaje basado en RDF para definir vocabularios para RDF
* SPARQL lenguaje declarativo (Protocol and RDF Query Language)
	* Extraer información de grafos RDF
* **Fundamentos**
	* Componente básico es la tripleta
		* Sujeto (recurso)
		* Predicado (propiedad)
		* Objeto (recurso)
		* Multiples formas y sintaxis
		* ![[Pasted image 20241231045025.png]]
* **Fundamentos para facilitar la interoperabilidad**
	* recursos y propiedades se identifican con URIs
	* Propiedades con definición clara y precisa y estar acordadas con una comunidad
		* Dublin Core
			* recursos bibliográficos
		* FOAF
			* personas y entidades y sus relaciones de amistad y pertenencia
		* SKOS
		* ...
* Blank Node
	* Desconocimiento
	* No existe una URI que represente a ese recurso todavía
* Nodo rectangular
	* especifica tipo de datos
	* se especifica el idioma en el que están escritos los valores de las propiedades
* ![[Pasted image 20241231050019.png]]
* GPT:
	* En **RDF**, la información se organiza en **tripletas**
		- **Sujeto**: Es el recurso del que se habla (por ejemplo, una persona, un lugar, o una cosa).
		- **Predicado**: Es la propiedad o característica del sujeto (por ejemplo, "tiene nombre" o "vive en").
		- **Objeto**: Es el valor o recurso relacionado con el sujeto a través del predicado (por ejemplo, "Raquel" o "España").
		- Ejemplo:  
		- "Raquel vive en España":
			- Sujeto: **Raquel**
			- Predicado: **vive en**
			- Objeto: **España**
### SPARQL
* Protocol and RDF Query Language
	* Lenguaje declarativo para extraer información de los grafos RDF
* La pregunta también puede expresarse en forma de grafo
	* ?ganador (ejemplo de nodo)
![[Pasted image 20241231050612.png]]
* **SPARQL** funciona en tres pasos básicos:
	1. Expresa la consulta como tripletas usando variables para los datos desconocidos o deseados.
	2. El motor de búsqueda compara estas tripletas con el grafo de la base de conocimiento.
	3. Cuando encuentra coincidencias, asigna valores a las variables y devuelve los resultados.

* Un **SPARQL Endpoint** es un servicio web que permite a los usuarios enviar consultas SPARQL a una base de datos RDF y recibir los resultados. Funciona como un punto de acceso público o privado para interactuar con datos estructurados en formato RDF.
	* Muchos públicos
		* DBpedia
		* Wikidata
		* ...