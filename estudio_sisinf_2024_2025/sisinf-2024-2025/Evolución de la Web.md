* Fuentes de datos
	* No estructurada
	* Estructurada
	* Semi-estructuradas o híbridas **(La web)**
### Web estática o tradicional (Web 1.0)
* **Internet
	* Nodos 
	* Protocolos
	* Comunicar y compartir datos
	* Compartir recursos
	* Surgen numerosas app (sistemas de información) gracias a seta infraestructura
		* FTP
		* correo electrónico
		* IRC
		* Telnet
		* World Wide Web (primera página web) (www)

* **Pre-web. Gopher (aun no era web 1.0)
	* Acceso a la información a través de menús
	* Superado por www

* **www
	* Sistema universal de identificadores
		* UDI/URL/URI
	* Lenguaje de publicación
		* HTML
	* Protocolo de transmisión
		* HTTP
	* Uniform Resource Identifier
		* ![[Pasted image 20241230225554.png]]
		* Todos los URL son URI, no todos los URI son URL
	* Uniform Resource Locator (URL)
		* Es un URI
		* http://www.example.com/index.html
	* Hyper Text Markup Language (HTML)
		- **GET:** Parámetros en la URL. Usado para obtener información. Usado para solicitar datos de un servidor.
			- https://example.com/buscar?producto=libro&precio=20
		- **POST:** Parámetros en el cuerpo. Usado para enviar datos al servidor.
			- https://example.com/registro
		- **Otros tipos de peticiones**
			- HEAD
			- PUT
			- DELETE
		- **Respuestas del servidor incluyen un código de estado**
			- 1xx (información)
			- 2xx (éxito)
			- 3xx (redirección)
			- 4xx (error cliente)
			- 5xx (error servidor)
* **Web de solo lectura**
	* Pocos emisores vs. muchos consumidores de la información
		* grandes corporaciones que difunden información
* **Mayor problema**
	* Información generalmente desactualizada
	* Coste de actualización alto
* **Ataques y amenazas**
	* Externas
		* Contra la disponibilidad
		* Contra la integridad
		* Contra la confidencialidad
		* Contra la conservación
	* Internas
		* Factor humano
		* Fallo técnico
		* Contenido de la web obsoleto
		* Interfaces pobres
### Web dinámica o de transición (Web 1.5)
* Cambio tecnológico con respecto a la Web 1.0
	* Proceso de crear páginas HTML en tiempo real al momento de ser solicitadas, utilizando información almacenada en bases de datos y plantillas predefinidas. Esto permite integrar datos actualizados de los sistemas de gestión con la web, evitando mostrar información obsoleta.
* Siguen siendo Read Only
* Surge concepto de sesión
	* HTTP protocolo sin estado
		* Alternativas
			* id sesión en cookies
			* transmitir id session en todas las URL
			* id sesión en campos ocultos de formularios
* **Características**
	* Cookies
		* ![[Pasted image 20241230232551.png]]
	* Búsqueda de información
		* Surgen los motores de búsqueda
	* Nuevos modelos de negocio
		* Tiendas de comercio electrónico
* **Ataques y amenazas**
	* Factor humano o fallo técnico
		* Comprobaciones de errores solo en el cliente permite manipular parámetros en la URL
		* SQL injection
		* Uso incorrecto de HTTPS 
			* HTTPS solo al inicio, luego se usa http, haciendo visible el id dela sesión.
		* Cross Site Scripting (XSS)
			* Inyectar scripts maliciosos al cliente para robarle datos
	* Interfaces pobres
		* Pantallas en blanco
		* Demasiado recargadas
		* Solución AJAX
			* Permite actualizar partes de una página web sin recargarla completamente. Esto mejora la fluidez y la experiencia del usuario al proporcionar respuestas rápidas y dinámicas, evitando pantallas en blanco y reduciendo la sobrecarga visual.
			* Asynchronous JavaScript and XML
			* ![[Pasted image 20241230233527.png]]
* **JavaScript**
	* Se ejecuta en el navegador
	* Efectos dinámicos en la páginas web
* **XML Extensible Markup Language**
* **HTTPS**
	* ![[Pasted image 20241230233806.png]]

### Web social (Web 2.0)
* Solo cambio de filosofía y uso con respecto a la Web dinámica
	* **Read-Write Web**
