* **Definición:** Permiten asociar fechas a eventos de manera que la comparación entre fechas permite determinar si los eventos están causalmente relacionados o no.
	* También generan una relación de orden parcial.

![[Pasted image 20241228203920.png]]
![[Pasted image 20241228204000.png]]
![[Pasted image 20241228204015.png]]
![[Pasted image 20241228204359.png]]
![[Pasted image 20241228204537.png]]

* **Características:**
	* Proporcionan orden parcial. 
		* Pero si date(e1) < date (e2) entonces e1 => e2.
	* Aunque dos procesos no interactúen directamente, sus relojes pueden sincronizarse a través de terceros.

* **Se intercambia un vector, al ser mas información que un mero entero puede dar problemas**
	* Técnica de Singhal Kshemkalyani
		* Cuando Pi envía msg a Pj, no le envía todo el vector.
		* Solo envía los últimos cambios desde el último msg de Pi a Pj.
		