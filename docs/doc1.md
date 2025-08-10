# **Documento de Requisitos Funcionales del Frontend (MVP - Fase 1)**

**Proyecto:** Simulador de Control de Pozos
**Versión:** 1.0 (MVP)

---

## **1. Objetivo del Documento**

El presente documento define los requisitos funcionales mínimos para la primera fase de desarrollo del frontend del simulador de control de pozos. El objetivo es establecer un conjunto de funcionalidades esenciales (Producto Mínimo Viable - MVP) que permitan al usuario interactuar con el motor de simulación de manera básica y visualizar los resultados clave en tiempo real.

## **2. Plataforma de Desarrollo**

La interfaz de usuario se desarrollará utilizando **React.js**. Esta elección estratégica permite una alta portabilidad, facilitando el despliegue inicial como una aplicación de escritorio (utilizando **Electron**) y preparando el terreno para una eventual migración a una plataforma web.

## **3. Inspiración del Diseño (UI/UX)**

El diseño de la interfaz se inspira en la estética y funcionalidad de la aplicación **"Drilling Simulator 3"** para iOS. Se priorizará una disposición de paneles clara y funcional que evite distracciones, presentando los datos en una forma que los ingenieros de perforación puedan interpretar rápidamente.

## **4. Requisitos Funcionales Mínimos (MVP)**

A continuación, se detallan las funcionalidades que deben ser implementadas en la primera fase del proyecto:

### **4.1. Estructura y Disposición de la Interfaz**

* **Panel de Parámetros de Simulación:** Un área dedicada para la configuración inicial de la simulación antes de su inicio.
* **Panel de Visualización Central:** El área principal de la pantalla, dedicada a mostrar gráficos y medidores en tiempo real.
* **Panel de Controles:** Un área con botones y controles para interactuar directamente con la simulación en curso.
* **Panel de Log de Eventos:** Un área de texto para mostrar mensajes del sistema y eventos importantes de la simulación.

### **4.2. Funcionalidades de Configuración e Interacción Básica**

* **[ ] Configuración del Pozo:** La interfaz debe permitir al usuario seleccionar un pozo predefinido (ej. "Pozo de Prueba #1") de una lista. Se mostrarán los parámetros clave de este pozo (ej. Profundidad, Tipo de Fluido).
* **[ ] Controles de la Bomba:** Un control (slider o campo de entrada numérico) para establecer la tasa de flujo de la bomba de lodo.
* **[ ] Botón de Inicio (`Start`):** Inicia la simulación con los parámetros configurados. Deshabilita los controles de configuración de pozo una vez que la simulación ha comenzado.
* **[ ] Botón de Detener/Reiniciar (`Stop`/`Reset`):** Detiene la simulación en curso y la reinicia a sus valores iniciales.

### **4.3. Visualización de Datos en Tiempo Real**

* **[ ] Gráfico de Presión en Standpipe:** Un gráfico de línea dinámico que se actualiza en tiempo real, mostrando la presión en el Standpipe (SPP) en función del tiempo.
* **[ ] Gráfico de Presión en Casing:** Un gráfico de línea dinámico que se actualiza en tiempo real, mostrando la presión en el Casing (CCP) en función del tiempo.
* **[ ] Medidores Numéricos:** Varios paneles tipo "dial" o medidores digitales que muestren los valores numéricos actuales de las variables más importantes, como:

  * Presión de Standpipe (SPP)
  * Presión de Casing (CCP)
  * Flujo de retorno (Return Flow)
  * Volumen de Lodo en superficie (Pit Volume)
* **[ ] Panel de Log:** El panel de eventos debe mostrar mensajes informativos y de advertencia, como:
  * "Simulación iniciada."
  * "La tasa de flujo de la bomba ha cambiado a X GPM."
  * "ALERTA: Posible Kick detectado."

### **4.4. Funcionalidad de Control de Pozos (MVP)**

* **[ ] Detección y Notificación de Kick:** La interfaz debe mostrar una alerta visual clara y un mensaje en el panel de log cuando el motor de simulación detecte una entrada de fluidos del pozo (`kick`).
* **[ ] Botón de Cierre de Pozo (`Shut-in`):** Un botón que, al ser presionado, detiene la bomba y cierra el pozo. Esto debe tener un efecto visible en los gráficos de presión.

## **5. Requisitos Técnicos y Contrato con el Backend (API REST)**

Cada requisito funcional del frontend se correlaciona con uno o más *endpoints* de la API REST del backend de Python. La siguiente tabla resume este contrato de alto nivel, sirviendo como guía para el desarrollo del backend.

| Requisito del Frontend         | Tipo de Petición HTTP | Endpoint de la API                 | Descripción                                                                        |
| :----------------------------- | :-------------------- | :--------------------------------- | :--------------------------------------------------------------------------------- |
| **Inicio de simulación**       | `POST`                | `/api/simulacion/start`            | Inicia una nueva simulación con los parámetros de configuración iniciales.         |
| **Obtención de datos**         | `GET`                 | `/api/simulacion/<sim_id>/status`  | Recupera los datos de estado actual de la simulación (presiones, flujos, etc.).    |
| **Control de bomba**           | `POST`                | `/api/simulacion/<sim_id>/command` | Envía comandos de control al simulador, como cambiar la tasa de flujo de la bomba. |
| **Cierre de pozo (`Shut-in`)** | `POST`                | `/api/simulacion/<sim_id>/command` | Envía el comando `shut_in` para cerrar el pozo.                                    |
| **Detección de Kick**          | N/A                   | (Integrado en `/status`)           | El backend enviará una bandera de `kick_detected` en la respuesta de estado.       |

## **6. Funcionalidades Fuera del Alcance (Fase 1)**

Las siguientes funcionalidades son candidatas para futuras versiones, pero no son necesarias para la primera fase del MVP:

* **Visualización en 3D del pozo.**
* **Cálculos y gráficos avanzados** (ej. perfiles de temperatura, presión anular).
* **Funcionalidades de guardar y cargar** simulaciones.
* **Múltiples perfiles de pozos** editables por el usuario.
* **Menús de usuario** con autenticación o perfiles de estudiante/instructor.
* **Modos de entrenamiento** con escenarios predefinidos.
