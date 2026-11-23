# jdrivesync

[![DeepWiki](https://img.shields.io/badge/DeepWiki-Documentaci%C3%B3n-blue)](https://deepwiki.com/eneekoruiz/jdrivesync)

Herramienta de línea de comandos (CLI) en Java para la sincronización incremental y bidireccional entre sistemas de archivos locales y Google Drive, optimizada para control de transferencias, verificación de integridad por hash y gestión de cuotas de API.

## Stack tecnológico

- **Lenguaje:** Java 8+
- **Integración cloud:** Google Drive REST API v3 y Google API Client Services
- **Autenticación:** OAuth 2.0 (Google OAuth Client)
- **Construcción:** Maven (empaquetado CLI y binario `.deb` para Linux)
- **Pruebas:** JUnit e integración con Drive API

## Arquitectura y decisiones clave

- **Planificador de sincronización determinista (`SyncPlanner`):** Genera un árbol diferencial comparando marcas de tiempo (timestamp) y sumas de verificación MD5 entre los archivos locales y los metadatos de Google Drive antes de ejecutar operaciones de red.
- **Gestión eficiente de cuotas y transferencias:** Implementa subidas y descargas por bloques (chunked upload) y reintentos exponenciales con jitter para prevenir bloqueos por límites de tasa (*rate limiting*) de la API de Google.
- **Detección de conflictos y borrados:** Permite configurar directivas estrictas de sincronización (unidireccional, bidireccional, preservación de archivos remotos eliminados localmente o propagación controlada).
- **Empaquetado para despliegue CLI:** Configuración de Maven para compilar ejecutables autocontenidos y paquetes Debian instalables en servidores sin entorno gráfico.

## Ejecución local

### Prerrequisitos

- Java JDK 8 o superior
- Maven 3.6+
- Credenciales de Google Cloud Platform (archivo `client_secrets.json` con acceso a Google Drive API habilitada)

### Instrucciones

1. **Compilar y generar el paquete JAR:**
   ```bash
   mvn clean package
   ```

2. **Ejecutar la suite de pruebas:**
   ```bash
   mvn test
   ```

3. **Ejecutar la sincronización mediante CLI:**
   ```bash
   java -jar target/jdrivesync.jar -l "/ruta/carpeta/local" -r "/CarpetaGoogleDrive"
   ```
