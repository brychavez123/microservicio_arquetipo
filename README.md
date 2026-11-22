# microservicio-arquetipo

Arquetipo Maven que sirve de **plantilla para todos los microservicios** del Sistema de Foros en Línea.
Desarrollo Full Stack III (DSY2205) — Experiencia 2.

Se construyó a partir de la estructura común de `ms-usuarios` y `ms-foro`, y con él se generó `ms-moderacion`.
Así los 3 microservicios comparten la misma arquitectura, configuración y buenas prácticas.

## Qué trae cada proyecto generado
| Elemento | Detalle |
|---|---|
| `pom.xml` | Spring Boot 3.5 · Java 21 · Web · JPA · Validation · Security · Actuator · Oracle (`ojdbc11` + `oraclepki`) · Lombok |
| Arquitectura por capas | `controller/`, `service/`, `repository/`, `model/`, `dto/`, `exception/`, `security/` |
| `{Nombre}Application` | Clase principal con el nombre que elijas |
| `InfoController` | `GET /api/info` público para comprobar el despliegue |
| `GlobalExceptionHandler` | Errores JSON uniformes (400, 401, 403, 404, 405, 409, 500) |
| Seguridad | HTTP Basic + BCrypt contra la tabla `USUARIO` compartida, sin estado, CORS configurable |
| `application.properties` | Oracle Cloud con Wallet, credenciales por `db.properties` o variables de entorno |
| `Dockerfile` | Multi-etapa (Maven → JRE Alpine), usuario sin privilegios y healthcheck |
| `.github/workflows/deploy-aws.yml` + `aws/` | En cada push a `main`: tests, imagen en Amazon ECR y despliegue en EC2 por Systems Manager (Wallet desde S3, credenciales desde Secrets Manager) |
| `.gitignore` / `.dockerignore` | El Wallet y `db.properties` nunca se suben |
| `mvnw` | Maven Wrapper |

## Parámetros
| Propiedad | Ejemplo | Uso |
|---|---|---|
| `groupId` | `com.duoc` | |
| `artifactId` | `ms-moderacion` | Nombre del proyecto y de la app |
| `package` | `com.duoc.moderacion` | Paquete base |
| `nombreClase` | `Moderacion` | Genera `ModeracionApplication` |
| `puerto` | `8083` | `server.port`, `EXPOSE` y healthcheck |
| `descripcion` | `Microservicio de moderación` | `pom.xml`, README y `/api/info` |

## Uso
```bash
# 1. Instalar el arquetipo en el repositorio local de Maven
cd microservicio_arquetipo
mvn clean install

# 2. Generar un microservicio nuevo
mvn archetype:generate -B \
  -DarchetypeGroupId=com.duoc \
  -DarchetypeArtifactId=microservicio-arquetipo \
  -DarchetypeVersion=1.0.0 \
  -DgroupId=com.duoc \
  -DartifactId=ms-moderacion \
  -Dpackage=com.duoc.moderacion \
  -DnombreClase=Moderacion \
  -Dpuerto=8083 \
  "-Ddescripcion=Microservicio de moderacion del foro"
```
En PowerShell, pon cada `-D...` entre comillas: `"-DartifactId=ms-moderacion"`.
