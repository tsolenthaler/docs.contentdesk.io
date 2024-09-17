# Produkte, Varianten und Angebote


## Übersicht Typen

- Einfaches Produkt [Product]

    * ohne weitere Angebote
    * mit weiteren Angeboten [offers]

- Produkt mit Variante [ProductGroup]

    * nach Farbe [color]
    * nach Material [material]
    * etc.

- Angebot [Offer]

    * Ein zusätzliches Angebot, das nur in Kombination mit dem ersten Basisangebot erhältlich ist (z.B. Zuschläge und Verlängerungen, die gegen einen Aufpreis erhältlich sind). [addOn]

- Service [Service]

    * 

## Use-Case / Beispiele

### Führungen mit Varianten

### Tagespass mit Angeboten / Leistungen

Die Angebote / Leistungen sind von anderen Leistungsträgern

### Produkte / Dienstleistungen mit Varianten

* Marketing zum Mitmachen

## Contentdesk und Schema.org Typen

| Contentdesk       | Schema.org         | Bemerkung                              |
| -----------       | --------------     | ------------------------------------   |
| Product-Model     | ProductGroup       | Produkt Variante                       |
| Product           | Product            |                                        |
|                   | ProductModel?      | Für Ähnlich wie Product mit weiteren spezifischen Properties wie isVariantOf, predecessorOf,successorOf |
| Group             | ProductCollection? |                                        |

``` mermaid
graph LR
    subgraph Contentdesk
        direction TB
        ContentdeskProduct -->|offers|Offer
        Offer-->|addOn|Offer
    end

    subgraph Contentdesk
        direction TB
        ContentdeskProduct -->|offers|Offer
        Offer-->|addOn|Offer
    end
```


## Schema.org "Varianten"

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