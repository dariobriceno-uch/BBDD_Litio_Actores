---
layout: default
title: BBDD Actores de la Gobernanza del Litio en Chile
---

# Base de Datos de Actores de la Gobernanza del Litio en Chile

Registro sistemático de los actores —personas y organizaciones— que
participan en la gobernanza del litio en Chile, con sus afiliaciones
institucionales y su participación en foros y eventos del campo. La base está
diseñada como infraestructura de datos para análisis de redes sociales (SNA):
sus módulos se convierten directamente en matrices de incidencia bipartitas
actor × organización y actor × evento.

## Documentos

- **[Informe de presentación](informe.md)** — justificación, construcción
  documental y contenido de la base (5 secciones).

## Datos y código

El repositorio completo — datos crudos y procesados, diccionario de datos,
bibliografía y script de reproducibilidad — está en
[GitHub]({{ site.github.repository_url }}):

- [Datos procesados (CSV tidy y Excel)]({{ site.github.repository_url }}/tree/main/data/processed)
- [Diccionario de datos]({{ site.github.repository_url }}/blob/main/data/data_dictionary.md)
- [Referencias (BibTeX)]({{ site.github.repository_url }}/blob/main/references/referencias.bib)
- [Script de procesamiento]({{ site.github.repository_url }}/blob/main/scripts/build_processed.py)

## La base en cifras

| Componente | Magnitud |
|---|---|
| Pestañas temáticas por tipo de actor | 9 pestañas, 1.402 entradas |
| Base de participaciones en foros | 1.404 registros, 1.120 actores únicos, 137 eventos |
| Índice de eventos caracterizados | 104 eventos |
| Actores con participación recurrente | 132 |
| Casos de multiafiliación tipificados | 61 |
| Matriz actor–organización (formato largo) | 65 actores, 305 afiliaciones |

## Licencia y cita

Datos, documentación e informe se distribuyen bajo
[CC BY 4.0]({{ site.github.repository_url }}/blob/main/LICENSE). Para citar la
base, ver las instrucciones del
[README]({{ site.github.repository_url }}#cómo-citar).
