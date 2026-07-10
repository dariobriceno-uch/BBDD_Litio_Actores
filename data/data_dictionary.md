# Diccionario de datos — BBDD Actores de la Gobernanza del Litio en Chile

Este documento describe las 14 pestañas del archivo
`data/raw/BBDD_Actores_reordenada_v2.xlsx`, sus campos, y el tipo de dato que
cada pestaña aporta a un análisis de redes sociales (SNA). Los conteos fueron
verificados programáticamente con `scripts/build_processed.py`; corresponden a
entradas con contenido, excluyendo filas decorativas (banners de sección `►`,
títulos y subtítulos).

**Convención de origen (formato del Excel crudo):** dentro de cada pestaña, las
filas `► NOMBRE DE SECCIÓN` agrupan entradas por subcategoría, y las entradas
individuales llevan el prefijo `└─`. En los CSV procesados ese agrupamiento se
convierte en una columna `seccion` y el prefijo se elimina del nombre.

## Clasificación de las pestañas según su aporte a una red

| Aporte | Pestañas |
|---|---|
| **Atributos de nodo** (quién es cada actor: sector, tipo, país, período) | Las 9 pestañas temáticas |
| **Afiliación actor–organización** (red bipartita de membresías) | Cruces Multiafiliacion; Multiafiliación - (matriz) |
| **Participación actor–evento** (red bipartita de co-presencia en eventos) | Foros- Base Completa (+ Índice de Eventos como atributos de evento) |
| **Centralidad descriptiva** (derivada, sin cálculo formal de red) | Foros - Nodos Centrales |

---

## 1. Pestañas temáticas (atributos de nodo) — 1.402 entradas

Unidad de registro: el actor (persona u organización) con participación
documentada en el ecosistema del litio chileno. Los campos varían levemente
entre pestañas; el núcleo común es: nombre, tipo/rol, período de actividad, rol
en el litio y notas.

| Pestaña | Entradas | Campos |
|---|---:|---|
| Academia e Investigacion | 374 | Nombre, Tipo, Institución, Director, Investigadores, Especialidad/Descripción, Código, Período, Web, Cruces/Multiafiliación, Notas manuales |
| Empresas Mineras | 255 | Nombre, Tipo/Rol, País/Región, Descripción, Período, Info Adicional, Cruces/Multiafiliación, Notas manuales |
| Instituciones Estatales | 216 | Nombre, Cargo, Institución, Gobierno, Rol en Litio, Período, Cruces/Multiafiliación, Notas Manuales |
| ONGs y ambiente | 199 | Nombre, Tipo, País, Cargo/Descripción, Rol en Litio, Período, Cruces/Multiafiliación, Notas Manuales, Escala de Acción, Correcciones |
| Comunidades Territoriales | 183 | Nombre, Tipo, Pueblo, Ubicación, Dirigente, Cargo, Rol en Litio, Período, Cruces/Multiafiliación, Notas manuales |
| Organismos Internacionales | 75 | Nombre, Tipo, País/Región, Rol en Litio Chile, Período, Notas manuales |
| Servicios Prof. y Consultoras | 47 | Nombre, Tipo, País/Región, Rol/Relación con Litio, Período, Notas Manuales |
| Actores Financieros | 34 | Nombre, Tipo, País/Región, Rol/Relación con Litio, Período, Notas Manuales |
| Sindicatos y Gremios | 19 | Nombre, Tipo, País/Región, Cargo/Rol, Rol/Relación con Litio, Período, Cruces/Multiafiliación, Notas Manuales |

Notas por pestaña:

- **Instituciones Estatales** incluye el campo `Gobierno` (administración a la
  que pertenece el funcionario: Piñera, Boric, Kast…), que funciona como
  atributo temporal-político del nodo.
- **Comunidades Territoriales** registra `Pueblo` (adscripción indígena),
  `Ubicación`, y el par `Dirigente`/`Cargo`, que vincula personas con sus
  organizaciones comunitarias (utilizable como lazo de afiliación).
- **Empresas Mineras** distingue en sus secciones la cadena de valor y las
  empresas de tecnología de extracción directa (DLE).
- **Academia e Investigacion** incluye proyectos con `Código` (p. ej. proyectos
  Anillo) y campos de equipos (`Director`, `Investigadores`) que también
  encierran lazos persona–proyecto.
- El campo `Cruces/Multiafiliación`, presente en varias pestañas, es una
  anotación en texto libre que remite al módulo de multiafiliación.

## 2. Módulo de foros y eventos (participación actor–evento)

### Foros- Base Completa — 1.404 registros

La capa relacional principal: cada fila es una participación de un actor en un
evento. 1.120 actores únicos (646 personas y 474 organizaciones; los registros
se reparten en 872 de personas y 532 de organizaciones) en 137 eventos.

| Campo | Contenido |
|---|---|
| Nombre | Actor participante |
| Tipo de Actor | Persona / Organización |
| Organización | Afiliación institucional declarada en el evento |
| Cargo | Cargo declarado en el evento |
| Tipo Participación | Panelista, Expositor, Keynote, Organizador, Delegación oficial, etc. |
| Evento | Nombre del evento (enlaza con el Índice de Eventos) |
| Fecha | Fecha del evento (ver nota de formato abajo) |
| País | País sede |
| Tema/Panel | Tema o panel específico |
| Fuente URL | Fuente documental de la participación |

