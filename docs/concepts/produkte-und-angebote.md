---
tags:
  - concept
hide:
  - navigation
---

# Produkte, Varianten und Angebote


## Übersicht von Möglichkeiten

- Einfaches Produkt [Product]

    * ohne weitere Angebote
    * mit weiteren Angeboten - via Verknüpfung [offers]

- Produkt mit Variante [ProductGroup]

    * nach Farbe [color]
    * nach Material [material]
    * etc.

- Angebot [Offer]

    * Ein zusätzliches Angebot, das nur in Kombination mit dem ersten Basisangebot erhältlich ist (z.B. Zuschläge und Verlängerungen, die gegen einen Aufpreis erhältlich sind). [addOn]

- *Service [Service]

    * 

## Use-Case / Beispiele

### Produkt Tagespass mit Angeboten / Leistungen

Die Angebote / Leistungen sind von anderen Leistungsträgern

### Produkte / Dienstleistungen mit Varianten

* Marketing zum Mitmachen

## Contentdesk und Schema.org Typen

| Contentdesk       | Schema.org         | Bemerkung                              |
| -----------       | --------------     | ------------------------------------   |
| Product-Model / Variante    | ProductGroup       | Produkt Variante                       |
| Product           | Product            |                                        |
|                   | ProductModel?      | Für Ähnlich wie Product mit weiteren spezifischen Properties wie isVariantOf, predecessorOf,successorOf |
| Group             | ProductCollection? |                                        |


### Mapping
``` mermaid
flowchart LR
    subgraph Contentdesk.io
        direction TB
        ContentdeskProduct[Product] -->|offers| ContentdeskOffer[Offer]
        ContentdeskOffer -->|addOn| ContentdeskOffer
        ContentdeskOffer -->|itemOffered| ContentdeskProduct
        ContentdeskOffer -->|itemOffered| ContentdeskService[Service]
    end

    subgraph discover.swiss
        direction TB
        discoverProduct[Product] -->|offers| discoverOffer[Offer?]
        discoverOffer -->|addOn| discoverOffer
        discoverOffer -->|itemOffered| discoverProduct
        discoverOffer -->|itemOffered| discoverService[Service?]
    end

    Contentdesk.io --> discover.swiss
```


## Schema.org "Varianten"

### Schema
``` mermaid
flowchart TB
    Product -->|offers| Offer
    Offer-->|addOn| Offer
    Offer-->|itemOffered| Product
    Offer-->|itemOffered| Service
```

* Product / ProductModel
* Product with offers
* ProductGroup with Variant
* 
* Offer with addOn
* 

### isVariantOf / hasVariant
https://schema.org/isVariantOf

https://schema.org/hasVariant

### offers



## Offene Punkte 

* [Service]

