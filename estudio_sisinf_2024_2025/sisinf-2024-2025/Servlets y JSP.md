![[Pasted image 20241231033314.png]]
### Servlet
* Normalmente utilizan protocolo HTTP, pero pueden usar cualquier protocolo cliente-servidor
* Un Servlet es un objeto que recibe una solicitud, procesa datos y genera una respuesta basada en esa solicitud. Puede generar HTML (páginas web dinámicas), pero también es capaz de manejar otras opciones.

![[Pasted image 20241231033733.png]]
* Cada Servlet puede estar asociado a una o mas URL, el contenedor de la aplicación asociara las URL a los Servlets
	* ![[Pasted image 20241231034129.png]]
![[Pasted image 20241231034212.png]]
* ¿doGet o doPost?
	* GET
		* reading
		* Datos visibles en la URL
	* POST
		* writing/updating
		* Datos no visibles en la URL
			* Escondidos en HTTP request header
* Mucha explicación de código, métodos..., ¿Entrará eso en el examen?
### JSP
* Tipo especial de servlet
	* Datos estáticos
	* elementos JSP (escritos en java)
* **JSTL**
	* JSTL (JavaServer Pages Standard Tag Library) es una biblioteca de etiquetas estándar para JSP que simplifica tareas comunes en aplicaciones web Java, como iteraciones, condicionales, manejo de colecciones, internacionalización, manipulación de XML y uso de expresiones con EL, reduciendo el código Java en las páginas y mejorando su legibilidad.
* Mucha explicación de código, métodos..., ¿Entrará eso en el examen?
### Sesión
* Session id in:
	* cookies
	* Each URL
	* Hidden fields in the forms
	* bases on parameters of the HTTP request (IP,time...)
### Patrones de diseño para arquitecturas web (y móviles)
* MVC - Model View Controller
	* Spring MVC, PHP...
	* View
		* Capa de visualización
	* Model
		* Data Access Object/Value Object + BD
	* Controller
		* Controla el tráfico entre el cliente (navegador) y el modelo, también entre el modelo y la vista
	* (Spring)![[Pasted image 20241231041126.png]]
	* (Jakarta)![[Pasted image 20241231041155.png]]
* MVP - Model View Presenter
	* Android, iOS, JSF...
* MVVM - Model View ViewModel
	* Android (por ejemplo Swift), Angular, React
* Muchas cosas con deployment y código ¿Entra al examen o era para el trabajo?