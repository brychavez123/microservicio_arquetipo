#set( $h = '#' )
$h ${artifactId}

${descripcion}.

Generado con **microservicio-arquetipo** (Spring Boot 3.5 + Java 21 + Oracle Cloud).

$h$h Estructura
```
src/main/java/${packageInPathFormat}
├── controller/   Endpoints REST (InfoController de ejemplo)
├── service/      Lógica de negocio
├── repository/   Spring Data JPA
├── model/        Entidades (Usuario y Rol de solo lectura)
├── dto/          Request / Response, ErrorResponse, MensajeResponse
├── exception/    GlobalExceptionHandler (@RestControllerAdvice)
└── security/     SecurityConfig, UsuarioDetailsService, UsuarioActual
```

$h$h Ejecutar en local
1. Descomprime el Wallet de Oracle en la raíz del proyecto.
2. Copia `db.properties.example` como `db.properties` y completa los datos.
3. `./mvnw spring-boot:run` y abre http://localhost:${puerto}/api/info

$h$h Docker
```bash
docker build -t ${artifactId} .
docker run -p ${puerto}:${puerto} --env-file db.properties -e DB_WALLET_PATH=/app/wallet -v ./Wallet_NOMBRE:/app/wallet:ro ${artifactId}
```
