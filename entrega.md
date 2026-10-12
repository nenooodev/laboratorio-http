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
| Lenguaje y runtime | | |
| Ejecución | | |
| Tipado y pruebas | | |
| Despliegue | | |
| Papel didáctico | | |

Conclusión contextual:

## 6. QUERY

1. Problema que resuelve: QUERY cubre el hueco entre GET y POST. GET lleva la consulta en la URI, que tiene límites de tamaño, se codifica mal para datos complejos y se registra más fácil en logs y marcapáginas. POST sí lleva la consulta en el cuerpo, pero no declara que la operación sea segura e idempotente. QUERY permite enviar la consulta en el cuerpo como POST, pero el método está definido explícitamente como seguro e idempotente (RFC 10008, sección 5.1).
2. Seguridad e idempotencia: Es seguro porque el cliente no pide ni espera un cambio en el estado del recurso objetivo: solo pide que se procese la consulta. Es idempotente porque repetir la misma QUERY produce el mismo efecto que ejecutarla una vez, de modo que puede reintentarse tras un fallo de conexión sin riesgo de mutaciones parciales. El registro de IANA del RFC 10008 lo declara así: Safe = yes, Idempotent = yes.
3. Contenido y `Content-Type`:
4. Verificaciones necesarias para adoptarlo:

## Comprobación final

- [ ] No hay cookies, tokens ni credenciales reales.
- [ ] No hay rutas o datos personales innecesarios.
- [ ] Las trazas son texto y están sanitizadas.
- [ ] Puedo reproducir y explicar todo el contenido.
- [ ] No he utilizado IA generativa.
