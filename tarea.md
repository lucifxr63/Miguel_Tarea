Me parece una excelente iniciativa. Organizar el desarrollo en fases claras es la mejor manera de asegurar que el dashboard cumpla con todos los requerimientos técnicos y visuales de Plásticos Andino S.A., manteniendo un código limpio y funcional sin necesidad de un backend.

A continuación, te presento la planificación estructurada desde el Paso 0 hasta la entrega final, seguida del prompt detallado que podrás copiar y pegar en Claude Code para generar el proyecto completo.

### Planificación de Desarrollo del Dashboard Front-end

**Paso 0: Arquitectura de Datos y Preparación del Entorno**

* **Objetivo:** Estructurar la base del proyecto (HTML, CSS con variables para modo oscuro/claro) y unificar los datos en formato JSON dentro de JavaScript.
* **Acciones:**
* Implementar el cascarón HTML y el CSS existente.
* Crear un objeto `const dashboardData = {}` que contenga: arrays mensuales (producción, consumo real, propuesto, costos, tarifas) y arrays financieros (CAPEX, OPEX, ahorros por sistema).
* Vincular la librería Chart.js desde CDN.



**Paso 1: Vista General y KPIs Clave**

* **Objetivo:** Mostrar la fotografía global del proyecto de eficiencia energética.
* **Acciones:**
* Crear el grid de tarjetas (KPIs) superior: Consumo Caso Base (**5.048.700 kWh**), Consumo Propuesto (**4.948.700 kWh**), Brecha Total (**100.000 kWh**), Producción total, Consumo real y Costo de energía real.


* Integrar gráficos de barras comparativos base vs. propuesto.



**Paso 2: Tablas de Conclusiones y Correcciones (Renderizado Condicional)**

* **Objetivo:** Visualizar el impacto mensual y las desviaciones detectadas en la auditoría.
* **Acciones:**
* **Tabla Verde/Rojo (Conclusiones):** Construir la tabla de consumo energético por mes (kWh, Consumo, Costo, Tarifa, Relación kWh/ton). Aplicar clases CSS condicionales para pintar de rojo suave los meses con "desfases considerables" (Julio a Diciembre) y de verde los meses dentro de la meta.


* **Tabla Verde/Gris (Correcciones):** Construir la tabla que muestre las reducciones aplicadas en los meses desfasados. Pintar de verde los meses corregidos y de gris (opaco) los meses que no requirieron intervención.





**Paso 3: Módulo de Sistemas, Medidas y Brechas**

* **Objetivo:** Desglosar el rendimiento técnico por área (Inyección, Auxiliar, Iluminación, Gestión).


* **Acciones:**
* Crear la tabla "Caso Base / Post Mejora" con promedios de consumo (kWh/ton).
* Crear la tabla "Sistemas/Brechas" con Área, Caso base, Caso propuesto, Brecha (kWh/año) y Costo por brecha.
* Diseñar tarjetas o un acordeón para las **Medidas Ejecutadas**, detallando el impacto por kWh y costo asociado de cada acción (ej. VDF en inyección, sensores LED, SCADA).





**Paso 4: Módulo Interactivo Dinámico (Filtros por Mes)**

* **Objetivo:** Permitir al usuario explorar los datos financieros a nivel micro.
* **Acciones:**
* Crear un selector desplegable (`<select>`) o una botonera con los meses del año y una opción "Todos los meses".
* Programar un "Event Listener" en JS que, al cambiar el mes, actualice dinámicamente una mini-tabla mostrando exclusivamente: Tarifa promedio [CLP/kWh], Costo mensual energía [CLP] y Consumo eléctrico [kWh].



**Paso 5: Evaluación Financiera y Escenario "What-If"**

* **Objetivo:** Mostrar la viabilidad económica (VAN, TIR, Payback) y simular el proyecto sin el sistema de menor rendimiento.
* **Acciones:**
* Renderizar las métricas estáticas del escenario completo.
* Implementar un botón interactivo: **"Excluir Sistema Auxiliar"**.
* Programar la lógica JS para que, al activar este botón, se resten los costos de inversión y ahorros del sistema auxiliar (ventilación y aire comprimido), y se recalculen automáticamente en tiempo real el Flujo de Caja a 10 años, el nuevo VAN y la nueva TIR, actualizando el gráfico correspondiente.





---

### Prompt para Claude Code

