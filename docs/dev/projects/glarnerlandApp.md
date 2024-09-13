# Glarnerland App


## Schema

``` mermaid
graph TD
    Product[Produkt - Tagespass]-->|erhältlich bei oder von|Place[Place - POI/Ort]

    Recommendation[Empfehlung - Ausflugstipps] -->|empfohlene Orte|Place
    Recommendation -->|ist verbunden mit|Product
```

### Schema.org / Discover.swiss
``` mermaid
graph TD
    Product-->|availableAtOrFrom|Place
    Recommendation -->|itemReviewed|Place
    Recommendation -->|itemReviewed|Product
    Recommendation -->|itemReviewed|Event
    Recommendation -->|itemReviewed|Tour
    Recommendation -->|isRelatedTo|Product
```

https://docs.discover.swiss/dev/concepts/reviews-and-recommendations/

### ER Model

``` mermaid
erDiagram
    RECOMMENDATION ||--o{ PLACE : itemReviewed
    RECOMMENDATION{
        array channel
    }
    RECOMMENDATION ||--o{ PRODUCT : itemReviewed
    
    RECOMMENDATION ||--o| PRODUCT : isRelatedTo
    RECOMMENDATION ||--o| EVENT : isRelatedTo
    RECOMMENDATION ||--o| PLACE : isRelatedTo

    PRODUCT{
        array channel
    }

    PLACE{
        array channel
        uuid avs_acceptance_point_id
    }

    EVENT{
        array channel
    }
```


### Types

* Place
* Produkt / Offer
* Recommendation

### Properties

* [availableAtOrFrom] 0..n - erhältlich bei oder von
* [itemReviewed] 0..n - empfohlene Orte
* [isRelatedTo] 0...1 - ist verbunden mit 
* [channel]
* [avs_acceptance_point_id]

[availableAtOrFrom]: ../../schema/availableAtOrFrom.md
[itemReviewed]: ../../schema/itemReviewed.md
[isRelatedTo]: ../../schema/isRelatedTo.md
[channel]: ../../schema/channel.md
[avs_acceptance_point_id]: ../../schema/avs_acceptance_point_id.md