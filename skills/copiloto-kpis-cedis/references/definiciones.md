# Contrato de cálculo · versión 1 · 2026-10-29

Definiciones operativas derivadas de las fuentes F1–F8 de [fuentes.md](fuentes.md). Las reglas para datos incompletos son convenciones explícitas de este paquete, no normas de la industria.

## Entradas mínimas y grano

| Archivo lógico | Una fila representa | Campos necesarios |
|---|---|---|
| Líneas | línea única de pedido, resumen acumulado al corte | linea_id, pedido, sku, cajas_pedidas, cajas_surtidas; para puntualidad fecha_compromiso y fecha_embarque; fecha_pedido para cobertura |
| Tareas | tarea única de un operador | tarea_id, fecha, operador, cajas, minutos; inicio para detectar solapes |
| Conteo | componente SKU/lote de una ubicación en un evento de conteo | ubicacion, sku, sistema_cajas, contado_cajas, fecha_conteo; lote/evento si hay más de uno |
| Citas | cita única, no una fila por SKU descargado | cita_id, proveedor, hora_cita, hora_llegada, minutos_descarga |

Puede mapearse piezas a cajas solo con factor explícito por SKU. No mezcles unidades. Conserva identificadores con ceros iniciales. Reconoce coma o punto y coma como separador y decimales locales por contexto inequívoco; no conviertas un dato ambiguo adivinando. Fechas de pedidos se comparan por día; citas necesitan fecha y hora completas, en la misma zona declarada. Fechas ambiguas o zonas incompatibles quedan pendientes. Mantén minutos decimales.

Por defecto se usa el universo completo adjunto, incluyendo pendientes al corte. Si hay filtro, explica sobre qué fecha aplica; para OTIF conserva todas las líneas de cada pedido seleccionado, no solo las del SKU filtrado. Un exporte que omite líneas/pedidos no embarcados no acredita servicio total: rotula «subconjunto exportado». No supongas cancelaciones: solo excluye cancelaciones explícitas y documentadas antes del corte; informa sus folios y conteo.

## Integridad sin esconder errores

- Duplicado idéntico de clave y contenido: conserva una copia, informa clave y cantidad retirada. Misma clave con valores distintos: no elijas uno; deja sus filas pendientes en el indicador afectado. Sin clave fiable, no deduzcas identidad por pedido+SKU: puede haber dos líneas legítimas.
- Si hay eventos parciales, agrupa por linea_id solo cuando el grano esté explícito. Cantidad pedida repetida se toma una vez; suma surtidos únicamente si son movimientos incrementales únicos. No sumes fotos acumuladas. Fecha de embarque es la del último evento necesario. Sin esa distinción el indicador afectado queda pendiente.
- Cantidades negativas, pedidas cero, números vacíos y tiempos negativos son pendientes, nunca ceros implícitos. Minutos de tarea cero es inválido incluso con cajas positivas. Excedentes positivos se conservan y señalan; no topes el fill rate a 100 % ni compenses faltantes para decidir pedido completo.
- Un pedido con alguna línea inválida se considera pendiente en OTIF/In full; no calcules un pedido completo usando solo sus líneas buenas. Para puntualidad, un faltante de fecha es desconocido salvo que el estado confirme «no embarcado». Si está explícitamente no embarcado y ya venció al corte, cuenta como no puntual; antes de vencer está abierto y se muestra separado. Sin corte suficiente, no infieras su estado.
- Tasas con registros pendientes se rotulan «sobre N válidos de M», con lista de excluidos; no son el resultado del universo completo. Se puede informar límite inferior/superior solo con fórmula explícita y desconocidos contados.
- Tareas simultáneas del mismo operador requieren confirmar si son minutos de esfuerzo o tiempo transcurrido compartido. Hasta aclararlo no sumes duración solapada para un ritmo válido. No sustituyas horas de tarea por horas pagadas.
- Inventario: compara sistema congelado y conteo al mismo corte. No sumes reconteos ni días distintos. Sin instrucción contraria, usa la última fecha de conteo disponible e indica cuáles se apartaron. Si hay varios eventos ese día sin secuencia clara, quedan pendientes. Si una ubicación tiene varios SKU/lotes, es exacta solo si TODOS coinciden; +2 y −2 no se compensan. Si faltan componentes de su conteo, la ubicación queda pendiente. El resultado describe ubicaciones contadas, no todo el inventario.
- Recibo: varias líneas SKU de la misma cita solo se consolidan si horas/proveedor/duración coinciden; duración de cita repetida se toma una vez. No sumes descargas repetidas. Citas sin llegada quedan pendientes; si consta inasistencia tras cierre de ventana, cuentan como no cumplidas, sin retraso ni descarga imputados. Cada promedio declara su propio n.

