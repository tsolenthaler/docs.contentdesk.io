---
tags:
  - projects
hide:
  - navigation
---

# Glarnerland App

## Konzepte

* Empfehlung - [Reviews and recommendations]
* Tagespass - [Gästekarte]
* [Produkte und Angebote]

[Reviews and recommendations]: ../concepts/reviews-and-recommendations.md
[Gästekarte]: ../concepts/gaestekarte.md
[Produkte und Angebote]: ../concepts/produkte-und-angebote.md

## Übersicht

### Systeme 
``` mermaid
graph LR
    SystemAVS[AVS]
    SystemCD[contentdesk.io]
    SystemDiscover[discover.swiss]
    SystemApp[App Binarium]

    SystemAVS -->|Manuel| SystemCD
    SystemCD -->|API| SystemDiscover
    SystemDiscover -->|API| SystemApp
```
### Typen

``` mermaid
graph LR
    subgraph avs
        direction TB
        CardTyp --> | hat 0..n| Akzeptanzstelle
    end
    subgraph contentdesk
        direction TB
        Produkt --> Angebot
        Empfehlung
    end
    subgraph discover
        direction TB
        Product
        Recommendations
    end
    subgraph app
        direction TB
        Tagespass
        Content
    end

    avs --> contentdesk
    contentdesk --> discover
    discover --> app
```

### Properties
``` mermaid
classDiagram
    namespace Avs {
        class CardTyp {
            uuid Id
            string Name
        }
        class Akzeptanzstelle {
            uuid Id
            string Name
            date Gültigkeit
        }

        CardTyp --> "0..n" Akzeptanzstelle : hat
    }
    namespace contentdesk {
        class Produkt {
            uuid Id
            string Name
            uuid avs_id
        }
        class Angebot {
            uuid Id
            string Name
            uuid avs_id

        }
        class Empfehlung {
            uuid Id
            string Name
        }

        Produkt --> "0..n" Angebot : offer
        Empfehlung --> Angebot
        Empfehlung --> POI
        Empfehlung --> Produkt
    }
    namespace discover {
        class Product{
            uuid Id
            string Name
            uuid sourceID
            uuid avs_id
        }
        class Recommendations{
            uuid Id
            string Name
        }
    }
    namespace app {
        class Tagespass {

        }
        class Content {

        }
    }
```


## Schema

### Beispiel Empfehlung / Content / Storie

``` mermaid
graph TD
    Recommendation[Ausflugstipps - Empfehlung]
    Recommendation -->|empfiehlt|PlaceA[POI A]
    Recommendation -->|empfiehlt|PlaceB[POI B]
    Recommendation -->|empfiehlt|PlaceC[POI C]

    Recommendation -->|empfiehlt|Product[Produkt]
    Recommendation -->|empfiehlt|Event[Veranstaltung]
    Recommendation -->|empfiehlt|Tour

    Recommendation -->|ist verbunden mit|Tagespass

    Tagespass[Tagespass - Produkt]
```

### Beispiel Tagespass
``` mermaid
graph TD
    Recommendation[Ausflugstipps - Empfehlung]
    Recommendation -->|ist verbunden mit|Tagespass

    Tagespass[Tagespass - Produkt]
    Tagespass -->|hat Leistungen/Angebot|OfferA
    Tagespass -->|hat Leistungen/Angebot|OfferB
    Tagespass -->|hat Leistungen/Angebot|OfferC
    
    OfferA[Leistung / Angebot A]
    OfferB[Leistung / Angebot B]
    OfferC[Leistung / Angebot C]

    OfferA -->|ist erhältlich bei|PlaceA[POI A]
    OfferB -->|ist erhältlich bei|PlaceB[POI B]
    OfferC -->|ist erhältlich bei|PlaceA

    OfferA -->|angeboten von|OrganisationA[Organisation X]
    OfferB -->|angeboten von|OrganisationA[Organisation Y]
    OfferC -->|angeboten von|OrganisationA[Organisation Z]

    OfferA -->|Angebot von Produkt| Tagespass
    OfferB -->|Angebot von Produkt| Tagespass
    OfferC -->|Angebot von Produkt| Tagespass
```

### Schema.org

#### Empfehlung
``` mermaid
graph TD
    Recommendation -->|itemReviewed|Place
    Recommendation -->|itemReviewed|Product
    Recommendation -->|itemReviewed|Event
    Recommendation -->|itemReviewed|Trail

    Recommendation -->|isRelatedTo|Product
```

[Docs discover.swiss ](https://docs.discover.swiss/dev/concepts/reviews-and-recommendations/)

#### Tagespass
``` mermaid
graph TD
    Product-->|offers|Offer

    Offer-->|itemOffered|Product
    Offer-->|availableAtOrFrom|Place
    Offer-->|offeredBy|Organization
    
    Organization-->|areaServed|Place
    Organization-->|makesOffer|Offer
```

### ER Model

``` mermaid
erDiagram
    Recommendation{
        array channel
    }
    Recommendation ||--o{ Place : itemReviewed
    Recommendation ||--o{ Product : itemReviewed
    Recommendation ||--o{ Event : itemReviewed
    Recommendation ||--o{ Place : itemReviewed
    Recommendation ||--o{ Trail : itemReviewed
    Recommendation ||--o| Product : isRelatedTo

    Product{
        string name
        string description
        array channel
        uuid avs_id
    }

    Product ||--o{ Offer : offers

    Offer{
        string name
        number price
        date validFrom
        date validThrough
        array channel
        uuid avs_id
    }

    Offer ||--|{ Product : itemOffered
    Offer ||--o{ Place : availableAtOrFrom

    Place{
        array channel
    }

    Event{
        array channel
    }

    Trail{
        array channel
    }

    Organization||--o{ Offer : makesOffer
    Organization||--o{ Place : areaServed
```

### Properties

* [availableAtOrFrom] 0..n - erhältlich bei oder von
* [itemReviewed] 0..n - empfohlene Objekte (Produkt, Event, Place, etc.)
* [isRelatedTo] 0...1 - ist verbunden mit 
* [channel]
* [avs_acceptance_point_id]
* [validFrom]
* [validThrough]
* [offeredBy] ?
* [makesOffer] ?
* [areaServed] ?
* [itemOffered] ?

[availableAtOrFrom]: ../../schema/availableAtOrFrom.md
[itemReviewed]: ../../schema/itemReviewed.md
[isRelatedTo]: ../../schema/isRelatedTo.md
[channel]: ../../schema/channel.md
[avs_id]: ../../schema/avs_id.md
[validFrom]: ../../schema/validFrom.md
[validThrough]: ../../schema/validThrough.md

### Types

* [Place]
* [Product]
* [Offer]
* [Recommendation]
* [Organization] ?

[Place]: ../../schema/Place.md
[Product]: ../../schema/Product.md
[Offer]: ../../schema/Offer.md
[Recommendation]: ../../schema/Recommendation.md
