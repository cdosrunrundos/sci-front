# EP001 — Ajustes de interfaz y exportacion de IPC

Esta epica agrupa los cambios solicitados sobre la interfaz de gestion del IPC manual para mejorar el filtrado visual, la identificacion de registros manuales y la consistencia de la exportacion.

## Definition of Ready (DoR)

- [ ] La User Story esta redactada con narrativa, precondicion y postcondicion para la interfaz de gestion del IPC manual.
- [ ] La User Story tiene trazabilidad al documento fuente papeles-de-trabajo-2.
- [ ] Los criterios de aceptacion son verificables desde el comportamiento visible de la pantalla o de la exportacion.
- [ ] No existen dudas funcionales pendientes sobre el ajuste puntual solicitado.
- [ ] La historia puede estimarse sin requerir definiciones adicionales de alcance.

### US001001 — Filtrar registros de IPC por usuario

**Precondicion**
El usuario se encuentra en la interfaz de gestion del IPC manual y existen registros visibles en la grilla.

**Narrativa**
Como usuario de la gestion del IPC manual quiero filtrar la grilla por usuario para localizar con mayor precision los registros cargados o generados por un usuario determinado.

**Postcondicion**
La grilla muestra solo los registros que cumplen con el filtro de usuario aplicado.

**DoR — Definition of Ready**
- [ ] Narrativa completa y sin ambiguedades
- [ ] Precondicion y postcondicion definidas
- [ ] Criterios de aceptacion presentes y verificables
- [ ] Sin dependencias bloqueantes no resueltas
- [ ] Estimable por el equipo de desarrollo

**Criterios de Aceptacion**
- La interfaz de gestion del IPC manual incorpora un filtro por usuario.
- Al aplicar el filtro por usuario, la grilla muestra solo los registros asociados al valor filtrado.
- Si no se aplica filtro de usuario, la grilla mantiene el comportamiento de consulta general.

**Items pendientes para completar el DoR**
Ninguno.

**Escenarios Gherkin**

**Escenario 1: Filtrado exitoso por usuario**
```gherkin
Given el usuario se encuentra en la interfaz de gestion del IPC manual
And existen registros asociados a distintos usuarios en la grilla
When el usuario aplica un filtro por usuario
Then la grilla muestra solo los registros asociados al usuario filtrado
```

**Escenario 2: Consulta sin filtro de usuario**
```gherkin
Given el usuario se encuentra en la interfaz de gestion del IPC manual
And no aplica un filtro de usuario
When el usuario consulta la grilla
Then el sistema mantiene la visualizacion general de registros segun los filtros vigentes
```

### US001002 — Resaltar en negrita los registros manuales

**Precondicion**
El usuario visualiza la grilla de gestion del IPC manual y existen registros de origen manual visibles.

**Narrativa**
Como usuario de la gestion del IPC manual quiero que los registros manuales se resalten en negrita para distinguirlos rapidamente de otros registros de la grilla.

**Postcondicion**
Los registros manuales visibles en la grilla quedan diferenciados visualmente en negrita.

**DoR — Definition of Ready**
- [ ] Narrativa completa y sin ambiguedades
- [ ] Precondicion y postcondicion definidas
- [ ] Criterios de aceptacion presentes y verificables
- [ ] Sin dependencias bloqueantes no resueltas
- [ ] Estimable por el equipo de desarrollo

**Criterios de Aceptacion**
- Los registros manuales visibles en la grilla se muestran en negrita.
- Los registros que no son manuales no se muestran en negrita por esta regla.
- El resaltado en negrita se mantiene al consultar o refrescar la grilla.

**Items pendientes para completar el DoR**
Ninguno.

**Escenarios Gherkin**

**Escenario 1: Resaltado visual de registros manuales**
```gherkin
Given el usuario visualiza registros manuales y no manuales en la grilla de IPC
When la grilla se muestra en pantalla
Then los registros manuales aparecen resaltados en negrita
And los registros no manuales no se muestran en negrita por esta regla
```

**Escenario 2: Persistencia del resaltado al refrescar la consulta**
```gherkin
Given existen registros manuales visibles en la grilla
When el usuario vuelve a consultar o refresca la grilla
Then los registros manuales continúan mostrandose en negrita
```

### US001003 — Exportar solo la grilla filtrada

**Precondicion**
El usuario se encuentra en la interfaz de gestion del IPC manual y la grilla presenta un conjunto de registros resultante de filtros aplicados.

**Narrativa**
Como usuario de la gestion del IPC manual quiero que la exportacion a Excel incluya solo los registros actualmente filtrados en la grilla para obtener un archivo consistente con la consulta realizada.

**Postcondicion**
El archivo Excel generado contiene exclusivamente los registros visibles en la grilla al momento de exportar.

**DoR — Definition of Ready**
- [ ] Narrativa completa y sin ambiguedades
- [ ] Precondicion y postcondicion definidas
- [ ] Criterios de aceptacion presentes y verificables
- [ ] Sin dependencias bloqueantes no resueltas
- [ ] Estimable por el equipo de desarrollo

**Criterios de Aceptacion**
- La exportacion a Excel toma como base solo los registros visibles en la grilla al momento de exportar.
- Los registros excluidos por filtros no se incorporan al archivo exportado.
- Si la grilla no tiene filtros adicionales, la exportacion refleja la totalidad de registros visibles en pantalla.

**Items pendientes para completar el DoR**
Ninguno.

**Escenarios Gherkin**

**Escenario 1: Exportacion de la grilla filtrada**
```gherkin
Given el usuario aplico filtros sobre la grilla de gestion del IPC manual
And la grilla muestra un subconjunto de registros
When el usuario exporta a Excel
Then el archivo exportado contiene solo los registros visibles en la grilla
```

**Escenario 2: Exportacion sin filtros adicionales**
```gherkin
Given el usuario no aplico filtros adicionales sobre la grilla visible
When el usuario exporta a Excel
Then el archivo exportado refleja la totalidad de registros visibles en pantalla
And no agrega registros que no formen parte de la consulta actual
```