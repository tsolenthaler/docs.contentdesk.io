# app.contentdesk.io

## Übersicht

### IST
``` mermaid
flowchart LR
    app.contentdesk.io-->Objekt
    Objekt-->Check
    Check-->AssociationType[Verknüpfungen]
    AssociationType[Verknüpfungen]-->Graph
    Objekt-->Connect[Verbindungen]
    Objekt-->Compare[Vergleichen]
```

### Vision

## Checks

### Objekt (Product)

#### Kategorie

Hat das Objekt eine Kategorie?

### Verknüpfung

Ist es mit weiteren eigenen (internen) Objekten verknüpft.

#### Graph

Zeigt einen Graph mit den internen verknüpfungen von diesem Objekt zu den weiteren Objekten.

### Attribut

#### Verbindungen

Sind weitere ID's hinterlegt?

Bspw. openstreetmap, googel Place ID, discover.swiss, etc.


## Connect / Verbindungen

Links zu den Verbundenen Systemen / Plattformen

Bspw. openstreetamp Edit Link, Google Place Link, discover.swiss, Outdooractive, etc.

## Compare

Vergleichen der Attribute mit den verbunden Systemen / Plattformen.

Bspw. sind die Daten gleich wie beim OpenStreetMap. Wenn nicht können diese übertragen oder übernommen werden.