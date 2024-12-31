### Introducción
**Datos vs Información vs Conocimiento**
* **Datos**
	* Valores
* **Información**
	* Colección de datos organizados proporcionando un valor añadido.
* **Conocimiento**
	* Conciencia o familiaridad adquirida

**Proceso vs Algoritmo vs Sistema**
* **Proceso 
	* Tareas lógicamente relacionadas que a partir de datos de entrada proporcionan resultados (datos de salida)
* **Algoritmo**
	* Lista ordenada de pasos o especificación de instrucciones para llevar a cabo una determinada tarea.
* ![[Pasted image 20241230213223.png]]
* **Sistema**
	* Conjunto de elementos (procesos, algoritmos, conocimiento, información y datos) que interactúan para lograr un objetivo
		* Programa de control médico con el objetivo de evitar la obesidad infantil
### Sistemas de información
**Definición de (R. Stair & G. Reynolds):**
Es un sistema que está compuesto por un conjunto de elementos interrelacionados que recogen (entrada), manipulan (proceso), almacenan información, y diseminan (salida) datos y, además, proporcionan mecanismos correctores (feedback) para alcanzar un determinado objetivo
* **Componentes cualquier tipo de sistema**
	* Entradas
	* Mecanismos de procesado
	* Salidas
	* Retroalimentación (feedback), para mejorar los mecanismos de procesado
		* Efectividad (métrica c.t.s)
			* Mide hasta que punto se ha alcanzado el objetivo
		* Eficiencia (métrica c.t.s)
			* Optimización de recursos
	* ![[Pasted image 20241230213457.png]]
	* Medidas de rendimiento estándar (métrica c.t.s) específicas al sistema
* **Componentes de un sistema de información**
	* Hardware
	* Software
	* Datos
		* Incluyendo la configuración del sistema y los datos específicos generados, almacenados y procesados.
	* Personas
	* Procedimientos y protocolos
		* Son las normas, métodos y políticas que regulan el uso, mantenimiento, seguridad y calidad del sistema, asegurando su correcto funcionamiento y cumplimiento de estándares.
	* **Clasificación**
		* ![[Pasted image 20241230214420.png]]
			* Cabe destacar que esto no es un dogma
		* Sistemas de procesado transaccional (TPS)
			* Gestionan información referente a las transacciones diarias en una organización (centrados en la recolección de datos)
				* Ventas de productos..
		* Sistemas de información de gestión (MIS)
			* Orientados a los responsables técnicos para la definición de procedimientos rutinarios
				* Generación de nominas...
		* Sistemas de apoyo a la toma de decisiones (DSS)
			* Soporte para la toma decisiones para un problema complejo. La información para analizar el problema no suele estar definida.
			* Ejemplo: Software destinado a la creación de Data Warehouses
				* Un Data Warehouse (almacén de datos) es una base de datos centralizada diseñada para almacenar grandes volúmenes de datos provenientes de múltiples fuentes. Su objetivo principal es facilitar el análisis y la toma de decisiones estratégicas dentro de una organización.
		* ![[Pasted image 20241230215354.png]]
		* Sistemas de información para ejecutivos (EIS)
			* DSS para altos directivos
			* Conseguir objetivos estratégicos de la empresa
### Aplicaciones empresariales

* Almacenan y manipulan datos
* Realizan transacciones
* Escalables
* Disponibles
* Seguras
* Integración
* Tipos de interfaces:
	* texto
	* de escritorio
	* web
	* móviles
* Arquitectura:
	* **Aplicaciones monocapa:**
		* Toda la lógica (interfaz de usuario, procesamiento y datos) se encuentra en un solo lugar, como en una hoja de cálculo o una aplicación de escritorio simple.
			* Ejemplo: Excel
		* Modelo de datos:
			* Dependiente de la aplicación en concreto, no tiene en cuenta la integración con el resto de sistemas de la empresa
		* Persistencia:
			* Ficheros
		* Ventajas:
			* Rápidas
			* Útiles para propósito específico
		* Inconvenientes
			* Instalación y re-compilación en todas las máquinas
			* Datos duplicados y necesidad de procesos ETL

	* **Aplicaciones de dos capas:**
		* Ejemplo Una aplicación que usa un cliente de escritorio conectado a una base de datos como SQL Server.
		* ![[Pasted image 20241230221328.png]]
		* Se separa interfaz y modelo
			* Modelo
				* Reglas de negocio, gestión de datos
			* Interfaz
				* Navegación y visualización
			* Ventajas:
				* Se reutiliza la capa modelo para diferentes dispositivos
				* Cada capa se puede desarrollar por personas con perfiles específicos
			* Inconvenientes:
				* Si se cambia el modelo hay que recompilar e instalar en todas las máquinas cliente

	* **Aplicaciones de tres capas:**
		* ![[Pasted image 20241230221914.png]]
		* Ventajas
			* Cambios de modelo solo afectan al servidor
			* Se reduce el coste de equipos de cliente (poca capacidad de procesamiento)
		* Inconvenientes
			* Cambios en la interfaz gráfica implica recompilar y reinstalar la aplicación cliente

	* **Aplicaciones de tres capas con interfaz Web**
		* ![[Pasted image 20241230222152.png]]
		* Ventajas:
			* Solo recompilar y reinstalar la capa interfaz en el servidor de la aplicación web
			* Servidores Web suelen ser
				* escalables
				* disponibles
	* **Aplicaciones de cuatro capas**
		* ![[Pasted image 20241230222348.png]]
		* Suele usarse cuando gráfica y modelo usan tecnologías diferentes 
* **Tecnologías**
	* Acceso a BD
		* API JDBC
		* API ODBC
	* Aplicaciones Web
		* Servlets y JSP para interfaz, Java EE para modelo
		* ...
	* Servidores Web
		* Tomcat
		* Wildfly
		* ...
* **Cloud computing**
	* ![[Pasted image 20241230222821.png]]
	* ![[Pasted image 20241230222839.png]]
	* Funcionalidad tipos
		* SaaS
			* Software
				* Software listo para usar
		* PaaS
			* Platform
				* entornos de desarrollo y despliegue de aplicaciones sin gestionar la infraestructura
		* IaaS
			* Infrastructure
			* ofrece recursos computacionales
				* almacenamiento
				* red
				* procesadores
	* Compartición tipos
		* Público
		* Privado
		* Híbrido
		* Comunitario