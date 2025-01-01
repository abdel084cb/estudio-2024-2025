* Data Warehouse
	* Un **Data Warehouse** es un repositorio centralizado que almacena datos estructurados de una empresa, integrando información histórica y actual para facilitar el análisis y la toma de decisiones estratégicas, sirviendo como base para herramientas de **Business Intelligence**.
* ![[Pasted image 20250101013101.png]]
* **Características de los almacenes de datos**
	* Orientados a un aspecto concreto
		* Tema de interés para los directivos de la entidad
	* Integrados
		* todos los datos de los sistemas operacionales de la empresa, entre otros datos
		* deben ser consistentes
	* No volátiles
		* no se borran ni actualizan
		* pensados para un horizonte mucho mayor que los datos operacionales
* ![[Pasted image 20250101013752.png]]
* **Procesos ETL**
	* Extracción
		* Para realizar una imagen inicial
		* Para actualizar una imagen ya existente
		* Muy costoso en tiempo, puede afectar al rendimiento de los sistemas fuentes de datos
	* Transformación
		* ![[Pasted image 20250101014034.png]]
	* Carga
		* Se cargan los datos de la fase anterior (transformación)
		* Completa
			* Primera carga (imagen inicial)
		* Incremental
			* Carga en intervalos de tiempo regulares y planificados
				* Streaming (volúmenes pequeños de datos)
				* Por lotes (grandes)
			* Mantenimiento de históricos (se puede hacer el seguimiento temporal de un dato)
	* Staging Area
		* ![[Pasted image 20250101014428.png]]
* **Modelos multidimensionales**
	* Un **Data Mart** es un subconjunto de un **Data Warehouse** diseñado para servir a las necesidades específicas de un departamento, área de negocio o grupo de usuarios dentro de una organización. Es una versión más pequeña y enfocada del Data Warehouse, optimizada para consultas y análisis específicos.
	* Como organizar los datos en un DW
	* Cubo (n-dimensionales)
		* Ejemplo 3 dimensiones![[Pasted image 20250101014830.png]]
		* ![[Pasted image 20250101015348.png]]
		* ![[Pasted image 20250101020927.png]]
		* Operación básica: la agregación
			* ¿Qué cantidad de productos de la marca X se han vendido durante el mes actual en las diferentes tiendas?
* **Implementación de los cubos**
	* Virtual: El modelo **virtual** es la opción más simple para organizar datos en análisis multidimensionales. Consiste en una única tabla donde las columnas representan las dimensiones (como tiempo, producto o región) y los datos de interés (como el número de ventas). Este modelo sigue un **esquema en estrella**, con una tabla central que contiene los datos principales y referencias a dimensiones relacionadas.
	- Físico: El modelo **físico** utiliza bases de datos multidimensionales, donde los datos se almacenan en una **matriz n-dimensional** que organiza los valores directamente según sus dimensiones. Este enfoque es más complejo, pero está optimizado para consultas rápidas en análisis de grandes volúmenes de datos.
- Arquitectura en estrella
	- Tabla central con información que se desea analizar. Conectada a las tablas que representan las dimensiones.
	- ![[Pasted image 20250101022108.png]]
	- ![[Pasted image 20250101022136.png]]
- Generación de informes
	- Configurables
	- Drill down
		- Detallar los resultados añadiendo un campo
	- Roll up
		- Agregar/Converger los resultados obtenidos eliminando un campo
	- ![[Pasted image 20250101022521.png]]
- **Dashboard (Tablero de mandos)**
	- ![[Pasted image 20250101022627.png]]
-
- **Factores de éxito**: Un Data Warehouse exitoso integra datos externos con datos internos de producción, gestionando historiales relevantes para el análisis. Se debe centrar en información útil alineada con los objetivos de la empresa, emplear datos de calidad (coherentes, actualizados y documentados) y diseñar una arquitectura flexible que permita la escalabilidad en hardware, software, usuarios, herramientas y volumen de negocio.
    
- **Errores comunes**: Entre los errores más frecuentes están incluir datos solo porque están disponibles, aunque no sean útiles, y diseñar el esquema como una base de datos relacional tradicional, lo que limita el análisis multidimensional. También es un error construir el Data Warehouse pensando únicamente en la tecnología a usar y asumir que el trabajo termina al cargar los datos, sin considerar herramientas para análisis e informes dinámicos.


![[Pasted image 20250101023314.png]]