# -PR-CTICA-WEB

# 🌐 Servicios Web: REST y SOAP

Este repositorio contiene material de estudio, ejemplos y buenas prácticas para la **creación y consumo de servicios web** bajo los estilos arquitectónicos **REST** y **SOAP**, con enfoque en interoperabilidad, seguridad, diseño y operaciones.

---

## 📚 Contenido

- [¿Qué es un servicio web?](#qué-es-un-servicio-web)
- [Comparativa: REST vs SOAP](#comparativa-rest-vs-soap)
- [Principios de REST](#principios-de-rest)
- [Características clave de SOAP](#características-clave-de-soap)
- [Seguridad](#seguridad)
- [Consumo de servicios](#consumo-de-servicios)
- [Pruebas y observabilidad](#pruebas-y-observabilidad)
- [Herramientas recomendadas](#herramientas-recomendadas)
- [Referencias](#referencias)

---

## ¿Qué es un servicio web?

Un **servicio web** es un software que expone funcionalidades a través de una interfaz accesible por red (generalmente HTTP/HTTPS), permitiendo la **interoperabilidad** entre distintas plataformas y lenguajes mediante formatos estándar como **JSON** o **XML**.

---

## Comparativa: REST vs SOAP

| Característica        | REST                                      | SOAP                                      |
|----------------------|-------------------------------------------|-------------------------------------------|
| **Estilo**           | Arquitectónico (basado en recursos)       | Protocolo (mensajería XML)                |
| **Formato**          | JSON, XML, otros                          | XML exclusivamente                        |
| **Contrato**         | Opcional (OpenAPI)                        | Obligatorio (WSDL)                        |
| **Simplicidad**      | Alta (nativo web)                         | Baja (más verboso)                        |
| **Seguridad**        | TLS + OAuth/JWT                           | WS-Security (a nivel de mensaje)          |
| **Casos de uso**     | APIs públicas, móviles, microservicios    | Banca, gobierno, sistemas legacy/ERP       |

---

## Principios de REST

REST (*Representational State Transfer*) se basa en las siguientes restricciones:

- **Cliente–Servidor**: separación de preocupaciones.
- **Sin estado (Stateless)**: cada petición contiene todo el contexto.
- **Caché**: respuestas marcadas como cacheables.
- **Interfaz uniforme**: uso consistente de URIs, métodos HTTP y representaciones.
- **Sistema en capas**: intermediarios como proxies o gateways.
- **Código bajo demanda** (opcional).

### Buenas prácticas en REST

- **URIs**: sustantivos en plural (`/productos`, `/usuarios/{id}`).
- **Métodos HTTP**: semántica correcta (GET, POST, PUT, PATCH, DELETE).
- **Códigos de estado**: 2xx, 4xx, 5xx según contexto.
- **Paginación**: `?page=1&size=20` o cursores.
- **Filtrado/orden**: `?estado=activo&sort=-fecha`.
- **Proyección**: `?fields=id,nombre`.
- **HATEOAS**: incluir enlaces navegables en las respuestas.

---

## Características clave de SOAP

- **Mensaje XML** con estructura: `Envelope`, `Header`, `Body`.
- **WSDL**: contrato formal que describe operaciones, tipos y endpoints.
- **Estilos**: `document/literal` (recomendado) vs `RPC`.
- **Extensibilidad**: mediante estándares **WS-\***:
  - WS-Security
  - WS-Addressing
  - WS-ReliableMessaging
  - WS-Policy

Ideal para entornos que requieren **transacciones distribuidas**, **seguridad a nivel de mensaje** o **garantías de entrega**.

---

## Seguridad

### REST
- **HTTPS obligatorio** (con HSTS).
- **Autenticación**: API Keys, JWT, OAuth 2.0, OpenID Connect.
- **Autorización**: scopes y roles (principio de mínimo privilegio).
- **CORS**, **rate limiting**, **validación de entrada** (JSON Schema, OWASP API Top 10).

### SOAP
- **WS-Security**: firmas digitales, cifrado, tokens (UsernameToken, SAML, X.509).
- **Prevención de replay**: timestamps y nonces.
- **Validación XML**: contra XSD.

---

## Consumo de servicios

### REST
- **Clientes**: `fetch`, `axios`, `HttpClient`, `requests`.
- **Resiliencia**: reintentos con *exponential backoff*, *circuit breakers*.
- **Caché condicional**: `ETag`, `If-None-Match`, `304 Not Modified`.
- **Generación de clientes**: desde OpenAPI (TypeScript, Python, Java, etc.).

### SOAP
- **Stubs generados** desde WSDL (`wsimport`, `svcutil`, Zeep).
- **Manejo de XML complejo** y validación contra esquemas.
- **Configuración de WS-Security** en cliente.

---

## Pruebas y observabilidad

- **Pruebas unitarias**: lógica de negocio.
- **Pruebas de integración**: endpoints reales (en contenedores).
- **Pruebas de contrato**: Postman/Newman, Pact.
- **Observabilidad**:
  - Logs estructurados (JSON).
  - Métricas: latencia, tasa de errores.
  - Trazas distribuidas: OpenTelemetry → Jaeger/Zipkin.

---

## Herramientas recomendadas

| Propósito             | Herramienta(s)                              |
|----------------------|---------------------------------------------|
| Documentación REST   | Swagger UI, Redoc, OpenAPI 3.1              |
| Pruebas REST         | Postman, Newman                             |
| Pruebas SOAP         | SoapUI, ReadyAPI                            |
| Generación de código | OpenAPI Generator, `wsimport`, `svcutil`    |
| Observabilidad       | OpenTelemetry, Prometheus, Grafana          |
| Despliegue           | Docker, Kubernetes, API Gateway             |

---

## Referencias

- Fielding, R. (2000). *Architectural Styles and the Design of Network-based Software Architectures*.
- IETF RFC 9110–9112 (HTTP/1.1, Semántica y Caché).
- W3C SOAP 1.2 y WSDL 1.1/2.0.
- OASIS WS-Security 1.1.1.
- OpenAPI Specification 3.1.
- OWASP API Security Top 10 (2023).
- OpenTelemetry Specification.

---

> ✨ **Consejo**: Usa este material como base para diseñar APIs robustas, seguras y mantenibles. ¡La elección entre REST y SOAP debe guiarse por los requisitos del dominio, no por modas!
