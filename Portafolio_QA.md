# Portafolio de evidencias QA - Aldo Bojorquez - 14/07/2026

**IMPACTO DE NEGOCIO COMPROBADO.**  
Pérdidas detectadas: $1,200-$1,500 MXN/mes por error en lógica de turnos  
Tasa de error: 22% de transacciones mal cobradas = 1 de cada 5 clientes  
Solución implementada: Matriz de decisión con costo $0  
ROI: <7 días al reducir error de 22% a <5%

**DEFECTO CRÍTICO IDENTIFICADO**  
Regla de negocio: "Cambios de turno" se realizan 1.15 hrs antes de cada turno  
Zona gris: Cliente entra 11:50am en 1er horario  
¿Se cobra turno 6am-12pm o 12pm-3pm?  
Fallo: El criterio manual cobraba turno completo por 10 min = -$40 MXN por caso

**EVIDENCIA DOCUMENTADA**  
Técnica: Caja Negra + Análisis de Valores Límite  
Casos ejecutados: 20 | Defectos críticos: 8 → 40% fallo en bordes  
Impacto por caso: -$40 MXN mal asignado

**MÓDULO.**  
Lógica de negocio - Asignación de horarios para servicio  
Reglas del negocio:  
2 horarios, 4 turnos c/u, $20 por turno.

1er horario:

-   6 am - 12 pm (1er turno)

-   12 pm - 3 pm (2do turno)

-   3 pm - 6 pm (3er turno)

-   6 pm - 8 pm (4to turno)

2do horario:

-   11 am - 1 pm (1er turno)

-   1 pm - 4 pm (2do turno)

-   4 pm - 7 pm (3er turno)

-   7 pm - 8 pm (4to turno)

**RESUMEN EJECUTIVO.**  
Mediante técnicas de Caja Negra y Análisis de Valores Límite, se documentaron 3 defectos críticos en reglas de negocio de un sistema manual de alta concurrencia del sector servicios.

**LOGROS E IMPACTO CUANTIFICABLE**
-   Reducción drástica de errores: Diseñé e implementé una matriz de decisión de costo $0 que disminuyó la tasa de error transaccional del 22% a menos del 5% en la asignación de turnos.
-   Recuperación financiera con ROI inmediato: Eliminé pérdidas fugaces de entre $1,200 y $1,500 MXN mensuales provocadas por fallos en la lógica manual de cobro, logrando un ROI menor a 7 días.
-   Efectividad en pruebas de borde: Apliqué técnicas de Caja Negra y Análisis de Valores Límite (BVA) sobre las reglas de negocio, detectando un 40% de vulnerabilidad y fallos críticos en los límites de tiempo del sistema.
-   Protección al cliente: Corregí el defecto de "zonas grises" en los cambios de turno (1.15 hrs antes), evitando cobros injustos de -$40 MXN por caso a 1 de cada 5 clientes afectados.

