# Entrega del laboratorio HTTP

## Identificación

- Alumno/a:
- Fecha: 12/10/26
- Java: 25
- Maven Wrapper: 3.9
- Herramienta HTTP utilizada: curl

## 1. Representaciones

| Endpoint | Estado | Content-Type | Método Java | Explicación |
|---|---:|---|---|---|
| `/` | 200 | `text/html;charset=UTF-8` | `home()` | Cadena HTML construida en el servidor; el `produces` del mapeo fija `text/html` |
| `/api/hello` | 200 | `application/json` | `hello()` | Mapa Java serializado a JSON por el conversor de mensajes (Jackson) |
| `/health` | 200 | `application/json` | `health()` | Mapa con el estado del ejemplo, serializado a JSON por el mismo conversor |

¿Por qué `/` devuelve HTML y `/api/hello` JSON si están en el mismo controlador?

El reparto no lo decide el controlador en su conjunto, sino el mapeo de cada método. `home()` declara produces = text/html y devuelve una cadena que ya es HTML, así que Spring la envía como tal. `hello()` no declara produces y devuelve un mapa Java: el tipo de retorno activa el conversor de mensajes (Jackson), que serializa el mapa a JSON y lo envía con application/json. El mismo camino sigue `health()`. En resumen: método mapeado, tipo de retorno y declaraciones de produces determinan la representación de cada respuesta.

## 2. Trazas y errores

Incluye solo fragmentos necesarios y sustituye secretos por `<REDACTED>`.

```http
GET /api/hello HTTP/1.1
Host: localhost:8080
User-Agent: curl/8.22.0
Accept: */*

HTTP/1.1 200
Content-Type: application/json
Content-Length: 36
Date: Mon, 12 Oct 2026 10:54:22 GMT

{"message":"Hola desde el servidor"}
```

Respuestas:

1. Método, destino, campos y contenido: El método es GET y el destino /api/hello sobre el Host localhost:8080. Los campos (cabeceras) son metadatos del intercambio: de petición (Host, User-Agent, Accept) y de respuesta (Content-Type, Content-Length, Date). El contenido es el cuerpo: el JSON {"message":"Hola desde el servidor"}, cuya representación describe Content-Type: application/json.
2. Estados observados: 200 en GET /api/hello  (éxito y cuerpo devuelto); 200 también en OPTIONS sobre /api/hello, sin  404 al pedir /no-existe, recurso inexistente. Cada estado resume el resultado de un solo vistazo: 2xx correcto, 4xx error de cliente y qué concreto falló.
3. Sí. La respuesta observada a OPTIONS /api/hello fue 200 con Allow: GET,HEAD,OPTIONS y Content-Length: 0.
4 Rutas internas y estructura de directorios del servidor, versiones exactas de software, trazas de pila del backend, credenciales, tokens o cookies, y datos de otras peticiones o usuarios.

## 3. Frontera cliente-servidor

1. Trabajo del navegador: Al abrir http://localhost:8080/ el navegador envía GET / y recibe el HTML con estado 200 y Content-Type text/html;charset=UTF-8. En la pestaña Red aparece esa petición del documento; el navegador parsea el HTML, construye el árbol DOM y pinta la página. Nada de eso ejecuta Java: el navegador solo interpreta la representación recibida.
2. Trabajo del servidor: El proceso Java (Spring Boot con Tomcat embebido) aceptó la conexión, DispatcherServlet recibió la petición, HelloController.home() construyó la cadena HTML y la devolvió con el estado y las cabeceras correspondientes. Todo el código de aplicación se ejecutó allí, en el servidor, antes de que el navegador viera un solo byte de HTML.
3. Modificación local del HTML: Las herramientas del navegador editan solo la copia en memoria del cliente (el DOM local). El HTML que sirve home() vive en el código Java del servidor y no se toca; en la siguiente petición vuelve a llegar la misma cadena original.
   
