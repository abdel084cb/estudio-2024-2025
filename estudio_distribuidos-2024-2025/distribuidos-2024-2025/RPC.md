![[Pasted image 20241229194950.png]]
![[Pasted image 20241229195119.png]]
![[Pasted image 20241229195153.png]]
### RPC
* Consiste en invocar un **procedimiento/método remoto como si fuera local**:
	* Cuando Pa invoca a Pb, Pa se queda bloqueado
	* Parámetros se envían de Pa a Pb
	* Ejecución en Pb
	* Resultado de Pb a Pa
	* Ni para Pa ni para Pb hay noción de paso de msg
	* ![[Pasted image 20241229195437.png]]
	* ![[Pasted image 20241229200613.png]]
	* ![[Pasted image 20241229200630.png]]
	* ![[Pasted image 20241229200655.png]]
* **Retos RPC**
	* Datos intercambiados entre emisor y receptor
		* Acuerdo
		* Serialización
		* Acuerdo mediante una interfaz común
			* IDL
			* Solución para heterogeneidad
	* Interacción e/r
		* interacción sea parecida a invocación
		* Interacción Síncrona vs Asíncrona
* **Interface Definition Language (IDL)**
	* Lenguaje de especificación de interfaces
	* Describir API de un componente de software independientemente del lenguaje
	* Puente entre diferentes lenguajes en la programación RPC
	* Se asignan identificadores únicos a los métodos (en forma de números) para que tanto el cliente como el servidor puedan reconocerlos de manera uniforme y eficiente. Estos números actúan como un **código de referencia** que permite identificar cada función o procedimiento dentro del sistema RPC.    ![[Pasted image 20241229201418.png]]
* **Serialización de Datos**
	* Acuerdo explícito entre e/r
		* Por ejemplo de forma manual
	* Datos incorporan metadatos sobre cómo se han codificado
		* paquete gob de Go
	* Datos en formato de texto
		* XML
		* JSON
* **Interacción vs Invocación**
	* Paso de Parámetros
		* Por valor
			* envío una copia
		* Por referencia
			* ¿hay que simularlo?
			* GPT: No se pueden pasar parámetros por referencia directamente en RPC debido a la separación de memoria entre cliente y servidor. Sin embargo, se puede lograr un efecto similar utilizando parámetros explícitos de salida o estructuras que contengan los resultados. Esto se adapta a las limitaciones inherentes de los sistemas distribuidos.
	* ![[Pasted image 20241229202601.png]]
	* ![[Pasted image 20241229202622.png]]
### Ejemplos RPC
* En C
	* ![[Pasted image 20241229202830.png]]
* En Java: RMI
	* OO de RPC
	* Casi exclusivamente para procesos Java
	* Protocolo de interacción ya no es un Request-Reply, utiliza un enfoque mas complejo
	* Dynamic Class Loading
		* Permite la transferencia de clases (código) entre cliente y servidor
* En Go
	* net / RPC
		* gob + HTTP
	* net / RPC JSON
		* JSON + HTTP
	* gRPC
		* Protocol buffers de Google
### Limitaciones de RPC
* No todas las interacciones son request-reply
	* Hay que usar un Bróker de intermediario