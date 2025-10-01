# CrediYa

<div align="center">
  <h3>📱 Plataforma Digital de Gestión de Préstamos Personales</h3>
  <p>Una solución integral que busca digitalizar y optimizar la gestión de solicitudes de préstamos personales, eliminando la necesidad de procesos manuales y presenciales.</p>
  
  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
  [![Java](https://img.shields.io/badge/Java-17%2B-orange.svg)](https://www.oracle.com/java/)
  [![Build Status](https://img.shields.io/badge/build-passing-brightgreen.svg)](#)
  [![Version](https://img.shields.io/badge/version-1.0.0--alpha-blue.svg)](#)
</div>

## 📋 Tabla de Contenidos

- [Acerca del Proyecto](#-acerca-del-proyecto)
- [Características Principales](#-características-principales)
- [Tecnologías Utilizadas](#-tecnologías-utilizadas)
- [Prerrequisitos](#-prerrequisitos)
- [Instalación](#-instalación)
- [Configuración](#-configuración)
- [Uso](#-uso)
- [Estructura del Proyecto](#-estructura-del-proyecto)
- [API Documentation](#-api-documentation)
- [Base de Datos](#-base-de-datos)
- [Testing](#-testing)
- [Despliegue](#-despliegue)
- [Contribución](#-contribución)
- [Roadmap](#-roadmap)
- [Solución de Problemas](#-solución-de-problemas)
- [Licencia](#-licencia)
- [Contacto](#-contacto)

## 🚀 Acerca del Proyecto

CrediYa es una plataforma innovadora diseñada para revolucionar el proceso de solicitud y gestión de préstamos personales. Mediante la digitalización completa del flujo de trabajo, eliminamos las barreras tradicionales y proporcionamos una experiencia fluida tanto para solicitantes como para instituciones financieras.

### Problema que Resuelve

- **Procesos manuales lentos**: Elimina el papeleo y reduce los tiempos de procesamiento
- **Falta de transparencia**: Proporciona seguimiento en tiempo real del estado de las solicitudes
- **Evaluación subjetiva**: Implementa algoritmos de scoring crediticio automatizados
- **Experiencia del usuario deficiente**: Interfaz intuitiva y accesible desde cualquier dispositivo

## ✨ Características Principales

- 🏦 **Gestión Integral de Solicitudes**: Desde la aplicación hasta la aprobación
- 📊 **Scoring Crediticio Automatizado**: Evaluación de riesgo basada en algoritmos
- 📱 **Interfaz Responsive**: Acceso desde dispositivos móviles y desktop
- 🔐 **Seguridad Avanzada**: Encriptación end-to-end y cumplimiento normativo
- 📈 **Dashboard Analytics**: Métricas y reportes en tiempo real
- 🔔 **Notificaciones**: Actualizaciones automáticas del estado de solicitudes
- 📋 **Documentación Digital**: Upload y verificación automática de documentos
- 💳 **Integración Bancaria**: Conexión con sistemas de core bancario

## 🛠 Tecnologías Utilizadas

### Backend
- **Java 17+** - Lenguaje de programación principal
- **Spring Boot 3.x** - Framework de aplicación
- **Spring Security** - Autenticación y autorización
- **Spring Data JPA** - Persistencia de datos
- **Maven** - Gestión de dependencias

### Base de Datos
- **PostgreSQL** - Base de datos principal
- **Redis** - Cache y sesiones
- **H2** - Base de datos para testing

### Frontend (Planificado)
- **Angular/React** - Framework de frontend
- **Bootstrap/Material UI** - UI Components
- **TypeScript** - Lenguaje tipado para frontend

### DevOps & Infraestructura
- **Docker** - Containerización
- **Docker Compose** - Orquestación local
- **GitHub Actions** - CI/CD
- **SonarQube** - Análisis de código

### Testing
- **JUnit 5** - Testing unitario
- **Mockito** - Mocking framework
- **TestContainers** - Testing de integración
- **Spring Boot Test** - Testing de aplicación

## 📋 Prerrequisitos

Antes de comenzar, asegúrate de tener instalado:

```bash
# Verificar versiones
java -version    # Java 17 o superior
mvn -version     # Maven 3.8 o superior
docker --version # Docker 20.10 o superior
git --version    # Git 2.30 o superior
```

### Requisitos del Sistema

- **Java Development Kit (JDK) 17+**
- **Apache Maven 3.8+**
- **Docker y Docker Compose**
- **PostgreSQL 13+** (o usar Docker)
- **Git**
- **IDE recomendado**: IntelliJ IDEA o Eclipse

## 🔧 Instalación

### 1. Clonar el Repositorio

```bash
git clone https://github.com/mrearsbig/CrediYa.git
cd CrediYa
```

### 2. Configurar Base de Datos con Docker

```bash
# Iniciar PostgreSQL y Redis
docker-compose up -d postgres redis

# Verificar que los servicios estén ejecutándose
docker-compose ps
```

### 3. Configurar Variables de Entorno

```bash
# Copiar archivo de configuración de ejemplo
cp src/main/resources/application-example.yml src/main/resources/application-dev.yml

# Editar configuración
nano src/main/resources/application-dev.yml
```

### 4. Instalar Dependencias y Compilar

```bash
# Limpiar e instalar dependencias
mvn clean install

# Saltar tests durante la instalación inicial (opcional)
mvn clean install -DskipTests
```

### 5. Ejecutar Migraciones de Base de Datos

```bash
# Ejecutar scripts de inicialización
mvn flyway:migrate
```

## ⚙️ Configuración

### Variables de Entorno

Crea un archivo `.env` en la raíz del proyecto:

```env
# Base de Datos
DB_HOST=localhost
DB_PORT=5432
DB_NAME=crediya
DB_USERNAME=crediya_user
DB_PASSWORD=your_secure_password

# Redis
REDIS_HOST=localhost
REDIS_PORT=6379
REDIS_PASSWORD=your_redis_password

# JWT
JWT_SECRET=your_jwt_secret_key_here
JWT_EXPIRATION=86400

# API Externa de Scoring
SCORING_API_URL=https://api.scoring-provider.com
SCORING_API_KEY=your_scoring_api_key

# Email
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USERNAME=your_email@gmail.com
SMTP_PASSWORD=your_app_password

# Logging
LOG_LEVEL=INFO
LOG_FILE_PATH=./logs/crediya.log
```

### Archivo de Configuración (application.yml)

```yaml
server:
  port: 8080
  servlet:
    context-path: /api/v1

spring:
  application:
    name: crediya
  
  datasource:
    url: jdbc:postgresql://${DB_HOST:localhost}:${DB_PORT:5432}/${DB_NAME:crediya}
    username: ${DB_USERNAME:crediya_user}
    password: ${DB_PASSWORD:password}
    driver-class-name: org.postgresql.Driver
  
  jpa:
    hibernate:
      ddl-auto: validate
    show-sql: false
    properties:
      hibernate:
        dialect: org.hibernate.dialect.PostgreSQLDialect
        format_sql: true
  
  redis:
    host: ${REDIS_HOST:localhost}
    port: ${REDIS_PORT:6379}
    password: ${REDIS_PASSWORD:}
    timeout: 2000ms

logging:
  level:
    com.crediya: ${LOG_LEVEL:INFO}
    org.springframework.security: DEBUG
  file:
    name: ${LOG_FILE_PATH:./logs/crediya.log}
```

## 🚀 Uso

### Desarrollo Local

```bash
# Ejecutar en modo desarrollo
mvn spring-boot:run -Dspring-boot.run.profiles=dev

# O usando el JAR compilado
java -jar target/crediya-1.0.0-SNAPSHOT.jar --spring.profiles.active=dev
```

### Usando Docker

```bash
# Construir la imagen
docker build -t crediya:latest .

# Ejecutar con Docker Compose
docker-compose up -d

# Ver logs
docker-compose logs -f crediya
```

### Acceso a la Aplicación

- **API Base URL**: `http://localhost:8080/api/v1`
- **Swagger UI**: `http://localhost:8080/swagger-ui.html`
- **Health Check**: `http://localhost:8080/actuator/health`

### Ejemplos de Uso de la API

#### Autenticación

```bash
# Registro de usuario
curl -X POST http://localhost:8080/api/v1/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "email": "usuario@ejemplo.com",
    "password": "Password123!",
    "firstName": "Juan",
    "lastName": "Pérez",
    "phone": "+57300123456"
  }'

# Login
curl -X POST http://localhost:8080/api/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "usuario@ejemplo.com",
    "password": "Password123!"
  }'
```

#### Gestión de Préstamos

```bash
# Crear solicitud de préstamo
curl -X POST http://localhost:8080/api/v1/loans \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "amount": 5000000,
    "termMonths": 24,
    "purpose": "PERSONAL",
    "monthlyIncome": 3000000
  }'

# Consultar solicitudes
curl -X GET http://localhost:8080/api/v1/loans \
  -H "Authorization: Bearer YOUR_JWT_TOKEN"

# Obtener detalles de una solicitud
curl -X GET http://localhost:8080/api/v1/loans/{loanId} \
  -H "Authorization: Bearer YOUR_JWT_TOKEN"
```

## 📁 Estructura del Proyecto

```
CrediYa/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/
│   │   │       └── crediya/
│   │   │           ├── CrediYaApplication.java
│   │   │           ├── config/           # Configuraciones
│   │   │           ├── controller/       # Controladores REST
│   │   │           ├── service/          # Lógica de negocio
│   │   │           ├── repository/       # Acceso a datos
│   │   │           ├── model/           # Entidades JPA
│   │   │           ├── dto/             # Data Transfer Objects
│   │   │           ├── security/        # Seguridad y JWT
│   │   │           ├── exception/       # Manejo de excepciones
│   │   │           └── util/           # Utilidades
│   │   └── resources/
│   │       ├── application.yml
│   │       ├── application-dev.yml
│   │       ├── application-prod.yml
│   │       └── db/migration/           # Scripts Flyway
│   └── test/
│       ├── java/                       # Tests unitarios
│       └── resources/                  # Recursos para testing
├── docker/
│   ├── Dockerfile
│   └── docker-compose.yml
├── docs/                              # Documentación adicional
├── scripts/                           # Scripts de utilidad
├── .github/
│   └── workflows/                     # GitHub Actions
├── pom.xml
├── .gitignore
├── README.md
└── LICENSE
```

## 📚 API Documentation

### Endpoints Principales

#### Autenticación
- `POST /auth/register` - Registro de usuario
- `POST /auth/login` - Inicio de sesión
- `POST /auth/refresh` - Renovar token
- `POST /auth/logout` - Cerrar sesión

#### Gestión de Usuarios
- `GET /users/profile` - Obtener perfil
- `PUT /users/profile` - Actualizar perfil
- `POST /users/documents` - Subir documentos

#### Préstamos
- `POST /loans` - Crear solicitud
- `GET /loans` - Listar solicitudes
- `GET /loans/{id}` - Obtener detalles
- `PUT /loans/{id}/status` - Actualizar estado

#### Administración
- `GET /admin/loans` - Gestionar todas las solicitudes
- `GET /admin/users` - Gestionar usuarios
- `GET /admin/reports` - Generar reportes

### Documentación Swagger

Una vez que la aplicación esté ejecutándose, puedes acceder a la documentación interactiva en:
`http://localhost:8080/swagger-ui.html`

## 🗄️ Base de Datos

### Esquema Principal

```sql
-- Usuarios
CREATE TABLE users (
    id BIGSERIAL PRIMARY KEY,
    email VARCHAR(255) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    phone VARCHAR(20),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Solicitudes de Préstamo
CREATE TABLE loan_applications (
    id BIGSERIAL PRIMARY KEY,
    user_id BIGINT REFERENCES users(id),
    amount DECIMAL(15,2) NOT NULL,
    term_months INTEGER NOT NULL,
    interest_rate DECIMAL(5,2),
    status VARCHAR(50) DEFAULT 'PENDING',
    purpose VARCHAR(100),
    monthly_income DECIMAL(15,2),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Documentos
CREATE TABLE documents (
    id BIGSERIAL PRIMARY KEY,
    loan_application_id BIGINT REFERENCES loan_applications(id),
    type VARCHAR(50) NOT NULL,
    filename VARCHAR(255) NOT NULL,
    file_path VARCHAR(500) NOT NULL,
    verified BOOLEAN DEFAULT FALSE,
    uploaded_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Migraciones

Las migraciones se manejan con Flyway y se encuentran en `src/main/resources/db/migration/`:

```bash
# Ejecutar migraciones
mvn flyway:migrate

# Ver estado de migraciones
mvn flyway:info

# Limpiar base de datos (¡Cuidado en producción!)
mvn flyway:clean
```

## 🧪 Testing

### Ejecutar Tests

```bash
# Todos los tests
mvn test

# Solo tests unitarios
mvn test -Dtest="*Test"

# Solo tests de integración
mvn test -Dtest="*IT"

# Con coverage
mvn test jacoco:report
```

### Estructura de Tests

```
src/test/java/
├── unit/                    # Tests unitarios
│   ├── service/
│   ├── controller/
│   └── util/
├── integration/             # Tests de integración
│   ├── repository/
│   └── api/
└── e2e/                    # Tests end-to-end
```

### Tests de Ejemplo

```java
@SpringBootTest
@TestPropertySource(locations = "classpath:application-test.properties")
class LoanServiceTest {
    
    @MockBean
    private LoanRepository loanRepository;
    
    @Autowired
    private LoanService loanService;
    
    @Test
    void shouldCreateLoanApplication() {
        // Given
        LoanApplicationDto dto = new LoanApplicationDto();
        dto.setAmount(BigDecimal.valueOf(5000000));
        dto.setTermMonths(24);
        
        // When
        LoanApplication result = loanService.createLoanApplication(dto);
        
        // Then
        assertThat(result.getAmount()).isEqualTo(BigDecimal.valueOf(5000000));
        assertThat(result.getStatus()).isEqualTo(LoanStatus.PENDING);
    }
}
```

## 🚀 Despliegue

### Entorno de Desarrollo

```bash
# Con Docker Compose
docker-compose -f docker-compose.dev.yml up -d
```

### Entorno de Producción

```bash
# Construir para producción
mvn clean package -Pprod

# Crear imagen Docker
docker build -t crediya:prod .

# Desplegar con Docker Compose
docker-compose -f docker-compose.prod.yml up -d
```

### Variables de Entorno para Producción

```env
SPRING_PROFILES_ACTIVE=prod
DB_HOST=your-prod-db-host
DB_PASSWORD=your-secure-prod-password
JWT_SECRET=your-very-secure-jwt-secret
```

### CI/CD con GitHub Actions

El pipeline incluye:
- ✅ Tests unitarios y de integración
- 🔍 Análisis de código con SonarQube
- 🐳 Construcción de imagen Docker
- 🚀 Despliegue automático

## 🤝 Contribución

¡Las contribuciones son bienvenidas! Para contribuir:

### 1. Fork y Clone

```bash
git clone https://github.com/tu-usuario/CrediYa.git
cd CrediYa
```

### 2. Crear Rama de Feature

```bash
git checkout -b feature/nueva-funcionalidad
```

### 3. Desarrollo

- Sigue las convenciones de código Java
- Escribe tests para el código nuevo
- Actualiza la documentación si es necesario

### 4. Commit y Push

```bash
git add .
git commit -m "feat: agregar nueva funcionalidad de scoring"
git push origin feature/nueva-funcionalidad
```

### 5. Pull Request

- Crea un PR describiendo los cambios
- Asegúrate de que pasen todos los tests
- Solicita revisión del código

### Convenciones de Código

- **Java**: Seguir Google Java Style Guide
- **Commits**: Conventional Commits
- **Naming**: camelCase para métodos, PascalCase para clases
- **Tests**: Arrange-Act-Assert pattern

## 🗺️ Roadmap

### Versión 1.0.0 (Q4 2025)
- [x] Configuración inicial del proyecto
- [ ] Sistema de autenticación y autorización
- [ ] CRUD de usuarios y solicitudes
- [ ] Algoritmo básico de scoring crediticio
- [ ] API REST completa

### Versión 1.1.0 (Q1 2026)
- [ ] Frontend web responsive
- [ ] Dashboard de administración
- [ ] Integración con servicios de scoring externos
- [ ] Sistema de notificaciones

### Versión 1.2.0 (Q2 2026)
- [ ] Aplicación móvil (React Native)
- [ ] Machine Learning para scoring avanzado
- [ ] Integración bancaria
- [ ] Reportes y analytics avanzados

### Futuras Mejoras
- [ ] Blockchain para trazabilidad
- [ ] IA para detección de fraude
- [ ] Microservicios architecture
- [ ] Multi-tenancy

## 🔧 Solución de Problemas

### Problemas Comunes

#### Error de Conexión a Base de Datos

```bash
# Verificar que PostgreSQL esté ejecutándose
docker ps | grep postgres

# Revisar logs de la base de datos
docker-compose logs postgres

# Reiniciar servicios
docker-compose restart postgres
```

#### Problemas de Autenticación JWT

```bash
# Verificar configuración del JWT secret
echo $JWT_SECRET

# Revisar logs de la aplicación
tail -f logs/crediya.log | grep JWT
```

#### Tests Fallando

```bash
# Limpiar y recompilar
mvn clean compile

# Ejecutar tests con información detallada
mvn test -X

# Verificar base de datos de test
mvn test -Dspring.profiles.active=test
```

### Logs y Debugging

```bash
# Ver logs en tiempo real
tail -f logs/crediya.log

# Filtrar por nivel de error
grep "ERROR" logs/crediya.log

# Debugging con IDE
# Configurar remote debugging en puerto 5005
java -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005 -jar target/crediya.jar
```

### Contacto para Soporte

Si encuentras problemas no documentados:
1. Revisa los [Issues existentes](https://github.com/mrearsbig/CrediYa/issues)
2. Crea un nuevo issue con detalles del problema
3. Incluye logs relevantes y pasos para reproducir

## 📄 Licencia

Este proyecto está licenciado bajo la Licencia MIT - ver el archivo [LICENSE](LICENSE) para más detalles.

```
MIT License

Copyright (c) 2025 ALEXANDER VIAFARA HURTADO

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction...
```

## 📞 Contacto

**ALEXANDER VIAFARA HURTADO**

- 📧 Email: [alexander.viafara@crediya.com](mailto:alexander.viafara@crediya.com)
- 💼 LinkedIn: [Alexander Viafara](https://linkedin.com/in/alexander-viafara)
- 🐙 GitHub: [@mrearsbig](https://github.com/mrearsbig)

### Enlaces del Proyecto

- 🌐 **Repositorio**: [https://github.com/mrearsbig/CrediYa](https://github.com/mrearsbig/CrediYa)
- 📋 **Issues**: [https://github.com/mrearsbig/CrediYa/issues](https://github.com/mrearsbig/CrediYa/issues)
- 📖 **Wiki**: [https://github.com/mrearsbig/CrediYa/wiki](https://github.com/mrearsbig/CrediYa/wiki)
- 🚀 **Releases**: [https://github.com/mrearsbig/CrediYa/releases](https://github.com/mrearsbig/CrediYa/releases)

---

<div align="center">
  <p>Hecho con ❤️ para revolucionar la industria financiera</p>
  <p>
    <a href="#top">Volver al inicio ⬆️</a>
  </p>
</div>
