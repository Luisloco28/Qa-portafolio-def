# 🔌 Pruebas de API — Urban Grocers

Proyecto de pruebas funcionales sobre la **API REST de Urban Grocers**, una plataforma de entrega de kits de comestibles. Las pruebas se ejecutaron con **Postman**, cubriendo dos endpoints clave: la gestión de productos dentro de un kit y el cálculo de disponibilidad/costo del servicio de entrega "Order and Go".

---

## 🎯 Objetivo

Validar que la API cumpla con las reglas de negocio definidas en los requisitos del backend, incluyendo límites de productos por kit, validación de tipos de datos y cálculo de disponibilidad de entrega según horario, peso y cantidad de productos.

---

## 🔍 Proceso de trabajo

1. **Análisis de requisitos** — Revisión del documento de requisitos del backend para identificar reglas de negocio, límites y formatos esperados.
2. **Diseño de casos de prueba** — Cobertura mediante:
   - Casos positivos y negativos
   - Clases de equivalencia
   - Valores límite (límite inferior, superior, y valores adyacentes)
   - Validación de tipos de datos incorrectos (string, null, objetos, campos faltantes)
3. **Ejecución** — Pruebas funcionales con **Postman** contra un servidor de pruebas.
4. **Reporte de bugs** — Documentación en Jira con pasos de reproducción, resultado actual y esperado.

---

## 📦 Endpoint 1 — Agregar productos a un kit
`POST /api/v1/kits/:id/products`

**15 casos de prueba** — 7 Passed / 8 Failed

| ID | Caso de prueba | Estado | Bug |
|----|-----------------|--------|-----|
| 1.0 | Agregar un producto existente al kit | ✅ Passed | |
| 2.0 | Agregar 30 productos únicos (límite máximo) | ✅ Passed | |
| 3.0 | Agregar 31 productos únicos (excede el límite) | ✅ Passed | |
| 4.0 | Agregar producto con ID no existente → 400 | ❌ Failed | S4-2 |
| 5.0 | Agregar productos a kit con ID no existente → 404 | ✅ Passed | |
| 6.0 | Enviar id como string → 400 | ❌ Failed | S4-3 |
| 7.0 | Agregar 29 productos únicos | ✅ Passed | |
| 8.0 | La cantidad no afecta el conteo de IDs únicos | ✅ Passed | |
| 9.0 | productsList vacío → 400 | ❌ Failed | S4-4 |
| 10.0 | Body sin campo productsList → 400 | ❌ Failed | S4-5 |
| 11.0 | productsList como null → 400 | ❌ Failed | S4-6 |
| 12.0 | productsList como objeto → 400 | ❌ Failed | S4-7 |
| 13.0 | quantity negativa → 400 | ❌ Failed | S4-8 |
| 14.0 | quantity = 0 no modifica el kit | ✅ Passed | |
| 15.0 | id de producto = 0 → 400 | ❌ Failed | S4-9 |

---

## 🚚 Endpoint 2 — Servicio de entrega "Order and Go"
`POST /order-and-go/v1/delivery`

**24 casos de prueba** — 11 Passed / 13 Failed

Cobertura de clases de equivalencia y valores límite para `deliveryTime` (08-22), `productsCount` (0-15) y `productsWeight` (0-6 kg).

| ID | Caso de prueba | Estado | Bug |
|----|-----------------|--------|-----|
| 1.0 | deliveryTime límite inferior (8) | ✅ Passed | |
| 2.0 | deliveryTime límite superior (22) | ✅ Passed | |
| 3.0 | deliveryTime por debajo del límite (7) → debería ser false | ❌ Failed | S4-10 |
| 4.0 | deliveryTime por encima del límite (23) → debería ser false | ❌ Failed | S4-10 |
| 5.0 | deliveryTime como string → 400 | ❌ Failed | S4-11 |
| 6.0 | deliveryTime como null → 400 | ❌ Failed | S4-12 |
| 7.0 | deliveryTime omitido → 400 | ❌ Failed | S4-13 |
| 8.0 | productsCount límite inferior (0) | ✅ Passed | |
| 9.0 | productsCount límite superior (15) | ✅ Passed | |
| 10.0 | productsCount por encima del límite → debería ser false | ❌ Failed | S4-14 |
| 11.0 | productsCount como string → 400 | ❌ Failed | S4-15 |
| 12.0 | productsCount como null → 400 | ❌ Failed | S4-15 |
| 13.0 | productsCount omitido → 400 | ❌ Failed | S4-16 |
| 14.0 | productsWeight límite inferior (0) | ✅ Passed | |
| 15.0 | productsWeight límite superior (6) | ✅ Passed | |
| 16.0 | productsWeight por encima del límite (6.1) → debería ser false | ❌ Failed | S4-17 |
| 17.0 | productsWeight como string → 400 | ❌ Failed | S4-18 |
| 18.0 | productsWeight como null → 400 | ❌ Failed | S4-18 |
| 19.0 | productsWeight omitido → 400 | ❌ Failed | S4-19 |
| 20.0 | deliveryTime una unidad mayor al límite inferior (9) | ✅ Passed | |
| 21.0 | deliveryTime una unidad menor al límite superior (21) | ✅ Passed | |
| 22.0 | productsWeight una unidad mayor al límite inferior (0.1) | ✅ Passed | |
| 23.0 | productsWeight una unidad menor al límite superior del primer rango (2.9) | ✅ Passed | |
| 24.0 | productsWeight en el límite superior del primer rango (3) | ✅ Passed | |

---

## 🐛 Resumen de bugs encontrados (18 en total)

Los hallazgos más relevantes:
- La API **no valida tipos de datos** en varios campos obligatorios (string, null, objetos), devolviendo 200 OK o 500 Internal Server Error en lugar de 400 Bad Request.
- El campo `isItPossibleToDeliver` **no refleja correctamente** los límites de horario, cantidad de productos y peso definidos en los requisitos.
- El endpoint para agregar productos **no valida la existencia del producto** ni rechaza valores como `id=0` o `quantity` negativa.

---

## 📊 Casos de prueba

Los casos de prueba completos con datos de entrada, pasos, resultados y enlaces a Jira están disponibles en:

📄 [`Proyecto_Sprint4_casos_de_prueba.xlsx`](./Proyecto_Sprint4_casos_de_prueba.xlsx)

---

## 🛠️ Herramientas utilizadas

- Postman
- Jira (gestión de bugs)
- Google Sheets / Excel (diseño de casos de prueba)
