# **Documento de Arquitectura y Selección de Tecnologías para el Frontend (Fase 1)**

**Proyecto:** Simulador de Control de Pozos
**Versión:** 1.0 (MVP)
**Fecha:** 10 de agosto de 2025
**Documento Relacionado:** Requisitos Funcionales Mínimos del Frontend

---

## **1. Objetivo del Documento**

El presente documento complementa el "Documento de Requisitos Funcionales Mínimos del Frontend" al especificar la pila de tecnologías y las librerías recomendadas para la implementación de la interfaz de usuario. El objetivo es proporcionar un plan técnico claro y justificado para la construcción del frontend utilizando el framework React.js, asegurando que las herramientas seleccionadas sean óptimas para el desarrollo de una aplicación con visualización de datos en tiempo real y alta interacción.

## **2. Arquitectura de Frontend Propuesta**

La arquitectura del frontend se basará en el **paradigma de componentes de React**. La aplicación se construirá como un conjunto de componentes reutilizables y atómicos (botones, medidores, gráficos, paneles) que se conectarán a un estado global gestionado de manera centralizada.

El rol principal de esta arquitectura será el de **presentación y visualización de datos**. El frontend se comunicará con la API REST del backend de Python para:

1. Enviar comandos al motor de simulación.
2. Recibir los datos de estado de la simulación en tiempo real.
3. Renderizar estos datos de forma visualmente atractiva y funcional (gráficos, medidores, etc.).

---

## **3. Pila de Tecnologías Recomendada (Selección Detallada)**

A continuación, se detalla la selección de herramientas para cada capa del frontend, con su propósito y justificación.

### **3.1. Configuración y Entorno de Desarrollo**

* **Herramienta:** **Vite**
  * **Propósito:** Es un `build tool` y servidor de desarrollo. Se encarga de la configuración inicial del proyecto, el empaquetado del código y la recarga en caliente del navegador durante el desarrollo.
  * **Justificación:** Se prefiere sobre Create React App (CRA) por su velocidad de arranque extremadamente rápida, que mejora significativamente la experiencia del desarrollador. Utiliza módulos ES nativos para el hot-reloading, lo que se traduce en un flujo de trabajo más ágil.

### **3.2. Gestión del Estado (State Management)**

* **Herramienta:** **Zustand**
  * **Propósito:** Permite crear y gestionar un estado global compartido por múltiples componentes. Es ideal para variables de la simulación que necesitan ser accesibles en toda la aplicación (ej. `presión`, `flujo`, `estado_de_simulacion`).
  * **Justificación:** Fue elegida por su simplicidad y bajo peso. A diferencia de Redux, no requiere una configuración extensa y se integra perfectamente con React Hooks. Su API es simple e intuitiva, lo que reduce la curva de aprendizaje y acelera el desarrollo.
  * **Alternativas:** `Redux Toolkit` (más complejo, para aplicaciones a gran escala), `React Context API` (incorporado en React, bueno para estados simples).

### **3.3. Fetching de Datos (Comunicación con la API)**

* **Herramienta:** **Axios** y **React Query**
  * **Propósito:**
    * **Axios** es un cliente HTTP basado en promesas para hacer peticiones a la API REST del backend.
    * **React Query** (o SWR) es una librería para la gestión, caché y sincronización del estado del servidor. Permite obtener datos del backend de forma eficiente y automática.
  * **Justificación:** `Axios` es una herramienta robusta y popular para las peticiones API. `React Query` es un complemento indispensable, ya que simplifica la lógica de las peticiones periódicas (polling) para obtener los datos en tiempo real de la simulación, gestiona automáticamente el estado de carga y el `caching` de los datos, liberando al desarrollador de esa complejidad.
  * **Alternativas:** `fetch` (API nativa de JavaScript), `SWR` (una alternativa a React Query).

### **3.4. Visualización de Datos y Gráficos**

* **Herramienta:** **Plotly.js** (con el paquete `react-plotly.js`)
  * **Propósito:** Crear gráficos de alta calidad, interactivos y optimizados para datos científicos y de ingeniería.
  * **Justificación:** `Plotly` es la mejor opción para este proyecto debido a su enfoque en la visualización de datos técnicos. Puede crear fácilmente gráficos de línea con múltiples series, medidores tipo "dial", y es altamente configurable. Su capacidad de manejar grandes conjuntos de datos y su interactividad lo hacen perfecto para los gráficos de presión y flujo del simulador.
  * **Alternativas:** `Chart.js` (más simple, buena para gráficos generales), `Recharts` (para gráficos centrados en componentes).

### **3.5. Componentes de la Interfaz (UI/UX)**

* **Herramienta:** **MUI (Material UI)**
  * **Propósito:** Proporcionar un conjunto completo de componentes de interfaz listos para usar (botones, sliders, diálogos, iconos, etc.).
  * **Justificación:** `MUI` es una de las librerías más populares y maduras, lo que garantiza una amplia gama de componentes bien diseñados, accesibilidad incorporada y excelente documentación. Su sistema de `themability` (personalización de temas) permite adaptar fácilmente el estilo para que coincida con la estética de un simulador de control.
  * **Alternativas:** `Chakra UI` (más minimalista y fácil de personalizar), `Ant Design` (más enfocado a aplicaciones empresariales).

## **4. Resumen de la Pila de Frontend Recomendada (Fase 1)**

| Categoría | Herramienta Recomendada | Propósito Principal |
| :--- | :--- | :--- |
| **Setup & Build Tool** | **Vite** | Entorno de desarrollo rápido y eficiente. |
| **Core Framework** | **React.js** | Base de la interfaz de usuario con componentes. |
| **Gestión de Estado** | **Zustand** | Almacenamiento y acceso global a los datos de la simulación. |
| **Fetching de Datos** | **Axios** | Cliente HTTP para la comunicación con la API. |
| **Gestión del Fetching** | **React Query** | Optimización de las peticiones para datos en tiempo real. |
| **Gráficos y Visualización** | **Plotly.js** | Creación de gráficos científicos y medidores. |
| **Componentes de UI** | **MUI** | Componentes preconstruidos para botones, sliders, etc. |
| **Pruebas (Opcional)** | **Vitest** | Framework de pruebas unitarias compatible con Vite. |

## **5. Próximos Pasos**

Con esta pila tecnológica definida, el siguiente paso es:

1. Configurar el proyecto inicial de React con Vite.
2. Instalar las librerías recomendadas.
3. Empezar a desarrollar los componentes del esqueleto de la interfaz, como los paneles de visualización y control, siguiendo los requisitos funcionales establecidos.
4. Simultáneamente, el desarrollo del backend puede comenzar, con la API REST como el principal punto de integración entre ambas partes.
