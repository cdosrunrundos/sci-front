# EP001 — Gestion manual y consulta de IPC

Esta epica cubre el acceso a la pantalla de IPC, la consulta de registros y la operacion manual de alta y modificacion de valores de IPC vigentes.

## Definition of Ready (DoR)

- [ ] La User Story esta redactada con narrativa, precondicion y postcondicion alineadas al proceso de IPC manual.
- [ ] La User Story tiene trazabilidad explicita a su epica y a los requerimientos funcionales de origen del analisis consolidado.
- [ ] Los criterios de aceptacion estan definidos con al menos un escenario de camino feliz y uno alternativo o de error.
- [ ] El periodo funcional alcanzado por la historia esta claro, considerando que la operatoria aplica desde diciembre de 2026 en adelante.
- [ ] Las dependencias con datos provenientes de TU190, vigencia del IPC o uso en Balance AXI estan identificadas cuando correspondan.
- [ ] No existen dudas funcionales abiertas con el referente de negocio o el analista funcional para la historia a planificar.
- [ ] La historia puede ser estimada por el equipo sin requerir definiciones adicionales de alcance.

### US001001 — Consultar registros de IPC

**Precondicion**
El usuario ingreso a la seccion Informativas y la funcionalidad aplica para periodos de diciembre de 2026 en adelante.

**Narrativa**
Como Usuario de Informativas quiero acceder al submenu IPC y consultar registros por periodo y estado para revisar los valores disponibles y su vigencia.

**Postcondicion**
El usuario visualiza la grilla de IPC con los registros que cumplen los filtros aplicados.

**DoR — Definition of Ready**
- [ ] Narrativa completa y sin ambiguedades
- [ ] Precondicion y postcondicion definidas
- [ ] Criterios de aceptacion presentes y verificables
- [ ] Sin dependencias bloqueantes no resueltas
- [ ] Estimable por el equipo de desarrollo

**Criterios de Aceptacion**
- El sistema muestra el submenu IPC dentro de la seccion Informativas.
- La pantalla IPC expone los filtros Periodo y Estado con las opciones Vigente y Baja.
- La consulta devuelve unicamente los registros que cumplen con los filtros ingresados.
- La grilla muestra como minimo las columnas Periodo, IPC, Estado, Fecha alta, Fecha baja y Usuario.

**Items pendientes para completar el DoR**
Ninguno.

**Escenarios Gherkin**

**Escenario 1: Consulta filtrada de registros vigentes**
```gherkin
Given el usuario accede al submenu IPC dentro de Informativas
And existen registros de IPC para periodos habilitados
When el usuario consulta por un periodo y estado Vigente
Then el sistema muestra solo los registros que cumplen ambos filtros
And la grilla exhibe Periodo, IPC, Estado, Fecha alta, Fecha baja y Usuario
```

**Escenario 2: Consulta sin resultados para el filtro aplicado**
```gherkin
Given el usuario accede a la pantalla IPC
And no existen registros que cumplan el periodo y estado seleccionados
When el usuario ejecuta la consulta
Then el sistema no muestra registros en la grilla para ese filtro
And mantiene visibles los filtros de busqueda disponibles
```

### US001002 — Registrar un IPC manual

**Precondicion**
El usuario se encuentra en la pantalla IPC y el periodo a informar no posee un registro vigente manual ni automatico.

**Narrativa**
Como Usuario de Informativas quiero registrar manualmente un valor de IPC para un periodo sin vigencia existente para poder trabajar provisoriamente con ese dato.

**Postcondicion**
Existe un nuevo registro manual de IPC en estado Vigente y con el legajo del usuario informado como usuario de alta.

**DoR — Definition of Ready**
- [ ] Narrativa completa y sin ambiguedades
- [ ] Precondicion y postcondicion definidas
- [ ] Criterios de aceptacion presentes y verificables
- [ ] Sin dependencias bloqueantes no resueltas
- [ ] Estimable por el equipo de desarrollo

**Criterios de Aceptacion**
- El sistema permite registrar un IPC manual solo si el periodo no posee un registro vigente.
- Si el periodo ya posee un registro IPC vigente, el sistema rechaza el alta.
- Ante rechazo por vigencia existente, el sistema muestra el mensaje "El periodo ya posee un registro IPC vigente".
- En un alta manual exitosa, el campo Usuario del registro creado se informa con el legajo del usuario que realizo la operacion.

**Items pendientes para completar el DoR**
Ninguno.

**Escenarios Gherkin**

**Escenario 1: Alta manual exitosa para periodo sin vigencia**
```gherkin
Given el usuario se encuentra en la pantalla IPC
And el periodo seleccionado no posee un registro IPC vigente
When el usuario registra un nuevo IPC manual
Then el sistema crea un registro en estado Vigente para ese periodo
And informa como usuario de alta el legajo del usuario que realizo la operacion
```

**Escenario 2: Rechazo de alta por vigencia existente**
```gherkin
Given el usuario se encuentra en la pantalla IPC
And el periodo seleccionado ya posee un registro IPC vigente
When el usuario intenta registrar un nuevo IPC manual
Then el sistema rechaza la operacion
And muestra el mensaje "El periodo ya posee un registro IPC vigente"
```

### US001003 — Modificar un IPC manual vigente

**Precondicion**
Existe un registro de IPC en estado Vigente cargado manualmente y el usuario se encuentra habilitado para operarlo.

**Narrativa**
Como Usuario de Informativas quiero modificar un IPC manual vigente para corregir su valor sin perder la trazabilidad del registro anterior.

**Postcondicion**
El registro manual previo queda en estado Baja y se genera un nuevo registro actualizado en estado Vigente.

**DoR — Definition of Ready**
- [ ] Narrativa completa y sin ambiguedades
- [ ] Precondicion y postcondicion definidas
- [ ] Criterios de aceptacion presentes y verificables
- [ ] Sin dependencias bloqueantes no resueltas
- [ ] Estimable por el equipo de desarrollo

**Criterios de Aceptacion**
- El sistema permite modificar unicamente registros manuales en estado Vigente.
- El sistema no permite modificar registros en estado Baja ni registros provenientes de TU190.
- Si se intenta modificar un registro no permitido, el sistema muestra el mensaje "error: solo se pueden modificar registros manuales vigentes".
- Al confirmar una modificacion valida, el sistema da de baja el registro anterior y crea un nuevo registro con los datos actualizados en estado Vigente.

**Items pendientes para completar el DoR**
Ninguno.

**Escenarios Gherkin**

**Escenario 1: Modificacion exitosa de un registro manual vigente**
```gherkin
Given existe un registro de IPC manual en estado Vigente
When el usuario modifica ese registro
Then el sistema da de baja el registro anterior
And genera un nuevo registro actualizado en estado Vigente
```

**Escenario 2: Rechazo de modificacion de registro no editable**
```gherkin
Given el usuario selecciona un registro en estado Baja o proveniente de TU190
When el usuario intenta modificar ese registro
Then el sistema rechaza la operacion
And muestra el mensaje "error: solo se pueden modificar registros manuales vigentes"
```