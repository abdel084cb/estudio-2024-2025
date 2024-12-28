* **Sistema de Comunicación
	* Hardware y software que permiten la comunicación a los procesos de un sistema distribuido.

* **Prestaciones de red
	* Latencia: retardo desde que se envía el mensaje del emisor hasta que comienza a llegar al destinatario
		* Depende de varias cosas como: sobrecargas del software, retrasos de encaminamiento, conflictos...
	* Velocidad: tasa a la que los datos pueden transmitirse a través de una red.
		* Depende de las características físicas del medio de transmisión.
	* Tiempo de transmisión: latencia + tamaño del mensaje / velocidad de transmisión

* **Tipos de redes:
	* LAN
		* Gran velocidad
	* WAN
		* Menor velocidad
		* Internet

* **Principios de Red de Comunicación:
	* Transmisión:
		* Se transmiten paquetes en secuencias de bytes
		* Los paquetes solo saben el destino, no el camino.
		* Los paquetes van llegando al los routers almacenándose en buffers.
		* Cada router decide por dónde se envía el paquete.
		* Esto permite que paquetes a distintos destinos compartan el link.
	* Protocolo de comunicación:
		* Conjunto de reglas y formatos para la codificación y envío de mensajes.
	* Protocolo de interacción:
		* Secuencia de mensajes entre procesos para realizar una tarea.
	* **Protocolos de transporte (TCP y UDP)
		![[Pasted image 20241228182258.png]]
		*  UDP
			* No fiable
			* Checksum para detección de fallos.
		* TCP
			* Fiable
			* Ventana deslizante.
			* Emisor y receptor acuerdan la creación de un canal de comunicación full-duplex.
			* read() bloqueante
			* write() "no bloqueante"
![[Pasted image 20241228185102.png]]