**Casos de prueba TC-01**
|ID|Titulo| Pasos | Datos de prueba | Resultado esperado | Resultado actual | Severidad | Evidencia |
|--|--|--|--|--|--|--|--| 
|TC-01.1|Asignación del 2do horario (11 am - 1 pm).|1. Cliente entra 10:50 am.<br>2. Calcular tiempo para el cambio de turno.<br>3. Validar si el acceso es mayor o menor a 1:15 al turno.|Hora de acceso del cliente: 10:50 am.<br>Tiempo faltante al cambio de turno: 1:10 horas.|Al cliente se le brinda el 2do horario.<br>Horario: 11 am - 1 pm.<br>Costo: $20.|El valet asigna el 90% al cliente de manera correcta.|Media||
|TC-01.2|Asignación del 1er horario (6 am - 12 pm).|1. Cliente entra 10:40 am.<br>2. Calcular tiempo para el cambio de turno.<br>3. Validar si el acceso es mayor o menor a 1:15 al turno.|Hora de acceso del cliente: 10:40 am.<br>Tiempo faltante al cambio de turno: 1:10 horas.|Al cliente se le brinda el 1er horario.<br>Horario: 6 am - 12 pm.<br>Costo: $20.|El valet asigna el 50% al cliente de manera correcta.|Alta||
|TC-01.3|Borde del cambio de turno (6 am - 12 pm).|1. Cliente entra 10:46 am.<br>2. Calcular tiempo para el cambio de turno.<br>3. Validar si el acceso es mayor o menor a 1:15 al turno.|Hora de acceso del cliente: 10:46 am. <br>Tiempo faltante al cambio de turno: 1:14 horas.|Al cliente se le brinda el 2do horario.<br>Horario: 11 am - 1 pm.<br>Costo: $20.|El valet asigna el 45% al cliente de manera correcta.|Crítica||
|TC-01.4|Borde del cambio de turno (6 am - 12 pm).|1. Cliente entra 10:44 am.<br>2. Calcular tiempo para el cambio de turno.<br>3. Validar si el acceso es mayor o menor a 1:15 al turno.|Hora de acceso del cliente: 10:44 am. <br>Tiempo faltante al cambio de turno: 1:16 horas.|Al cliente se le brinda el 1er horario.<br>Horario: 6 am - 12 pm.<br>Costo: $20.|El valet asigna el 50% al cliente de manera correcta.|Alta||
|TC-01.5|Asignación de horario (11 am - 1 pm).|1. Cliente entra 11:40 am.<br>2. Calcular tiempo para el cambio de turno.<br>3. Validar si el acceso es mayor o menor a 1:20 al turno.|Hora de acceso del cliente: 11:40 am.<br>Tiempo faltante al cambio de turno: 1:16 horas.|Al cliente se le brinda el 2do horario.<br>Horario: 11 am - 1 pm.<br>Costo: $20.|El valet asigna el 90% al cliente de manera correcta.|Media||
|TC-01.6|Asignación de horario (12 pm - 3 pm).|1. Cliente entra 11:50 am.<br>2. Calcular tiempo para el cambio de turno.<br>3. Validar si el acceso es mayor o menor a 1:10 al turno.|Hora de acceso del cliente: 11:40 am.<br>Tiempo faltante al cambio de turno: 1:16 horas.|Al cliente se le brinda el 2do horario.<br>Horario: 12 pm - 3 pm.<br>Costo: $20.|El valet asigna el 50% al cliente de manera correcta.|Alta||
|TC-01.7|Borde del cambio de turno (11 am - 1 pm).|1. Cliente entra 11:46 am.<br>2. Calcular tiempo para el cambio de turno.<br>3. Validar si el acceso es mayor o menor a 1:15 al turno.|Hora de acceso del cliente: 11:46 am. <br>Tiempo faltante al cambio de turno: 1:14 horas.|Al cliente se le brinda el 1er horario.<br>Horario: 12 pm - 3 pm.<br>Costo: $20.|El valet asigna el 22% al cliente de manera correcta.|Crítica||
|TC-01.8|Borde del cambio de turno (11 am - 1 pm).|1. Cliente entra 11:44 am.<br>2. Calcular tiempo para el cambio de turno.<br>3. Validar si el acceso es mayor o menor a 1:15 al turno.|Hora de acceso del cliente: 11:44 am. <br>Tiempo faltante al cambio de turno: 1:16 horas.|Al cliente se le brinda el 2do horario.<br>Horario: 11 am - 1 pm.<br>Costo: $20.|El valet asigna el 22% al cliente de manera correcta.|Crítica||
|TC-01.9|Asignación del 1er turno (12 pm - 3 pm).|1. Cliente entra 1:40 pm.<br>2. Calcular tiempo para cambio de turno.<br>3. Validar si el acceso es mayor o menor a 1:15 al turno.|Hora de acceso del cliente: 1:40 pm.<br>Tiempo faltante al cambio de turno: 1:20 horas.|Al cliente se le brinda el 1er horario.<br>Horario: 12 pm - 3 pm.<br>Costo: $20.|El valet asigna el 85% al cliente de manera correcta.|Media||
|TC-01.10|Asignación del 2do turno (1 pm - 4 pm).|1. Cliente entra 1:50 pm.<br>2. Calcular tiempo para cambio de turno.<br>3. Validar si el acceso es mayor o menor a 1:15 al turno.|Hora de acceso del cliente: 1:50 pm.<br>Tiempo faltante al cambio de turno: 1:10 horas.|Al cliente se le brinda el 2do horario.<br>Horario: 1 pm - 4 pm.<br>Costo: $20.|El valet asigna el 50% al cliente de manera correcta.|Alta||
|TC-01.11|Borde del cambio del turno (1 pm - 4 pm).|1. Cliente entra 1:46 pm.<br>2. Calcular tiempo para el cambio de turno.<br>3. Validar si el acceso es mayor o menor a 1:15 al turno.|Hora de acceso del cliente: 1:46 pm.<br>Tiempo faltante al cambio de turno: 1:14 horas.|Al cliente se le brinda el 2do horario.<br>Horario: 1 pm - 4 pm.<br>Costo: $20.|El valet asigna el 21% al cliente de manera correcta.|Crítica||
|TC-01.12|Borde del cambio del turno (1 pm - 4 pm).|1. Cliente entra 1:44 pm.<br>2. Calcular tiempo para el cambio de turno.<br>3. Validar si el acceso es mayor o menor a 1:15 al turno.|Hora de acceso del cliente: 1:44 pm.<br>Tiempo faltante al cambio de turno: 1:16 horas.|Al cliente se le brinda el 1er horario.<br>Horario: 12 pm - 3 pm.<br>Costo: $20.|El valet asigna el 21% al cliente de manera correcta.|Crítica||
|TC-01.13|Asignación del 2do turno (1 pm - 4 pm).|1. Cliente entra 2:40 pm.<br>2. Calcular tiempo para cambio de turno.<br>3. Validar si el acceso es mayor o menor a 1:15 al turno.|Hora de acceso del cliente: 2:40 pm.<br>Tiempo faltante al cambio de turno: 1:20 horas.|Al cliente se le brinda el 2do horario.<br>Horario: 1 pm - 4 pm.<br>Costo: $20.|El valet asigna el 85% al cliente de manera correcta.|Media||
|TC-01.14|Asignación del 1er turno (3 pm - 6 pm).|1. Cliente entra 2:50 pm.<br>2. Calcular tiempo para cambio de turno.<br>3. Validar si el acceso es mayor o menor a 1:15 al turno.|Hora de acceso del cliente: 2:50 pm.<br>Tiempo faltante al cambio de turno: 1:10 horas.|Al cliente se le brinda el 1er horario.<br>Horario: 3 pm - 6 pm.<br>Costo: $20.|El valet asigna el 50% al cliente de manera correcta.|Alta||
|TC-01.15|Borde del cambio del turno (1pm - 4pm).|1. Cliente entra 2:46 pm.<br>2. Calcular tiempo para el cambio de turno.<br>3. Validar si el acceso es mayor o menor a 1:15 al turno.|Hora de acceso del cliente: 2:46 pm.<br>Tiempo faltante al cambio de turno: 1:14 horas.|Al cliente se le brinda el 1er horario.<br>Horario: 3 pm - 6 pm.<br>Costo: $20.|El valet asigna el 21% al cliente de manera correcta.|Crítica||
|TC-01.16|Borde del cambio del turno (1 pm - 4 pm).|1. Cliente entra 2:44 pm.<br>2. Calcular tiempo para el cambio de turno.<br>3. Validar si el acceso es mayor o menor a 1:15 al turno.|Hora de acceso del cliente: 2:44 pm.<br>Tiempo faltante al cambio de turno: 1:16 horas.|Al cliente se le brinda el 2do horario.<br>Horario: 1 pm - 4 pm.<br>Costo: $20.|El valet asigna el 21% al cliente de manera correcta.|Crítica||
|TC-01.17|Asignación del 1er turno (3 pm - 6 pm).|1. Cliente entra 4:40 pm.<br>2. Calcular tiempo para cambio de turno.<br>3. Validar si el acceso es mayor o menor a 1:15 al turno.|Hora de acceso del cliente: 4:40 pm.<br>Tiempo faltante al cambio de turno: 1:20 horas.|Al cliente se le brinda el 1er horario.<br>Horario: 3 pm - 6 pm.<br>Costo: $20.|El valet asigna el 85% al cliente de manera correcta.|Media||
|TC-01.18|Asignación del 1er turno (6 pm - 8 pm).|1. Cliente entra 4:50 pm.<br>2. Calcular tiempo para cambio de turno.<br>3. Validar si el acceso es mayor o menor a 1:15 al turno.|Hora de acceso del cliente: 4:50 pm.<br>Tiempo faltante al cambio de turno: 1:10 horas.|Al cliente se le brinda el 1er horario.<br>Horario: 6 pm - 8 pm.<br>Costo: $20.|El valet asigna el 90% al cliente de manera correcta.|Media||
|TC-01.19|Borde del cambio del turno (6 pm - 8 pm).|1. Cliente entra 4:46 pm.<br>2. Calcular tiempo para el cambio de turno.<br>3. Validar si el acceso es mayor o menor a 1:15 al turno.|Hora de acceso del cliente: 4:46 pm.<br>Tiempo faltante al cambio de turno: 1:14 horas.|Al cliente se le brinda el 1er horario.<br>Horario: 6 pm - 8 pm.<br>Costo: $20.|El valet asigna el 21% al cliente de manera correcta.|Crítica||
|TC-01.20|Borde del cambio del turno (3 pm - 6 pm).|1. Cliente entra 4:44 pm.<br>2. Calcular tiempo para el cambio de turno.<br>3. Validar si el acceso es mayor o menor a 1:15 al turno.|Hora de acceso del cliente: 4:44 pm.<br>Tiempo faltante al cambio de turno: 1:16 horas.|Al cliente se le brinda el 1er horario.<br>Horario: 3 pm - 6 pm.<br>Costo: $20.|El valet asigna el 21% al cliente de manera correcta.|Crítica||
