# 🖥️ Pruebas de UI — Urban Routes

Proyecto de pruebas manuales sobre **Urban Routes**, una aplicación web de transporte tipo ride-hailing. El objetivo fue validar el flujo completo de reserva de un viaje: selección de tarifa, mapa, método de pago y comportamiento del botón "Reservar".

---

## 🎯 Objetivo

Verificar que la interfaz cumpla con el diseño y los requisitos funcionales definidos, identificando inconsistencias visuales y errores de lógica en el flujo de reserva.

---

## 🔍 Proceso de trabajo

1. **Análisis del diseño** — Comparación de la interfaz contra el diseño de referencia (Figma) para detectar diferencias visuales.
2. **Diseño de casos de prueba** — Cobertura de:
   - Checklist de diseño (mapa, tarifas, botón "Reservar", ventana de auto reservado)
   - Validaciones del formulario de método de pago (valores límite)
   - Lógica del botón "Reservar" según el estado del formulario
   - Flujo completo de reserva (inicio, cancelación, errores)
3. **Ejecución** — Pruebas manuales en **Firefox** y **Chrome**.
4. **Reporte de bugs** — Documentación en Jira con pasos de reproducción, resultado actual, resultado esperado y entorno.

---

## 🐛 Bugs encontrados (17 en total)

| ID | Resumen | Severidad |
|----|---------|-----------|
| KAN-4 | El botón "Reservar" no está anclado en la parte inferior del formulario en Firefox | Medium |
| KAN-5 | Los vehículos no aparecen en el mapa ni muestran comportamientos esperados al seleccionar una tarifa e iniciar el viaje | Medium |
| KAN-6 | Las características de la tarifa "Camping" no coinciden con los requisitos ("puertas Bluetooth · equipo de acampada") | Medium |
| KAN-7 | El sistema permite agregar un método de pago con valores no numéricos | Medium |
| KAN-8 | No aparecen los últimos 4 dígitos de la tarjeta al agregarla | Medium |
| KAN-9 | No aparece ningún aviso al intentar reservar sin completar los campos obligatorios | Medium |
| KAN-10 | El botón "Agregar método de pago y reservar" inicia el viaje en lugar de abrir la ventana de pago | Medium |
| KAN-11 | El botón "Cancelar" no muestra la ventana de confirmación al cancelar un viaje | Medium |
| KAN-12 | Al borrar las direcciones durante una reserva activa, el sistema no actualiza el botón y el viaje queda en un estado inconsistente | Medium |
| KAN-13 | El mapa tiene un nivel de zoom demasiado alto al ingresar las direcciones del viaje | Low |
| KAN-14 | El temporizador de tiempo de espera gratuito se congela en 0:01 y nunca llega a 0:00 | Medium |
| KAN-15 | La página queda atrapada en un bucle si el temporizador se congela y el botón "Cancelar" no funciona | High |
| KAN-16 | La ventana "Automóvil reservado" no muestra la marca ni la placa del vehículo y los elementos se empalman | Medium |
| KAN-17 | El botón "Agregar licencia de conducir y reservar" no abre la ventana correspondiente al hacer clic | Medium |

---

## 📊 Casos de prueba

Los casos de prueba completos (checklist de diseño, método de pago, lógica del botón "Reservar" y flujo de reserva) están disponibles en:

📄 [`casos-de-prueba.xlsx`](./casos-de-prueba.xlsx)

---

## 🛠️ Herramientas utilizadas

- Navegadores: Firefox, Chrome (DevTools)
- Jira (gestión de bugs)
- Google Sheets / Excel (diseño de casos de prueba)
