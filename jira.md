# JIRA — CoursePlace Admin Panel
> Panel Administrativo para Gestión Académica de Programas de Posgrado

---

## CONVENCIONES

| Prefijo | Tipo         |
|---------|--------------|
| EP      | Epic         |
| US      | User Story   |
| ST      | Subtask      |

**Prioridades:** `Critical` · `High` · `Medium` · `Low`
**Estados:** `To Do` · `In Progress` · `Done`
**Story Points (SP):** Estimación en Fibonacci: 1, 2, 3, 5, 8, 13

---

---

# EP-02 — Dashboard y Navegación Principal

**Descripción:** Panel central de la aplicación que sirve como punto de entrada y navegación hacia todas las secciones funcionales del sistema de gestión académica.
**Prioridad:** High
**Estado:** In Progress

---

### US-02.1 — Visualización del Dashboard Principal

**Como** administrador,
**Quiero** ver un panel de inicio con acceso rápido a todas las secciones,
**Para** navegar eficientemente entre las áreas del sistema.

**Criterios de Aceptación:**

```gherkin
Scenario: Tarjetas de acceso visibles en el dashboard
  Given que el administrador ha iniciado sesión
  When accede al dashboard principal
  Then se muestran tarjetas de acceso para las 5 secciones: Competencias, Resultados de Aprendizaje, Programas, Cursos y Micro Aprendizajes

Scenario: Información en cada tarjeta
  Given que el administrador está en el dashboard
  When visualiza una tarjeta de sección
  Then la tarjeta muestra nombre, descripción e icono representativo

Scenario: Animación hover en tarjetas
  Given que el administrador está en el dashboard
  When coloca el cursor sobre una tarjeta
  Then la tarjeta muestra un efecto hover con animación visual

Scenario: Header con información del sistema
  Given que el administrador está en el dashboard
  When observa el encabezado de la página
  Then el header muestra el logo, el nombre del sistema y el avatar del usuario

Scenario: Diseño responsive del dashboard
  Given que el administrador accede al dashboard
  When lo visualiza desde un dispositivo móvil o desktop
  Then el diseño se adapta correctamente al tamaño de pantalla
```

**Prioridad:** High | **SP:** 3

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-02.1.1 | Crear estructura HTML del dashboard con grid de tarjetas | 2 |
| ST-02.1.2 | Implementar estilos responsive para 1, 2 y 3 columnas   | 2  |
| ST-02.1.3 | Agregar efectos hover y animaciones en tarjetas          | 1  |
| ST-02.1.4 | Integrar navegación funcional desde cada tarjeta         | 1  |

---

### US-02.2 — Resumen de Estadísticas en el Dashboard

