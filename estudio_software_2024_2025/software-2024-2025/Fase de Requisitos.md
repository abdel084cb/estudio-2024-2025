**La fase de requisitos es la descripción del problema. ¿Cuál es el problema?

* Hay requisitos del sistema y del usuario. La asignatura se centra en requisitos del sistema.
	* Funcionales: Independientes de la implementación. "que"
		* "El sistema debe permitir a los usuarios registrarse proporcionando su nombre, correo electrónico y contraseña."
		* "El sistema debe permitir a los usuarios buscar productos por nombre, categoría o rango de precio."
		* "El sistema debe enviar una notificación por correo electrónico cuando un usuario complete una compra."
	* No funcionales: Dependientes de la implementación. "como" (seguridad, accesibilidad, como de bien de funcionar el sistema en ciertos casos (limites)...)
		* "El sistema debe responder a las consultas de búsqueda en menos de 2 segundos."
		* "El sistema debe estar disponible el 99.9% del tiempo, excepto durante el mantenimiento programado."
		* "El sistema debe cifrar toda la información sensible utilizando el estándar AES-256."
* Restricciones: limitaciones o condiciones externas que restringen cómo se puede diseñar, desarrollar, implementar o usar un sistema.
	* "El sistema debe ser desarrollado utilizando el lenguaje de programación Python y el framework Django."
	* "El sistema debe funcionar en Android"
	* "El costo total del desarrollo del sistema no debe exceder los $50,000 USD."
	* "El sistema debe cumplir con el Reglamento General de Protección de Datos (GDPR) para manejar la información personal de los usuarios en la Unión Europea."
De momento no me extiendo mas en Fase de Requisitos. Hay ejercicios por si te da tiempo a hacerlos.
### Tabla de requisitos
Codificación MoSCoW para indicar la prioridad:
* M MUST: Requisitos totalmente imprescindibles que tienen que estar incluidos ya que si no se llevan a cabo el proyecto no puede salir adelante
* S SHOULD: Requisitos que deberían de llevarse acabo si es posible, es decir, requisitos importantes y de gran valor para el producto que se está construyendo
* C COULD: Requisitos que podrían incluirse si no afecta a nada más, es decir, requisitos que sería bueno tener y podrían incluirse porque no cuesta demasiado implementarlos
* W WON'T: Requisitos que no se implementarán en la iteración actual, pero que serán tenidos en cuenta en el futuro

![[Pasted image 20241224022747.png]]

Ejercicio de captura de requisitos de la aplicación de “Gestión del aula informática”
![[Pasted image 20241224022927.png]]

### Arboles/Tablas de decisión
Si un requisito describe una toma de decisión, se puede especificar mediante un árbol o una tabla de decisión para evitar malas interpretaciones

En la raíz del árbol comienza la secuencia de decisión, la rama a seguir depende de las condiciones. La parte final es la acción.

![[Pasted image 20241224023353.png]]

![[Pasted image 20241224023445.png]]

![[Pasted image 20241224023540.png]]

![[Pasted image 20241224023627.png]]