Esta pestaña define directamente una matriz de incidencia bipartita
actor × evento; el campo `Organización` permite además derivar lazos
actor–organización vigentes a la fecha del evento.

### Foros - Índice de Eventos — 104 eventos

Catálogo de eventos con: Evento, Organizador, Fecha, País/Ciudad,
N° Participantes, Tipo (Multilateral, Académico, Industria, Parlamentario,
Gubernamental, Gremial y combinaciones), Alcance y Fuente. Alcance verificado:
43 nacionales, 33 globales, 18 regionales, 6 locales, 2 internacionales y 2
con categorías específicas. Opera como tabla de atributos del modo "evento".
El índice cataloga un subconjunto curado de los 137 eventos que aparecen en la
base de participaciones.

### Foros - Nodos Centrales — 132 actores

Actores con participación recurrente: Nombre, Organización Principal, Cargo,
N° Eventos, Ámbitos, Organizaciones detectadas, Cargos detectados y Lista de
eventos. Es un primer indicio descriptivo de centralidad (grado en la red
bipartita actor–evento) sin cálculo formal de red. Máximos verificados: Aurora
Williams (16 eventos) y Máximo Pacheco (12); el resto participa en 7 o menos.

## 3. Módulo de multiafiliación (afiliación actor–organización)

### Cruces Multiafiliacion — 61 casos

Casos documentados de actores con afiliaciones simultáneas, organizados en 8
secciones tipificadas. Campos: Nombre, Afiliaciones/Roles Simultáneos, Tipo de
Cruce, Detalle del Cruce, Hojas Relacionadas. Distribución verificada:

| Tipo de cruce | Casos |
|---|---:|
| Estado–Empresa | 16 |
| Academia–Estado–ONG ("triple frontera") | 14 |
| Público → Privado (puerta giratoria) | 7 |
| Comunidad–ONG–Academia | 6 |
| Internacionales y articuladores transfronterizos | 6 |
| Consultores y actores financieros con roles múltiples | 5 |
| Estado–Academia–Empresa | 4 |
| Nodo legal (Carey y Cía.) | 3 |

### Multiafiliación - (matriz) — 65 actores, 305 afiliaciones

Matriz ancha que despliega el portafolio de cada actor multiafiliado en 10
grupos sectoriales de columnas: Operadores litio, Minería ampliada,
Empresarial no minero, Regulación y política, Centros pensamiento, Sociedad
civil ambiental, Comunidades del salar, Mediación, Proceso constituyente y Sin
clasificar. Cada actor ocupa un bloque de tres filas: organizaciones, cargos
(entre paréntesis) y períodos.

En la versión procesada esta pestaña se exporta como
`multiafiliacion_matriz_larga.csv` en formato largo — una fila por afiliación:
`actor, sector, organizacion, cargo, periodo` — es decir, una lista de aristas
(edge list) bipartita actor–organización lista para SNA. Distribución por
sector: Regulación y política (81), Centros de pensamiento (48), Minería
ampliada (47), Empresarial no minero (37), Operadores litio (36), Sociedad
civil ambiental (24), Mediación (18), Comunidades del salar (10), Proceso
constituyente (2), Sin clasificar (2).

---

## Inconsistencias detectadas y tratamiento

1. **Fechas guardadas como año 1905** (`Foros - Índice de Eventos`, 2 celdas).
   "4° Lithium Latin America Congress" y "LatAm & Argentina Critical Minerals
   Summit 2025" tenían fechas 1905-07-15 y 1905-07-17: alguien escribió solo el
   año (2023 y 2025) en celdas con formato de fecha y Excel lo interpretó como
   número serial (día 2.023 y 2.025 desde el 1-1-1900). **Corregido en la
   versión procesada** a los años "2023" y "2025" como texto; el día y mes
   originales no existen en el dato. El crudo se conserva sin modificar.
2. **Formato heterogéneo de fechas** (`Foros- Base Completa`). De 1.404
   registros, 626 tienen fecha de tipo fecha y 778 tienen texto libre
   ("14-16 May 2024", "2023-2027", "2024-actual"). No se corrigió: el texto
   conserva información de rangos que una fecha única perdería. Quien requiera
   fechas uniformes debe parsear este campo según su criterio de corte.
3. **Registros históricos de 1993** (`Foros- Base Completa`, 4 registros).
   Corresponden al evento "Contrato Corfo-SQM 1993 y privatización 1995". Son
   **válidos** (hito histórico documentado deliberadamente), no un error de
   digitación; se conservan tal cual.
4. **Períodos con años futuros** en pestañas temáticas (p. ej. "2018-2060" en
   contratos de largo plazo, "2025-2035" en proyecciones). Son vigencias
   contractuales o proyecciones declaradas en la fuente, no errores.
5. **Discrepancia entre base y índice de foros**: la base de participaciones
   contiene 137 eventos únicos; el índice cataloga 104. Los 33 restantes son
   eventos con participaciones registradas pero aún sin ficha en el índice
   (base viva, en actualización).

## Reproducibilidad

`data/processed/` se genera íntegramente desde `data/raw/` ejecutando:

```bash
python scripts/build_processed.py
```

No editar los archivos de `data/processed/` a mano: cualquier corrección debe
hacerse en el script (queda así documentada y auditable) o en el crudo con
nota en este diccionario.
