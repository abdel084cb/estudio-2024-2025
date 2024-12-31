### HTML

* tag based
	* `<tag>content</tag>`
	* `<tag atributte = "value">...</tag>`
		* con comillas simples también
	* * <!-- comentario -->
	* `<html lang = "es">`
	* etc
	* ![[Pasted image 20241231012554.png]]
* ![[Pasted image 20241231012702.png]]
* La declaración `<!DOCTYPE html>` se utiliza para definir el tipo de documento en una página web HTML. Especifica que el documento sigue la versión más reciente de HTML (HTML5 en este caso).

* Tag `<form>` en HTML
   * **Uso**
      * Permite crear formularios para enviar datos al servidor.
      * Es esencial para interacciones como:
         * Registro de usuarios.
         * Inicio de sesión.
         * Realizar búsquedas.
   * **Atributos comunes**
      * **`action`**
         * Especifica la URL a la que se enviarán los datos del formulario.
      * **`method`**
         * Define el método HTTP utilizado para enviar los datos (`GET` o `POST`).
      * **`enctype`**
         * Determina el tipo de codificación para los datos (especialmente útil para enviar archivos).
   * **Ejemplo**
      ```html
      <form action="/submit" method="POST">
         <input type="text" name="username" placeholder="Usuario">
         <button type="submit">Enviar</button>
      </form>
      ```
      * Este formulario envía un nombre de usuario al servidor.

* Diferencias entre GET y POST
   * **GET**
      * **Uso**
         * Se utiliza para solicitar datos del servidor.
      * **Parámetros**
         * Los datos se envían en la URL como parte de la consulta (después de `?`).
         * Ejemplo: `https://example.com?user=juan&age=30`
      * **Visibilidad**
         * Los datos son visibles en la barra de direcciones.
      * **Seguridad**
         * Menos seguro, ya que los datos son visibles y pueden almacenarse en el historial o caché.
         * No recomendado para enviar información sensible.
      * **Tamaño**
         * Está limitado por la longitud máxima de la URL.
      * **Caché**
         * Las solicitudes GET pueden ser almacenadas en caché por el navegador.
   * **POST**
      * **Uso**
         * Se utiliza para enviar datos al servidor (formularios, archivos, etc.).
      * **Parámetros**
         * Los datos se envían en el cuerpo de la solicitud, no en la URL.
         * Ejemplo: Envío de datos JSON o formularios en el cuerpo HTTP.
      * **Visibilidad**
         * Los datos no son visibles en la barra de direcciones.
      * **Seguridad**
         * Más seguro para enviar información confidencial, como contraseñas.
      * **Tamaño**
         * Permite enviar grandes cantidades de datos, ya que no está limitado por la URL.
      * **Caché**
         * Por defecto, las solicitudes POST no se almacenan en caché.

### CSS
* Tags can have atributes
* No puedes usar el mismo valor de atributo id en más de un elemento dentro de un mismo documento HTML. El atributo id debe ser único, ya que se utiliza para identificar de manera exclusiva un elemento en el DOM (Document Object Model).


* Mucha explicación de código ¿Entrará eso al examen?