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
| `/` | | | | |
| `/api/hello` | | | | |
| `/health` | | | | |

## 2. Trazas y errores

Incluye solo fragmentos necesarios y sustituye secretos por `<REDACTED>`.

```http
<traza sanitizada>
```

Respuestas:

1. Método, destino, campos y contenido:
2. Estados observados:
3. Resultado de OPTIONS:
4. Información que no debe aparecer en errores:

## 3. Frontera cliente-servidor

1. Trabajo del navegador: Al abrir http://localhost:8080/ el navegador envía GET / y recibe el HTML con estado 200 y Content-Type text/html;charset=UTF-8. En la pestaña Red aparece esa petición del documento; el navegador parsea el HTML, construye el árbol DOM y pinta la página. Nada de eso ejecuta Java: el navegador solo interpreta la representación recibida.
2. Trabajo del servidor: El proceso Java (Spring Boot con Tomcat embebido) aceptó la conexión, DispatcherServlet recibió la petición, HelloController.home() construyó la cadena HTML y la devolvió con el estado y las cabeceras correspondientes. Todo el código de aplicación se ejecutó allí, en el servidor, antes de que el navegador viera un solo byte de HTML.
3. Modificación local del HTML: Las herramientas del navegador editan solo la copia en memoria del cliente (el DOM local). El HTML que sirve home() vive en el código Java del servidor y no se toca; en la siguiente petición vuelve a llegarse la misma cadena original. Es como subrayar un libro prestado: cambia tu ejemplar, no el del autor.
4. Validación duplicada:
5. Tres ventajas y dos costes:

## 4. Recorrido y mecanismos

```text
cliente -> ... -> respuesta
```

Comparación con CGI y FastCGI:

## 5. Spring Boot y Laravel

| Criterio | Spring Boot | Laravel |
|---|---|---|
| Lenguaje y runtime | | |
| Ejecución | | |
| Tipado y pruebas | | |
| Despliegue | | |
| Papel didáctico | | |

Conclusión contextual:

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