## Fórmulas fijas

| Indicador | Operación | Fuente |
|---|---|---|
| Fill rate cajas | 100 × suma surtidas / suma pedidas, mismas líneas válidas | F2 |
| Fill rate líneas | 100 × líneas con surtidas = pedidas / líneas válidas | F2 |
| In full | 100 × pedidos con igualdad en TODAS sus líneas / pedidos evaluables | F3, F7 |
| On time | 100 × pedidos con embarque ≤ compromiso en TODAS sus líneas / pedidos evaluables para puntualidad | F3, F7 |
| OTIF de embarque | 100 × pedidos completos Y puntuales / pedidos evaluables en ambas condiciones | F3, F7 |
| Productividad | suma cajas / (suma minutos / 60), por operador y total | F4 |
| Diferencia vs total | 100 × (ritmo operador − ritmo total) / ritmo total, con cifras sin redondear | F4 |
| Exactitud por ubicación | 100 × ubicaciones sin ninguna diferencia / ubicaciones válidas contadas en ese corte | F7 |
| Cumplimiento cita | 100 × citas con −15 ≤ llegada−cita ≤ +15 minutos / citas evaluables | F5, F7 |
| Retraso firmado | promedio de (llegada−cita) en minutos: anticipos negativos, no truncar | F5 |
| Descarga | suma minutos_descarga / citas con duración válida | F5 |

OTIF aquí mide salida del almacén, **no entrega al cliente**. No uses fecha de factura como embarque. Completo requiere igualdad por línea: un excedente en otra línea nunca compensa un faltante. On time e In full pueden tener universos distintos por datos faltantes: muéstralos, no los multipliques para estimar OTIF. El ritmo global es ponderado por minutos, no promedio simple de ritmos.

La ventana de cita es inclusiva: −15 y +15 cumplen; −16 y +16 no. El texto narrativo de la guía F5 es ambiguo respecto a anticipos: manda su fórmula ABS(retraso) ≤ 15. La descarga no es el tiempo total de recibo: sin inicio/fin de espera, descarga, registro y acomodo, esos tramos quedan [SIN DATO LOCAL]. No conviertas retraso en tiempo de espera.

Exactitud por unidades no se calcula por defecto: no hay fórmula fijada en estas fuentes. Ocupación, cobertura en días y ABC (F6) son contexto diferente y quedan fuera de los cinco grupos; no equivalen a exactitud.

## Controles de borde para revisar una respuesta

| Caso | Resultado correcto |
|---|---|
| Dos líneas 10/8 y 10/12 en un pedido | Fill cajas 100 %; líneas 0 %; In full y OTIF 0 %, aunque ambas salgan puntuales |
| Compromiso y embarque el mismo día | Puntual |
| Sin filas válidas o denominador cero | No calculable; nunca 0 % |
| Dos operadores 10 cajas/10 min y 10 cajas/30 min | Total 20/(40/60)=30 cajas/h, no promedio 40 |
| Una ubicación, dos SKU con diferencias +2 y −2 | Ubicación inexacta |
| Mismo conteo repetido en otra fecha | No suma otra ubicación ni otro evento al corte elegido |
| Falta tareas, existen citas | Calcula recibo, productividad sin dato |
| Fecha de embarque vacía sin estado | Puntualidad pendiente; no convertir en puntual |
