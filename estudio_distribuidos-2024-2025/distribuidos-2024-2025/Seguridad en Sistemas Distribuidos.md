* **Seguridad**
	* Objetivo seguridad: restringir acceso a la información y a recursos, sólo a aquellos autorizados con acceso.
	* **Acceso seguro** a la información / recursos
		* Confidencialidad
		* Integridad
			* contra la manipulación no autorizada
		* Disponibilidad
			* contra interferencia no deseada
	* security policies / normas de seguridad
		* normas utilizarán mecanismos para garantizar la seguridad
	* ![[Pasted image 20250110011713.png]]

* **Amenazas y ataques**
	* Filtración
	* Manipulación
	* Vandalismo
		* sin beneficio para el autor
	* Espionaje (snooping) ((confidencialidad))
	* Enmascaramiento (fishing) ((integridad))
		* Enviar o recibir mensajes utilizando la identidad de otro
	* Manipulación de datos / mensajes ((Integridad))
		* El ataque de intermediario ocurre cuando un atacante intercepta mensajes entre dos partes, altera su contenido y los reenvía, haciéndose pasar por uno de los participantes. En el caso de intercambio de claves de cifrado, el atacante sustituye las claves originales con otras comprometidas, lo que le permite descifrar los mensajes, leer su contenido y luego cifrarlos nuevamente antes de enviarlos al destinatario, sin que las partes lo noten.
	* Denegación de servicio ((disponibilidad))

![[Pasted image 20250110012402.png]]

### Criptografía
* **Tipos**
	* Clave simétrica
		* Misma para cifrado y descifrado
		* AES, Blowfish...
	* Clave pública
		* cifrado / descifrado con diferentes claves
		* RSA, DSA, ECC...
	* Funciones hash
		* MD5, SHA1, SHA512...
* Los algoritmos criptográficos deben ser robustos, con claves suficientemente largas (por ejemplo, RSA de 1024 a 4096 bits y AES de 128 a 256 bits) para dificultar su descifrado.
* Coste computacional: hash < simétrica < pública

* Los mecanismos de seguridad en sistemas distribuidos emplean cifrado en distintos niveles: **aplicación** (Kerberos, simétrico y SSH, combinación), **transporte** (SSL/TLS, combinación) y **red** (IPSec, combinación)

* **Certificados digitales**
	* Los certificados digitales autentican a una persona o entidad en una red y permiten el intercambio seguro de información utilizando criptografía de clave pública. Contienen la clave pública del titular, información básica (nombre, fecha de caducidad, etc.) y una firma digital de una entidad certificadora externa.
		* ![[Pasted image 20250110020234.png]]
		* ![[Pasted image 20250110020336.png]]
		* Posibilidad de auto-firmarse certificados si puedes distribuirlo de forma fiable
		* Existe un conjunto de autoridades certificadoras para firmar certificados que puedan utilizarse en Internet (VeriSign, GlobalSign, cacert.org,. . . )

### Distribución de Claves Públicas
* Las **claves públicas** son flexibles, pero su distribución fiable depende de mecanismos como la **PKI (Infraestructura de Clave Pública)**. La PKI relaciona identidades con claves públicas mediante certificados digitales firmados por **Autoridades Certificadoras (CA)**, que venden certificados y establecen cadenas de confianza. Las claves privadas no se incluyen, ya que cada usuario las guarda de forma segura.
	* Kerberos integra ya la distribución de claves secretas
* Obtener certificados válidos:
	* Firma digital por entidad fiable la que da validez
	* ![[Pasted image 20250110022232.png]]
* Expiran...
* Confianza...
### Protocolo SSL/TLS
* El protocolo **SSL/TLS (Secure Sockets Layer/Transport Layer Security)** garantiza la seguridad de las comunicaciones en redes como Internet al proporcionar confidencialidad, integridad y autenticación. Utiliza cifrado para proteger los datos, certificados digitales para autenticar servidores y, opcionalmente, clientes, y un proceso de "handshake" para negociar claves de cifrado y algoritmos seguros. Es ampliamente utilizado en **HTTPS**, correos electrónicos y VPNs para proteger datos sensibles mediante cifrado y evitar manipulaciones o interceptaciones durante la transmisión.
 * ![[Pasted image 20250110180945.png]]
 * **Transport Layer Security**
	 * **TLS (Transport Layer Security)** es un protocolo criptográfico diseñado para proporcionar **seguridad** en las comunicaciones a través de redes, como Internet. Es el sucesor de **SSL (Secure Sockets Layer)** y mejora sus características para garantizar **confidencialidad**, **integridad** y **autenticación** en las conexiones.
	 * ![[Pasted image 20250110182104.png]]
	 * ![[Pasted image 20250110182148.png]]
	 * ![[Pasted image 20250110182212.png]]
		 * Autenticación del servidor (y opcionalmente del cliente).
		- Generación de claves compartidas.
		- Configuración de cifrado e integridad para el resto de la sesión

### Kerberos

**Kerberos** es un protocolo de autenticación en redes que utiliza criptografía de clave simétrica para garantizar la comunicación segura entre usuarios y servicios. Es especialmente utilizado en sistemas distribuidos.

Características principales:
1. **Autenticación centralizada**: Un servidor de autenticación (Key Distribution Center o KDC) valida a los usuarios y les proporciona tickets para acceder a servicios.
2. **Tickets de sesión**: Los usuarios no envían contraseñas directamente, sino que reciben un ticket cifrado que sirve como prueba de autenticidad para los servicios.
3. **Seguridad**: Utiliza claves temporales (tickets de sesión) para reducir el riesgo de exposición de credenciales.
4. **Resistencia a ataques**: Protege contra ataques de repetición y evita la transmisión de contraseñas en texto claro.

Kerberos es ampliamente usado en entornos corporativos, como en sistemas Windows y aplicaciones basadas en redes, para ofrecer autenticación segura y gestión de identidades.

![[Pasted image 20250110184249.png]]
![[Pasted image 20250110184351.png]]
![[Pasted image 20250110184415.png]]
![[Pasted image 20250110184440.png]]
* Debilidades
	* KDC contiene todas las claves y distribuye
	* Replicación de KDC, con consistencia eventual
	* Un acceso no autorizado a KDC compromete las claves