* Ejemplos
	* Wikipedia
	* Facebook
	* Blogger
	* YouTube
	* Twitter
	* Instagram
* Nuevos modelos de negocio
	* Airbnb
	* Uber
* **Búsqueda de información**
	* Contenido crece exponencialmente
		* Necesidad de escalar sistemas de búsqueda
			* buscadores distribuidos vs centralizados
			* escalabilidad horizontal vs vertical
		* Buscadores específicos vs generalistas, verticales vs horizontales
* **Ataques amenazas y vulnerabilidades**
	* Contrastar información y fuentes de los datos
		* fake news...
	* Dificultad de localización de contenidos (sobre todo cuando no se busca lo que la mayoría)
	* Web oculta o profunda
		* ![[Pasted image 20241230234509.png]]
		* Muchas formas de esconder el contenido
			* Tor...
			* Contenido que no esta en HTML (buscadores no lo reconocían)...

### Web semántica (Web 3.0)
* **Características**
	* Objetivo
		* Orientada a máquinas y personas, no solo a personas como las anteriores
		* los agentes SW pueden interactuar de forma automática para lograr sus objetivos
		* La **Web 3.0**, o **web semántica**, es una evolución de Internet diseñada para que las máquinas comprendan e interpreten los datos como lo hacen los humanos. Esto permite experiencias más inteligentes y personalizadas al conectar información de manera estructurada y relevante.
	* Ejemplos:
		* Siri
		* Google Knowledge Graph
	* **Read-Write and Executed Web** se añade la ejecución
	* Cambio tecnológico basado en tres pilares:
		* Anotación de recursos con metadatos
		* Ontologías o vocabularios estandarizados comunes
		* Uso de reglas y razonadores (motores de inferencia) para deducir nuevos datos que permitan tomar decisiones
	* **Tecnologías para la anotación de recursos Web**
		* integración de información semántica en la web, que las máquinas puedan interpretar
			* RDFa 
		* Recuperar información semántica
			* SPARQL
				* "Como un SQL para la web semántica"
		* ![[Pasted image 20241231000105.png]]
		* ![[Pasted image 20241231000129.png]]
	* **Ontologías o vocabularios estandarizados comunes**
		* ejemplo: FOAF
		* ![[Pasted image 20241231000408.png]]
		* ![[Pasted image 20241231000420.png]]
		* ![[Pasted image 20241231000432.png]]
		* **Tecnologías para definir ontologías**
			* RDF
			* RDFS
			* OWL
		* **Reglas y razonadores**
			* Motores de inferencia automáticos
				* Ratón animal AND animales seres vivos THEN ratón ser vivo
			* Motores de razonamiento
				* Varios ejemplos
* **Inicios de la web semántica: La web de datos enlazados**
	* En resumen, la **Web semántica** y los **datos enlazados** buscan transformar la web de un conjunto de documentos no estructurados en un ecosistema de datos interconectados y entendibles por las máquinas, mejorando la accesibilidad y la integración de la información global
	* Aplicación que demostró la viabilidad de la Web Semántica:
		* DBpedia
			* DBpedia es un proyecto de la Web Semántica que extrae datos estructurados de Wikipedia y los convierte en datos enlazados accesibles a través de la web. Permite a las máquinas interpretar y relacionar información de forma inteligente, como fechas, lugares y conceptos, utilizando estándares como RDF y SPARQL. Es una herramienta clave para conectar datos de múltiples fuentes y fomentar la interoperabilidad en la Web de datos enlazados.
	* ![[Pasted image 20241231001258.png]]
### ¿Cuál es la próxima generación? (Web 4.0)
* Fumadotes de realidad virtual y aumentada
### Web3
* **Características**
	* Basado en tecnología Block Chain
	* Web descentralizada
	* Token based economics
	* Sin permisos
	* Pagos nativos
	* Seguridad de datos
	* Privacidad
	* Resistencia a la censura
	* Escalabilidad
	* Pero también 
		* Falta de moderación
		* Perdida de privacidad debido a una mayor recolección de datos
		* Coste transacciones
		* Falta de conocimiento
		* Dependencia de una estructura centralizada
* **Relacionado**
	* DeFi
	* DAO
	* tokens
	* smart contracts
	* criptomonedas
	* ...
### Directorios vs motores de búsqueda
![[Pasted image 20241231002022.png]]
