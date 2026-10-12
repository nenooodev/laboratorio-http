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
cliente -> Tomcat embebido -> DispatcherServlet -> HelloController -> conversor JSON -> respuesta
```

Comparación con CGI y FastCGI: En Hello Server el proceso Java con Tomcat embebido permanece activo desde el arranque; cada petición entra en ese mismo proceso y la ejecuta DispatcherServlet con el resto de la cadena. En CGI, en cambio, el servidor web lanzaba un proceso nuevo por petición, que arrancaba el intérprete, ejecutaba el script y terminaba: el código de aplicación no residía en un proceso estable. PHP-FPM/FastCGI mejora CGI usando un pool de procesos PHP preexistentes y un protocolo persistente entre el web server y los workers, pero sigue separando el runtime de PHP del servidor web. El componente que ejecuta el código de aplicación es, en cada caso, distinto: en Spring Boot lo hace la propia JVM del proceso embebido; en FastCGI, los workers de FPM.

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
