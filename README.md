# SolicitudesReembolso

# Proceso RPA – Procesamiento de Solicitudes de Reembolso

Este proyecto desarrollado en **Automation Anywhere 360** automatiza el procesamiento de solicitudes de reembolso enviados por los empleados a través de archivos Excel. El bot se encarga de validar las solicitudes, generar un resumen de ejecución y mantener una estructura organizada de carpetas, incluyendo logs y plantillas.

---

## 📋 Descripción del Caso

Los empleados guardan archivos `.xlsx` con solicitudes de reembolso en una carpeta compartida. Cada archivo contiene los siguientes campos:

- **NOMBRE**: Nombre del empleado  
- **FECHA**: Fecha del gasto  
- **DESCRIPCION**: Detalle del gasto  
- **MONTO**: Valor del gasto  
- **ESTADO**: Estado de aprobación (`pendiente`, `aprobado`, `rechazado`)

---

## ✅ Requerimientos Funcionales

1. **Leer archivos**
   - El bot lee todos los archivos `.xlsx` de la carpeta `inputs/`.

2. **Validar solicitudes**
   - Por cada fila con `ESTADO = pendiente`:
     - Validar que el `MONTO` sea mayor a 0.
     - Validar que la `FECHA` no sea posterior al día actual.
     - Si ambas validaciones se cumplen, el `ESTADO` cambia a `aprobado`, caso contrario a `rechazado`.

3. **Generar resumen**
   - Crear un archivo de resumen basado en `resources/Template.xlsx` con las columnas:
     - **ARCHIVO**: Nombre del archivo procesado
     - **APROBADOS**: Cantidad de solicitudes aprobadas
     - **RECHAZADOS**: Cantidad de solicitudes rechazadas
     - **EJECUCION**: Fecha y hora de ejecución

4. **Manejo de archivos**
   - Mover cada archivo procesado a una subcarpeta dentro de `historico/` con el nombre de la fecha de ejecución (`YYYY-MM-DD`).
   - Generar un log de ejecución por archivo en `log/`.

5. **Archivos de muestra**
   - Si no existen archivos en `inputs/`, el bot crea automáticamente un archivo de muestra con las columnas obligatorias.

---

## 📂 Estructura de Carpetas

El bot crea la siguiente estructura automáticamente si no existe:

