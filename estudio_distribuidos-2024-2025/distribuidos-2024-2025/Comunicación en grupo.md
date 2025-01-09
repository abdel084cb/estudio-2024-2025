![[Pasted image 20250109163600.png]]

![[Pasted image 20250109163707.png]]
- **Comunicación entre pares**:
    - Es la forma más común en sistemas distribuidos, donde un proceso se comunica directamente con otro, usando protocolos como TCP o UDP.
    - Este enfoque es simple, pero no siempre eficiente en escenarios donde múltiples procesos necesitan recibir el mismo mensaje.
- **Comunicación 1-N**:
    - En ciertos casos, un proceso necesita comunicarse con varios procesos simultáneamente (por ejemplo, en un sistema distribuido donde un líder debe informar a todos los seguidores).
    - Puede simularse enviando el mensaje N veces, uno para cada destinatario. Sin embargo:
        - **Ineficiencia**: Requiere múltiples mensajes, lo que puede sobrecargar la red.
        - **Tolerancia a fallos**: Si uno de los mensajes falla, la comunicación con algunos procesos podría interrumpirse.
- **Multicast es una solución:** permite enviar un único mensaje que puede ser recibido por varios procesos simultáneamente, reduciendo la sobrecarga y mejorando la eficiencia.

* **Problema Mutex Distribuido**
	* Un grupo de procesos necesita coordinarse para acceder, uno a la vez, a una **sección crítica (SC)**, asegurando la **exclusión mutua**.
* **Problema Consenso Distribuido**
	* Un grupo de procesos debe ponerse de acuerdo sobre un valor común, incluso si algunos procesos fallan o actúan de forma inesperada.
 * **Publish-Subscribe**
	- **N fuentes de datos** generan información periódica.
	- **M consumidores** eligen recibir información de ciertas fuentes.
	- Un sistema intermedio gestiona y conecta las fuentes de datos con los consumidores interesados.

![[Pasted image 20250109171438.png]]

* **Requisitos de comunicación en grupo:**
	* Cada grupo con dirección IP
	* Grupos de tamaño dinámico
	* Miembros en cualquier parte de internet
	* Miembros pueden unir y abandonar un grupo
	* Pertenencia a un grupo no se conoce a priori
	* Emisores no tienen porque ser miembros del grupo
	* Analogía:
		* Radio frecuencia: cualquiera puede transmitir y cualquiera puede conectarse y escuchar
* **Pertenencia al Grupo**
	* Mensajes al grupo se reciben por todos los miembros
	* Si los procesos se añaden / borran de un grupo, todos los miembros activos son notificados, manteniendo la consistencia
	* Todo mensaje se entrega siguiendo configuraciones específicas que garantizan su precisión. Sin embargo, siempre se busca asegurar que:
		- **Atomicidad:** El mensaje se entrega completo o no se entrega en absoluto.
		- **Uniformidad:** Todos los nodos reciben el mismo mensaje de manera consistente.
		- **Terminación:** El proceso de entrega siempre llega a completarse, sin quedarse indefinidamente pendiente.
- **Retos de Comunicación en Grupo VAOG** 
	- Vivacidad y Tolerancia a fallos
		- Fiabilidad en entrega
	- Atomic Multicast
		- O se entrega a todos o nadie lo recibe
	- Orden de llegada de los mensajes
		- ¿Orden de llegada como orden de emisión?
	- Gestión de la pertenencia al grupo
		- Dinamismo (los procesos pueden unirse o salir del grupo en cualquier momento, requiriendo actualizaciones consistentes para evitar pérdida de mensajes o envío a miembros inactivos...) y garantías de identidad anónima (comunicarse sin revelar identidad)
	- **Ordenación de mensajes**
		- **Best-Effort (sin control alguno):** Envía mensajes sin garantizar entrega ni orden.
			- ![[Pasted image 20250109181126.png]]
		- **Reliable Multicast:** Asegura que todos los procesos entregan el mensaje o ninguno lo hace.
			- ![[Pasted image 20250109181357.png]]
		- **FIFO Multicast:** Garantiza que los mensajes de un emisor llegan en el orden en que fueron enviados.
			- ![[Pasted image 20250109182205.png]]
		- **Causal Broadcast:** Mantiene relaciones de causalidad entre mensajes.
			- ![[Pasted image 20250109183011.png]]
			- broadcast(m1) − > broadcast(m2)
			* broadcast(m1) − > broadcast(m3)
			* Ordenes válidos: (m1, m2, m3), (m1, m3, m2) 
		- **Total Order Broadcast:** Todos los procesos reciben los mensajes en el mismo orden.
			- ![[Pasted image 20250109184204.png]]

### Diseño e implementación de Comunicación en Grupo
* Alternativas
	* **Unicast:**
		* Emisor envía msg repetidamente punto a punto.
		* Poco eficiente en recursos
	* **IP Multicast**, aprovecha la infraestructura de red para una transmisión eficiente, ideal para redes locales o controladas.
		* Soporte hardware
		* ![[Pasted image 20250109193517.png]]
		* IP Multicast típicamente sobre UDP: no fiable
		* Operaciones
			* recepción
			* envío
			* gestión de pertenencia al grupo
		* Multicast routing
			* Problemas potenciales de denegación de servicio
			* Costoso económicamente
			* El gran tamaño de los estados que los routers deben mantener en Multicast routing es un desafío significativo, especialmente en redes grandes o con muchos grupos Multicast activos.
			* Buena solución para una LAN que uno controla
	* **Overlay Multicast** es más flexible y aplicable a Internet global pero a costa de mayor complejidad y overhead en la gestión de mensajes.
		* Comunicación en Grupo en internet
		* ![[Pasted image 20250109194446.png]]
		* Una **overlay network** es una red lógica construida sobre una red física subyacente. Los nodos de la overlay se conectan a través de enlaces virtuales o lógicos que utilizan caminos en la red base. Ejemplos incluyen sistemas distribuidos cliente-servidor y peer-to-peer, que operan sobre Internet como una capa adicional.
			* ![[Pasted image 20250109200105.png]]
				* El nodo emisor envía un mensaje directamente a cada nodo destinatario de forma independiente
			* ![[Pasted image 20250109200334.png]]
			* ![[Pasted image 20250109200346.png]]
			* ![[Pasted image 20250109200402.png]]
			* ![[Pasted image 20250109200414.png]]


**Conclusiones**
- **Comunicación en grupo**
    - Los sistemas distribuidos requieren de comunicación en grupo.
    - Muchas aplicaciones necesitan enviar mensajes a un conjunto de procesos.
    - La comunicación punto a punto (**unicast**) es la más extendida, pero resulta ineficiente respecto a la red.
    - La comunicación en grupo enfrenta varios retos:
        - Dinamismo de los grupos.
        - Privacidad.
        - Seguridad.
        - Orden de los mensajes.
        - Carencias en los proveedores de internet para implementarlo.
    - En las **LAN** puede utilizarse **IP Multicast**, pero generalmente no es viable en Internet.
    - Existen alternativas a **IP Multicast** para implementar comunicación en grupo, aunque son menos eficientes.