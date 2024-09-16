---
hide:
  - navigation
  #- toc
---

# app.contentdesk.io

## Übersicht

### IST
``` mermaid
flowchart LR
    app.contentdesk.io-->Objekt
    app.contentdesk.io-->Report
    Objekt-->Check
    Report-->|prüft mehrere|Objekt
    Report-->|wöchentlich / monatlich|Check
    Check-->Associations[Verknüpfungen]
    Associations[Verknüpfungen]-->Graph
    Check-->Connect[Verbindungen]
    Check-->Compare[Vergleichen]
    Compare-->Place[Orts-Daten]
    Place-->OpenStreetMap
    Place-->GooglePlace
```

### Vision
``` mermaid
flowchart LR
    app.contentdesk.io-->Objekt
    Objekt-->Check
    Check-->AssociationType[Verknüpfungen]
    AssociationType[Verknüpfungen]-->Graph
    Objekt-->Connect[Verbindungen]
    Objekt-->Compare[Vergleichen]
```

### Ziel des Apps

* Assistent der einzelne Objekte prüft und verbesserungen vorschlägt, die evlt. angepasst und per Klick übernommen werden können.
* Expert Editor nach Schema.org JSON-LD
* Speicherquelle ändern. Bspw. DB --> ObjectStorage
* Import/Export erweitern bspw. JSON-D
* Embedded Objekt via Widget

## Checks

### Objekt (Product)

#### Kategorie

Hat das Objekt eine Kategorie?

### Verknüpfung / AssociationType

- [ ] Hat es überhaupt gepflegte Verknüpfungen?
- [ ] Zeigen der internen verknüpfer Objekte
  * [ ] als Liste
  * [ ] als Graph / examples mermaid graph
    * [ ] mit Verlinkung im Graph

#### Graph

Zeigt einen Graph mit den internen verknüpfungen von diesem Objekt zu den weiteren Objekten.
https://mermaid.js.org/syntax/examples.html#basic-flowchart

### Attribut

#### Verbindungen

Sind weitere ID's hinterlegt?

Bspw. openstreetmap, googel Place ID, discover.swiss, etc.


## Verbindungen (Connect)

Links zu den Verbundenen Systemen / Plattformen

Bspw. openstreetamp Edit Link, Google Place Link, discover.swiss, Outdooractive, etc.

## Vergleich (Compare)

Vergleichen der Attribute mit den verbunden Systemen / Plattformen.

Bspw. sind die Daten gleich wie beim OpenStreetMap. Wenn nicht können diese übertragen oder übernommen werden.

### Place / Orts-Daten

* Abgleich der Koordinanten mit OpenStreetMap
* * via ID --> Vergleich
* * via Koordinanten --> Vergleich