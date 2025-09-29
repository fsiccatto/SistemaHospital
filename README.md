# Sistema de Gestión Hospitalaria - Explicación General
El sistema desarrollado es una aplicación orientada a objetos que modela la gestión integral de un hospital, implementando las operaciones fundamentales para administrar pacientes, personal médico, instalaciones y citas médicas.

## Arquitectura del Sistema
Estructura Jerárquica: El sistema está organizado alrededor de una entidad central Hospital que contiene múltiples Departamentos especializados. Cada departamento agrupa médicos de la misma especialidad y gestiona sus propias salas médicas.

Herencia y Polimorfismo: Se implementa una clase abstracta Persona que sirve como base para Paciente y Medico, compartiendo atributos comunes como datos personales, tipo de sangre y validaciones. Esta arquitectura permite extensibilidad para agregar otros tipos de personal hospitalario.

Gestión de Relaciones: El sistema maneja relaciones bidireccionales sincronizadas entre entidades. Por ejemplo, cuando se asigna un médico a un departamento, ambos objetos actualizan sus referencias mutuas automáticamente, manteniendo la consistencia de datos.

## Funcionalidades Principales
Gestión de Pacientes: Cada paciente recibe automáticamente una historia clínica única con identificador generado (HC-DNI-AÑO). La historia permite registrar diagnósticos, tratamientos y alergias de forma incremental.

Sistema de Citas Médicas: La clase Cita actúa como entidad asociativa, resolviendo la relación muchos-a-muchos entre pacientes, médicos y salas. Incluye validaciones de negocio como verificación de disponibilidad y compatibilidad de especialidades.

Validaciones de Integridad: El sistema implementa múltiples capas de validación:

· Formato de datos (DNI, matrícula médica, números de identificación)

· Reglas de negocio (fechas futuras, costos positivos, disponibilidad)

· Consistencia referencial (especialidad médico-departamento-sala)

## Persistencia y Recuperacion
Serialización CSV: Se implementa un sistema de persistencia personalizado que convierte objetos complejos a formato CSV, manejando caracteres especiales y referencias entre entidades. La carga reversa reconstruye el grafo de objetos manteniendo todas las relaciones.

Gestión de Estado: El CitaManager mantiene índices optimizados (ConcurrentHashMap) para búsquedas eficientes por paciente, médico o sala, evitando recorridos lineales en operaciones frecuentes.
