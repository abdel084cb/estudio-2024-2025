* **Replicación**
	* Para mejorar tolerancia a fallos
	* Para mejorar las prestaciones (escalar)
		* Mantener todas las réplicas consistentes puede suponer un enorme coste en prestaciones
			* Sincronización global
		* Solución: relajar la consistencia
			* Diferentes modelos
				* Dependiendo del modelo de consistencia adoptado, las réplicas pueden ofrecer distintas propiedades, como rapidez de acceso, tolerancia a fallos o exactitud en los datos, lo que debe elegirse en función de los requisitos específicos del sistema.
	* En ambos casos hay que mejorar la consistencia

* **Modelos de consistencia**
	* Consistencia secuencial
		* ![[Pasted image 20250109222832.png]]
		* Lo importante es que **todos los procesos ven las mismas operaciones en el mismo orden**:
		- En el primer caso, el orden observado por **P3** y **P4** es: `b` primero, luego `a`.
		- Aunque el orden real de escritura sea diferente, **este orden es consistente para todos los procesos**
		- ¿Segundo caso no válido?

	- Consistencia casual
		- ![[Pasted image 20250109223749.png]]
	- Consistencia eventual
		- ![[Pasted image 20250109224401.png]]

### Transacciones distribuidas
* **Una transacción distribuida** define una secuencia de operaciones en un conjunto de servidores. Se garantiza que la secuencia es atómica, o se ejecuta completamente o no se ejecuta. Además, pueden coexistir múltiples clientes y múltiples servidores y todos ellos pueden fallar.
	* Transacción
		* termina comprometida (commited), con efectos visibles
		* se aborta (aborted), sin efectos visibles
		* **Servidores: all commit or all abort**
	* Transacciones anidadas
		* Se estructuran a partir de conjuntos de otras transacciones
		* Especialmente útiles en SSDD porque permiten concurrencia adicional

* **Consenso vs Transacción**
	* ![[Pasted image 20250109231808.png]]
	* **Consenso**: Diseñado para llegar a un acuerdo sobre un valor propuesto, incluso en presencia de fallos, siempre que haya quórum.
	- **Atomic Commit**: Garantiza que las transacciones distribuidas sean atómicas (todo o nada), pero es más sensible a los fallos, ya que depende de la participación activa de todos los nodos

- **Propiedades ACID**
	- **Atómica**
		- Una T o se ejecuta completamente o no se ejecuta
	- **Consistente**
		- Una T lleva al sistema de un estado consistente a otro también consistente
		- Normalmente responsabilidad del programador y de los clientes dejar contenidos de las bases de datos consistentes (dependientes de la aplicación, no del protocolo de transacción)
		- El término consistente tiene múltiples connotaciones dependiendo del contexto
	- **Isolation**
		- Al ejecutar una T concurrentemente con otras transacciones no hay condiciones de carrera
	- **Durabilidad**
		- Después de una T exitosa, todos sus efectos se guardan en el almacenamiento permanente

* **Control de la Concurrencia en T
	* La actualización perdida
		* ![[Pasted image 20250109234422.png]]
		* No se aumenta 1.1 dos veces sino una única vez ignorando la actualización.
	* Recuperaciones inconsistentes
		* ![[Pasted image 20250109235035.png]]

* **Equivalencia serial**
	* Se dice que un entrelazado de dos transacciones V y W es un equivalente serial, si el resultado de ejecutar V y W con ese entrelazado es el miso que ejecutarlas de forma aislada o secuencialmente.
		* **Equivalente serial** asegura que el entrelazado (mezcla) de las operaciones no afecta la consistencia de los datos.
		- Aunque las transacciones se ejecuten al mismo tiempo, el resultado es como si primero se hubiera ejecutado toda la transacción **V** y luego **W**, o viceversa.
	- Buscar la equivalencia serial aprovecha mejor los recursos.

* **Operaciones conflictivas**
	* Se dice que dos operaciones op1 y op2 son conflictivas si el resultado final de su ejecución depende del orden en el que se ejecutaron.
		* read(a); write(a) vs write(a); read(a)
	* ![[Pasted image 20250110003235.png]]

* **locks (mutex)**
	* Pueden aparecer bloqueos
		* detección
		* prevención
	* Alternativa al locking es el Control Optimista
		* El **Control Optimista** de concurrencia asume que las operaciones en conflicto son poco probables. En lugar de bloquear recursos, permite que las transacciones avancen sin restricciones. Solo al final, antes de confirmar los cambios (commit), se verifica si hubo conflictos en los objetos modificados. Si no hay conflictos, la transacción se completa; de lo contrario, se descartan los cambios. Esta técnica mejora la concurrencia cuando los conflictos son raros.

* **Two-Phase Commit (2PC)
	* El **Two-Phase Commit** (2PC), propuesto por Jim Gray en 1978, es una solución clásica al problema de _atomic commit_. Garantiza que en una transacción distribuida, todos los participantes (servidores) lleguen al mismo estado: si algún servidor falla, todos abortan y vuelven al estado anterior; si todos completan con éxito, todos comprometen los cambios. Este protocolo, comúnmente utilizado para implementar transacciones distribuidas, involucra tres actores principales: el cliente que inicia la transacción, los servidores que ejecutan las operaciones y un coordinador que gestiona el proceso para asegurar la consistencia global.
		* ![[Pasted image 20250110003805.png]]
	* Fases
		* Fase inicial: el cliente envía mensaje de comienzo de la transacción a los servidores
		- Fase operacional: el cliente interactúa con los servidores y realiza las operaciones correspondientes
		- Fase 1a: el cliente le indica al coordinador el fin de la transacción
		- Fase 1b: el coordinador envía el mensaje (prepare) a todos los servidores para que indiquen si voto: commit o abort
		- Fase 1c: los servidores envían el voto al coordinador
		- Fase 2a: el coordinador recoge todos los votos: si alguno es abort, el resultado final es abort. Si todos son commit, el resultado es commit.
		- Fase 2c: cada servidor espera el mensaje de confirmación: commit o abort.
	- Máquinas de estado
		- ![[Pasted image 20250110004126.png]]
		- ![[Pasted image 20250110004140.png]]
	- ![[Pasted image 20250110004536.png]]

### Conclusiones
![[Pasted image 20250110004642.png]]
