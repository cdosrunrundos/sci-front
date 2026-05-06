# Backlog Generado — Ingreso de IPC manual

> Documento generado a partir de: resultado-analisis.md consolidado del módulo Ingreso de IPC manual  
> Fecha: 2026-05-06

---

## Índice de Épicas

| ID | Nombre | N° de US |
|----|--------|----------|
| EP001 | Gestión manual y consulta de IPC | 3 |
| EP002 | Actualización automática de IPC desde TU190 | 2 |
| EP003 | Exportación de registros IPC | 1 |
| EP004 | Uso de IPC en Balance AXI | 3 |

---

## Definition of Ready (DoR)

- [ ] La User Story está redactada con narrativa, precondición y postcondición alineadas al proceso de IPC manual.
- [ ] La User Story tiene trazabilidad explícita a su épica y a los requerimientos funcionales de origen del análisis consolidado.
- [ ] Los criterios de aceptación están definidos con al menos un escenario de camino feliz y uno alternativo o de error.
- [ ] El período funcional alcanzado por la historia está claro, considerando que la operatoria aplica desde diciembre de 2026 en adelante.
- [ ] Las dependencias con datos provenientes de TU190, vigencia del IPC o uso en Balance AXI están identificadas cuando correspondan.
- [ ] No existen dudas funcionales abiertas con el referente de negocio o el analista funcional para la historia a planificar.
- [ ] La historia puede ser estimada por el equipo sin requerir definiciones adicionales de alcance.

## Definition of Done (DoD)

- [ ] Todos los escenarios Gherkin de la User Story fueron validados satisfactoriamente.
- [ ] El comportamiento final respeta las reglas funcionales de vigencia, origen del IPC y restricciones sobre Balance AXI Actual.
- [ ] El analista funcional validó que la solución implementada cumple la historia y sus criterios de aceptación.
- [ ] El referente usuario o de negocio confirmó el resultado esperado para la operatoria alcanzada por la historia.
- [ ] La documentación funcional vigente del módulo IPC quedó actualizada si la historia modificó comportamiento observable.
- [ ] No se introdujeron regresiones sobre alta manual, modificación, recepción automática desde TU190, exportación o uso en balance.

---

## EP001 — Gestión manual y consulta de IPC

Esta épica cubre el acceso a la pantalla de IPC, la consulta de registros y la operación manual de alta y modificación de valores de IPC vigentes.

### US001001 — Consultar registros de IPC

**Precondición**
El usuario ingresó a la sección Informativas y la funcionalidad aplica para períodos de diciembre de 2026 en adelante.

**Narrativa**
Como Usuario de Informativas quiero acceder al submenú IPC y consultar registros por período y estado para revisar los valores disponibles y su vigencia.

**Postcondición**
El usuario visualiza la grilla de IPC con los registros que cumplen los filtros aplicados.

**DoR — Definition of Ready**
- [ ] Narrativa completa y sin ambigüedades
- [ ] Precondición y postcondición definidas
- [ ] Criterios de aceptación presentes y verificables
- [ ] Sin dependencias bloqueantes no resueltas
- [ ] Estimable por el equipo de desarrollo

**Criterios de Aceptación**
- El sistema muestra el submenú IPC dentro de la sección Informativas.
- La pantalla IPC expone los filtros Período y Estado con las opciones Vigente y Baja.
- La consulta devuelve únicamente los registros que cumplen con los filtros ingresados.
- La grilla muestra como mínimo las columnas Período, IPC, Estado, Fecha alta, Fecha baja y Usuario.

**Items pendientes para completar el DoR**
Ninguno.

**Escenarios Gherkin**

**Escenario 1: Consulta filtrada de registros vigentes**
```gherkin
Given el usuario accede al submenú IPC dentro de Informativas
And existen registros de IPC para períodos habilitados
When el usuario consulta por un período y estado Vigente
Then el sistema muestra solo los registros que cumplen ambos filtros
And la grilla exhibe Período, IPC, Estado, Fecha alta, Fecha baja y Usuario
```

