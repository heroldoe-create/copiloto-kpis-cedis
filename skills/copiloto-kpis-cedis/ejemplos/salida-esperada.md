# Andén Norte · caso FICTICIO · corte 2026-07-31 al cierre

## Control de datos

Definición base v1 del paquete. Unidad: cajas. Objetivo: priorizar excepciones operativas. Exportes completos según declaración del caso [DECLARADO]; cifras calculadas sobre esos exportes, sin auditoría de piso. Horas locales comunes. No hay metas aportadas.

| Archivo | Cobertura | Leídas / retiradas / pendientes / usadas [MEDIDO: conteo filas] | Mapeo y alcance |
|---|---|---|---|
| lineas_pedido.csv | Captura 2026-07-01; compromisos 02–03; embarques al corte | 7 / 0 / 0 / 7 | Encabezados directos; 3 pedidos completos en el exporte |
| tareas_surtido.csv | 2026-07-01 | 7 / 0 / 0 / 7 | minutos de esfuerzo, no horas pagadas |
| citas_recibo.csv | 2026-07-29 a 30 | 5 / 0 / 0 / 5 | una fila por cita |
| conteo_inventario.csv | 2026-07-31 | 10 / 0 / 0 / 10 | una fila por ubicación y SKU; 10 ubicaciones |

Cada archivo satisface leídas = usadas + retiradas + pendientes. Claves únicas, sin duplicados ni tiempos solapados. No unir tareas a líneas ni atribuir el faltante del 2 de julio a recibos del 29 de julio.

## Indicadores

Todos los resultados numéricos de esta tabla son **[MEDIDO]**, calculados de los archivos y operaciones indicados.

| Indicador | Resultado | Numerador / denominador u operación | Archivo y claves |
|---|---:|---|---|
| Fill rate cajas | 93.33 % | 70/75 × 100 | lineas_pedido, líneas 1–7: pedidas 10+5+8+20+10+12+10; surtidas 10+5+8+15+10+12+10 |
| Fill rate líneas | 85.71 % | 6/7 × 100 | lineas_pedido, igualdad en todas salvo línea 4 |
| OTIF de embarque | 66.67 % | 2/3 × 100 | lineas_pedido, PED-A y PED-C cumplen ambas condiciones |
| On time | 66.67 % | 2/3 × 100 | lineas_pedido, PED-B tiene línea 5 tardía |
| In full | 66.67 % | 2/3 × 100 | lineas_pedido, PED-B tiene línea 4 incompleta |
| Productividad total | 39.3 cajas/h | 70/(107/60) | tareas_surtido, tareas 1–7: 33+74 min |
| Exactitud por ubicación | 90.00 % | 9/10 × 100 | conteo_inventario, todas salvo P08-N5-02 |
| Cumplimiento de cita ±15 min | 40.00 % | 2/5 × 100 | citas_recibo, CIT-004 y CIT-005 |
| Retraso firmado promedio | +27.0 min | (50+35+55+5−10)/5 | citas_recibo, CIT-001 a 005 |
| Descarga promedio | 66.0 min | (60+70+80+55+65)/5 | citas_recibo, CIT-001 a 005 |

## Desglose y excepciones

Todas las cantidades y clasificaciones siguientes son **[MEDIDO]** con las operaciones indicadas. Las posibles causas se separan del hecho.

| Pedido | Cajas surtidas/pedidas | Completo | A tiempo | OTIF | Evidencia en lineas_pedido |
|---|---:|---|---|---|---|
| PED-A | 23/23 | Sí | Sí | Sí | líneas 1–3; embarques el día comprometido |
| PED-B | 25/30 | No | No | No | línea 4: 15 de 20; línea 5: embarque 03-jul contra 02-jul |
| PED-C | 22/22 | Sí | Sí | Sí | líneas 6–7; embarques el día comprometido |

Clasificación exhaustiva: solo completo y puntual 2; solo completo 0; solo puntual 0; ninguna condición 1; suma 3 pedidos. Los porcentajes On time e In full coinciden aquí; su producto no es OTIF.

| SKU con faltante | Surtidas/pedidas | Fill cajas | Faltante | Evidencia |
|---|---:|---:|---:|---|
| SKU-0001 | 35/40 | 87.50 % | 5 cajas | lineas_pedido, líneas 1+4+7; faltante solo línea 4 |

SKU-0001 concentra 5/5=100.00 % del faltante y aparece en 1/1 pedidos incompletos, PED-B. No demuestra desabasto: revisar disponibilidad, liberación y ejecución de la línea 4.

