# Copiloto de KPIs de CEDIS

De tus exportes del sistema de almacén o de administración a tablas listas para pegar en tu reporte: fill rate (porcentaje surtido), OTIF (pedidos completos y embarcados a tiempo), cajas por hora por operador, exactitud por ubicación y tiempos de recibo. Incluye excepciones por folio y acciones con dueño propuesto y prueba de cierre. Precio previsto de uso empresarial: **USD 20**; paquete construido, pendiente del ciclo de revisión antes de publicarse.

## Úsalo en tres pasos

1. Activa `copiloto-kpis-cedis` con el conector de Agensi en claude.ai cuando esté disponible, o sube `copiloto-kpis-cedis.zip` como skill en un chat que admita skills. El ZIP lleva `SKILL.md` en su raíz.
2. Adjunta tus CSV o pega sus tablas. Puedes empezar con cualquiera: líneas de pedidos, tareas, conteos o citas. Si tienes periodo, corte o definición empresarial, inclúyelos en el mensaje; no necesitas configurar nada.
3. Escribe: «Calcula los KPIs con lo recibido y entrega las tablas, excepciones y acciones listas para copiar». Para probar sin datos propios: «Usa el caso ficticio incluido de Andén Norte y entrega su reporte».

No requiere terminal, scripts, API ni acceso directo a tu sistema. Cada archivo necesario viaja dentro del ZIP. El caso también está en [entrada completa](skills/copiloto-kpis-cedis/ejemplos/entrada-completa.md), pegable en un mensaje, y su [salida esperada](skills/copiloto-kpis-cedis/ejemplos/salida-esperada.md) permite revisar las cuentas a mano.

## Qué necesitas y qué recibes

| Lo que adjuntas | Resultado |
|---|---|
| Líneas con pedido, cantidades pedidas/surtidas y fechas compromiso/embarque | Fill rate y OTIF de embarque, detalle por pedido y faltantes |
| Tareas con operador, cajas y minutos | Ritmos ponderados por tiempo, sin atribuir culpas por velocidad |
| Conteo físico contra sistema al mismo corte | Exactitud por ubicaciones contadas y diferencias por componente |
| Citas con proveedor, fecha/hora de cita y llegada y duración de descarga | Cumplimiento ±15 min, retraso firmado y descarga, por proveedor |

Los encabezados equivalentes se mapean. Datos faltantes o contradictorios dejan pendientes concretos y los demás cálculos avanzan. No se inventan ceros, compromisos, metas ni causas. Si el chat no lee el adjunto completo, declara la cobertura sin extrapolar. La exactitud describe la muestra contada; el OTIF mide embarque, no entrega. No se garantiza que el exporte refleje toda la operación.

Pre-revisa, cruza y arma evidencia. **No sustituye al contador, al agente aduanal ni al SAT**, ni acredita una auditoría física. No modifica sistemas ni autoriza ajustes. Usa datos que tengas autorización para compartir en tu chat y reemplaza identificadores personales innecesarios por códigos. Todos los datos de demostración son **FICTICIOS de Andén Norte**.

Las fórmulas y controles están en [definiciones](skills/copiloto-kpis-cedis/references/definiciones.md), y cada fuente tiene URL y fecha de consulta en [fuentes](skills/copiloto-kpis-cedis/references/fuentes.md).

---


## Licencia

**Propiedad intelectual de Heroldo Escobedo**, con el código a la vista ([Licencia de uso de Heroldo 1.0](LICENSE)):

- **Uso personal: gratis.** Léelo, pruébalo y adáptalo para aprender o en tus propios datos.
- **Uso en una empresa o con fines de lucro: solo con compra.** Cómpralo en [Agensi](https://agensi.io/skills/copiloto-kpis-cedis)
  o escribe a heroldo@lolo-enterprises.com. La compra cubre a tu empresa.
- **Siempre se cita la fuente:** «Basado en una skill de Heroldo Escobedo — heroldo.org».
- No se revende ni se vuelve a publicar.

> **In English:** Source-available, not open source. Free for personal use. Business use requires purchase on
> [Agensi](https://agensi.io/skills/copiloto-kpis-cedis). Attribution to Heroldo Escobedo — heroldo.org is always required.