**Escenario 2: Consulta sin resultados para el filtro aplicado**
```gherkin
Given el usuario accede a la pantalla IPC
And no existen registros que cumplan el período y estado seleccionados
When el usuario ejecuta la consulta
Then el sistema no muestra registros en la grilla para ese filtro
And mantiene visibles los filtros de búsqueda disponibles
```

### US001002 — Registrar un IPC manual

**Precondición**
El usuario se encuentra en la pantalla IPC y el período a informar no posee un registro vigente manual ni automático.

**Narrativa**
Como Usuario de Informativas quiero registrar manualmente un valor de IPC para un período sin vigencia existente para poder trabajar provisoriamente con ese dato.

**Postcondición**
Existe un nuevo registro manual de IPC en estado Vigente y con el legajo del usuario informado como usuario de alta.

**DoR — Definition of Ready**
- [ ] Narrativa completa y sin ambigüedades
- [ ] Precondición y postcondición definidas
- [ ] Criterios de aceptación presentes y verificables
- [ ] Sin dependencias bloqueantes no resueltas
- [ ] Estimable por el equipo de desarrollo

**Criterios de Aceptación**
- El sistema permite registrar un IPC manual solo si el período no posee un registro vigente.
- Si el período ya posee un registro IPC vigente, el sistema rechaza el alta.
- Ante rechazo por vigencia existente, el sistema muestra el mensaje "El período ya posee un registro IPC vigente".
- En un alta manual exitosa, el campo Usuario del registro creado se informa con el legajo del usuario que realizó la operación.

**Items pendientes para completar el DoR**
Ninguno.

**Escenarios Gherkin**

**Escenario 1: Alta manual exitosa para período sin vigencia**
```gherkin
Given el usuario se encuentra en la pantalla IPC
And el período seleccionado no posee un registro IPC vigente
When el usuario registra un nuevo IPC manual
Then el sistema crea un registro en estado Vigente para ese período
And informa como usuario de alta el legajo del usuario que realizó la operación
```

**Escenario 2: Rechazo de alta por vigencia existente**
```gherkin
Given el usuario se encuentra en la pantalla IPC
And el período seleccionado ya posee un registro IPC vigente
When el usuario intenta registrar un nuevo IPC manual
Then el sistema rechaza la operación
And muestra el mensaje "El período ya posee un registro IPC vigente"
```

### US001003 — Modificar un IPC manual vigente

**Precondición**
Existe un registro de IPC en estado Vigente cargado manualmente y el usuario se encuentra habilitado para operarlo.

**Narrativa**
Como Usuario de Informativas quiero modificar un IPC manual vigente para corregir su valor sin perder la trazabilidad del registro anterior.

**Postcondición**
El registro manual previo queda en estado Baja y se genera un nuevo registro actualizado en estado Vigente.

**DoR — Definition of Ready**
- [ ] Narrativa completa y sin ambigüedades
- [ ] Precondición y postcondición definidas
- [ ] Criterios de aceptación presentes y verificables
- [ ] Sin dependencias bloqueantes no resueltas
- [ ] Estimable por el equipo de desarrollo

**Criterios de Aceptación**
- El sistema permite modificar únicamente registros manuales en estado Vigente.
- El sistema no permite modificar registros en estado Baja ni registros provenientes de TU190.
- Si se intenta modificar un registro no permitido, el sistema muestra el mensaje "error: solo se pueden modificar registros manuales vigentes".
- Al confirmar una modificación válida, el sistema da de baja el registro anterior y crea un nuevo registro con los datos actualizados en estado Vigente.

**Items pendientes para completar el DoR**
Ninguno.

**Escenarios Gherkin**

**Escenario 1: Modificación exitosa de un registro manual vigente**
```gherkin
Given existe un registro de IPC manual en estado Vigente
When el usuario modifica ese registro
Then el sistema da de baja el registro anterior
And genera un nuevo registro actualizado en estado Vigente
```

