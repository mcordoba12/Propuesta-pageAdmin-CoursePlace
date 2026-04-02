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

# EP-01 — Autenticación y Control de Acceso

**Descripción:** Implementar el sistema de login, gestión de sesiones y control de roles para que solo los administradores autorizados accedan al panel de administración.
**Prioridad:** Critical
**Estado:** To Do

---

### US-01.1 — Inicio de Sesión del Administrador

**Como** administrador del sistema,
**Quiero** poder ingresar con mis credenciales (correo y contraseña),
**Para** acceder de forma segura al panel de administración.

**Criterios de Aceptación:**
- El formulario de login tiene campos de correo y contraseña.
- Se muestra un mensaje de error si las credenciales son incorrectas.
- Se genera un token de sesión al autenticar correctamente.
- Redirige al dashboard después de un login exitoso.
- El campo contraseña muestra/oculta caracteres.

**Prioridad:** Critical | **SP:** 5

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-01.1.1 | Diseñar la vista/página de login con formulario         | 2  |
| ST-01.1.2 | Implementar validación de campos (email, contraseña)    | 1  |
| ST-01.1.3 | Integrar llamada a API de autenticación (POST /auth/login) | 3 |
| ST-01.1.4 | Manejar y almacenar el token JWT en el cliente          | 2  |
| ST-01.1.5 | Redirigir al dashboard post-login                       | 1  |
| ST-01.1.6 | Mostrar mensajes de error según respuesta de API        | 1  |

---

### US-01.2 — Cierre de Sesión

**Como** administrador autenticado,
**Quiero** poder cerrar mi sesión desde cualquier pantalla,
**Para** proteger el acceso al panel cuando no lo esté usando.

**Criterios de Aceptación:**
- Botón de "Cerrar sesión" visible en el header.
- Al cerrar sesión, se elimina el token del cliente.
- Redirige a la página de login.
- Las rutas protegidas no son accesibles sin sesión activa.

**Prioridad:** Critical | **SP:** 3

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-01.2.1 | Agregar botón "Cerrar sesión" en el componente Header   | 1  |
| ST-01.2.2 | Limpiar token de sesión al cerrar sesión                | 1  |
| ST-01.2.3 | Implementar guard de rutas para redirigir a login       | 2  |
| ST-01.2.4 | Manejar expiración automática de sesión (timeout)       | 2  |

---

### US-01.3 — Recuperación de Contraseña

**Como** administrador,
**Quiero** poder recuperar mi contraseña olvidada mediante mi correo,
**Para** no perder acceso al sistema.

**Criterios de Aceptación:**
- Enlace "¿Olvidaste tu contraseña?" en el login.
- Formulario para ingresar correo registrado.
- Se envía email con enlace de recuperación.
- El enlace expira en 30 minutos.

**Prioridad:** Medium | **SP:** 5

#### Subtareas:

