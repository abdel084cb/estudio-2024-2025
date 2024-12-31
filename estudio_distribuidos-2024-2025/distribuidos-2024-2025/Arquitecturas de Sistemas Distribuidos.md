### Arquitectura Software
* Estructura de un sistema en términos de componentes y sus relaciones
* Abstracción sobre el código fuente
* Vistas
	* Estática
	* Funcional
	* Dinámica
	* Despliegue
* **Diseño Arquitectural**
	* Satisfacer requisitos y restricciones
	* Propósito, funcionalidad, QoS y restricciones del sistema
	* Importante:
		* se toma al principio
		* difíciles de cambiar
		* impacto a largo plazo
	* En los SSDD:
		* Heterogeneidad, Escalabilidad, Seguridad, QoS, etc.
		* No diseñar desde 0
			* Patrones, arquitecturas...
* **Patrones Arquitecturales**
	* Patrones habituales y conocidos
	* Elementos
		* Descripción y utilidad
		* Modelo arquitectural
		* Código fuente
### Modelos Físicos
* elementos hardware de un SD
* abstracción de detalles específicos de computadores y redes
* ejemplo:
	* ![[Pasted image 20241229225123.png]]
* ![[Pasted image 20241229225318.png]]
### Tipos de componentes
* **Desde  la programación**
	* Programas, Módulos, Objetos
		* Componentes (Con gestión de recursos)
	* Servicios
		* SOA, serverless (Sin gestión de recursos)
### Comunicación
* **Formas**
	* Directa
	* Indirecta
		* Linda, publish-subscribe, colas de mensaje...
		* ![[Pasted image 20241229230311.png]]
		* ![[Pasted image 20241229230324.png]]
		* 
* **Protocolos de comunicación
	* Formato de msg
	* IPC
		* Sockets IPC: TCP/UDP
		* RPC
		* Canales síncronos/asíncronos
* **Protocolos de Interacción**
	* Msg intercambiados entre procesos para conseguir una coordinación/sincronización
	* ![[Pasted image 20241229230246.png]]
* **Tipo y grado de acoplamiento**
	* Acoplamiento espacial
		* Procesos deben conocerse unos a otros
	* Acoplamiento temporal
		* Procesos deben coincidir en el tiempo
	* Lo ideal es minimizar el grado de acoplamiento
* **Análisis acoplamiento Linda**
	* Se minimiza el acoplamiento espacial
		* Solo conocen a Linda
	* No hay acoplamiento temporal

### Patrones arquitecturales
* **Útiles:**
	* Problemas frecuentes
	* Soluciones reutilizables
	* Se pueden adaptar al contexto
* **Cliente-Servidor
	* N procesos: N-1 clientes 1 servidor
	* Servidor ofrece funcionalidad o recurso
	* Cliente interacciona para la funcionalidad o recurso
	* Variantes
		* Servidor secuencial
			* Atiende peticiones una tras otra
			* ![[Pasted image 20241229233357.png]]
			* ![[Pasted image 20241229233410.png]]
		* Servidor concurrente
			* Atiende peticiones simultáneamente
			* ![[Pasted image 20241229233454.png]]
			* ![[Pasted image 20241229233513.png]]
	* **Master-Worker
		* Generalización de Cliente-Servidor
		* Clientes
			* Manda trabajo al master
		* 1 Master
			* Recibe trabajo de algún cliente
			* Puede descomponer o no el trabajo (para repartirlo)
				* Cuando reciba los resultados si se ha descompuesto la tarea las va a tener que agregar
			* Envía el trabajo a los Workers
			* Típicamente devuelve el resultado al cliente
		* Workers
			* Recibe la tarea y la realiza
			* Típicamente devuelve el resultado al master
			* Puede devolver el resultado al cliente
		* ![[Pasted image 20241229233920.png]]
		* ![[Pasted image 20241229233938.png]]
* **Peer-to-Peer p2p
	* Todos los procesos rol similar
	* Interacción entre ellos es cooperativa
	* Escala bien (a diferencia de cliente-servidor)
	* Generalizando, todos ejecutan mismo código y proporcionan misma interfaz de interacción
### Asignación de tareas
* Objetivos
	* ¿Trabajo tengo?¿Recursos tengo?
	* Garantizar QoS
	* Maximizar uso recursos compartidos
	* Minimizar coste energético, económico...