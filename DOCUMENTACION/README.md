
<p align="center">
  <img src="https://www.dime.com.co/wp-content/uploads/2024/01/DIME-Logo-Acreditacion-01-2048x830.png" alt="Sublime's custom image"/>
</p>



# 1. **Roles**

### 1. **Definición de Roles Intermedios**
   
   Próposito. 
   
   - Lista completa de los roles de gestión mínimanente requeridos (coordinador, supervisor, analista de soporte, validador de solicitudes, etc.).

   - Descripción breve de las funciones principales de cada rol, incluyendo las responsabilidades específicas en los procesos de gestión de incidencias, inventarios, activos y otros módulos de GLPI.
   
   - Indicación de cómo estos roles se relacionan con los perfiles existentes en GLPI (como Supervisor, Technician o customizados), para evitar duplicidades y optimizar la estructura.

### 2. **Especificación de Permisos por Rol**
   - Para cada rol, un mapeo detallado de permisos en los módulos clave de GLPI. Esto incluye:
     - **Activos (Assets)**: Permisos para leer, actualizar, crear, eliminar o purgar elementos como inventarios de hardware, software, redes, etc.
     - **Asistencia (Assistance)**: Acceso a tickets, seguimientos, tareas, validaciones, problemas y cambios; por ejemplo, si el rol puede asignar tickets, ver estadísticas o gestionar plantillas.
     - **Gestión (Management)**: Permisos sobre elementos financieros, contratos, proveedores, etc.
     - **Herramientas (Tools)**: Acceso a notas, feeds RSS, reportes, reservas, base de conocimiento o tareas de proyectos.
     - **Administración (Administration)**: Nivel de control sobre usuarios, entidades y reglas de negocio (con restricciones para evitar privilegios completos).
     - **Configuración (Setup)**: Permisos para personalizaciones, listas desplegables u opciones de seguridad como 2FA.
     - **Ciclo de Vida (Life Cycle)**: Gestión de estados en tickets, problemas y cambios.
   

### 3. **Estandarización según Procesos y Unidades Operativas**
   
   Por favor describir: 

   - Descripción de los procesos clave de la organización (por ejemplo: gestión de incidencias IT, soporte técnico, validación de solicitudes, supervisión de equipos).
   - Identificación de las unidades operativas (departamentos, áreas o entidades en GLPI) y cómo se segmentan los roles por estas (por ejemplo, un supervisor solo para el área de TI vs. uno global).
   - Mapeo de cómo los roles se integran con el Directorio Activo (LDAP) actual: grupos de LDAP asociados a perfiles, reglas de autorización dinámica basadas en atributos LDAP (como grupo de pertenencia, ubicación o cargo).
   - Requerimientos de seguridad: riesgos operativos identificados, controles granulares para mitigarlos (ej. acceso solo lectura a datos sensibles) y cualquier restricción adicional para evitar sobre-privilegios.

### 4. **Información Adicional para la Implementación**

   - Entidades y estructuras organizacionales actuales en GLPI (árbol de entidades) para asegurar que los perfiles se apliquen correctamente.
   - Ejemplos o escenarios de uso: casos prácticos donde se apliquen estos roles (ej. un analista que valida tickets sin poder eliminarlos).
   - Prioridades y plazos: qué roles son críticos para implementar primero.
   - Validación posterior: criterios para probar y aprobar la configuración (ej. pruebas de usuarios con perfiles asignados).


En el contexto de la customización de GLPI para DIME  se han idnetificado procesos estructurados, donde se busca segmentación de roles sin sobrecargar la configuración (bajo nivel de complejidad). De esta manera los roles mínimos requeridos se centran en cubrir las funciones esenciales: atención al usuario final, resolución de incidencias, supervisión y administración básica. Esto se alinea con la integración LDAP existente y evita riesgos al implementar perfiles intermedios con permisos granulares.

