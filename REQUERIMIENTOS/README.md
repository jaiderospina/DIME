# REQUERIMIENTOS.


# Formulario de Requerimientos para Customización de GLPI: Creación de Usuarios de Gestión Intermedios

Este formulario está diseñado para recopilar la información necesaria del usuario final (o cliente) en el marco del proyecto de customización de GLPI. Se basa en los requerimientos de implementación de perfiles de gestión intermedios y estandarización de roles y permisos. El objetivo es asegurar una configuración precisa, alineada con las necesidades operativas y minimizando riesgos de seguridad.

Por favor, complete las secciones a continuación de manera detallada. Utilice tablas o listas donde sea aplicable para mayor claridad. Una vez completado, envíelo al proveedor para proceder con la implementación.

**Instrucciones Generales:**
- Proporcione ejemplos concretos donde sea posible.
- Si una sección no aplica, indíquelo con "N/A".
- Adjunte cualquier documento adicional (ej. diagramas de procesos o estructuras organizacionales).
- Fecha de envío: [Inserte fecha]
- Nombre del responsable: [Inserte nombre]
- Unidad operativa: [Inserte unidad]

## 1. Definición de Roles Intermedios
Proporcione una lista completa de los roles de gestión intermedios requeridos. Incluya descripciones y relaciones con perfiles existentes en GLPI.

| Rol Propuesto | Descripción de Funciones Principales | Relación con Perfiles Existentes en GLPI (ej. Basado en Technician, Supervisor) | Responsabilidades Específicas en Módulos de GLPI (ej. Gestión de tickets, inventarios) |
|---------------|--------------------------------------|---------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| Ejemplo: Coordinador | Supervisar equipo de soporte, asignar tareas diarias. | Basado en Supervisor, con ajustes. | Asignar tickets en Asistencia, validar inventarios en Activos.                          |
|               |                                      |                                                                                 |                                                                                         |
|               |                                      |                                                                                 |                                                                                         |
|               |                                      |                                                                                 |                                                                                         |

**Notas adicionales sobre roles:**  
[Espacio para texto libre, ej. "Se requieren al menos 5 roles para cubrir las unidades de TI y Finanzas."]

## 2. Especificación de Permisos por Rol
Para cada rol definido en la sección 1, especifique los permisos detallados por módulo de GLPI. Indique niveles como: Leer (R), Actualizar (U), Crear (C), Eliminar (D), Purgar (P). Marque si son recursivos (aplican a entidades hijas) o dinámicos (basados en reglas).

Utilice la siguiente tabla por rol (duplique la tabla según sea necesario para cada rol).

**Rol: [Inserte nombre del rol, ej. Supervisor]**

| Módulo de GLPI          | Permisos (R/U/C/D/P) | Restricciones Específicas (ej. Solo entidades propias) | Recursivo (Sí/No) | Dinámico (Sí/No) | Permisos Adicionales (ej. Interfaz simplificada, notificaciones) |
|-------------------------|----------------------|---------------------------------------------------------|-------------------|------------------|-------------------------------------------------------------------|
| Activos (Assets)        | Ej. R/U             | Solo lectura en hardware sensible.                      | Sí                | No               | Acceso a reservas de activos.                                     |
| Asistencia (Assistance) |                     |                                                         |                   |                  |                                                                   |
| Gestión (Management)    |                     |                                                         |                   |                  |                                                                   |
| Herramientas (Tools)    |                     |                                                         |                   |                  |                                                                   |
| Administración (Administration) |                     |                                                         |                   |                  |                                                                   |
| Configuración (Setup)   |                     |                                                         |                   |                  |                                                                   |
| Ciclo de Vida (Life Cycle) |                     |                                                         |                   |                  |                                                                   |

**Notas adicionales sobre permisos:**  
[Espacio para texto libre, ej. "Evitar permisos de eliminación en datos financieros para todos los roles intermedios."]

## 3. Estandarización según Procesos y Unidades Operativas
Describa los procesos clave y cómo se segmentan los roles.

- **Procesos Clave de la Organización:**  
  [Liste y describa, ej.  
  - Gestión de incidencias IT: Reporte, resolución y cierre de tickets.  
  - Soporte técnico: Mantenimiento de activos.  
  - Validación de solicitudes: Aprobación de cambios.]

- **Unidades Operativas (Departamentos/Áreas/Entidades en GLPI):**  
  [Liste, ej.  
  - TI: Soporte general.  
  - Finanzas: Gestión de contratos.  
  - Recursos Humanos: Acceso limitado a tickets de empleados.]

- **Segmentación de Roles por Unidades:**  
  [Describa, ej. "Supervisor solo para TI: Acceso restringido a entidades de TI. Supervisor global: Acceso a todas las entidades."]

- **Integración con Directorio Activo (LDAP):**  
  - Grupos de LDAP asociados a perfiles: [Liste, ej. "Grupo_AD_TI -> Perfil Technician."]  
  - Reglas de autorización dinámica: [Describa, ej. "Basado en atributo 'cargo' en LDAP."]  
  - Atributos LDAP relevantes: [Liste, ej. "Grupo de pertenencia, ubicación, cargo."]

- **Requerimientos de Seguridad:**  
  - Riesgos operativos identificados: [Liste, ej. "Acceso no autorizado a datos sensibles."]  
  - Controles granulares propuestos: [Describa, ej. "Acceso solo lectura a módulos financieros."]  
  - Restricciones adicionales: [Ej. "Prohibir sobre-privilegios en administración."]

## 4. Información Adicional para la Implementación
- **Entidades y Estructuras Organizacionales Actuales en GLPI:**  
  [Describa el árbol de entidades, ej. "Raíz > TI > Soporte Nivel 1; Raíz > Finanzas." Adjunte diagrama si aplica.]

- **Ejemplos o Escenarios de Uso:**  
  [Proporcione casos prácticos, ej.  
  - Escenario 1: Un analista valida un ticket sin poder eliminarlo.  
  - Escenario 2: Supervisor asigna tickets a técnicos en su unidad.]

- **Prioridades y Plazos:**  
  - Roles críticos para implementar primero: [Liste, ej. "Técnico de Soporte y Supervisor."]  
  - Plazos sugeridos: [Ej. "Implementación inicial en 2 semanas."]

- **Validación Posterior:**  
  - Criterios para probar y aprobar: [Liste, ej.  
    - Pruebas con usuarios asignados: Verificar accesos y restricciones.  
    - Auditoría de permisos: Confirmar no hay sobre-privilegios.  
    - Integración LDAP: Simular login y asignación de perfiles.]

**Notas Finales o Comentarios Adicionales:**  
[Espacio para texto libre.]

Al completar este formulario, el proveedor podrá avanzar en la creación y configuración de perfiles en GLPI. Si requiere asistencia para llenarlo o modificaciones, contacte al equipo de proyecto.