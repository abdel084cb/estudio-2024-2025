* Estrategias **preventivas
* Estrategias **reactivas**
### Fallos

![[Pasted image 20241229170918.png]]
* **Detección de fallos**
	* Mediante paso de mensajes
	* Timeout
		* Se conocen los tiempos de comunicación, ejecución, overhead
			* Se puede ajustar
		* No se conocen los tiempos
			* Se aumenta timeout: exponential backoff en cada reintento
	* **Métricas sobre fallo**:
		* Localización
			* Donde se origina
			* No siempre se puede saber
				* máquina
				* red
		* Origen
			* componente que lo origina
		* Estampilla temporal
		* Duración
			* permanente
			* intermitente
			* temporal
		* Gravedad (subjetivo)
			* bajo
			* medio
			* alto
		* Comportamiento
			* crash
				* falla y deja de funcionar
			* omission
				* no se recibe respuesta tras petición
			* timing
				* se recibe respuesta con retardo
				* No se puede distinguir entre timing y omission
					* Se pueden generar respuestas duplicadas
			* response
				* respuesta incorrecta
			* byzantine
				* respuesta maliciosa semánticamente
				* intencionalmente incorrecta
	* **Ideas:**
		* Redundancia temporal
		* Redundancia física
		* Ignorar el fallo
		* Pedir ayuda

### Redundancia Cliente
![[Pasted image 20241229172743.png]]
* **Algoritmo 1: redundancia temporal**
	* Proxy gestiona los fallos
	* Proxy fija timeout y reintenta k veces
	* Se detecta
		* Crash
		* Omission
		* Timing
* **Algoritmo 2: redundancia física y temporal**
	* Proxy
		* Gestiona fallos
		* Fija timeout
		* Envía petición a N servidores
		* Reintenta K veces
		* En cuanto llega una respuesta se redirecciona al cliente
	* Se detecta
		* Crash
		* Omission
		* Timing

![[Pasted image 20241229175621.png]]
* **Algoritmos de Detección de Fallos Bizantinos**
	* Cliente-Servidor
		* Interacción Síncrona, Lamport
			* consenso entre k+1 réplicas
		* Interacción Asíncrona, Castro-Liskov
			* consenso entre `3*k + 1 `replicas
		* k es el número de procesos que fallan bizantinamente

### Redundancia Servidor

* **Detector Fallos: Latido**
	* señal periódica
	* o en momentos puntuales
* **Estado servidor**
	* Con estado
		* Hay que mantener la integridad de un almacén de datos
	* Sin estado
* **Algoritmos de elección de líder**
	* Cualquier proceso del grupo electivo puede servir de coordinador y puede iniciar elección
	* Cada proceso solo puede tener una elección al mismo tiempo
	* Cada nodo tiene un único identificador
	* Al final, se ha elegido un solo proceso  los demás procesos conocen su identidad como líder
* **Algoritmo del Matón**
	* Cada proceso conoce el PID de los demás procesos, sabe cuales son mayores
	* Interacción síncrona gestionada por timeouts
	* Red sin fallos
	* Inicia elección si el líder no responde
	* Procesos con mayor PID intimidan a los de menor para expulsarlos de la elección quedando al final un único proceso.
	* Cuando un proceso fallido re-arranca, inicia una elección automáticamente
	* 4 tipos de msg:
		* Elección: anuncia elección
		* Respuesta: respuesta a elección
		* Coordinador: anuncia líder elegido
		* Latido: msg que se envía al coordinador, si contesta está vivo
	* Proceso lanza elección:
		* timeout expirado, el coordinador no responde
		* recibe Elección
			* Si ya estaba en elección contesta si procede pero no vuelve a lanzar Elección
	* Proceso empieza elección
		* Envía Elección a todos los procesos con PID mas alto
		* Si no se recibe Respuesta se convierte en líder y manda el msg Coordinador a todos los procesos vivos
		* Si llega Respuesta, entonces espera Coordinador durante un tiempo
		* Si no llega el msg Coordinador entonces reinicia la Elección
		* Si un proceso sabe que su PID es el mas alto entonces puede responder inmediatamente con Coordinador
		* Se deben ajustar los tiempos de expiración
			* `(2*RTT + Tprocesado)`
		* Si hay error durante la detección de fallo, la elección seguirá adelante.
![[Pasted image 20241229182205.png]]
![[Pasted image 20241229182240.png]]
* **Algoritmo de elección en Anillo**
	* Cada P conoce su posición en el anillo (ordenados por PID)
	* Cada proceso conoce al resto
	* Se asume que no hay fallos durante elección
	* Es asíncrono
	* Elegir líder al proceso vivo cuyo PID es el mayor
	* 3 tipos de msg:
		* Elección: reenviar datos de elección
		* Coordinador: anuncio del coordinador elegido
		* Latido: timeout para determinar si el líder sigue vivo
	* **Algoritmo**
		* Pi comienza elección tras timeout
		* Pi envía Elección junto con su PID al primer vecino
		* Cuando un proceso recibe Elección compara su PID con el recibido
			* Si su PID es mayor lo reemplaza y lo reenvía al anillo
			* Si su PID es menor reenvía msg Elección recibido
			* Si su PID es el del msg Elección entonces se convierte en líder
		* Finalmente reenvía msg Coordinador
		* Los procesos que han recibido Elección no inician otra elección hasta recibir Coordinador
