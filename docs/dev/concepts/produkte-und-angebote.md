# Produkte, Varianten und Angebote




## Use-Case / Beispiele


### Führungen mit Varianten

### Tagespass mit Angeboten / Leistungen - Product offers

### Produkte / Dienstleistungen mit Varianten

## Contentdesk - Schema.org

| Contentdesk       | Schema.org     | Bemerkung                              |
| -----------       | -------------- | ------------------------------------   |
| Product-Model     | ProductGroup   | Produkt Variante                       |
| Product           | Product        |                                        |
|                   | ProductModel?  | Ähnlich wie Product mit weiteren spezifischen Properties wie isVariantOf, predecessorOf,successorOf |
| Group             |                |                                        |

``` mermaid
graph LR
    subgraph Contentdesk
        direction TB
        ContentdeskProduct -->|offers association-type|Offer
        ContentdeskProduct -->|
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

