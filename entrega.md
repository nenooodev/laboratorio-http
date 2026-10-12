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

1. Trabajo del navegador:
2. Trabajo del servidor:
3. Modificación local del HTML:
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