**Como** administrador,
**Quiero** ver contadores de los registros existentes en cada sección (# programas, # cursos, etc.),
**Para** tener una visión rápida del estado del catálogo académico.

**Criterios de Aceptación:**

```gherkin
Scenario: Contador de registros por sección
  Given que el administrador está en el dashboard
  When la página termina de cargar
  Then cada tarjeta muestra el número total de registros de su sección

Scenario: Actualización en tiempo real de contadores
  Given que el administrador está en el dashboard
  When se agrega o elimina un registro en cualquier sección
  Then el contador de esa tarjeta se actualiza automáticamente desde la API

Scenario: Formato de los contadores
  Given que el administrador está en el dashboard
  When visualiza un contador de sección
  Then el dato se muestra formateado, por ejemplo "12 Competencias"
```

**Prioridad:** Medium | **SP:** 3

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-02.2.1 | Diseñar UI para mostrar contadores en tarjetas          | 1  |
| ST-02.2.2 | Integrar llamadas GET a cada API para obtener totales   | 3  |
| ST-02.2.3 | Manejar estado de carga (skeleton/spinner)              | 2  |

---

### US-02.3 — Header Global de la Aplicación

**Como** administrador,
**Quiero** tener un header persistente con navegación contextual,
**Para** saber en qué sección estoy y poder regresar fácilmente al inicio.

**Criterios de Aceptación:**

```gherkin
Scenario: Logo en el header
  Given que el administrador está en cualquier página
  When observa el header
  Then se muestra el logo de CoursePlace

Scenario: Título de sección activa
  Given que el administrador está en una sección interior
  When observa el header
  Then se muestra el título de la sección activa

Scenario: Botón de regreso al inicio
  Given que el administrador está en una página interior
  When hace clic en el botón "← Inicio"
  Then es redirigido al dashboard principal

Scenario: Información del usuario autenticado
  Given que el administrador está autenticado
  When observa el header
  Then se muestran el avatar y nombre del usuario autenticado

Scenario: Header sticky al hacer scroll
  Given que el administrador está en una página con contenido largo
  When hace scroll hacia abajo
  Then el header permanece visible en la parte superior de la pantalla
```

**Prioridad:** High | **SP:** 3

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-02.3.1 | Crear componente Header reutilizable                    | 3  |
| ST-02.3.2 | Implementar lógica de navegación de regreso             | 1  |
| ST-02.3.3 | Mostrar nombre/avatar del usuario autenticado           | 2  |

---

---

# EP-03 — Gestión de Competencias

**Descripción:** Módulo para crear, editar, listar y asociar competencias académicas con sus respectivos Resultados de Aprendizaje.
**Prioridad:** High
**Estado:** In Progress

---

### US-03.1 — Listar Competencias

**Como** administrador,
**Quiero** ver un listado de todas las competencias registradas,
**Para** conocer el catálogo completo y acceder rápidamente a cada una.

**Criterios de Aceptación:**

```gherkin
Scenario: Visualización del listado de competencias
  Given que existen competencias registradas en el sistema
  When el administrador accede a la sección de Competencias
  Then se listan todas las competencias con: índice (C-001), nombre, descripción y número de RAs asignados

Scenario: Contador total de competencias
  Given que el administrador está en la vista de Competencias
  When la página carga el listado
  Then se muestra un contador con el total de competencias registradas

Scenario: Empty state sin registros
  Given que no existe ninguna competencia registrada
  When el administrador accede a la sección de Competencias
  Then se muestra un mensaje de "empty state" indicando que no hay registros

Scenario: Botón de edición por competencia
  Given que el administrador está viendo el listado de competencias
  When visualiza una tarjeta de competencia
  Then la tarjeta tiene un botón de acción "Editar"
```

**Prioridad:** High | **SP:** 3

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-03.1.1 | Integrar API GET /competencias para obtener listado     | 2  |
| ST-03.1.2 | Renderizar tarjetas de competencias con datos dinámicos | 2  |
| ST-03.1.3 | Implementar componente de "empty state"                 | 1  |
| ST-03.1.4 | Mostrar contador total de registros                     | 1  |

---

### US-03.2 — Buscar Competencias

**Como** administrador,
**Quiero** buscar competencias por nombre o descripción,
**Para** encontrar rápidamente la que necesito modificar.

**Criterios de Aceptación:**

```gherkin
Scenario: Campo de búsqueda visible
  Given que el administrador está en la vista de Competencias
  When carga la página
  Then se muestra un campo de búsqueda en la parte superior del listado

Scenario: Filtrado en tiempo real
  Given que el administrador está en la vista de Competencias
  When escribe texto en el campo de búsqueda
  Then el listado se filtra inmediatamente sin necesidad de presionar Enter

Scenario: Búsqueda case-insensitive
  Given que el administrador escribe texto en el buscador
  When usa mayúsculas o minúsculas indistintamente
  Then se muestran resultados coincidentes sin importar el caso

Scenario: Contador actualizado según resultados filtrados
  Given que el administrador ha aplicado un filtro de búsqueda
  When el listado muestra los resultados
  Then el contador de competencias refleja el número de resultados filtrados

Scenario: Empty state sin coincidencias
  Given que el administrador busca un término que no existe
  When no hay competencias que coincidan con la búsqueda
  Then se muestra el componente de "empty state"
```

**Prioridad:** High | **SP:** 2

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-03.2.1 | Implementar filtrado por texto en el lado cliente       | 2  |
| ST-03.2.2 | Sincronizar contador con resultados filtrados           | 1  |

---

### US-03.3 — Crear Competencia

**Como** administrador,
**Quiero** crear una nueva competencia con nombre, descripción y RAs asociados,
**Para** ampliar el catálogo de competencias del programa académico.

**Criterios de Aceptación:**

```gherkin
Scenario: Campos del formulario de creación
  Given que el administrador accede al formulario de nueva competencia
  When visualiza el formulario
  Then encuentra un campo Nombre (obligatorio) y un campo Descripción (opcional)

Scenario: Validación del campo nombre vacío
  Given que el administrador deja el campo Nombre vacío
  When intenta guardar la competencia
  Then se muestra un mensaje de error visual indicando que el nombre es obligatorio

Scenario: Modal de selección múltiple de RAs
  Given que el administrador está completando el formulario
  When hace clic para asociar Resultados de Aprendizaje
  Then se abre un modal de multi-selección con buscador interno

Scenario: Visualización de RAs seleccionados
  Given que el administrador ha seleccionado RAs en el modal
  When confirma la selección
  Then los RAs seleccionados se muestran como badges numerados en el formulario

Scenario: Toast de éxito al crear
  Given que el administrador ha completado correctamente el formulario
  When guarda la nueva competencia
  Then aparece una notificación de éxito (toast)

Scenario: Reseteo del formulario tras crear
  Given que el administrador acaba de crear una competencia exitosamente
  When el toast de confirmación aparece
  Then el formulario se resetea y queda listo para un nuevo registro
```

**Prioridad:** High | **SP:** 5

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-03.3.1 | Diseñar formulario de creación de competencias          | 2  |
| ST-03.3.2 | Implementar validación de campos obligatorios           | 2  |
| ST-03.3.3 | Construir modal de selección múltiple de RAs            | 3  |
| ST-03.3.4 | Integrar API POST /competencias para guardar            | 2  |
| ST-03.3.5 | Mostrar toast de confirmación al crear                  | 1  |

---

### US-03.4 — Editar Competencia

**Como** administrador,
**Quiero** editar una competencia existente,
**Para** actualizar su nombre, descripción o los RAs asociados.

**Criterios de Aceptación:**

```gherkin
Scenario: Carga de datos en el formulario de edición
  Given que el administrador hace clic en "Editar" sobre una competencia
  When se abre el formulario de edición
  Then los campos nombre, descripción y RAs se pre-cargan con los datos actuales

Scenario: RAs previos pre-seleccionados en el modal
  Given que el administrador abre el modal de RAs en modo edición
  When visualiza la lista de RAs disponibles
  Then los RAs previamente asignados aparecen ya marcados

Scenario: Modificar RAs asociados
  Given que el administrador está en el modal de RAs en modo edición
  When agrega o quita RAs de la selección
  Then los cambios se reflejan en los badges del formulario

Scenario: Toast de confirmación al guardar cambios
  Given que el administrador ha realizado cambios en la competencia
  When guarda los cambios
  Then aparece un toast de confirmación de actualización

Scenario: Regreso al listado tras guardar
  Given que el administrador ha guardado los cambios de una competencia
  When el proceso finaliza exitosamente
  Then es redirigido a la vista de listado de competencias
```

**Prioridad:** High | **SP:** 5

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-03.4.1 | Cargar datos de la competencia en el formulario         | 2  |
| ST-03.4.2 | Pre-seleccionar RAs asignados en el modal               | 2  |
| ST-03.4.3 | Integrar API PUT /competencias/:id para actualizar      | 2  |
| ST-03.4.4 | Mostrar toast de confirmación al actualizar             | 1  |

---

### US-03.5 — Eliminar Competencia

**Como** administrador,
**Quiero** eliminar una competencia que ya no sea necesaria,
**Para** mantener el catálogo limpio y actualizado.

**Criterios de Aceptación:**

```gherkin
Scenario: Botón de eliminar disponible por competencia
  Given que el administrador está en el listado de competencias
  When visualiza una tarjeta de competencia
  Then la tarjeta muestra un botón "Eliminar"

Scenario: Modal de confirmación antes de eliminar
  Given que el administrador hace clic en "Eliminar" sobre una competencia
  When el sistema procesa la acción
  Then se muestra un modal de confirmación antes de ejecutar la eliminación

Scenario: Eliminación y refresco del listado
  Given que el administrador confirma la eliminación en el modal
  When el sistema elimina la competencia
  Then la competencia desaparece del listado y la lista se refresca automáticamente

Scenario: Toast de confirmación de eliminación
  Given que el administrador confirma la eliminación
  When la competencia es eliminada exitosamente
  Then se muestra un toast de confirmación de eliminación
```

**Prioridad:** Medium | **SP:** 3

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-03.5.1 | Agregar botón "Eliminar" en la tarjeta de competencia   | 1  |
| ST-03.5.2 | Implementar modal de confirmación de eliminación        | 2  |
| ST-03.5.3 | Integrar API DELETE /competencias/:id                   | 2  |
| ST-03.5.4 | Actualizar lista y mostrar toast tras eliminar          | 1  |

---

---

# EP-04 — Gestión de Resultados de Aprendizaje

**Descripción:** Módulo para administrar los Resultados de Aprendizaje (RAs) y sus asociaciones bidireccionales con Competencias.
**Prioridad:** High
**Estado:** In Progress

---

### US-04.1 — Listar Resultados de Aprendizaje

**Como** administrador,
**Quiero** ver el listado completo de Resultados de Aprendizaje,
**Para** conocer todos los RAs definidos y sus competencias asociadas.

**Criterios de Aceptación:**

```gherkin
Scenario: Visualización del listado de RAs
  Given que existen RAs registrados en el sistema
  When el administrador accede a la sección de Resultados de Aprendizaje
  Then se listan todos los RAs con: índice (RA-001), nombre, descripción y badge de competencias asociadas

Scenario: Contador total de RAs
  Given que el administrador está en la vista de Resultados de Aprendizaje
  When la página carga el listado
  Then se muestra un contador con el total de RAs registrados

Scenario: Empty state sin registros
  Given que no existe ningún RA registrado
  When el administrador accede a la sección de Resultados de Aprendizaje
  Then se muestra un mensaje de "empty state"

Scenario: Botón de edición por RA
  Given que el administrador está viendo el listado de RAs
  When visualiza una tarjeta de RA
  Then la tarjeta tiene un botón "Editar"
```

**Prioridad:** High | **SP:** 3

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-04.1.1 | Integrar API GET /resultados para obtener listado       | 2  |
| ST-04.1.2 | Renderizar tarjetas de RAs con datos dinámicos          | 2  |
| ST-04.1.3 | Implementar empty state y contador                      | 1  |

---

### US-04.2 — Buscar Resultados de Aprendizaje

**Como** administrador,
**Quiero** buscar RAs por nombre o descripción,
**Para** localizarlos rápidamente en el listado.

**Criterios de Aceptación:**

```gherkin
Scenario: Filtrado en tiempo real de RAs
  Given que el administrador está en la vista de Resultados de Aprendizaje
  When escribe texto en el campo de búsqueda
  Then el listado se filtra inmediatamente mostrando coincidencias en nombre y descripción

Scenario: Contador actualizado según búsqueda
  Given que el administrador ha aplicado un filtro de búsqueda en RAs
  When el listado muestra los resultados filtrados
  Then el contador refleja el número de RAs encontrados
```

**Prioridad:** High | **SP:** 2

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-04.2.1 | Implementar filtrado por texto en el listado de RAs     | 2  |

---

### US-04.3 — Crear Resultado de Aprendizaje

**Como** administrador,
**Quiero** crear un nuevo Resultado de Aprendizaje con nombre, descripción y competencias asociadas,
**Para** ampliar los objetivos de aprendizaje del programa.

**Criterios de Aceptación:**

```gherkin
Scenario: Campos del formulario de creación de RA
  Given que el administrador accede al formulario de nuevo RA
  When visualiza el formulario
  Then encuentra un campo Nombre (obligatorio) y un campo Descripción (opcional)

Scenario: Modal de selección múltiple de competencias
  Given que el administrador está completando el formulario de RA
  When hace clic para asociar competencias
  Then se abre un modal de multi-selección con buscador interno

Scenario: Competencias seleccionadas como badges
  Given que el administrador ha seleccionado competencias en el modal
  When confirma la selección
  Then las competencias seleccionadas se muestran como badges en el formulario

Scenario: Validación del nombre vacío
  Given que el administrador deja el campo Nombre vacío
  When intenta guardar el RA
  Then se muestra feedback visual indicando que el nombre es obligatorio

Scenario: Toast de confirmación al crear RA
  Given que el administrador ha completado correctamente el formulario
  When guarda el nuevo RA
  Then aparece un toast de confirmación
```

**Prioridad:** High | **SP:** 5

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-04.3.1 | Diseñar formulario de creación de RA                    | 2  |
| ST-04.3.2 | Implementar modal de selección múltiple de competencias | 3  |
| ST-04.3.3 | Integrar API POST /resultados                           | 2  |
| ST-04.3.4 | Mostrar toast de confirmación                           | 1  |

---

### US-04.4 — Editar Resultado de Aprendizaje

**Como** administrador,
**Quiero** editar un RA existente,
**Para** actualizar su información y sus competencias asociadas.

**Criterios de Aceptación:**

```gherkin
Scenario: Formulario pre-cargado con datos del RA
  Given que el administrador hace clic en "Editar" sobre un RA
  When se abre el formulario de edición
  Then los campos nombre y descripción se pre-cargan con los datos actuales del RA

Scenario: Competencias asociadas pre-seleccionadas
  Given que el administrador abre el modal de competencias en modo edición
  When visualiza la lista de competencias disponibles
  Then las competencias previamente asociadas al RA aparecen ya marcadas

Scenario: Modificar competencias asociadas
  Given que el administrador está en el modal de competencias en modo edición
  When agrega o quita competencias de la selección
  Then los cambios se reflejan en los badges del formulario

Scenario: Toast de confirmación al guardar cambios del RA
  Given que el administrador ha realizado cambios en un RA
  When guarda los cambios
  Then aparece un toast de confirmación de actualización
```

**Prioridad:** High | **SP:** 5

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-04.4.1 | Cargar datos del RA en el formulario de edición         | 2  |
| ST-04.4.2 | Pre-seleccionar competencias asociadas en el modal      | 2  |
| ST-04.4.3 | Integrar API PUT /resultados/:id                        | 2  |

---

### US-04.5 — Eliminar Resultado de Aprendizaje

**Como** administrador,
**Quiero** eliminar un RA obsoleto,
**Para** mantener actualizado el catálogo de aprendizaje.

**Criterios de Aceptación:**

```gherkin
Scenario: Botón de eliminar disponible por RA
  Given que el administrador está en el listado de RAs
  When visualiza una tarjeta de RA
  Then la tarjeta muestra un botón "Eliminar"

Scenario: Modal de confirmación antes de eliminar RA
  Given que el administrador hace clic en "Eliminar" sobre un RA
  When el sistema procesa la acción
  Then se muestra un modal de confirmación antes de ejecutar la eliminación

Scenario: Toast de confirmación tras eliminar RA
  Given que el administrador confirma la eliminación de un RA
  When el sistema lo elimina exitosamente
  Then se muestra un toast de confirmación de eliminación
```

**Prioridad:** Medium | **SP:** 3

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-04.5.1 | Agregar botón eliminar en tarjeta de RA                 | 1  |
| ST-04.5.2 | Modal de confirmación de eliminación                    | 2  |
| ST-04.5.3 | Integrar API DELETE /resultados/:id                     | 2  |

---

---

# EP-05 — Gestión de Cursos

**Descripción:** Módulo completo para crear, editar, listar y configurar cursos académicos, incluyendo asignación de créditos, horas, modalidad, imagen, áreas de conocimiento, competencias y Resultados de Aprendizaje con niveles de dominio.
**Prioridad:** High
**Estado:** In Progress

---

### US-05.1 — Listar Cursos

**Como** administrador,
**Quiero** ver todos los cursos en una tabla con su información básica,
**Para** tener una visión general del catálogo de cursos disponibles.

**Criterios de Aceptación:**

```gherkin
Scenario: Tabla de cursos con columnas completas
  Given que existen cursos registrados en el sistema
  When el administrador accede a la sección de Cursos
  Then se muestra una tabla con columnas: Nombre, Créditos, Horas, Modalidad, Electiva, Comp/RAs, Acciones

Scenario: Badges visuales por tipo y asignaciones
  Given que el administrador está viendo la tabla de cursos
  When visualiza una fila de curso
  Then se muestran badges para tipo (Electivo/Obligatorio), créditos y RAs asignados

Scenario: Buscador en tiempo real de cursos
  Given que el administrador está en la vista de Cursos
  When escribe texto en el buscador
  Then la tabla se filtra en tiempo real mostrando los cursos coincidentes

Scenario: Botones de acción por fila
  Given que el administrador está viendo la tabla de cursos
  When visualiza una fila
  Then cada fila tiene botones de "Editar" y "Eliminar"
```

**Prioridad:** High | **SP:** 3

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-05.1.1 | Integrar API GET /cursos para obtener listado           | 2  |
| ST-05.1.2 | Renderizar tabla con datos dinámicos y badges           | 3  |
| ST-05.1.3 | Implementar buscador por nombre                         | 1  |

---

### US-05.2 — Crear Curso

**Como** administrador,
**Quiero** crear un curso con toda su información académica,
**Para** ampliar el catálogo de cursos del programa.

**Criterios de Aceptación:**

```gherkin
Scenario: Campos del formulario de creación de curso
  Given que el administrador accede al formulario de nuevo curso
  When visualiza el formulario
  Then encuentra campos: Nombre (obligatorio), Créditos, Horas, Modalidad (Virtual/Presencial/Híbrido), Descripción y Objetivo General

Scenario: Toggle de curso electivo
  Given que el administrador está completando el formulario de curso
  When activa el toggle "Curso Electivo"
  Then el curso queda marcado como electivo

Scenario: Validación de campos obligatorios
  Given que el administrador deja campos obligatorios vacíos
  When intenta guardar el curso
  Then se muestran mensajes de error visual en cada campo faltante

Scenario: Toast de éxito al crear curso
  Given que el administrador ha completado correctamente el formulario
  When guarda el nuevo curso
  Then aparece un toast de éxito
```

**Prioridad:** High | **SP:** 5

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-05.2.1 | Diseñar formulario de creación de curso                 | 2  |
| ST-05.2.2 | Implementar validación de campos (nombre, créditos, horas) | 2 |
| ST-05.2.3 | Integrar API POST /cursos                               | 2  |
| ST-05.2.4 | Implementar toggle de curso electivo                    | 1  |

---

### US-05.3 — Cargar Imagen de Curso

**Como** administrador,
**Quiero** subir una imagen representativa del curso,
**Para** que los estudiantes puedan identificarlo visualmente en el catálogo.

**Criterios de Aceptación:**

```gherkin
Scenario: Zona de carga de imagen
  Given que el administrador está en el formulario de curso
  When visualiza la sección de imagen
  Then encuentra una zona de drag & drop o clic para seleccionar imagen

Scenario: Formatos de imagen aceptados
  Given que el administrador intenta subir una imagen
  When selecciona un archivo con formato PNG, JPG o WEBP
  Then el archivo es aceptado por el sistema

Scenario: Límite de tamaño de imagen
  Given que el administrador intenta subir una imagen mayor a 5MB
  When el sistema valida el archivo
  Then se muestra un mensaje de error indicando que el tamaño supera el límite

Scenario: Preview de imagen seleccionada
  Given que el administrador ha seleccionado una imagen válida
  When el archivo es procesado
  Then se muestra una vista previa de la imagen en el formulario

Scenario: Eliminar imagen seleccionada
  Given que el administrador tiene una imagen cargada en el formulario
  When hace clic en el botón para eliminar la imagen
  Then la imagen se elimina y la zona de carga queda vacía

Scenario: Error por formato no válido
  Given que el administrador intenta subir un archivo con formato no permitido
  When el sistema valida el archivo
  Then se muestra un mensaje de error indicando el formato no válido
```

**Prioridad:** Medium | **SP:** 5

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-05.3.1 | Implementar componente drop zone de imágenes            | 3  |
| ST-05.3.2 | Validar tipo de archivo y tamaño máximo (5MB)           | 2  |
| ST-05.3.3 | Mostrar preview de la imagen cargada                    | 1  |
| ST-05.3.4 | Implementar botón para limpiar imagen                   | 1  |
| ST-05.3.5 | Integrar subida de imagen a almacenamiento (API/S3)     | 3  |

---

### US-05.4 — Asignar Áreas de Conocimiento al Curso

**Como** administrador,
**Quiero** asignar una o más áreas de conocimiento (Worlds) a un curso,
**Para** clasificarlo temáticamente dentro del catálogo académico.

**Criterios de Aceptación:**

```gherkin
Scenario: Listado de áreas disponibles
  Given que el administrador está en el formulario de curso
  When accede al selector de áreas de conocimiento
  Then ve las áreas disponibles: Datos, Frontend, Backend, Cloud, Mobile, IA, Design

Scenario: Selección múltiple de áreas
  Given que el administrador está en el selector de áreas
  When selecciona varias áreas mediante chips o checkboxes
  Then todas las áreas seleccionadas quedan marcadas

Scenario: Chips removibles de áreas seleccionadas
  Given que el administrador ha seleccionado áreas de conocimiento
  When visualiza la sección de áreas en el formulario
  Then las áreas seleccionadas se muestran como chips removibles

Scenario: Persistencia de áreas al editar curso
  Given que el administrador abre un curso existente en modo edición
  When visualiza el selector de áreas
  Then las áreas previamente asignadas aparecen ya seleccionadas
```

**Prioridad:** Medium | **SP:** 3

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-05.4.1 | Construir selector de áreas con multi-selección         | 2  |
| ST-05.4.2 | Mostrar chips removibles de áreas seleccionadas         | 1  |
| ST-05.4.3 | Integrar áreas en el payload de creación/edición        | 1  |

---

### US-05.5 — Asignar Competencias y Resultados de Aprendizaje al Curso

**Como** administrador,
**Quiero** asociar competencias y RAs a un curso indicando el nivel de dominio,
**Para** definir el mapa curricular y el aporte de cada curso al perfil de egreso.

**Criterios de Aceptación:**

```gherkin
Scenario: Modal de dos pasos para asociar Competencia-RA
  Given que el administrador está en el formulario de curso
  When abre el modal de asociación de Competencias y RAs
  Then el modal presenta 2 pasos: Paso 1 selecciona competencia y Paso 2 selecciona RAs de esa competencia

Scenario: Múltiples pares Competencia-RA
  Given que el administrador ha completado una asociación Competencia-RA
  When agrega otra asociación
  Then puede agregar múltiples pares Competencia-RA independientes

Scenario: Tabla de asociaciones con niveles de dominio
  Given que el administrador ha agregado asociaciones Competencia-RA
  When visualiza la tabla resultante
  Then muestra columnas: Competencia, RA, y checkboxes I/F/V (Introduce / Fortalece / Valora)

Scenario: Eliminar asociación de la tabla
  Given que el administrador está viendo la tabla de asociaciones
  When hace clic en eliminar una fila
  Then la asociación es removida de la tabla

Scenario: Persistencia de asociaciones al editar
  Given que el administrador abre un curso existente en modo edición
  When visualiza la tabla de asociaciones
  Then las asociaciones previamente configuradas aparecen pre-cargadas
```

**Prioridad:** High | **SP:** 8

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-05.5.1 | Diseñar modal de 2 pasos para selección Competencia-RA  | 3  |
| ST-05.5.2 | Implementar Paso 1: selección single de competencia     | 2  |
| ST-05.5.3 | Implementar Paso 2: selección multi de RAs              | 2  |
| ST-05.5.4 | Construir tabla de asociaciones con checkboxes I/F/V    | 3  |
| ST-05.5.5 | Permitir eliminar filas de la tabla de asociaciones     | 1  |
| ST-05.5.6 | Integrar asociaciones en el payload de la API           | 2  |

---

### US-05.6 — Editar Curso

**Como** administrador,
**Quiero** editar la información de un curso existente,
**Para** mantener actualizado el catálogo académico.

**Criterios de Aceptación:**

```gherkin
Scenario: Pre-carga de datos al editar curso
  Given que el administrador hace clic en "Editar" sobre un curso
  When se abre el formulario de edición
  Then todos los campos del curso se pre-cargan con sus datos actuales

Scenario: Edición de todos los elementos del curso
  Given que el administrador está en el formulario de edición de un curso
  When modifica cualquier sección del formulario
  Then puede actualizar campos, imagen, áreas de conocimiento y asociaciones Competencias/RAs

Scenario: Toast de confirmación al guardar cambios del curso
  Given que el administrador ha realizado cambios en un curso
  When guarda los cambios
  Then aparece un toast de confirmación
```

**Prioridad:** High | **SP:** 5

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-05.6.1 | Integrar API GET /cursos/:id para cargar datos          | 2  |
| ST-05.6.2 | Pre-cargar todos los campos del formulario              | 2  |
| ST-05.6.3 | Pre-seleccionar áreas y asociaciones Comp-RA            | 2  |
| ST-05.6.4 | Integrar API PUT /cursos/:id para guardar cambios       | 2  |

---

### US-05.7 — Eliminar Curso

**Como** administrador,
**Quiero** eliminar un curso del catálogo,
**Para** remover cursos que ya no se ofrecen.

**Criterios de Aceptación:**

```gherkin
Scenario: Botón de eliminar en la tabla de cursos
  Given que el administrador está viendo la tabla de cursos
  When visualiza una fila
  Then la fila tiene un botón "Eliminar"

Scenario: Modal de confirmación antes de eliminar curso
  Given que el administrador hace clic en "Eliminar" sobre un curso
  When el sistema procesa la acción
  Then se muestra un modal de confirmación antes de ejecutar la eliminación

Scenario: Toast de confirmación y actualización de lista
  Given que el administrador confirma la eliminación de un curso
  When el sistema lo elimina exitosamente
  Then se muestra un toast de confirmación y la lista se actualiza inmediatamente
```

**Prioridad:** Medium | **SP:** 3

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-05.7.1 | Implementar modal de confirmación de eliminación        | 2  |
| ST-05.7.2 | Integrar API DELETE /cursos/:id                         | 2  |

---

---

# EP-06 — Gestión de Programas Académicos

**Descripción:** Módulo para administrar programas de posgrado (Maestrías, Especializaciones, Certificaciones, Doctorados), incluyendo su estructura curricular por semestres y la asignación de competencias y áreas de conocimiento.
**Prioridad:** High
**Estado:** In Progress

---

### US-06.1 — Listar Programas Académicos

**Como** administrador,
**Quiero** ver el listado de todos los programas académicos registrados,
**Para** tener una vista general de la oferta de posgrado.

**Criterios de Aceptación:**

```gherkin
Scenario: Tarjetas de programas con información completa
  Given que existen programas registrados en el sistema
  When el administrador accede a la sección de Programas
  Then se muestra una lista de tarjetas con: imagen, nombre, descripción truncada, tipo, modalidad, créditos, semestres, SNIES, tags y número de cursos

Scenario: Badge de programa destacado
  Given que un programa está marcado como "Destacado"
  When el administrador visualiza la tarjeta de ese programa
  Then la tarjeta muestra un badge de "Destacado"

Scenario: Buscador en tiempo real de programas
  Given que el administrador está en la vista de Programas
  When escribe texto en el buscador
  Then el listado se filtra en tiempo real

Scenario: Contador total de programas
  Given que el administrador está en la vista de Programas
  When la página carga el listado
  Then se muestra un contador con el total de programas

Scenario: Botón de edición por programa
  Given que el administrador está viendo el listado de programas
  When visualiza una tarjeta de programa
  Then la tarjeta tiene un botón "Editar"
```

**Prioridad:** High | **SP:** 3

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-06.1.1 | Integrar API GET /programas                             | 2  |
| ST-06.1.2 | Renderizar tarjetas con todos los datos y badges        | 3  |
| ST-06.1.3 | Implementar buscador y contador                         | 1  |

---

### US-06.2 — Crear Programa Académico

**Como** administrador,
**Quiero** crear un nuevo programa académico con toda su información,
**Para** registrar la oferta de posgrado en el sistema.

**Criterios de Aceptación:**

```gherkin
Scenario: Campos del formulario de creación de programa
  Given que el administrador accede al formulario de nuevo programa
  When visualiza el formulario
  Then encuentra campos: Nombre (obligatorio), Descripción, Perfil del Egresado, Tipo (Maestría/Especialización/Certificación/Doctorado), Modalidad y SNIES

Scenario: Imagen de portada con drag & drop
  Given que el administrador está en el formulario de programa
  When accede a la sección de imagen
  Then puede arrastrar o seleccionar una imagen de portada

Scenario: Campo de tags con chip input
  Given que el administrador está en el formulario de programa
  When escribe una palabra clave y presiona coma o Enter
  Then la palabra se agrega como un chip/tag al campo de palabras clave

Scenario: Toggle destacado en programa
  Given que el administrador está completando el formulario de programa
  When activa el toggle "Destacado"
  Then el programa queda marcado para ser destacado

Scenario: Validación de campos obligatorios del programa
  Given que el administrador deja campos obligatorios vacíos
  When intenta guardar el programa
  Then se muestran mensajes de error visual en cada campo faltante

Scenario: Toast de éxito al crear programa
  Given que el administrador ha completado correctamente el formulario
  When guarda el nuevo programa
  Then aparece un toast de éxito
```

**Prioridad:** High | **SP:** 8

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-06.2.1 | Diseñar formulario de creación de programa              | 3  |
| ST-06.2.2 | Implementar campo de tags (chip input)                  | 2  |
| ST-06.2.3 | Implementar drop zone de imagen para programas          | 2  |
| ST-06.2.4 | Implementar toggle "Destacado"                          | 1  |
| ST-06.2.5 | Implementar validación de campos obligatorios           | 2  |
| ST-06.2.6 | Integrar API POST /programas                            | 2  |

---

### US-06.3 — Asignar Competencias al Programa

**Como** administrador,
**Quiero** asociar competencias al programa académico,
**Para** definir el perfil de competencias que desarrollarán los graduados.

**Criterios de Aceptación:**

```gherkin
Scenario: Modal de selección múltiple de competencias para programa
  Given que el administrador está en el formulario de programa
  When abre el selector de competencias
  Then se muestra un modal de multi-selección con buscador interno

Scenario: Chips de competencias seleccionadas en programa
  Given que el administrador ha seleccionado competencias en el modal
  When confirma la selección
  Then las competencias seleccionadas se muestran como chips removibles en el formulario

Scenario: Persistencia de competencias al editar programa
  Given que el administrador abre un programa existente en modo edición
  When visualiza la sección de competencias
  Then las competencias previamente asociadas aparecen ya seleccionadas
```

**Prioridad:** High | **SP:** 3

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-06.3.1 | Construir modal de selección múltiple de competencias   | 3  |
| ST-06.3.2 | Mostrar chips de competencias seleccionadas             | 1  |
| ST-06.3.3 | Integrar competencias en el payload del programa        | 1  |

---

### US-06.4 — Asignar Áreas de Conocimiento al Programa

**Como** administrador,
**Quiero** asociar áreas de conocimiento (Worlds) al programa,
**Para** clasificarlo temáticamente.

**Criterios de Aceptación:**

```gherkin
Scenario: Selector de áreas con multi-selección para programa
  Given que el administrador está en el formulario de programa
  When accede al selector de áreas de conocimiento
  Then puede seleccionar múltiples áreas simultáneamente

Scenario: Chips removibles de áreas en programa
  Given que el administrador ha seleccionado áreas de conocimiento
  When visualiza la sección de áreas
  Then las áreas seleccionadas se muestran como chips removibles

Scenario: Persistencia de áreas al editar programa
  Given que el administrador abre un programa existente en modo edición
  When visualiza el selector de áreas
  Then las áreas previamente asignadas aparecen ya seleccionadas
```

**Prioridad:** Medium | **SP:** 2

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-06.4.1 | Construir selector de áreas para programas              | 2  |
| ST-06.4.2 | Integrar áreas en el payload del programa               | 1  |

---

### US-06.5 — Definir Estructura de Cursos por Semestre

**Como** administrador,
**Quiero** organizar los cursos del programa por semestres/períodos,
**Para** construir el plan de estudios estructurado del programa.

**Criterios de Aceptación:**

```gherkin
Scenario: Layout visual por semestres
  Given que el administrador está en la sección de estructura curricular
  When visualiza el plan de estudios
  Then se muestra una interfaz con una columna por semestre

Scenario: Cursos dentro de cada semestre
  Given que un semestre tiene cursos asignados
  When el administrador visualiza esa columna
  Then los cursos aparecen como tarjetas dentro del semestre

Scenario: Agregar curso a un semestre
  Given que el administrador está en la vista de estructura curricular
  When hace clic en el botón de agregar cursos de un semestre
  Then se abre un modal selector de cursos desde el catálogo

Scenario: Eliminar curso de un semestre
  Given que un semestre tiene cursos asignados
  When el administrador elimina un curso de un semestre
  Then el curso es removido de ese semestre pero permanece en el catálogo

Scenario: Contador total de cursos en el programa
  Given que el administrador está viendo la estructura curricular
  When visualiza el resumen del programa
  Then se muestra el total de cursos asignados al programa

Scenario: Persistencia de la estructura al guardar
  Given que el administrador ha configurado la estructura por semestres
  When guarda el programa
  Then la estructura semestral se guarda junto con los demás datos del programa
```

**Prioridad:** High | **SP:** 13

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-06.5.1 | Diseñar layout horizontal de columnas por semestre      | 3  |
| ST-06.5.2 | Renderizar tarjetas de cursos dentro de cada semestre   | 2  |
| ST-06.5.3 | Construir modal selector de cursos desde el catálogo    | 3  |
| ST-06.5.4 | Implementar lógica de agregar/quitar curso por semestre | 2  |
| ST-06.5.5 | Mostrar contador total de cursos en el programa         | 1  |
| ST-06.5.6 | Integrar estructura semestral en el payload de la API   | 2  |

---

### US-06.6 — Destacar Programa Académico

**Como** administrador,
**Quiero** marcar un programa como "Destacado",
**Para** que aparezca resaltado en la plataforma estudiantil.

**Criterios de Aceptación:**

```gherkin
Scenario: Toggle de destacado en el formulario del programa
  Given que el administrador está en el formulario de programa
  When activa o desactiva el toggle "Destacado"
  Then el estado del programa cambia a destacado o no destacado

Scenario: Indicador visual de programa destacado en el listado
  Given que un programa está marcado como "Destacado"
  When el administrador visualiza la tarjeta de ese programa en el listado
  Then la tarjeta muestra un icono de estrella indicando que está destacado

Scenario: Persistencia del estado destacado al editar
  Given que el administrador abre un programa destacado en modo edición
  When visualiza el formulario
  Then el toggle "Destacado" aparece activado
```

**Prioridad:** Low | **SP:** 2

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-06.6.1 | Implementar toggle y lógica de "Destacado"              | 1  |
| ST-06.6.2 | Mostrar indicador visual (estrella) en tarjeta          | 1  |

---

### US-06.7 — Editar Programa Académico

**Como** administrador,
**Quiero** editar un programa existente,
**Para** actualizar su información, estructura o cursos asignados.

**Criterios de Aceptación:**

```gherkin
Scenario: Pre-carga completa de datos al editar programa
  Given que el administrador hace clic en "Editar" sobre un programa
  When se abre el formulario de edición
  Then todos los campos del programa se pre-cargan con sus datos actuales

Scenario: Pre-carga de elementos relacionados al editar
  Given que el administrador está en el formulario de edición de un programa
  When visualiza las secciones de selección
  Then competencias, áreas, tags y semestres aparecen pre-cargados con los valores actuales

Scenario: Toast de confirmación al guardar cambios del programa
  Given que el administrador ha realizado cambios en un programa
  When guarda los cambios
  Then aparece un toast de confirmación
```

**Prioridad:** High | **SP:** 5

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-06.7.1 | Integrar API GET /programas/:id para cargar datos       | 2  |
| ST-06.7.2 | Pre-cargar todos los campos, selecciones y semestres    | 3  |
| ST-06.7.3 | Integrar API PUT /programas/:id                         | 2  |

---

### US-06.8 — Eliminar Programa Académico

**Como** administrador,
**Quiero** eliminar un programa académico del sistema,
**Para** mantener actualizada la oferta registrada.

**Criterios de Aceptación:**

```gherkin
Scenario: Botón de eliminar en tarjeta de programa
  Given que el administrador está en el listado de programas
  When visualiza una tarjeta de programa
  Then la tarjeta tiene un botón "Eliminar"

Scenario: Modal de confirmación antes de eliminar programa
  Given que el administrador hace clic en "Eliminar" sobre un programa
  When el sistema procesa la acción
  Then se muestra un modal de confirmación antes de ejecutar la eliminación

Scenario: Toast de confirmación tras eliminar programa
  Given que el administrador confirma la eliminación de un programa
  When el sistema lo elimina exitosamente
  Then se muestra un toast de confirmación
```

**Prioridad:** Medium | **SP:** 3

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-06.8.1 | Modal de confirmación de eliminación                    | 2  |
| ST-06.8.2 | Integrar API DELETE /programas/:id                      | 2  |

---

---

# EP-07 — Gestión de Micro Aprendizajes

**Descripción:** Módulo para crear y administrar módulos de aprendizaje cortos (Workshops, Seminarios, Talleres, Diplomados, Masterclasses) con estructura de lecciones, precio y modalidad.
**Prioridad:** High
**Estado:** In Progress

---

### US-07.1 — Listar Micro Aprendizajes

**Como** administrador,
**Quiero** ver todos los micro aprendizajes en una tabla,
**Para** gestionar el catálogo de formación complementaria.

**Criterios de Aceptación:**

```gherkin
Scenario: Tabla de micro aprendizajes con columnas completas
  Given que existen micro aprendizajes registrados
  When el administrador accede a la sección de Micro Aprendizajes
  Then se muestra una tabla con columnas: Nombre, Modalidad, Tipo, Destacado, Precio, Acciones

Scenario: Pills de colores por modalidad y tipo
  Given que el administrador está viendo la tabla de micro aprendizajes
  When visualiza una fila
  Then se muestran pills de colores diferenciados por modalidad (Virtual/Híbrido) y tipo

Scenario: Badge de destacado en la tabla
  Given que un micro aprendizaje está marcado como "Destacado"
  When el administrador visualiza su fila en la tabla
  Then la fila muestra un badge "Destacado"

Scenario: Precio formateado
  Given que un micro aprendizaje tiene precio asignado
  When el administrador visualiza la columna de precio
  Then el precio se muestra formateado con separador de miles

Scenario: Buscador en tiempo real de micro aprendizajes
  Given que el administrador está en la vista de Micro Aprendizajes
  When escribe texto en el buscador
  Then la tabla se filtra en tiempo real

Scenario: Botones de acción por fila en micro aprendizajes
  Given que el administrador está viendo la tabla de micro aprendizajes
  When visualiza una fila
  Then cada fila tiene botones: Editar, Eliminar y Ver Lecciones
```

**Prioridad:** High | **SP:** 3

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-07.1.1 | Integrar API GET /microaprendizajes                     | 2  |
| ST-07.1.2 | Renderizar tabla con badges de modalidad y tipo         | 2  |
| ST-07.1.3 | Implementar buscador y contador                         | 1  |

---

### US-07.2 — Crear Micro Aprendizaje

**Como** administrador,
**Quiero** crear un nuevo micro aprendizaje,
**Para** ampliar la oferta de formación complementaria.

**Criterios de Aceptación:**

```gherkin
Scenario: Campos del formulario de creación de micro aprendizaje
  Given que el administrador accede al formulario de nuevo micro aprendizaje
  When visualiza el formulario
  Then encuentra campos: Nombre (obligatorio), Descripción (obligatorio), Modalidad, Tipo, Categoría y Precio

Scenario: Toggle de destacado en micro aprendizaje
  Given que el administrador está completando el formulario
  When activa el toggle "Destacado"
  Then el micro aprendizaje queda marcado como destacado

Scenario: Validación del precio
  Given que el administrador ingresa un valor en el campo Precio
  When el valor es menor a 0
  Then se muestra un mensaje de error indicando que el precio debe ser mayor o igual a 0

Scenario: Validación de campos obligatorios del micro aprendizaje
  Given que el administrador deja campos obligatorios vacíos
  When intenta guardar el micro aprendizaje
  Then se muestran mensajes de error visual en cada campo faltante

Scenario: Toast de éxito al crear micro aprendizaje
  Given que el administrador ha completado correctamente el formulario
  When guarda el nuevo micro aprendizaje
  Then aparece un toast de éxito
```

**Prioridad:** High | **SP:** 5

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-07.2.1 | Diseñar formulario de creación de micro aprendizaje     | 2  |
| ST-07.2.2 | Implementar validación completa de campos               | 2  |
| ST-07.2.3 | Implementar toggle "Destacado"                          | 1  |
| ST-07.2.4 | Integrar API POST /microaprendizajes                    | 2  |

---

### US-07.3 — Editar Micro Aprendizaje

**Como** administrador,
**Quiero** editar un micro aprendizaje existente,
**Para** actualizar su información.

**Criterios de Aceptación:**

```gherkin
Scenario: Pre-carga de datos al editar micro aprendizaje
  Given que el administrador hace clic en "Editar" sobre un micro aprendizaje
  When se abre el formulario de edición
  Then todos los campos se pre-cargan con los datos actuales del módulo

Scenario: Validación en modo edición
  Given que el administrador está editando un micro aprendizaje
  When intenta guardar con campos obligatorios vacíos
  Then se aplican las mismas validaciones que en la creación

Scenario: Toast de confirmación al guardar cambios del micro aprendizaje
  Given que el administrador ha realizado cambios en un micro aprendizaje
  When guarda los cambios
  Then aparece un toast de confirmación
```

**Prioridad:** High | **SP:** 3

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-07.3.1 | Integrar API GET /microaprendizajes/:id                 | 2  |
| ST-07.3.2 | Pre-cargar campos del formulario                        | 1  |
| ST-07.3.3 | Integrar API PUT /microaprendizajes/:id                 | 2  |

---

### US-07.4 — Eliminar Micro Aprendizaje

**Como** administrador,
**Quiero** eliminar un micro aprendizaje del sistema,
**Para** remover módulos que ya no están disponibles.

**Criterios de Aceptación:**

```gherkin
Scenario: Botón de eliminar en la tabla de micro aprendizajes
  Given que el administrador está viendo la tabla de micro aprendizajes
  When visualiza una fila
  Then la fila tiene un botón "Eliminar"

Scenario: Modal de confirmación antes de eliminar micro aprendizaje
  Given que el administrador hace clic en "Eliminar" sobre un micro aprendizaje
  When el sistema procesa la acción
  Then se muestra un modal de confirmación antes de ejecutar la eliminación

Scenario: Toast de confirmación tras eliminar micro aprendizaje
  Given que el administrador confirma la eliminación
  When el sistema lo elimina exitosamente
  Then se muestra un toast de confirmación
```

**Prioridad:** Medium | **SP:** 3

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-07.4.1 | Modal de confirmación de eliminación                    | 2  |
| ST-07.4.2 | Integrar API DELETE /microaprendizajes/:id              | 2  |

---

### US-07.5 — Gestionar Lecciones de un Micro Aprendizaje

**Como** administrador,
**Quiero** agregar, editar y eliminar lecciones dentro de un micro aprendizaje,
**Para** estructurar el contenido del módulo.

**Criterios de Aceptación:**

```gherkin
Scenario: Acceso a la vista de lecciones
  Given que el administrador está en la tabla de micro aprendizajes
  When hace clic en "Ver Lecciones" de un módulo
  Then se abre la vista de "Estructura de Lecciones" del micro aprendizaje seleccionado

Scenario: Listado de lecciones con su información
  Given que el administrador está en la vista de lecciones
  When visualiza el listado
  Then cada lección muestra: Nombre, Descripción y Duración en minutos

Scenario: Formulario para agregar nueva lección
  Given que el administrador está en la vista de lecciones
  When accede al formulario de nueva lección
  Then puede ingresar Nombre, Descripción y Duración en minutos

Scenario: Botones de edición y eliminación por lección
  Given que el administrador está viendo el listado de lecciones
  When visualiza una lección
  Then cada lección tiene botones Editar y Eliminar

Scenario: Panel lateral con resumen del micro aprendizaje
  Given que el administrador está en la vista de lecciones
  When visualiza la pantalla completa
  Then se muestra un panel lateral con el resumen del micro aprendizaje asociado

Scenario: Breadcrumb de navegación contextual
  Given que el administrador está en la vista de lecciones
  When observa la navegación en la parte superior
  Then se muestra el breadcrumb: Micro Aprendizajes > [Nombre del Módulo] > Lecciones
```

**Prioridad:** High | **SP:** 8

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-07.5.1 | Diseñar vista de gestión de lecciones                   | 2  |
| ST-07.5.2 | Implementar formulario CRUD de lecciones                | 3  |
| ST-07.5.3 | Integrar APIs de lecciones (GET/POST/PUT/DELETE)        | 3  |
| ST-07.5.4 | Implementar panel lateral con resumen del módulo        | 1  |
| ST-07.5.5 | Implementar breadcrumb de navegación contextual         | 1  |

---

---

# EP-08 — Persistencia de Datos y Backend

**Descripción:** Implementar el backend y la capa de persistencia para que todos los datos del sistema se almacenen en una base de datos real y sean accesibles a través de APIs REST.
**Prioridad:** Critical
**Estado:** To Do

---

### US-08.1 — API REST de Competencias

**Como** desarrollador,
**Quiero** una API REST para gestionar competencias,
**Para** que el frontend pueda hacer operaciones CRUD con persistencia real.

**Criterios de Aceptación:**

```gherkin
Scenario: Listar todas las competencias
  Given que existen competencias en la base de datos
  When se hace una petición GET a /api/competencias
  Then la respuesta retorna un listado de todas las competencias con código HTTP 200

Scenario: Obtener competencia por ID
  Given que existe una competencia con un ID específico
  When se hace una petición GET a /api/competencias/:id
  Then la respuesta retorna la competencia con código HTTP 200

Scenario: Obtener competencia inexistente
  Given que no existe una competencia con el ID solicitado
  When se hace una petición GET a /api/competencias/:id
  Then la respuesta retorna código HTTP 404

Scenario: Crear nueva competencia
  Given que el cliente envía datos válidos de competencia
  When se hace una petición POST a /api/competencias
  Then la competencia es creada y la respuesta retorna código HTTP 201

Scenario: Actualizar competencia existente
  Given que existe una competencia con un ID específico
  When se hace una petición PUT a /api/competencias/:id con datos válidos
  Then la competencia es actualizada y la respuesta retorna código HTTP 200

Scenario: Eliminar competencia existente
  Given que existe una competencia con un ID específico
  When se hace una petición DELETE a /api/competencias/:id
  Then la competencia es eliminada y la respuesta retorna código HTTP 200

Scenario: Error por datos inválidos al crear o actualizar
  Given que el cliente envía datos con campos obligatorios faltantes
  When se hace una petición POST o PUT
  Then la respuesta retorna código HTTP 400
```

**Prioridad:** Critical | **SP:** 5

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-08.1.1 | Definir esquema de base de datos para Competencias      | 1  |
| ST-08.1.2 | Implementar endpoints CRUD de Competencias              | 3  |
| ST-08.1.3 | Validaciones de input en el servidor                    | 2  |
| ST-08.1.4 | Escribir tests de integración para cada endpoint        | 3  |

---

### US-08.2 — API REST de Resultados de Aprendizaje

**Como** desarrollador,
**Quiero** una API REST para gestionar Resultados de Aprendizaje,
**Para** persistir y consultar los RAs del sistema.

**Criterios de Aceptación:**

```gherkin
Scenario: CRUD completo de Resultados de Aprendizaje
  Given que el sistema tiene la API de RAs configurada
  When se realizan peticiones GET, POST, PUT y DELETE a /api/resultados
  Then cada operación retorna el código HTTP correspondiente (200, 201, 404, 400)

Scenario: Filtrar RAs por competencia asociada
  Given que existen RAs asociados a una competencia específica
  When se hace una petición GET a /api/resultados con filtro por competencia
  Then la respuesta retorna únicamente los RAs de esa competencia
```

**Prioridad:** Critical | **SP:** 5

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-08.2.1 | Definir esquema de BD para Resultados de Aprendizaje    | 1  |
| ST-08.2.2 | Implementar endpoints CRUD de Resultados                | 3  |
| ST-08.2.3 | Endpoint para listar RAs por competencia                | 2  |
| ST-08.2.4 | Tests de integración                                    | 3  |

---

### US-08.3 — API REST de Cursos

**Como** desarrollador,
**Quiero** una API REST para gestionar Cursos con todas sus relaciones,
**Para** persistir cursos con imágenes, áreas y asociaciones Competencia-RA.

**Criterios de Aceptación:**

```gherkin
Scenario: CRUD completo de Cursos
  Given que el sistema tiene la API de Cursos configurada
  When se realizan peticiones GET, POST, PUT y DELETE a /api/cursos
  Then cada operación retorna el código HTTP correspondiente (200, 201, 404, 400)

Scenario: Subida y almacenamiento de imágenes de cursos
  Given que el cliente envía una imagen válida junto con los datos del curso
  When se hace una petición POST o PUT a /api/cursos
  Then la imagen es almacenada y su URL es retornada en la respuesta

Scenario: Gestión de asociaciones Competencia-RA-Nivel
  Given que existe un endpoint para gestionar asociaciones de cursos
  When se hace una petición para crear, actualizar o eliminar una asociación Competencia-RA
  Then la asociación es persistida con su nivel de dominio (I/F/V)
```

**Prioridad:** Critical | **SP:** 8

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-08.3.1 | Definir esquema de BD para Cursos (con tablas relacion) | 2  |
| ST-08.3.2 | Implementar endpoints CRUD de Cursos                    | 3  |
| ST-08.3.3 | Implementar endpoint de subida de imágenes              | 3  |
| ST-08.3.4 | Implementar endpoints de asociaciones Comp-RA           | 3  |
| ST-08.3.5 | Tests de integración                                    | 3  |

---

### US-08.4 — API REST de Programas Académicos

**Como** desarrollador,
**Quiero** una API REST para gestionar Programas con su estructura semestral,
**Para** persistir la información completa de los programas de posgrado.

**Criterios de Aceptación:**

```gherkin
Scenario: CRUD completo de Programas Académicos
  Given que el sistema tiene la API de Programas configurada
  When se realizan peticiones GET, POST, PUT y DELETE a /api/programas
  Then cada operación retorna el código HTTP correspondiente (200, 201, 404, 400)

Scenario: Persistencia de estructura semestral
  Given que el cliente envía un programa con estructura de semestres y cursos
  When se hace una petición POST o PUT a /api/programas
  Then la estructura semestral es persistida correctamente

Scenario: Filtrado de programas por criterios
  Given que existen programas con distintos tipos, modalidades y estado destacado
  When se hace una petición GET a /api/programas con parámetros de filtro (tipo, modalidad, destacado)
  Then la respuesta retorna únicamente los programas que cumplen los criterios
```

**Prioridad:** Critical | **SP:** 8

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-08.4.1 | Definir esquema de BD para Programas y semestres        | 2  |
| ST-08.4.2 | Implementar endpoints CRUD de Programas                 | 3  |
| ST-08.4.3 | Endpoint para gestionar estructura semestral            | 3  |
| ST-08.4.4 | Filtros de consulta (tipo, modalidad, destacado)        | 2  |
| ST-08.4.5 | Tests de integración                                    | 3  |

---

### US-08.5 — API REST de Micro Aprendizajes y Lecciones

**Como** desarrollador,
**Quiero** una API REST para gestionar Micro Aprendizajes y sus lecciones,
**Para** persistir el catálogo de formación complementaria.

**Criterios de Aceptación:**

```gherkin
Scenario: CRUD completo de Micro Aprendizajes
  Given que el sistema tiene la API de Micro Aprendizajes configurada
  When se realizan peticiones GET, POST, PUT y DELETE a /api/microaprendizajes
  Then cada operación retorna el código HTTP correspondiente (200, 201, 404, 400)

Scenario: CRUD de lecciones como sub-recurso
  Given que existe un micro aprendizaje con un ID específico
  When se realizan peticiones GET, POST, PUT y DELETE a /api/microaprendizajes/:id/lecciones
  Then las lecciones son gestionadas como sub-recurso del micro aprendizaje con los códigos HTTP correctos
```

**Prioridad:** Critical | **SP:** 8

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-08.5.1 | Definir esquema BD para Micro Aprendizajes y Lecciones  | 2  |
| ST-08.5.2 | Implementar CRUD de Micro Aprendizajes                  | 3  |
| ST-08.5.3 | Implementar CRUD de Lecciones como sub-recurso          | 3  |
| ST-08.5.4 | Tests de integración                                    | 3  |

---

---

# EP-09 — Diseño del Sistema y Experiencia de Usuario

**Descripción:** Consolidar el sistema de diseño visual, los componentes reutilizables y los patrones de interacción para garantizar consistencia en toda la aplicación.
**Prioridad:** Medium
**Estado:** In Progress

---

### US-09.1 — Sistema de Notificaciones (Toast)

**Como** administrador,
**Quiero** recibir notificaciones visuales al completar acciones,
**Para** saber si las operaciones fueron exitosas o si ocurrió un error.

**Criterios de Aceptación:**

```gherkin
Scenario: Toast de éxito al crear o actualizar
  Given que el administrador crea o actualiza un registro exitosamente
  When la operación finaliza
  Then se muestra un toast verde de éxito

Scenario: Toast de eliminación
  Given que el administrador elimina un registro exitosamente
  When la operación finaliza
  Then se muestra un toast rojo de confirmación de eliminación

Scenario: Toast de error al fallar una operación
  Given que una operación falla en el sistema
  When el error es detectado
  Then se muestra un toast naranja indicando el error

Scenario: Posición del toast
  Given que se dispara cualquier toast
  When aparece en pantalla
  Then se muestra en la esquina inferior derecha de la pantalla

Scenario: Auto-dismiss del toast
  Given que un toast ha aparecido en pantalla
  When han transcurrido 2.5 segundos
  Then el toast se desvanece automáticamente

Scenario: Animación de aparición del toast
  Given que se dispara un toast
  When aparece en pantalla
  Then se muestra con una animación slide-up
```

**Prioridad:** High | **SP:** 3

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-09.1.1 | Crear componente Toast reutilizable                     | 2  |
| ST-09.1.2 | Implementar tipos: success, error, warning, info        | 1  |
| ST-09.1.3 | Implementar animaciones y auto-dismiss                  | 1  |

---

### US-09.2 — Sistema de Modales

**Como** administrador,
**Quiero** que los modales de selección sean consistentes y funcionales,
**Para** realizar selecciones de datos de forma cómoda en cualquier sección.

**Criterios de Aceptación:**

```gherkin
Scenario: Estructura del modal
  Given que el administrador abre cualquier modal de selección
  When el modal aparece en pantalla
  Then tiene overlay oscuro, encabezado, cuerpo scrollable y footer

Scenario: Buscador integrado en el modal
  Given que el administrador está dentro de un modal
  When escribe en el buscador interno
  Then la lista de opciones se filtra en tiempo real

Scenario: Soporte para selección única y múltiple
  Given que el administrador está usando un modal
  When el modal está configurado para selección única o múltiple
  Then permite seleccionar uno o varios elementos según la configuración

Scenario: Botones de acción en el footer del modal
  Given que el administrador está dentro de un modal
  When visualiza el footer
  Then encuentra los botones "Cancelar" y "Confirmar"

Scenario: Cerrar modal con Escape
  Given que el administrador tiene un modal abierto
  When presiona la tecla Escape
  Then el modal se cierra sin guardar cambios

Scenario: Cerrar modal con clic en overlay
  Given que el administrador tiene un modal abierto
  When hace clic en el overlay oscuro fuera del modal
  Then el modal se cierra sin guardar cambios
```

**Prioridad:** High | **SP:** 5

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-09.2.1 | Crear componente Modal genérico y reutilizable          | 3  |
| ST-09.2.2 | Implementar buscador interno del modal                  | 1  |
| ST-09.2.3 | Soporte para modo single-select y multi-select          | 2  |
| ST-09.2.4 | Cerrar con Escape y clic en overlay                     | 1  |

---

### US-09.3 — Diseño Responsive

**Como** administrador que puede acceder desde distintos dispositivos,
**Quiero** que la aplicación funcione correctamente en móvil y desktop,
**Para** administrar el contenido desde cualquier lugar.

**Criterios de Aceptación:**

```gherkin
Scenario: Layout del dashboard en móvil
  Given que el administrador accede al dashboard desde un móvil
  When la página carga
  Then el layout muestra 1 columna

Scenario: Layout del dashboard en desktop
  Given que el administrador accede al dashboard desde un desktop
  When la página carga
  Then el layout muestra 3 columnas

Scenario: Scroll horizontal en tablas en pantallas pequeñas
  Given que el administrador accede a una sección con tabla desde un dispositivo móvil
  When la tabla no cabe en el ancho de la pantalla
  Then la tabla tiene scroll horizontal disponible

Scenario: Formularios adaptados al ancho de pantalla
  Given que el administrador accede a un formulario desde cualquier dispositivo
  When la pantalla es pequeña
  Then el formulario se adapta correctamente al ancho disponible

Scenario: Botones con tamaño adecuado para táctil
  Given que el administrador usa la aplicación desde un dispositivo táctil
  When visualiza los botones de acción
  Then los botones son suficientemente grandes para interacción táctil
```

**Prioridad:** Medium | **SP:** 5

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-09.3.1 | Auditar y corregir responsive en todas las páginas      | 3  |
| ST-09.3.2 | Implementar scroll horizontal en tablas en móvil        | 1  |
| ST-09.3.3 | Ajustar tamaños de botones para interacción táctil      | 1  |

---

### US-09.4 — Validación Visual de Formularios

**Como** administrador,
**Quiero** recibir feedback visual inmediato cuando un formulario tiene errores,
**Para** saber exactamente qué campos necesitan corrección antes de guardar.

**Criterios de Aceptación:**

```gherkin
Scenario: Borde rojo en campo obligatorio vacío
  Given que el administrador intenta guardar un formulario con campos obligatorios vacíos
  When el sistema valida el formulario
  Then los campos vacíos muestran un borde rojo

Scenario: Animación shake en campo con error
  Given que un campo tiene error de validación
  When el sistema lo resalta
  Then el campo ejecuta una animación de "shake" para llamar la atención

Scenario: Mensaje de error descriptivo bajo el campo
  Given que un campo tiene error de validación
  When el administrador visualiza el campo
  Then se muestra un mensaje de error descriptivo debajo del campo

Scenario: Focus automático al primer campo con error
  Given que el formulario tiene múltiples campos con error
  When el sistema valida al intentar guardar
  Then el foco se mueve automáticamente al primer campo con error
```

**Prioridad:** High | **SP:** 3

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-09.4.1 | Estandarizar estilos de error en todos los formularios  | 2  |
| ST-09.4.2 | Implementar animación shake en campos inválidos         | 1  |
| ST-09.4.3 | Mover focus automáticamente al primer campo con error   | 1  |

---

### US-09.5 — Estados de Carga (Loading States)

**Como** administrador,
**Quiero** ver indicadores de carga mientras la aplicación obtiene o guarda datos,
**Para** saber que la aplicación está procesando y no está bloqueada.

**Criterios de Aceptación:**

```gherkin
Scenario: Skeleton loader o spinner al cargar listados
  Given que el administrador navega a una sección con listado
  When los datos aún están siendo obtenidos de la API
  Then se muestra un skeleton loader o spinner en lugar del contenido

Scenario: Estado "Guardando..." en botón de submit
  Given que el administrador hace clic en guardar un formulario
  When la petición a la API está en proceso
  Then el botón de guardado muestra el texto "Guardando..."

Scenario: Botones deshabilitados durante el procesamiento
  Given que el administrador ha iniciado una operación de guardado
  When la petición a la API está en proceso
  Then los botones de acción se deshabilitan para evitar envíos duplicados
```

**Prioridad:** Medium | **SP:** 3

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-09.5.1 | Implementar skeleton loader para listados               | 2  |
| ST-09.5.2 | Deshabilitar botones y mostrar spinner durante guardado | 2  |

---

---

# RESUMEN EJECUTIVO

## Tabla de Épicas

| ID    | Épica                                     | User Stories | Subtareas | SP Total | Prioridad |
|-------|-------------------------------------------|:------------:|:---------:|:--------:|-----------|
| EP-02 | Dashboard y Navegación Principal          | 3            | 10        | 18       | High      |
| EP-03 | Gestión de Competencias                   | 5            | 21        | 23       | High      |
| EP-04 | Gestión de Resultados de Aprendizaje      | 5            | 14        | 18       | High      |
| EP-05 | Gestión de Cursos                         | 7            | 27        | 42       | High      |
| EP-06 | Gestión de Programas Académicos           | 8            | 30        | 57       | High      |
| EP-07 | Gestión de Micro Aprendizajes             | 5            | 18        | 35       | High      |
| EP-08 | Persistencia de Datos y Backend           | 5            | 23        | 52       | Critical  |
| EP-09 | Diseño del Sistema y Experiencia de Usuario | 5          | 17        | 24       | Medium    |
| **TOTAL** |                                       | **43**       | **160**   | **269**  |           |

---

## Distribución por Prioridad

| Prioridad  | Épicas | Story Points |
|------------|:------:|:------------:|
| Critical   | 1      | 52           |
| High       | 6      | 193          |
| Medium     | 1      | 24           |
| Low        | 0      | —            |

---

## Estado Actual del Prototipo

| Módulo                     | Estado Funcional            | Persistencia |
|----------------------------|-----------------------------|:------------:|
| Dashboard / Navegación     | Implementado (HTML estático) | Sin backend |
| Competencias               | CRUD completo en UI         | Solo memoria |
| Resultados de Aprendizaje  | CRUD completo en UI         | Solo memoria |
| Cursos                     | CRUD completo en UI         | Solo memoria |
| Programas Académicos       | CRUD completo en UI         | Solo memoria |
| Micro Aprendizajes         | CRUD completo en UI         | Solo memoria |
| Backend / API REST         | No implementado             | —            |

---

*Documento generado el 2026-04-01 basado en análisis del prototipo CoursePlace Admin Panel.*