Copia el siguiente bloque y entrégaselo a Claude Code para que ejecute todo el desarrollo de una sola vez.

```markdown
Eres un Desarrollador Frontend Experto. Tu tarea es crear un Dashboard de Eficiencia Energética en un solo archivo `index.html` (HTML, CSS y Vanilla JavaScript) utilizando Chart.js (v4.4.0) vía CDN. No utilices frameworks adicionales ni backend.

El diseño debe seguir una estética moderna, limpia y responsiva (preferentemente un tema oscuro con acentos verdes, azules, ámbar y rojos, similar a un dashboard financiero/técnico).

Implementa la funcionalidad siguiendo estrictamente estos requerimientos:

**1. ESTRUCTURA DE DATOS (JavaScript)**
Agrupa todos los datos en un objeto principal constante. Utiliza estos valores de referencia:
* Producción anual: 14.310 ton.
* Consumo Caso Base: 5.048.700 kWh.
* Consumo Propuesto (Objetivo): 4.948.700 kWh.
* Brecha Total: 100.000 kWh.
* Los meses desfasados (que generan la brecha) son: Julio, Agosto, Octubre, Noviembre y Diciembre.

**2. SECCIÓN: VISTA GENERAL**
* Un Grid de KPIs mostrando: Consumo Real, Objetivo Proyectado (4.948.700), Brecha Total, Producción Total, Intensidad Real (kWh/ton), y Costo Energía Real.
* Gráfico de barras de Producción vs Consumo.

**3. SECCIÓN: TABLAS DE CONCLUSIONES Y CORRECCIONES**
* **Tabla Conclusiones (Verde y Rojo):** Una tabla de 12 filas (una por mes) mostrando Producción, Consumo eléctrico, Costo, Tarifa y Relación kWh/ton. Usa JS para que, si el mes es Julio, Agosto, Octubre, Noviembre o Diciembre, la fila tenga un fondo rojizo translúcido (desfase), y el resto fondo verde translúcido.
* **Tabla Correcciones (Verde y Gris):** Otra tabla que muestre la Reducción de Consumo aplicada. Si el mes tiene reducción (Julio-Dic), fondo verde; si la reducción es 0, texto y fondo gris/deshabilitado.

**4. SECCIÓN: BRECHAS Y MEDIDAS EJECUTADAS**
* **Tabla Caso Base vs Post Mejora:** Columnas: Mes, Producción, Consumo Eléctrico Real, Consumo (kWh/ton), y Totales/Promedios al pie de la tabla.
* **Tabla Sistemas/Brechas:** Columnas: Área/Sistema, Caso Base (kWh), Caso Propuesto (kWh), Brecha (kWh/año), Costo por brecha. (Sistemas: Inyección, Iluminación, Auxiliar, Gestión).
* **Medidas Ejecutadas:** Un listado visual (tarjetas) con el desglose de medidas por área (ej. automatización VDF, sensores de presencia, tableros SCADA), indicando su aporte a la reducción de kWh.

**5. SECCIÓN: TABLA DINÁMICA INTERACTIVA**
* Crea una interfaz con un `<select>` para elegir el mes (Enero a Diciembre, o "Todos").
* Abajo, una tabla que reaccione al evento `change` del selector. Debe mostrar únicamente: Tarifa promedio [CLP/kWh], Costo mensual energía [CLP] y Consumo eléctrico [kWh] del mes seleccionado.

**6. SECCIÓN: EVALUACIÓN FINANCIERA DINÁMICA**
* Muestra KPIs de VAN, TIR, Inversión (CAPEX) y Payback.
* Muestra un gráfico de barras con el Flujo de Caja a 10 años.
* **Requerimiento Crítico:** Añade un switch/botón llamado "Simular sin Sistema Auxiliar". Al hacer clic, una función JS debe:
  1. Restar el CAPEX del Sistema Auxiliar al CAPEX total.
  2. Restar los Ahorros del Sistema Auxiliar a los ahorros anuales totales.
  3. Recalcular el Flujo de Caja neto a 10 años.
  4. Actualizar dinámicamente el Gráfico de Flujo de Caja y los números de VAN, TIR e Inversión mostrados en pantalla.

Genera el código completo, asegurándote de que el CSS sea atractivo, los gráficos de Chart.js se rendericen correctamente, y la lógica de la simulación financiera y la tabla dinámica funcionen a la perfección.

```