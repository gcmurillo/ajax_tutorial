# Tutorial de AJAX
AJAX, según lo define [MDN](https://developer.mozilla.org/es/docs/Web/Guide/AJAX),  no es una tecnología por sí misma, es un término que describe un nuevo modo de utilizar conjuntamente varias tecnologías existentes. Esto incluye: HTML o XHTML, CSS, JavaScript, DOM, XML, XSLT, y lo más importante, el objeto XMLHttpRequest.

Esta tecnología es importante el desarrollo de aplicaciones web interactivas dado que permite actualizarse continuament sin tener que volver a cargar la página completa, es decir nos permite ofrecer una mejor experiencia de usuario.

## Requisitos para el tutorial
* Conocimientos básicos de desarrollo Web con HTML y Javascript.

## Un poco más sobre AJAX
El término AJAX (*Asynchronous JavaScript + XML*), se presentó por primera vez en el artículo
[*AJAX: A New Approach to Web Aplications*](https://pdfs.semanticscholar.org/c440/ae765ff19ddd3deda24a92ac39cef9570f1e.pdf?_ga=2.96316956.1880424890.1593881953-241537876.1593881953) en 2005 por Jame Garret, donde lo definen como la unión de varias tecnologías de una manera *nueva y sorprendente*

Dichas tecnologías son:
* XHTML y CSS, para crear una presentación basada en estándares.
* DOM, para la interacción y manipulación dinámica de la presentación.
* XML, XSLT y JSON, para el intercambio y la manipulación de información.
* XMLHttpRequest, para el intercambio asíncrono de información.
* JavaScript, para unir todas las demás tecnologías.

En dicho artículo también presenta la diferencia entre el modelo tradicional y el basado en Ajax.

![models](https://github.com/gcmurillo/ajax_tutorial/blob/master/capturas/f0102.gif)

En el modelo tradicional, aunque las aplicaciones funcionan correctamente, no crean una buena experiencia de usuario, debido a que si este realiza varias peticiones al servidor, debe de esperar a que se recargue la página según la cantidad de cambios solicitados. Ajax permite mejorar considerablemente la experiencia evitando recargas constantes de la página, ya que el intercambio de información se produce en segundo plano.

## Un ejemplo sencillo - *Hola al mundo de Ajax*

En este ejemplo sencillo, se descarga un archivo del servidor y se muestra el contenido sin necesidad de recargar la página.

El ejemplo se compone de cuatro grandes bloques: instanciar el objeto `XMLHttpRequest`, preparar la función de respuesta, realizar petición al servidor y ejecutar la función de respuesta.

El objeto `XMLHttpRequest` es clave para realizar las comunicaciones con el servidor en segundo plano, sin necesidad de recargar las paginas.

``` Javascript 
// Obtener la instancia del objeto XMLHttpRequest
if (window.XMLHttpRequest) {  // Navegadores que siguen los estandares
    peticion_http = new XMLHttpRequest();
}
else if (window.ActiveXObject) {  // Navegadores obsoletos
    peticion_http = new ActiveXObject("Microsoft.XMLHTTP");
}
```

Los navegadores que sigen los estandares (Firefox, Safari, IE > 7) implementan el objeto `XMLHttpRequest` de forma nativa por medio del objeto `window`. Los navegadores obsoletos (IE < 6) implementan el objeto `XMLHttpRequest` por medio del objeto tipo `ActiveX`

``` Javascript
// Preparar la funcion de respuesta
peticion_http.onreadystatechange = muestraContenido;
```

La línea anterior, especifica que función se debe ejecturar cuando la aplicación reciba la respuesta del servidor.

Luego se realiza la peticion HTTP al servidor, en este caso obtendremos el contenido de un archivo txt.

``` Javascript
// Realizar peticion HTTP
peticion_http.open('GET', 'https://raw.githubusercontent.com/gcmurillo/ajax_tutorial/mastcode/holamundo.txt', true);
peticion_http.send(null);
```

La peticion realizada es de tipo `GET` que no envia ningun parametro al servidor. La peticion se crea mediante el metido `open()`, en el que incluye el tipo de peticion (`GET`), la URL solicitada (*'https://raw.githubusercontent.com/gcmurillo/ajax_tutorial/mastcode/holamundo.txt'*) y un tercer parametro que vale `true`. Una vez creada la peticion HTTP, se envia al servidor mediante el metodo `send()`.


``` Javascript
function muestraContenido() {
    if (peticion_http.readyState == 4) {
        if (peticion_http.status == 200) {
            alert(peticion_http.responseText);
        }
    }
}
```
La funcion `muestraContenido()` comprueba que se ha recibido la respuesta del servidor (`readyState`), si esta ha sido recibida, comprueba que sea correcta y valida (`status == 200`). Si todo es correcto, se muestra el contenido en un *alert* (`responseText`).

Puede ver el ejemplo completo en el [repo](https://github.com/gcmurillo/ajax_tutorial/blob/master/code/index.html) 


## Referencias

* [MDN](https://developer.mozilla.org/es/docs/Web/Guide/AJAX)
* [Uniwebsidad: Introduccion a AJAX](https://uniwebsidad.com/libros/ajax)