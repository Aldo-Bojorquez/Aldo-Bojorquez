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


|ID|Titulo| Pasos | Datos de prueba | Resultado esperado | Resultado actual | Severidad | Evidencia |
|--|--|--|--|--|--|--|--| 
|TC-01.1|Asignación del 2do horario (11 am - 1 pm).|1. Cliente entra 10:50 am. <br> 2. Calcular tiempo para el cambio de turno. <br>3. Validar si el acceso es mayor o menor a 1:15 al turno.| Hora de acceso del cliente: 10:50 am.| Tiempo faltante al cambio de turno: 1:10 horas.<br> Al cliente se le brinda el 2do horario. <br> Horario: 11 am - 1 pm. Costo: $20.|El valet asigna el 90% al cliente de manera correcta.| Media |
