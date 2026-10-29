# Caso FICTICIO · Andén Norte

Calcula los cinco grupos de KPIs, explica las excepciones y entrega acciones con dueño propuesto. Usa todos los registros de cada archivo sin unirlos entre sí. Corte del reporte: 2026-07-31 al cierre; fechas y horas locales comunes, sin cambio de zona. Exportes declarados completos para este caso: pedidos capturados el 1 de julio con todas sus líneas y embarques al corte; tareas del 1 de julio; citas del 29–30 de julio; conteo completo de las diez ubicaciones indicadas del 31 de julio. Son coberturas distintas: no infieras causalidad entre ellas. No hay cancelaciones ni metas declaradas. Las cantidades están en cajas. Los tiempos de tarea representan minutos de esfuerzo exclusivos sin solapes; cada conteo compara el sistema congelado con el físico del mismo corte. No hay datos de peso, recorrido o dificultad de tareas.

## citas_recibo.csv

```csv
cita_id,fecha,proveedor,anden,hora_cita,hora_llegada,minutos_descarga
CIT-001,2026-07-29,PRV-07,3,2026-07-29T08:00,2026-07-29T08:50,60
CIT-002,2026-07-29,PRV-07,3,2026-07-29T10:00,2026-07-29T10:35,70
CIT-003,2026-07-30,PRV-07,4,2026-07-30T14:00,2026-07-30T14:55,80
CIT-004,2026-07-30,PRV-02,1,2026-07-30T09:00,2026-07-30T09:05,55
CIT-005,2026-07-30,PRV-02,2,2026-07-30T11:00,2026-07-30T10:50,65
```

## conteo_inventario.csv

```csv
ubicacion,sku,sistema_cajas,contado_cajas,fecha_conteo
P01-N1-01,SKU-0002,200,200,2026-07-31
P02-N1-02,SKU-0004,150,150,2026-07-31
P03-N2-01,SKU-0005,180,180,2026-07-31
P04-N2-02,SKU-0003,90,90,2026-07-31
P05-N3-01,SKU-0002,60,60,2026-07-31
P06-N3-02,SKU-0004,240,240,2026-07-31
P07-N4-01,SKU-0005,75,75,2026-07-31
P08-N5-02,SKU-0001,120,118,2026-07-31
P09-N5-01,SKU-0003,310,310,2026-07-31
P10-N4-02,SKU-0001,45,45,2026-07-31
```

## lineas_pedido.csv

```csv
linea_id,pedido,fecha_pedido,tipo_cliente,sku,cajas_pedidas,cajas_surtidas,fecha_compromiso,fecha_embarque
1,PED-A,2026-07-01,Tienda de barrio,SKU-0001,10,10,2026-07-02,2026-07-02
2,PED-A,2026-07-01,Tienda de barrio,SKU-0002,5,5,2026-07-02,2026-07-02
3,PED-A,2026-07-01,Tienda de barrio,SKU-0003,8,8,2026-07-02,2026-07-02
4,PED-B,2026-07-01,Mayorista,SKU-0001,20,15,2026-07-02,2026-07-02
5,PED-B,2026-07-01,Mayorista,SKU-0004,10,10,2026-07-02,2026-07-03
6,PED-C,2026-07-01,Minisúper,SKU-0005,12,12,2026-07-03,2026-07-03
7,PED-C,2026-07-01,Minisúper,SKU-0001,10,10,2026-07-03,2026-07-03
```

## tareas_surtido.csv

```csv
tarea_id,fecha,operador,pedido,sku,cajas,inicio,minutos
1,2026-07-01,OP-13,PED-A,SKU-0001,10,2026-07-01T12:41,10.0
2,2026-07-01,OP-13,PED-A,SKU-0003,8,2026-07-01T13:05,8.0
3,2026-07-01,OP-13,PED-B,SKU-0001,15,2026-07-01T14:20,15.0
4,2026-07-01,OP-17,PED-A,SKU-0002,5,2026-07-01T12:41,12.0
5,2026-07-01,OP-17,PED-B,SKU-0004,10,2026-07-01T15:10,22.0
6,2026-07-01,OP-17,PED-C,SKU-0005,12,2026-07-01T16:00,20.0
7,2026-07-01,OP-17,PED-C,SKU-0001,10,2026-07-01T16:40,20.0
```