**Escenario 2: Rechazo de modificación de registro no editable**
```gherkin
Given el usuario selecciona un registro en estado Baja o proveniente de TU190
When el usuario intenta modificar ese registro
Then el sistema rechaza la operación
And muestra el mensaje "error: solo se pueden modificar registros manuales vigentes"
```

---

## EP002 — Actualización automática de IPC desde TU190

Esta épica cubre la incorporación automática de registros informados por TU190 y las reglas de reemplazo de la vigencia existente para un período.

### US002001 — Registrar IPC automático desde TU190

**Precondición**
El SCI recibe un nuevo valor de IPC desde la interfaz TU190 para un período alcanzado por la funcionalidad.

**Narrativa**
Como Responsable del proceso informativo quiero que el SCI registre automáticamente los IPC recibidos desde TU190 para evitar la carga manual cuando exista dato oficial.

**Postcondición**
Existe un nuevo registro de IPC creado automáticamente con usuario de alta "Sistema".

**DoR — Definition of Ready**
- [ ] Narrativa completa y sin ambigüedades
- [ ] Precondición y postcondición definidas
- [ ] Criterios de aceptación presentes y verificables
- [ ] Sin dependencias bloqueantes no resueltas
- [ ] Estimable por el equipo de desarrollo

**Criterios de Aceptación**
- Al recibir un nuevo IPC desde TU190, el SCI crea automáticamente un registro para el período informado.
- El alta automática no requiere intervención manual del usuario.
- El campo Usuario del registro automático se informa con el valor "Sistema".

**Items pendientes para completar el DoR**
Ninguno.

**Escenarios Gherkin**

**Escenario 1: Alta automática exitosa de IPC desde TU190**
```gherkin
Given el SCI recibe un nuevo IPC desde TU190 para un período habilitado
When el dato es procesado por el sistema
Then el sistema crea un nuevo registro de IPC para ese período
And informa "Sistema" como usuario de alta
```

**Escenario 2: Recepción de IPC para un período fuera del alcance funcional**
```gherkin
Given el SCI recibe un IPC para un período anterior a diciembre de 2026
When el dato es evaluado por la operatoria de IPC manual
Then el sistema no lo considera dentro del alcance de esta funcionalidad
And la operatoria vigente de IPC manual no se aplica sobre ese período
```

### US002002 — Sustituir la vigencia por un IPC de TU190

**Precondición**
Existe un registro de IPC vigente para el período informado y el SCI recibe un nuevo IPC desde TU190 para ese mismo período.

**Narrativa**
Como Responsable del proceso informativo quiero que el IPC recibido desde TU190 pase a ser el registro vigente del período para que el SCI utilice el dato oficial más reciente.

**Postcondición**
El nuevo registro de TU190 queda en estado Vigente y el registro vigente anterior queda en estado Baja.

**DoR — Definition of Ready**
- [ ] Narrativa completa y sin ambigüedades
- [ ] Precondición y postcondición definidas
- [ ] Criterios de aceptación presentes y verificables
- [ ] Sin dependencias bloqueantes no resueltas
- [ ] Estimable por el equipo de desarrollo

**Criterios de Aceptación**
- Si existe un registro manual vigente para el período y llega un IPC desde TU190, el sistema da de baja el registro manual previo.
- Si excepcionalmente el registro vigente previo también fuera automático, el nuevo registro automático lo sustituye y el anterior queda en Baja.
- Luego de la recepción del nuevo IPC desde TU190, solo un registro queda en estado Vigente para el período.

**Items pendientes para completar el DoR**
Ninguno.

**Escenarios Gherkin**

**Escenario 1: Reemplazo de registro manual vigente por IPC oficial**
```gherkin
Given existe un registro manual vigente para un período
And el SCI recibe un nuevo IPC desde TU190 para ese mismo período
When el sistema procesa el nuevo IPC
Then el registro manual previo pasa a estado Baja
And el nuevo registro de TU190 queda en estado Vigente
```

