# Triage Queue — Gestor de Colas de Prioridad

Aplicación ligera de línea de comandos desarrollada en Python para gestionar una cola de espera hospitalaria mediante niveles de prioridad y orden FIFO.

Los pacientes son atendidos según su nivel de triaje: primero los pacientes críticos, después los urgentes y, finalmente, los estándar. Dentro de un mismo nivel de prioridad, se respeta el orden de llegada.

Este proyecto se desarrolló como parte de una actividad educativa de **4Geeks Academy**.

## Funcionalidades

- **Registro de pacientes:** Añadir pacientes con nombre, nivel de triaje y fecha y hora de llegada.
- **Gestión por prioridades:** Atender correctamente a pacientes críticos (1), urgentes (2) y estándar (3).
- **Orden FIFO:** Respetar el orden de llegada entre pacientes del mismo nivel de prioridad.
- **Consulta del siguiente paciente:** Identificar quién debe ser atendido sin retirarlo de la cola.
- **Visualización de la cola:** Mostrar todos los pacientes pendientes en el orden previsto de atención.
- **Estadísticas:** Consultar el número de pacientes en espera por nivel de triaje.
- **Validación de entradas:** Rechazar niveles de triaje no válidos y gestionar nombres vacíos.
- **Interfaz CLI interactiva:** Administrar la cola desde un menú en la terminal.

## Cómo funciona

La aplicación utiliza tres instancias independientes de `collections.deque`, una para cada nivel de triaje.

```python
self._queues = {
    1: deque(),  # Crítico
    2: deque(),  # Urgente
    3: deque(),  # Estándar
}
```

Esta estructura permite mantener el orden de prioridad sin tener que ordenar toda la colección después de cada inserción.

| Operación | Complejidad temporal |
|---|---:|
| Encolar | O(1) |
| Desencolar | O(1) |
| Consultar siguiente (peek) | O(1) |
| Listar la cola | O(n) |
| Consultar estadísticas | O(1) |

La prioridad se mantiene consultando las colas en orden (1 → 2 → 3). El orden FIFO se conserva de forma natural dentro de cada cola.

## Requisitos

- Python 3.11 o superior.
- No requiere dependencias externas de Python.

La aplicación utiliza módulos de la biblioteca estándar de Python, entre ellos `collections.deque`, `dataclasses`, `datetime` y `sys`.

## Instalación y ejecución

Desde el directorio del proyecto, ejecuta:

```bash
python3 triage_queue.py
```

En Windows también puedes utilizar:

```bash
python triage_queue.py
```

## Opciones disponibles

El menú interactivo ofrece cinco operaciones:

1. Añadir un nuevo paciente.
2. Llamar al siguiente paciente.
3. Consultar la cola actual.
4. Consultar las estadísticas de la cola.
5. Salir de la aplicación.

## Estructura del proyecto

```text
triage-queue/
├── triage_queue.py   # Modelo de paciente, cola de prioridad e interfaz CLI
├── DESIGN.md         # Decisiones sobre estructuras de datos y análisis de concurrencia
└── README.md         # Documentación del proyecto
```

## Decisiones de diseño

El documento `DESIGN.md` explica por qué se eligieron tres colas independientes y compara esta solución con otras alternativas:

- Una única `deque` ordenada.
- Una cola de prioridad implementada con `heapq`.
- Tres listas convencionales de Python.

También analiza posibles problemas de concurrencia y propone `threading.Lock` como estrategia de sincronización para una futura implementación con múltiples trabajadores.

**La protección frente a concurrencia no está implementada en la aplicación actual.** El programa funciona como una aplicación de terminal monohilo.

## Alcance y limitaciones

Este proyecto es una simulación educativa de una cola de espera basada en prioridades, no un sistema hospitalario de producción.

- Los datos de los pacientes se mantienen en memoria y no se guardan de forma persistente.
- No dispone de interfaz gráfica ni integración con bases de datos.
- No admite procesamiento concurrente ni múltiples usuarios.
- Los niveles de triaje están simplificados para el ejercicio y no implementan un protocolo completo de evaluación clínica.

---

**Developer Wendy Sanchez**