GLPI cuenta con perfiles estándar predefinidos que sirven de base para estos roles, permitiendo una estandarización conforme a procesos operativos como la gestión de tickets, activos e incidencias. Para un nivel intermedio, se recomiendan al menos cuatro roles mínimos: uno para usuarios finales, uno para soporte operativo, uno para supervisión y uno para administración. Estos se pueden crear o adaptar desde la sección de Administración > Perfiles en GLPI, asignando permisos específicos por módulo (por ejemplo, solo lectura en activos para roles no administrativos).

A continuación, se definen y caracterizan estos roles mínimos en una tabla para mayor claridad:

| Rol                  | Descripción                                                                 | Características y Permisos Principales                                                                 |
|----------------------|-----------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|
| **Usuario Final (Self-Service)** | Perfil para empleados o usuarios externos que reportan incidencias o solicitudes, sin acceso a funciones técnicas. Representa al "requester" en el módulo de Asistencia. | - Interfaz simplificada.<br>- Crear y seguir tickets propios (añadir follow-ups, validar soluciones, participar en encuestas).<br>- Acceso limitado a herramientas como FAQ, reservas de activos y base de conocimiento.<br>- Sin permisos de edición o eliminación en módulos como Activos, Gestión o Administración.<br>- Visibilidad: Solo tickets personales; notificaciones por email para actualizaciones. |
| **Técnico de Soporte (Technician)** | Rol intermedio para el personal TIC que resuelve incidencias diarias, procesa tickets y realiza mantenimiento básico. Equivale al "technician" en flujos ITIL. | - Interfaz estándar.<br>- Leer, actualizar, crear y eliminar en el módulo de Asistencia (tickets, follow-ups, tareas, problemas, cambios).<br>- Acceso de lectura a Activos (inventario de hardware/software) y Herramientas (notas, reportes básicos).<br>- Asignar tickets a sí mismo, gestionar estados (pendiente/resuelto) y calcular prioridades.<br>- Visibilidad: Tickets personales y de grupo; notificaciones para asignaciones y resoluciones.<br>- Sin permisos administrativos completos (ej. no configurar entidades o reglas). |
| **Supervisor/Coordinador (Supervisor)** | Perfil para líderes de equipo TIC que supervisan procesos, asignan tareas y validan solicitudes, sin necesidad de accesos globales. Actúa como "validator" y overseer. | - Interfaz estándar.<br>- Todos los permisos del Técnico, más gestión de equipo: asignar tickets a otros, ver estadísticas, horarios y reportes avanzados en Asistencia.<br>- Acceso de lectura/actualización en Gestión (contratos, proveedores) y Herramientas (proyectos, base de conocimiento).<br>- Validar cambios y problemas; supervisar flujos de ciclo de vida.<br>- Visibilidad: Tickets globales de grupo/entidad; notificaciones para eventos de supervisión (ej. tickets no cerrados).<br>- Restricciones: No purgar datos sensibles ni configurar administración general. |
| **Administrador (Admin)** | Rol para el responsable TIC senior que maneja la configuración del sistema, usuarios y entidades, pero limitado a necesidades operativas intermedias. | - Interfaz estándar.<br>- Acceso completo en Administración (usuarios, entidades, reglas de negocio, autorizaciones LDAP).<br>- Leer/actualizar/crear/eliminar en Activos, Gestión y Herramientas; configuración de plantillas y listas desplegables.<br>- Supervisión global en Asistencia (estadísticas, exportaciones).<br>- Visibilidad: Todo el sistema por entidad; notificaciones para alertas administrativas.<br>- Exclusiones: No incluye permisos de Super-Admin para cambios críticos en reglas o comportamientos del sistema, minimizando riesgos. |

Estos roles mínimos aseguran una estructura estandarizada: el Usuario Final enfocado en autoservicio, el Técnico en ejecución, el Supervisor en control intermedio y el Administrador en mantenimiento. Para implementarlos, se recomienda mapearlos a grupos LDAP (ej. basados en cargo o unidad), aplicar recursividad en entidades y probar escenarios de uso. Si la madurez evoluciona, se pueden agregar roles como "Observer" (para monitoreo pasivo) o "Hotliner" (para soporte inicial). 

