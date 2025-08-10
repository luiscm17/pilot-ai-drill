# **Descripción Detallada del Boceto de la UI**

Imagina la pantalla de tu aplicación de escritorio o web. La hemos dividido en tres grandes paneles, como si fuera la consola de un equipo de perforación.

## **1. Panel Izquierdo: Controles y Medidores**

Este panel ocupa aproximadamente el 25% del ancho de la pantalla y se enfoca en los controles y medidores en tiempo real.

* **Parte Superior:** Contiene los medidores analógicos más importantes, diseñados como "diales" o relojes.
  * **Medidor de Presión de Bomba:** En la esquina superior izquierda, con una escala de `0 a 5000 psi`. La aguja se moverá en tiempo real.
  * **Medidor de Carga del Gancho (`Hook Load`):** El medidor más grande y central de este panel. La aguja indicará el peso actual sobre el gancho, con valores negativos (para cuando se está liberando peso).
  * **Medidor de Torque Rotatorio:** Un medidor más pequeño, a la derecha del medidor de carga, mostrando el torque del motor rotatorio.

* **Parte Media (Controles y Display):**
  * **Lecturas Digitales:** Debajo de los medidores, un grupo de lecturas numéricas en tiempo real. Por ejemplo: `Bit Depth`, `MW IN` (densidad del lodo de entrada), `SPM` (golpes por minuto de la bomba), `Flow In`, etc.
  * **Controles de Bomba:** Un control (podría ser un `slider` o `+` y `-` botones) para ajustar las SPM (Strokes per Minute) o GPM (Gallons per Minute).
  * **Botones de Interacción:** Botones clave como `Auto Driller` (para futuras fases) y, de manera crucial para la V1.0, un botón `Shut-in` que represente el cierre del pozo.

## **2. Panel Central: Vista del Pozo y la Sarta de Perforación**

Este es el panel más estrecho, ocupando aproximadamente el 15% del ancho, y sirve como una referencia visual.

* **Representación del Pozo:** Un diagrama vertical simple que muestra el interior del pozo.
* **Elementos Visuales:** Se visualizan la sarta de perforación, la broca (`Bit`), la tubería de revestimiento (`Casing`) y el nivel de lodo.
* **Medidas de Profundidad:** Pequeños marcadores de texto o líneas a los lados del pozo que indican la profundidad actual en pies o metros.
* **Vista de BOP:** Un diagrama simple del `BOP` (Blowout Preventer) en la parte superior, con indicadores de luz (rojo/verde) para mostrar su estado (abierto/cerrado).

## **3. Panel Derecho: Gráficos y Consola de Log**

Este es el panel más ancho, ocupando el 60% restante de la pantalla, y se enfoca en el análisis de datos.

* **Sección de Gráficos:** Ocupa la parte superior de este panel.
  * **Gráfico Principal (Trazado de Tendencias):** Un gráfico que muestra múltiples líneas superpuestas a lo largo del tiempo o la profundidad. En la V1.0, este gráfico tendrá al menos dos líneas:
    * **Presión de Standpipe (SPP):** Una línea que cambia dinámicamente con la simulación.
    * **Presión de Casing (CCP):** Otra línea que cambia dinámicamente, y que reaccionará de manera crítica a eventos como un `kick` o un `shut-in`.
  * **Gráfico Secundario (Opcional en V1.0):** Un gráfico más pequeño debajo del principal para visualizar otras variables como los flujos de entrada y salida de lodo.

* **Sección de Consola de Log:** Ocupa la parte inferior de este panel.
  * **Cuadro de Indicadores Clave:** Un área con lecturas numéricas de las variables más importantes para el control de pozos, como `DP Pressure`, `Kill Pressure`, `Choke Pressure`, `Flow Out`, `Flow In`, `Active Volume`, etc.
  * **Log de Eventos:** Una ventana de texto con capacidad de `scroll` que mostrará un registro cronológico de los eventos de la simulación, como "Simulación Iniciada", "Flujo anormal detectado", "Se ha cerrado el pozo", etc.

## **Conclusión**

Esta descripción detallada del boceto es tu "plano" para la implementación. Puedes usarla como una guía para crear tus componentes de React, sabiendo exactamente qué elementos deben ir en cada parte de la pantalla y cómo se espera que funcionen.
