# Base de Datos de Actores de la Gobernanza del Litio en Chile

Registro sistemático de los actores —personas y organizaciones— que participan
en la gobernanza del litio en Chile: empresas operadoras y su cadena de valor,
instituciones estatales, comunidades territoriales e indígenas, academia, ONGs,
organismos internacionales, actores financieros, consultoras y gremios, junto
con sus afiliaciones institucionales y su participación en foros y eventos del
campo.

La base está diseñada como **infraestructura de datos para análisis de redes
sociales (SNA)**: sus módulos de multiafiliación y de foros se convierten
directamente en matrices de incidencia bipartitas (actor × organización y
actor × evento), y sus campos de período permiten cortes longitudinales por
hitos de gobernanza. El informe que la presenta y justifica está en
[`docs/informe.pdf`](docs/informe.pdf) (fuente Quarto en
[`docs/informe.qmd`](docs/informe.qmd)).

## Contenido en cifras

| Componente | Magnitud |
|---|---|
| Pestañas temáticas por tipo de actor | 9 pestañas, 1.402 entradas |
| Base de participaciones en foros | 1.404 registros, 1.120 actores únicos, 137 eventos |
| Índice de eventos caracterizados | 104 eventos |
| Actores con participación recurrente | 132 |
| Casos de multiafiliación tipificados | 61 |
| Matriz actor–organización (formato largo) | 65 actores, 305 afiliaciones |

Los conteos se verifican programáticamente con `scripts/build_processed.py`.

## Estructura del repositorio

```
├── README.md                  este archivo
├── LICENSE                    CC BY 4.0
├── data/
│   ├── raw/                   Excel original, sin modificaciones
│   ├── processed/             versión procesada (generada por script)
│   │   ├── BBDD_Actores_procesada.xlsx    con pestaña RESUMEN y fechas corregidas
│   │   └── csv/               un CSV tidy (UTF-8) por pestaña
│   └── data_dictionary.md     documentación de pestañas, campos e inconsistencias
├── docs/                      informe de presentación y su render
│   ├── informe.qmd            fuente del informe (Quarto)
│   ├── informe.html           informe renderizado (HTML autocontenido)
│   ├── informe.pdf            informe renderizado (PDF)
│   └── Estructura_informe_BBDD.pdf
├── references/
│   └── referencias.bib        obras citadas en el informe (BibTeX, con DOI)
└── scripts/
    └── build_processed.py     genera data/processed/ desde data/raw/
```

## Cómo se construyó la base

Recolección documental con triangulación de tres tipos de fuente:

1. **Prensa y medios especializados** — corpus de noticias del sector
   (recolección asistida por scrapers más revisión manual).
2. **Fuentes secundarias** — literatura académica e informes de organismos.
3. **Documentos primarios** — actas y registros de comisiones e instancias de
   gobernanza, memorias corporativas y registros de participación en foros y
   eventos.

Criterio de inclusión: actor (persona u organización) con participación
documentada en el ecosistema del litio chileno. Criterio de afiliación:
membresía institucional formal (cargo, directorio, comisión). Cada
participación en foros registra su fuente (URL). La justificación metodológica
completa está en la sección 3 del [informe](docs/informe.pdf).

## Reproducibilidad

La versión procesada se regenera desde el crudo con:

```bash
python scripts/build_processed.py
```

Requiere Python ≥ 3.10 y `openpyxl`. El script no altera `data/raw/`; toda
corrección aplicada al procesado está codificada en el script y documentada en
[`data/data_dictionary.md`](data/data_dictionary.md) (sección
"Inconsistencias detectadas y tratamiento").

## Informe

El informe de presentación se edita en `docs/informe.qmd` y se renderiza a
[PDF](docs/informe.pdf) con [Quarto](https://quarto.org):

```bash
quarto render docs/informe.qmd --to pdf
```

El mismo comando sin `--to pdf` genera además una versión HTML local (no
versionada).

## Limitaciones

- **Sesgo de visibilidad mediática**: los actores periféricos —especialmente
  del sector comunitario— tienden al subregistro respecto de los actores con
  presencia frecuente en prensa y eventos.
- **Base viva**: la ventana de observación final sigue abierta; los conteos
  corresponden a la versión archivada en `data/raw/`.
- 33 de los 137 eventos de la base de participaciones aún no tienen ficha en
  el índice de eventos.

## Licencia y uso de datos

Datos, documentación e informe se distribuyen bajo
[Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE):
cualquier persona puede copiar, redistribuir y transformar el material,
incluso con fines comerciales, siempre que dé crédito apropiado.

Notas de uso:

- La base compila **información pública** sobre cargos y participaciones
  institucionales de personas identificables. Quien la reutilice debe
  considerar las normas de protección de datos personales aplicables a su
  contexto (en Chile, Ley 19.628 y su reforma, Ley 21.719).
- La carpeta local `bibliografía/` (PDFs de editoriales) no forma parte del
  repositorio publicado; las obras citadas están referenciadas con DOI en
  `references/referencias.bib`.