**Escenario 2: Sustitución excepcional de automático por automático**
```gherkin
Given existe un registro automático vigente para un período
And el SCI recibe un nuevo IPC desde TU190 para ese mismo período
When el sistema procesa el nuevo IPC
Then el registro automático previo pasa a estado Baja
And el nuevo registro automático queda como único vigente del período
```

---

## EP003 — Exportación de registros IPC

Esta épica cubre la salida operativa de la información consultada en pantalla para su uso externo o revisión manual.

### US003001 — Exportar la grilla filtrada de IPC

**Precondición**
El usuario ejecutó una consulta de IPC y la grilla presenta resultados según los filtros seleccionados.

**Narrativa**
Como Usuario de Informativas quiero exportar a Excel la grilla filtrada para poder trabajar la información fuera del sistema.

**Postcondición**
El sistema genera un archivo Excel con el contenido de la grilla filtrada en pantalla.

**DoR — Definition of Ready**
- [ ] Narrativa completa y sin ambigüedades
- [ ] Precondición y postcondición definidas
- [ ] Criterios de aceptación presentes y verificables
- [ ] Sin dependencias bloqueantes no resueltas
- [ ] Estimable por el equipo de desarrollo

**Criterios de Aceptación**
- La pantalla IPC expone la acción Exportar.
- Al accionar Exportar, el sistema genera un archivo Excel con los registros visibles en la grilla filtrada.
- El nombre del archivo exportado es "AAAAMM_IPC_SCI".
- Las columnas del archivo exportado mantienen el mismo formato y orden que la grilla en pantalla.

**Items pendientes para completar el DoR**
Ninguno.

**Escenarios Gherkin**

**Escenario 1: Exportación exitosa de la consulta actual**
```gherkin
Given el usuario visualiza una grilla de IPC resultante de una consulta
When el usuario acciona la opción Exportar
Then el sistema genera un archivo Excel llamado "AAAAMM_IPC_SCI"
And el archivo conserva el mismo orden y formato de columnas que la grilla
```

**Escenario 2: Exportación sin registros visibles**
```gherkin
Given el usuario ejecutó una consulta sin resultados visibles en la grilla
When el usuario acciona la opción Exportar
Then el sistema genera el archivo de exportación correspondiente a la consulta aplicada
And el contenido del archivo refleja la ausencia de registros para ese filtro
```

---

## EP004 — Uso de IPC en Balance AXI

Esta épica cubre la aplicación del IPC vigente en el Balance AXI Actual y las restricciones funcionales cuando el balance se apoya en un IPC cargado manualmente.

### US004001 — Aplicar el IPC vigente al Balance AXI Actual

**Precondición**
Existe un Balance AXI Actual para un período en trabajo y existe un único registro IPC vigente para ese período.

**Narrativa**
Como Usuario de Balance quiero que el sistema tome el IPC vigente del período para construir el Balance AXI Actual con el valor aplicable.

**Postcondición**
El Balance AXI Actual utiliza el IPC vigente del período en trabajo, sea de origen manual o automático.

**DoR — Definition of Ready**
- [ ] Narrativa completa y sin ambigüedades
- [ ] Precondición y postcondición definidas
- [ ] Criterios de aceptación presentes y verificables
- [ ] Sin dependencias bloqueantes no resueltas
- [ ] Estimable por el equipo de desarrollo

**Criterios de Aceptación**
- El sistema identifica el registro IPC en estado Vigente correspondiente al período en trabajo.
- El Balance AXI Actual utiliza ese registro IPC vigente para el trabajo preliminar del balance.
- El origen del IPC vigente puede ser manual o automático sin alterar la selección del registro aplicable.

**Items pendientes para completar el DoR**
Ninguno.

**Escenarios Gherkin**

**Escenario 1: Aplicación del IPC vigente al balance del período**
```gherkin
Given existe un Balance AXI Actual para un período en trabajo
And existe un único IPC en estado Vigente para ese período
When el usuario trabaja sobre el balance actual
Then el sistema utiliza el IPC vigente del período
And aplica ese valor al trabajo preliminar del balance
```