5. Validación duplicada: El navegador podría validar en cliente un campo de un formulario (por ejemplo, que un email tenga formato válido) para dar respuesta inmediata sin viaje al servidor; pero esa validación es solo experiencia, no seguridad, porque cualquiera puede saltársela con curl. Cualquier regla que importe para la integridad de los datos debe repetirse en el servidor, que es quien decide de verdad qué es válido.
6. Tres ventajas y dos costes: Ventajas: el contenido puede personalizarse por usuario o contexto en el momento de la petición; los datos se generan al consultar la fuente de verdad y la lógica queda centralizada en el servidor, donde se audita y se cambia una sola vez.
Costes: cada petición consume CPU y memoria en el servidor que servir  un archivo estático , y la complejidad de desarrollo y despliegue crece, porque hay código que mantener, probar y operar.

## 4. Recorrido y mecanismos

```text
cliente -> Tomcat embebido -> DispatcherServlet -> HelloController -> conversor JSON -> respuesta
```

Comparación con CGI y FastCGI: En Hello Server el proceso Java con Tomcat embebido permanece activo desde el arranque; cada petición entra en ese mismo proceso y la ejecuta DispatcherServlet con el resto de la cadena. En CGI, en cambio, el servidor web lanzaba un proceso nuevo por petición, que arrancaba el intérprete, ejecutaba el script y terminaba: el código de aplicación no residía en un proceso estable. PHP-FPM/FastCGI mejora CGI usando un pool de procesos PHP preexistentes y un protocolo persistente entre el web server y los workers, pero sigue separando el runtime de PHP del servidor web. El componente que ejecuta el código de aplicación es, en cada caso, distinto: en Spring Boot lo hace la propia JVM del proceso embebido; en FastCGI, los workers de FPM.

Server o X-Powered-By son cabeceras que la propia aplicación o su contenedor pueden escribir, omitir o falsear (se pueden ocultar por seguridad o añadir por capas intermedias como CDNs y proxies). No prueban qué proceso ejecuta el código ni cómo está montada la arquitectura; solo declaran lo que quien genera la respuesta dice de sí mismo. Para afirmar mecanismos hace falta observar el comportamiento (como las trazas de este laboratorio), no fiarse de un banner.

## 5. Spring Boot y Laravel

| Criterio | Spring Boot | Laravel |
|---|---|---|
| Lenguaje y runtime | Java sobre la JVM; en este laboratorio, Java 25 | PHP (runtime PHP-FPM o similar) |
| Ejecución | Proceso único persistente con Tomcat embebido; DispatcherServlet enruta al controlador | Servidor web + FPM; las peticiones se despachan al framework vía FastCGI |
| Tipado y pruebas | Tipado estático fuerte; pruebas con JUnit y Spring Test (como la suite de Hello Server) | Tipado dinámico; pruebas con PHPUnit |
| Despliegue | Empaquetado ejecutable (jar) autocontenido con el servidor dentro | Árbol de archivos servido por Apache/Nginx + PHP, habitualmente con despliegues compartidos |
| Papel didáctico | Permite estudiar el ciclo de una petición HTTP, desde su recepción por el servidor embebido hasta su procesamiento por el controlador y la generación de la respuesta | Permite contrastar el modelo de ejecución habitual de PHP, identificando la interacción entre el servidor web, PHP-FPM y el framework durante el procesamiento de las peticiones |


Conclusión contextual: Elegiría Spring Boot cuando el proyecto encaja con la JVM, se quiere un proceso embebido autocontenido y tipado estático con un ecosistema de pruebas robusto, como este Hello Server que se arranca con un solo comando. Elegiría Laravel cuando el equipo trabaja con PHP, se prioriza la velocidad de desarrollo de CRUDs y se acepta el modelo cliente-servidor con FPM (que ya es habitual en hosting compartido, por ejemplo).

## 6. QUERY

1. Problema que resuelve:
2. Seguridad e idempotencia:
3. Contenido y `Content-Type`:
4. Verificaciones necesarias para adoptarlo:

## Comprobación final

- [ ] No hay cookies, tokens ni credenciales reales.
- [ ] No hay rutas o datos personales innecesarios.
- [ ] Las trazas son texto y están sanitizadas.
- [ ] Puedo reproducir y explicar todo el contenido.
- [ ] No he utilizado IA generativa.
