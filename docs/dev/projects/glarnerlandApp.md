---
hide:
  - navigation
  #- toc
---

# Glarnerland App


## Schema

``` mermaid
graph TD
    Tagespass[Produkt - Tagespass]
    Tagespass -->|hat Leistungen/Angeobte|OfferA
    Tagespass -->|hat Leistungen/Angeobte|OfferB
    Tagespass -->|hat Leistungen/Angeobte|OfferC
    OfferA[Leistung / Angebot A]
    OfferA -->|ist erhältlich bei|PlaceA[POI A]
    OfferB[Leistung / Angebot B]
    OfferB -->|ist erhältlich bei|PlaceB[POI B]
    OfferC[Leistung / Angebot C]
    OfferC -->|ist erhältlich bei|PlaceA

    Recommendation[Empfehlung - Ausflugstipps] -->|empfohlen|PlaceA
    Recommendation[Empfehlung - Ausflugstipps] -->|empfohlen|Product[Produkt]
    Recommendation[Empfehlung - Ausflugstipps] -->|empfohlen|Event[Veranstaltung]
    Recommendation[Empfehlung - Ausflugstipps] -->|empfohlen|Tour
    Recommendation -->|ist verbunden mit|Tagespass
    
```

### Schema.org / Discover.swiss
``` mermaid
graph TD
    Recommendation -->|itemReviewed|Place
    Recommendation -->|itemReviewed|Product
    Recommendation -->|itemReviewed|Event
    Recommendation -->|itemReviewed|Tour
    Recommendation -->|isRelatedTo|Product
    Product-->|offers|Offer
    Offer-->|availableAtOrFrom|Place
```

[Discover.swiss Docs](https://docs.discover.swiss/dev/concepts/reviews-and-recommendations/)

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
    RECOMMENDATION ||--o| TRAIL : isRelatedTo

    PRODUCT{
        array channel
        uuid avs_acceptance_point_id
    }

    PRODUCT ||--o{ OFFER : offers

    OFFER{
        uuid avs_acceptance_point_id
    }

    OFFER ||--o{ PLACE : availableAtOrFrom

    PLACE{
        array channel
    }

    EVENT{
        array channel
    }
```


### Types

* [Place]
* [Product]
* [Offer]
* [Recommendation]

[Place]: ../../schema/Place.md
[Product]: ../../schema/Product.md
[Offer]: ../../schema/Offer.md
[Recommendation]: ../../schema/Recommendation.md

### Properties

* [availableAtOrFrom] 0..n - erhältlich bei oder von
* [itemReviewed] 0..n - empfohlene Objekte (Produkt, Event, Place, etc.)
* [isRelatedTo] 0...1 - ist verbunden mit 
* [channel]
* [avs_acceptance_point_id]

[availableAtOrFrom]: ../../schema/availableAtOrFrom.md
[itemReviewed]: ../../schema/itemReviewed.md
[isRelatedTo]: ../../schema/isRelatedTo.md
[channel]: ../../schema/channel.md
[avs_acceptance_point_id]: ../../schema/avs_acceptance_point_id.md