**Escenario 2: Selección del IPC vigente independientemente del origen**
```gherkin
Given existe un IPC vigente para el período en trabajo
And el IPC vigente puede ser manual o automático
When el sistema prepara el Balance AXI Actual
Then el sistema toma el registro que se encuentra vigente
And no altera la selección por el origen del dato
```

### US004002 — Restringir el uso de IPC manual al Balance AXI Actual del mismo mes

**Precondición**
Existe un IPC manual vigente y el usuario trabaja sobre un Balance AXI.

**Narrativa**
Como Usuario de Balance quiero que el IPC manual solo pueda utilizarse en el Balance AXI Actual del mes informado para evitar usos fuera del alcance definido.

**Postcondición**
El IPC manual queda habilitado solo para el Balance AXI Actual correspondiente al mismo mes del período del IPC.

**DoR — Definition of Ready**
- [ ] Narrativa completa y sin ambigüedades
- [ ] Precondición y postcondición definidas
- [ ] Criterios de aceptación presentes y verificables
- [ ] Sin dependencias bloqueantes no resueltas
- [ ] Estimable por el equipo de desarrollo

**Criterios de Aceptación**
- Un IPC manual puede utilizarse únicamente en el Balance AXI Actual.
- El sistema solo permite asociar el IPC manual al balance del mismo mes señalado por ese IPC.
- El sistema no habilita el uso del IPC manual en otros balances o períodos distintos.

**Items pendientes para completar el DoR**
Ninguno.

**Escenarios Gherkin**

**Escenario 1: Uso permitido de IPC manual en el mes correspondiente**
```gherkin
Given existe un IPC manual vigente para un período
When el usuario trabaja sobre el Balance AXI Actual del mismo mes
Then el sistema permite utilizar ese IPC manual en ese balance
And mantiene el uso restringido a ese contexto
```

**Escenario 2: Rechazo de uso de IPC manual fuera del alcance permitido**
```gherkin
Given existe un IPC manual vigente para un período
When el usuario intenta utilizarlo en otro balance o en un período distinto
Then el sistema no permite ese uso
And mantiene la restricción al Balance AXI Actual del mismo mes
```

### US004003 — Impedir presentaciones con IPC manual

**Precondición**
El Balance AXI Actual del período está asociado a un IPC manual.

**Narrativa**
Como Usuario de Balance quiero que el sistema impida generar una presentación cuando el balance usa un IPC manual para evitar presentar información construida con un dato provisorio.

**Postcondición**
La presentación no se genera y el usuario recibe un mensaje de error explícito.

**DoR — Definition of Ready**
- [ ] Narrativa completa y sin ambigüedades
- [ ] Precondición y postcondición definidas
- [ ] Criterios de aceptación presentes y verificables
- [ ] Sin dependencias bloqueantes no resueltas
- [ ] Estimable por el equipo de desarrollo

**Criterios de Aceptación**
- Si el Balance AXI Actual está asociado a un IPC manual, el sistema impide generar una presentación.
- Ante el intento de generación, el sistema muestra el mensaje "No esta permitido generar una presentación asociada a un IPC manual".
- Si el Balance AXI Actual utiliza un IPC automático vigente, la restricción anterior no aplica.

**Items pendientes para completar el DoR**
Ninguno.

**Escenarios Gherkin**

**Escenario 1: Bloqueo de presentación con IPC manual**
```gherkin
Given el Balance AXI Actual está asociado a un IPC manual
When el usuario intenta generar una presentación
Then el sistema impide la generación
And muestra el mensaje "No esta permitido generar una presentación asociada a un IPC manual"
```

**Escenario 2: Generación permitida con IPC no manual**
```gherkin
Given el Balance AXI Actual está asociado a un IPC vigente no manual
When el usuario intenta generar una presentación
Then el sistema permite continuar con la generación
And no muestra el mensaje de restricción por IPC manual
```

---