| Operador | Tareas | Cajas | Minutos | Cajas/h | Diferencia vs total |
|---|---:|---:|---:|---:|---:|
| OP-13 | 3 | 33 | 33.0 | 60.0 | +52.86 % |
| OP-17 | 4 | 37 | 74.0 | 30.0 | −23.57 % |
| Total | 7 | 70 | 107.0 | 39.3 | 0.00 % |

Fuente tareas_surtido: OP-13 tareas 1–3, OP-17 tareas 4–7. Ritmo = cajas/(minutos/60); diferencia usa el total sin redondear 70×60/107. Cuadre: 33+37=70 cajas y 33+74=107 min. Las tareas suman las mismas 70 cajas surtidas de las líneas del caso; la igualdad no prueba por sí sola correspondencia en otros exportes. No hay datos de dificultad/peso/recorrido: mezcla comparable **[SIN DATO LOCAL]**. No atribuir menor desempeño a OP-17.

| Proveedor | Citas | Dentro ±15 | Cumplimiento | Retraso firmado promedio | Descarga promedio |
|---|---:|---:|---:|---:|---:|
| PRV-07 | 3 | 0 | 0.00 % | +46.7 min = 140/3 | 70.0 min = 210/3 |
| PRV-02 | 2 | 2 | 100.00 % | −2.5 min = −5/2 | 60.0 min = 120/2 |
| Total | 5 | 2 | 40.00 % | +27.0 min = 135/5 | 66.0 min = 330/5 |

Fuente citas_recibo: PRV-07 CIT-001,002,003 con retrasos +50,+35,+55; PRV-02 CIT-004,005 con +5,−10. La muestra de PRV-07 tiene tres llegadas fuera de ventana; investigar agenda y trayecto, sin generalizar a todas sus citas ni afirmar culpa. Descarga no mide espera ni recibo completo.

| Ubicación | SKU | Sistema | Contado | Diferencia contado−sistema | Evidencia |
|---|---|---:|---:|---:|---|
| P08-N5-02 | SKU-0001 | 120 | 118 | −2 cajas | conteo_inventario, fecha 2026-07-31 |

Las otras nueve ubicaciones no tienen diferencias: 9+1=10. No extrapolar la exactitud a ubicaciones no contadas ni autorizar ajuste con un único conteo.

## Acciones

Dueños y plazos **propuestos, por confirmar**; la prioridad organiza la revisión y no representa una meta contractual.

| Prioridad | Acción | Dueño propuesto | Evidencia | Plazo propuesto | Prueba de cierre |
|---|---|---|---|---|---|
| 1 | Revisar reserva, disponibilidad y liberación de línea 4; documentar causa y plan para faltante | Supervisor de surtido | PED-B, 5 cajas faltantes [MEDIDO] | Antes del siguiente corte | Folio de revisión y disposición de las 5 cajas; recálculo del siguiente corte sin reescribir este |
| 2 | Contrastar secuencia de preparación y salida de línea 5 | Jefe de embarques | PED-B embarcado 03-jul vs compromiso 02-jul [MEDIDO] | Antes del siguiente corte | Causa sustentada por registro horario y acción asignada |
| 3 | Contrastar con proveedor y transporte las tres citas fuera de ventana y acordar corrección de agenda | Coordinador de recibo | PRV-07, 0/3 dentro de ventana [MEDIDO] | Antes de su próxima cita | Agenda confirmada y llegada de próxima cita registrada para volver a medir |
| 4 | Recontar y revisar movimientos al corte de P08-N5-02 antes de tramitar un ajuste | Encargado de inventarios | 118−120=−2 cajas [MEDIDO] | Antes del siguiente corte | Reconteo y movimientos documentados; diferencia confirmada o aclarada |
| 5 | Comparar dificultad, recorrido y esperas de tareas de ambos operadores antes de evaluar desempeño | Supervisor de surtido | OP-17 30.0 vs total 39.3 cajas/h [MEDIDO] | Antes del siguiente corte | Muestra comparable registrada con cajas y minutos; nueva tasa por tipo de tarea |

## Pendientes y alcance

| Dato faltante | A quién pedirlo | Decisión que impide |
|---|---|---|
| Mezcla, peso, recorrido y esperas [SIN DATO LOCAL] | Supervisor de surtido | Atribuir la diferencia de ritmo a método o desempeño |
| Inicio/fin de espera, registro y acomodo [SIN DATO LOCAL] | Coordinador de recibo | Medir tiempo total de recibo |
| Metas empresariales [SIN DATO LOCAL] | Gerencia de operación | Clasificar resultados contra objetivo |

Pre-revisión de exportes: cruza y arma evidencia. No sustituye al contador, al agente aduanal ni al SAT; tampoco acredita una auditoría física ni autoriza ajustes de inventario.

Basado en una skill de Heroldo Escobedo — heroldo.org
