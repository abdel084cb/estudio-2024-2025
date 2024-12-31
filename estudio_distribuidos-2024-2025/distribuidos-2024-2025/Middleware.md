![[Pasted image 20241229192929.png]]
* Formas de comunicación entre componentes
	* Directa
	* Indirecta
* Protocolos de comunicación
	* UDP y TCP son protocolos de comunicación
* Protocolos de interacción
	* Request - Reply es un protocolo de interacción
* Codificación de los datos
	* Serialización/Marshalling

### Codificación de los Datos
* **Operaciones TCP/IP**
	* read(data byte[]) bloqueante
	* write(data byte[]) no bloqueante
* Se debe codificar el byte[]
	* Acuerdo entre emisor y receptor
	* Metadatos en los mensajes
	* Datos en texto -> XML/JSON
### Middleware
![[Pasted image 20241229193500.png]]
* **Invocación remota:
	* RPC
		* Invocar procedimiento remoto como si fuese local
		* servidor publica una interfaz
		* se genera código automático para serializar los datos
		* el cliente invoca al procedimiento como si fuese local
		* ![[Pasted image 20241229193622.png]]
		* ![[Pasted image 20241229193911.png]]
* Modelo Actor
	* Actor
		* proceso
		* enviar y recibir msg asíncronamente
		* solo memoria local
		* un proceso recibe los msg en un buzón
		* cada proceso tiene un único PID
		* ![[Pasted image 20241229194049.png]]
* Comunicación Indirecta
	* ![[Pasted image 20241229194121.png]]
	* Modelo: Cola de Mensajes
		* Emisor y receptor desacoplados espacial y temporalmente
		* Comunicación 1 a 1
	* Modelo: Publish - Subscribe
		* Emisor y receptor desacoplados espacial y temporalmente
		* Comunicación N a M
	* Implementación: El bróker de Mensajes
		* Posibilita la comunicación indirecta, actúa como intermediario
		* El bróker tiene wrappers, pudiendo transformar y adaptar mensajes entre procesos
![[Pasted image 20241229194825.png]]
