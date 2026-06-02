# Reporte de Auditoría - Proyecto: CITYFIX-C.-FERLEY

## 🏗️ 1. Estructura del Proyecto
Tras la revisión del árbol de directorios del repositorio, se determinó que el proyecto está configurado como un **Microservicio Backend aislado o API** desarrollado en **Node.js (JavaScript)**, prescindiendo de la capa de interfaz móvil (Expo/React Native).

La distribución de los componentes principales se define de la siguiente manera:
* `node_modules/`: Carpeta local que aloja las dependencias y librerías de Node.js necesarias para la ejecución del servicio.
* `src/`: Directorio raíz del código fuente que contiene la lógica del negocio.
* `src/utils/`: Subcarpeta que almacena los módulos operativos centrales, específicamente el motor de reportes (`reportEngine.js`) y su suite de pruebas unitarias (`reportEngine.test.js`).

---

## ⚙️ 2. Control de Entorno y Configuración
* **Fijación de Dependencias (`package.json`):** Contiene la declaración base de los scripts de ejecución (como `npm test`) y las librerías requeridas. *(Nota: Se detecta la ausencia del archivo de bloqueo `package-lock.json`)*.
* **Filtros de Versiones (`.gitignore`):** Configurado correctamente en la raíz para evitar la fuga o subida accidental de dependencias locales pesadas al repositorio remoto.
* **Documentación (`README.md`):** Presente en la raíz, proporcionando la guía inicial y los requisitos técnicos para el despliegue del proyecto.

---

## 🐳 3. Infraestructura y Contenedorización
El servicio está completamente preparado para ser desplegado en entornos aislados mediante contenedores:
* **`Dockerfile`**: Define la construcción de la imagen base de Node.js y la instalación interna de dependencias.
* **`docker-compose.yml`**: Orquesta el levantamiento del contenedor (`cityfix`), permitiendo ejecutar las pruebas unitarias de Jest de forma automatizada mediante el comando `docker compose up --build`.

---

## 🚨 4. Hallazgos y Puntos de Mejora (Recomendaciones del Auditor)
1. **Ausencia de `package-lock.json`:** Se recomienda generar este archivo ejecutando `npm install` localmente antes de realizar el despliegue definitivo. Esto garantiza que todas las dependencias instalen exactamente las mismas versiones en cualquier máquina o contenedor, evitando fallas por actualizaciones de terceros.
2. **Aislamiento de Configuración (Falta de `.env`):** No se detecta un archivo `.env` en la raíz. Es obligatorio verificar el archivo `docker-compose.yml` para asegurar que no se hayan escrito credenciales, contraseñas o llaves API "en duro" (hardcoded), lo cual representa un riesgo crítico de seguridad.


NPM TEST:

 PASS  src/utils/reportEngine.test.js
  CityFix E2E Live Network
    ✓ Debe obtener los reportes guardados en Supabase (1204 ms)
    ✓ Cada reporte debe tener los datos (128 ms)
cityfix-1  | 
Test Suites: 1 passed, 1 total
cityfix-1  | Tests:       2 passed, 2 total
cityfix-1  | Snapshots:   0 total
cityfix-1  | Time:        2.053 s
cityfix-1  | Ran all test suites.

cityfix-1 exited with code 0