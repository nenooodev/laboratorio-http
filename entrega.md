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