| ID      | Descripción                                              | SP |
|---------|----------------------------------------------------------|----|
| ST-01.3.1 | Diseñar vista de recuperación de contraseña             | 2  |
| ST-01.3.2 | Integrar API de envío de email (POST /auth/recovery)    | 3  |
| ST-01.3.3 | Diseñar vista de restablecimiento (con token URL)       | 2  |
| ST-01.3.4 | Validar y actualizar nueva contraseña vía API           | 2  |

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
- El dashboard muestra tarjetas de acceso para las 5 secciones: Competencias, Resultados de Aprendizaje, Programas, Cursos y Micro Aprendizajes.
- Cada tarjeta muestra nombre, descripción e icono representativo.
- Las tarjetas tienen efecto hover con animación visual.
- El header muestra el logo, nombre del sistema y avatar del usuario.
- El diseño es responsive (desktop y móvil).

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
- Cada tarjeta del dashboard muestra el número total de registros de su sección.
- Los contadores se actualizan en tiempo real desde la API.
- Los datos se muestran formateados (ej.: "12 Competencias").

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
- El header muestra el logo de CoursePlace.
- Muestra el título de la sección activa.
- Incluye botón "← Inicio" funcional en todas las páginas interiores.
- Muestra el avatar y nombre del usuario autenticado.
- Es sticky (permanece visible al hacer scroll).

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
- Se listan todas las competencias con: índice (C-001), nombre, descripción y número de RAs asignados.
- Se muestra un contador total de competencias.
- Se muestra un "empty state" cuando no hay registros.
- Las competencias tienen botón de acción "Editar".

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
- Campo de búsqueda visible en la vista de listado.
- La búsqueda filtra en tiempo real (sin necesidad de presionar Enter).
- La búsqueda es case-insensitive.
- Se actualiza el contador según los resultados filtrados.
- Muestra "empty state" si no hay coincidencias.

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
- Formulario con campo Nombre (obligatorio) y Descripción (opcional).
- El nombre no puede estar vacío al guardar (validación con feedback visual).
- Permite asociar Resultados de Aprendizaje mediante un modal de multi-selección.
- El modal de RAs tiene buscador interno.
- Los RAs seleccionados se muestran como badges numerados.
- Al guardar, aparece una notificación de éxito (toast).
- El formulario se resetea después de crear.

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
- Al hacer clic en "Editar", el formulario carga los datos actuales.
- Permite modificar nombre, descripción y RAs.
- Los RAs previamente asignados aparecen ya marcados en el modal.
- Se puede agregar o quitar RAs.
- Al guardar, aparece un toast de confirmación.
- Regresa a la vista de listado tras guardar.

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
- Botón "Eliminar" disponible en la tarjeta de cada competencia.
- Aparece un modal de confirmación antes de eliminar.
- Al confirmar, la competencia se elimina y se refresca la lista.
- Se muestra un toast de confirmación de eliminación.

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
- Lista todos los RAs con: índice (RA-001), nombre, descripción y badge de competencias asociadas.
- Muestra contador total de RAs.
- Empty state cuando no hay registros.
- Cada RA tiene botón "Editar".

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
- Campo de búsqueda con filtrado en tiempo real.
- Búsqueda en nombre y descripción.
- Actualiza contador según resultados.

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
- Formulario con Nombre (obligatorio) y Descripción (opcional).
- Modal de multi-selección de competencias con buscador.
- Las competencias seleccionadas se muestran como badges.
- Validación visual si el nombre está vacío.
- Toast de confirmación al crear.

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
- Formulario pre-cargado con los datos del RA seleccionado.
- Las competencias asociadas aparecen pre-seleccionadas.
- Permite agregar/quitar competencias.
- Toast de confirmación al guardar.

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
- Botón "Eliminar" en la tarjeta de cada RA.
- Modal de confirmación antes de eliminar.
- Toast de confirmación tras la eliminación.

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
- Tabla con columnas: Nombre, Créditos, Horas, Modalidad, Electiva, Comp/RAs, Acciones.
- Badge visual para tipo (Electivo/Obligatorio), créditos, RAs asignados.
- Buscador en tiempo real.
- Botones de "Editar" y "Eliminar" por fila.

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
- Campos: Nombre (obligatorio), Créditos, Horas, Modalidad (Virtual/Presencial/Híbrido), Descripción, Objetivo General.
- Toggle para marcar como Curso Electivo.
- Todos los campos obligatorios son validados antes de guardar.
- Toast de éxito al crear.

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
- Zona de drag & drop o click para seleccionar imagen.
- Formatos aceptados: PNG, JPG, WEBP.
- Límite de tamaño: 5MB.
- Se muestra preview de la imagen seleccionada.
- Botón para eliminar imagen seleccionada.
- Mensaje de error si el formato o tamaño no es válido.

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
- Listado de áreas disponibles: Datos, Frontend, Backend, Cloud, Mobile, IA, Design.
- Selección múltiple mediante chips/checkboxes.
- Las áreas seleccionadas se muestran como chips removibles.
- Persiste la selección al editar el curso.

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
- Modal de 2 pasos: Paso 1 selecciona competencia, Paso 2 selecciona RAs de esa competencia.
- Se puede agregar múltiples pares Competencia-RA.
- Tabla resultante muestra: Competencia, RA, y checkboxes I/F/V (Introduce / Fortalece / Valora).
- Se puede eliminar una asociación de la tabla.
- Persiste la configuración al editar.

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
- Al hacer clic en "Editar", el formulario se pre-carga con todos los datos del curso.
- Se pueden modificar todos los campos, imagen, áreas y Competencias/RAs.
- Toast de confirmación al guardar cambios.

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
- Botón "Eliminar" en cada fila de la tabla.
- Modal de confirmación antes de ejecutar.
- Toast de confirmación tras eliminar.
- La lista se actualiza inmediatamente.

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
- Lista de tarjetas con: imagen, nombre, descripción truncada, tipo, modalidad, créditos, semestres, SNIES, tags y número de cursos.
- Badge de "Destacado" para programas marcados.
- Buscador en tiempo real.
- Contador total de programas.
- Botón "Editar" por tarjeta.

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
- Campos: Nombre (obligatorio), Descripción, Perfil del Egresado, Tipo (Maestría/Especialización/Certificación/Doctorado), Modalidad, SNIES.
- Imagen de portada (drag & drop).
- Tags/palabras clave (chip input con coma o Enter).
- Toggle "Destacado".
- Validación de campos obligatorios.
- Toast de éxito al crear.

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
- Modal de multi-selección con buscador.
- Las competencias seleccionadas se muestran como chips removibles.
- Persiste selección en modo edición.

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
- Selector de áreas con multi-selección.
- Chips removibles de áreas seleccionadas.
- Persiste en modo edición.

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
- Interfaz visual con una columna por semestre.
- Cada semestre muestra sus cursos como tarjetas.
- Botón para agregar cursos a cada semestre (modal selector desde catálogo).
- Se puede eliminar un curso del semestre (sin eliminarlo del catálogo).
- Contador total de cursos en el programa.
- Los cambios se guardan junto con el programa.

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
- Toggle de "Destacado" en el formulario del programa.
- Icono de estrella en la tarjeta del listado cuando está destacado.
- El estado persiste al editar.

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
- Formulario pre-cargado con todos los datos del programa.
- Competencias, áreas, tags y semestres pre-cargados.
- Toast de confirmación al guardar.

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
- Botón "Eliminar" en la tarjeta del programa.
- Modal de confirmación antes de eliminar.
- Toast de confirmación tras eliminar.

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
- Tabla con columnas: Nombre, Modalidad, Tipo, Destacado, Precio, Acciones.
- Pills de colores por modalidad (Virtual/Híbrido) y tipo.
- Badge "Destacado" cuando aplica.
- Precio formateado con separador de miles.
- Buscador en tiempo real.
- Botones: Editar, Eliminar, Ver Lecciones.

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
- Campos: Nombre (obligatorio), Descripción (obligatorio), Modalidad, Tipo, Categoría, Precio.
- Toggle "Destacado".
- Precio debe ser >= 0.
- Validación de todos los campos obligatorios con mensajes de error.
- Toast de éxito al crear.

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
- Formulario pre-cargado con los datos del módulo seleccionado.
- Validación igual a la creación.
- Toast de confirmación al guardar.

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
- Botón "Eliminar" en la fila de la tabla.
- Modal de confirmación antes de ejecutar.
- Toast de confirmación tras eliminar.

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
- Vista de "Estructura de Lecciones" accesible desde la tabla principal.
- Lista de lecciones con: Nombre, Descripción, Duración en minutos.
- Formulario para agregar nueva lección.
- Botones Editar y Eliminar por lección.
- Panel lateral con resumen del micro aprendizaje.
- Breadcrumb de navegación: Micro Aprendizajes > [Nombre] > Lecciones.

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
- `GET /api/competencias` — Lista todas las competencias.
- `GET /api/competencias/:id` — Obtiene una competencia por ID.
- `POST /api/competencias` — Crea competencia.
- `PUT /api/competencias/:id` — Actualiza competencia.
- `DELETE /api/competencias/:id` — Elimina competencia.
- Respuestas con códigos HTTP correctos (200, 201, 404, 400).

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
- CRUD completo: `GET`, `POST`, `PUT`, `DELETE` en `/api/resultados`.
- Soporte para filtrar por competencia asociada.

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
- CRUD completo en `/api/cursos`.
- Soporte para subida y almacenamiento de imágenes.
- Endpoint para gestionar asociaciones Competencia-RA-Nivel.

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
- CRUD completo en `/api/programas`.
- Soporte para estructura semestral (JSON anidado o tabla relacional).
- Filtrado por tipo, modalidad y highlight.

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
- CRUD completo en `/api/microaprendizajes`.
- Sub-recurso: `/api/microaprendizajes/:id/lecciones` con CRUD.

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
- Toast de éxito (verde) al crear o actualizar registros.
- Toast de eliminación (rojo) al borrar un registro.
- Toast de error (naranja) al fallar una operación.
- El toast aparece en la esquina inferior derecha.
- Se desvanece automáticamente después de 2.5 segundos.
- Animación slide-up al aparecer.

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
- Modal con overlay oscuro, encabezado, cuerpo scrollable y footer.
- Buscador integrado dentro del modal.
- Soporte para selección única y múltiple.
- Botones "Cancelar" y "Confirmar" en el footer.
- Se puede cerrar con Escape o clic en el overlay.

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
- El dashboard tiene layout de 1 columna en móvil y 3 en desktop.
- Las tablas tienen scroll horizontal en pantallas pequeñas.
- Los formularios se adaptan al ancho de la pantalla.
- Los botones son suficientemente grandes para interacción táctil.

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
- Los campos obligatorios vacíos muestran borde rojo al intentar guardar.
- Animación de "shake" para llamar la atención al campo con error.
- Mensaje de error descriptivo debajo del campo.
- El foco se mueve automáticamente al primer campo con error.

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
- Skeleton loader o spinner al cargar listados.
- Botones de guardado muestran estado "Guardando..." mientras procesan.
- Los botones se deshabilitan durante el procesamiento.

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
| EP-01 | Autenticación y Control de Acceso         | 3            | 11        | 26       | Critical  |
| EP-02 | Dashboard y Navegación Principal          | 3            | 10        | 18       | High      |
| EP-03 | Gestión de Competencias                   | 5            | 21        | 23       | High      |
| EP-04 | Gestión de Resultados de Aprendizaje      | 5            | 14        | 18       | High      |
| EP-05 | Gestión de Cursos                         | 7            | 27        | 42       | High      |
| EP-06 | Gestión de Programas Académicos           | 8            | 30        | 57       | High      |
| EP-07 | Gestión de Micro Aprendizajes             | 5            | 18        | 35       | High      |
| EP-08 | Persistencia de Datos y Backend           | 5            | 23        | 52       | Critical  |
| EP-09 | Diseño del Sistema y Experiencia de Usuario | 5          | 17        | 24       | Medium    |
| **TOTAL** |                                       | **46**       | **171**   | **295**  |           |

---

## Distribución por Prioridad

| Prioridad  | Épicas | Story Points |
|------------|:------:|:------------:|
| Critical   | 2      | 78           |
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
| Autenticación              | No implementada             | —            |
| Backend / API REST         | No implementado             | —            |

---

*Documento generado el 2026-04-01 basado en análisis del prototipo CoursePlace Admin Panel.*
