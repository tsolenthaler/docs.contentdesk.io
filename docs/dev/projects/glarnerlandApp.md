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

### Systems
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
### Types

#### Diagramm

``` mermaid
graph LR
    subgraph avs
        direction TB
        CardTyp --> | hat 0..n| Akzeptanzstelle
    end
    subgraph contentdesk
        direction TB
        Touristcard --> |offers| Angebot
        Touristcard --> |availableAtOrFrom| Ort["POI / Place"]
        Angebot --> |itemOffered| Angebot2["Produkt / Service"]
        Empfehlung --> |itemReviewed| item["Place, Event oder Produkt"]
    end
    subgraph discover
        direction TB
        Product
        Recommendations
    end
    subgraph app
        direction TB
        Tagespass --> Leistung
        Content["Empfehlung"]
    end

    avs --> contentdesk
    contentdesk --> discover
    discover --> app
```

#### Table

| AVS                           | contentdesk.io    | discover.swiss      | App / Binarium            |
| -----------                   | -------------     | -------------       | -------------             |   
| Card Typ                      | [Touristcard]       | Touristcard?      | Tagespass                 |
|                               | [Product]           | [Product2]        | Produkt                   |
| Akzeptanzstelle / Leistung?   | [Offer]             | Offer?            | Leistung                  |       
|                               | [Recommendation]    | Recommendation    | Empfehlung                |
|                               | [Place]             | Place             | Place                     |
|                               | [Organization]      | Organization      | Organization              |

[Touristcard]: ../../schema/Touristcard.md
[Place]: ../../schema/Place.md
[Product]: ../../schema/Product.md
[Offer]: ../../schema/Offer.md
[Recommendation]: ../../schema/Recommendation.md
[Organization]: ../../schema/Organization.md

[PRoduct2]: https://docs.discover.swiss/dev/reference/dataschema/definition/infocenter-classes/Product/

### Properties

#### Diagramm
``` mermaid
classDiagram
    direction TB
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
    }
    CardTyp --> "0..n" Akzeptanzstelle : hat

    namespace contentdesk {
        class Touristcard {
            uuid Id
            string Name
            uuid avs_id
            string disambiguatingDescription
            date validFrom
            date validThrough
        }
        class Produkt {
            uuid Id
            string Name
            array channel
            string disambiguatingDescription
        }
        class Angebot {
            uuid Id
            string Name
            uuid avs_id
            array channel
            string disambiguatingDescription
        }
        class Empfehlung {
            uuid Id
            string Name
            array channel
            string disambiguatingDescription
        }
        class Ort["POI / Place"] {
            uuid Id
            string Name
            array channel
            string disambiguatingDescription
            string HowToDirection
            string publicTransport
            string parking
            string leisure
        }
    }
    Touristcard --> "0..n" Angebot : offer
    Empfehlung --> Angebot : itemReviewed
    Empfehlung --> Ort : itemReviewed
    Empfehlung --> Produkt : itemReviewed

    Touristcard --> "0..n" Ort : availableAtOrFrom

    namespace discover {
        class TouristcardType{
            uuid Id
            string Name
            uuid sourceID
            uuid avs_id
        }
        class Product{
            uuid Id
            string Name
            uuid sourceID
        }
        class Recommendations {
            uuid Id
            string Name
        }

        class Place["Place / Product / Event"]

        class Product["Place / Produkt"]
    }

    Recommendations --> "0..1" Place : isRelatedTo 
    Recommendations --> "0..n" Product : itemReviewed
    namespace app {
        class Tagespass {

        }
        class Content {

        }
    }
```

#### List / Table

* [availableAtOrFrom] 0..n - erhältlich bei oder von
* [itemReviewed] 0..n - empfohlene Objekte (Produkt, Event, Place, etc.)
* [isRelatedTo] 0...1 - ist verbunden mit 
* [channel]
* [avs_id]
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

## Schema

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

## Offene Punkte

- [ ] discover.swiss 
    * [ ] Type [Touristcard]? --> Ansonsten Propertie zum identifizieren der Gästekarte
    * [ ] [Offer]? und [offers]?
- [ ] 


### Beispiele

#### Empfehlung

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

#### Tagespass
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