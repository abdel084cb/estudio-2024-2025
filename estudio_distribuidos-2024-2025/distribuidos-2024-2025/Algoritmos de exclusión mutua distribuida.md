* **Algoritmos centralizados**
	* Ventajas: simplicidad.
	* Inconvenientes: escalabilidad, mucha responsabilidad en un punto.
* **Algoritmos descentralizados
	* Todos los procesos con la misma responsabilidad.
	* Ningún proceso conoce el estado global del SD.
	* Los procesos toman decisiones basándose en las ordenaciones de los eventos y en la información local.
	* Se necesita algún tipo de comunicación, IPC.
		* directa, indirecta, asíncrona, síncrona, etc,

### **Algoritmo Mútex Distribuido en Anillo**

...

### **Algoritmo Mútex Distribuido de Lamport**

* Requisitos:
	* Se asume que no hay errores de red.

![[Pasted image 20241228222806.png]]
![[Pasted image 20241228222945.png]]
### **Algoritmo de Ricart-Agrawala**

* Requisitos y Características:
	* Se asume que no hay errores de red.
	* Orden de recepción distinto de orden de envío.

![[Pasted image 20241228225346.png]]
![[Pasted image 20241228225414.png]]
![[Pasted image 20241228225452.png]]
![[Pasted image 20241228230129.png]]
![[Pasted image 20241228230307.png]]

![[Pasted image 20241228230216.png]]
![[Pasted image 20241228230225.png]]
![[Pasted image 20241228230236.png]]
### **Generalizaciones del Mútex distribuido**
#### Algoritmo de Raymond
* SD con N procesos
* K procesos en SC, K < N
* Un proceso puede entrar en SC cuando reciba N-K ACKs
* Se debe tener en cuenta el número de ACKs para no contarlos en sucesivas peticiones
	* El resto de ACKs pueden llegar en la SC
	* esperando otra vez para acceder a la SC

#### Lectores y Escritores Distribuidos
* 2 operaciones que deben realizarse en exclusión mutua. 
	* read()
	* write()
* Se permiten varios read simultáneos
* No puede haber varios write simultáneos
![[Pasted image 20241228235046.png]]
![[Pasted image 20241228235258.png]]
![[Pasted image 20241228235310.png]]
