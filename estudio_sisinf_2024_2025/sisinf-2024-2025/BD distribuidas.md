### BD distribuidas
* BD centralizada
	* Cuellos de botella
	* Latencias
	* Distintas frecuencias de acceso
	* ...
* Un sistema de BBDD distribuidas es una colección de varias BBDD que se encuentran lógicamente interrelacionadas y desplegadas sobre una red de ordenadores.
	* Los datos deben estar repartidos en varios nodos
	* Deben compartir un esquema global que las integre, como si fuesen una sola
	* Coordinar las operaciones entre nodos para garantizar la consistencia e integridad de los datos
* Un sistema de gestión de bases de datos distribuidas (SGBDD) es el software que permite el manejo de sistemas de BBDD distribuidas (BDD) y que hace dicha distribución transparente al usuario (semántica vs implementación)
* **Diseño top-down**
	* E/R global
	* Fragmentación del esquema global
	* Elaboración de los esquemas locales y asignación de los fragmentos a ellos
		* Incrementa el nivel de concurrencia de las t (BIEN)
		* Algunas t se degradan si tienen que trabajar con varios fragmentos (MAL)
		* ![[Pasted image 20241231235446.png]]
* **Fragmentación**
	* **Tipos de fragmentación**
		* Horizontal
			* ![[Pasted image 20241231235645.png]]
		* Vertical
			* ![[Pasted image 20241231235715.png]]
		* Híbrida
			* ![[Pasted image 20241231235747.png]]
	* **Debe ser**
		* Completa
		* Reconstruible
		* Con intersección vacía
	* **Asignación**
		* Sin replicación
			* Positivo para la actualización
			* Negativo para las consultas
		* Replicación total
			* Positivo para las consultas
			* Negativo para la actualización
		* Replicación parcial
			* Compromiso entre actualizaciones y consultas
		* ![[Pasted image 20250101001020.png]]
* **Arquitectura: Factores**
	* **Distribución**
		* Una **base de datos distribuida** divide sus datos entre múltiples componentes (BD locales), pero estos están integrados para funcionar como un único sistema lógico. Las bases locales tienen un grado de autonomía, pero no operan como sistemas completamente aislados. Esto diferencia a las BD distribuidas de simples conjuntos de bases de datos independientes.
	* **Autonomía**
		* Control del SGBD sobre cada BD local
			* de diseño
				* Cada administrador de una base de datos local puede modificar su **esquema conceptual** (estructura de tablas, relaciones, etc.) sin depender del sistema distribuido.
			* de comunicación
				* La base de datos local puede decidir **cuándo y cómo comunicarse** con las otras BD del sistema distribuido
			* de ejecución
				* La base de datos local puede decidir en qué **orden** ejecutar transacciones globales (que afectan a varias BD) y transacciones locales (que afectan solo a esa BD).
			* de participación
				* La base de datos local puede decidir **si y cómo** participar en el sistema distribuido.
	* **Heterogeneidad**
		* La heterogeneidad en sistemas distribuidos implica que los nodos pueden tener diferencias en hardware, sistemas operativos, modelos de datos o SGBD, lo que añade complejidad a la integración y comunicación entre ellos. Un sistema distribuido debe manejar esta diversidad para funcionar como un todo coherente.
		* Semántica
			* Sinonimia
			* Homonimia 
			* Hiperonimia
			* Hiponimia
			* Agregación
			* ![[Pasted image 20250101003726.png]]

### BD federadas
Las **bases de datos federadas** integran múltiples BD independientes bajo un esquema global común, manteniendo su autonomía local.
* Esquema global se obtiene de abajo a arriba
* No hay que fragmentar, y la redundancia probablemente ya existe
* Problema de obtener esquema global a partir de N esquemas locales
	* Traducción
		* Convertir todos los esquemas locales a un modelo común
	* Integración
		* Combinar esos esquemas traducidos en uno solo, resolviendo conflictos y redundancias. Esto permite trabajar con las bases de datos distribuidas como si fueran una sola.
* El **modelo de datos canónico** utilizado para crear el **esquema global** es clave para garantizar que todas las bases de datos locales (que pueden ser heterogéneas) puedan integrarse y funcionar como un sistema único.
* ![[Pasted image 20250101004429.png]]
	* En la fase de **traducción**, se toma el esquema exportado de las bases de datos locales (por ejemplo, tablas y atributos relacionales) y se transforma a un modelo más rico, identificando entidades, relaciones y atributos. Este proceso incluye un **enriquecimiento semántico**, donde pueden surgir nuevas entidades, como especializaciones (subtipos) o generalizaciones (supertipos), para representar mejor los datos y sus significados.

	* En la fase de **integración**, se combinan los esquemas traducidos aplicando reglas semánticas entre las entidades y relaciones de los esquemas locales. Esto implica resolver conflictos como **sinonimia** (nombres diferentes para conceptos iguales), **unión** (fusión de entidades similares) y **generalización o especialización** (ajustar jerarquías entre entidades), creando un esquema global coherente y consistente.
* Las consultas deben responderse sobre los esquemas locales
	* Información de enlace
		* Relación entre los elementos del esquema global y los del local necesarios para poder responder a las consultas
* ![[Pasted image 20250101004928.png]]
	* Las entidades `estudiantes` y `alumnos` se consideran **sinónimos** y se combinan en una entidad global llamada `Estudiantes`.
	- Se define un enlace entre las tablas de ambas bases utilizando una consulta SQL con `UNION` para fusionar los datos de **BD1** y **BD2**.
	- La entidad `est-2ºciclo` se mantiene como una entidad global derivada de **BD1**.
### BD interoperantes
Las **bases de datos interoperantes** permiten la comunicación y cooperación entre BD distintas, sin necesidad de un esquema global, adaptándose a la heterogeneidad de los sistemas.
* El usuario es consciente de que trabaja con varias BD
