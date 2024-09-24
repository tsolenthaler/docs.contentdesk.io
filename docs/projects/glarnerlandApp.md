---
tags:
  - projects
hide:
  - navigation
  - toc
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
#### AVS -> contentdesk.io
Manueller übertrag der AVS ID

#### contentdesk.io -> discover.swiss
Ein mal täglich um ca. 04:00 Uhr

#### discover.swiss -> App Binarium
?

### Types

#### Diagramm Types

``` mermaid
graph LR
    subgraph avs
        direction TB
        CardTyp --> | hat 0..n| Akzeptanzstelle
    end
    subgraph contentdesk
        direction TB
        Gaestekarte["Gästekarte"] --> |offers| Angebot
        Gaestekarte --> |availableAtOrFrom| Ort["POI / Place"]
        Angebot --> |itemOffered| Angebot2["Produkt / Service"]
        Empfehlung --> |itemReviewed| item["Place, Event oder Produkt"]
        Angebot --> |offeredBy| Organization
        Organization -->|location| Ort
    end
    subgraph discover
        direction TB
        Touristcard["Touristcard?/Product? mit Angebot"] -->|itemOffered| Product
        Touristcard -->|availableAtOrFrom|Place
        Recommendations -->|itemReviewed|Place["Place (POI / Product)"]
        Recommendations -->|isRelatedTo|Place2["Place / Product / Event"]
    end
    subgraph app
        direction TB
        Tagespass --> Leistung
        EmpfehlungApp["Empfehlung"]
        EmpfehlungApp --> ItemApp["POI, Event, Produkt"]
    end

    avs --> contentdesk
    contentdesk --> discover
    discover --> app
```

#### Table Types

| AVS                           | contentdesk.io        | discover.swiss                | App / Binarium            |
| -----------                   | -------------         | -------------                 | -------------             |   
| Card Typ                      | [Touristcard]         | [Touristcard discover]❓       | Tagespass                 |
|                               | [Product]             | [Product discover]            | Produkt                   |
| Akzeptanzstelle / Leistung?   | [Offer]               | [Offer discover]              | Leistung                  |       
|                               | [Recommendation]      | [Recommendation discover]     | Empfehlung                |
|                               | [Place]               | [Place discover]              | Place                     |
|                               | [Organization]        | [Organization discover]       | -                         |

[Touristcard]: ../../schema/Touristcard
[Place]: ../../schema/Place
[Product]: ../../schema/Product
[Offer]: ../../schema/Offer
[Recommendation]: ../../schema/Recommendation
[Organization]: ../../schema/Organization

[Product discover]: https://docs.discover.swiss/dev/reference/dataschema/definition/infocenter-classes/Product/
[Recommendation discover]: https://docs.discover.swiss/dev/reference/dataschema/definition/infocenter-classes/Review/
[Place discover]: https://docs.discover.swiss/dev/reference/dataschema/definition/infocenter-classes/Place/
[Organization discover]: https://docs.discover.swiss/dev/reference/dataschema/definition/infocenter-classes/Organization/

### Properties

#### Diagramm Properties
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
    Touristcard --> "0..n" Angebot : offers
    Touristcard --> "0..n" Ort : availableAtOrFrom

    Empfehlung --> "0..n" Angebot : itemReviewed
    Empfehlung --> "0..n" Ort : itemReviewed
    Empfehlung --> "0..n" Produkt : itemReviewed

    Angebot --> "0..n" Produkt : itemOffered

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

#### Table Properties

| AVS         | contentdesk.io                          | discover.swiss                    | App / Binarium            | Comment |
| ----------- | -------------                           | -------------                     | -------------             |   |
|             | Type **[Touristcard]**?                 | Type **TouristcardTyp**❓         | -                         |   |
|             | -                                       | [ID discover]                     | -                         |
| -           | [identifier] (ID)                       | [sourceId discover]               | -                         |
| ID          | [avs_id]                                | [additionalProperty discover]     | -                         |   |
|             | [validFrom]                             | [validFrom discover]              | -                         |          
|             | [validThrough]                          | [validThrough discover]           | -                         |
|             | Type **[Place]**                        | Type **[Place discover]**         | -                         |
|             | [HowToDirection]                        | [gettingThere]                    | -                         |
|             | [publicTransport]                       | [publicTransport]                 | -                         |
|             | [parking]                               | [parking]                         | -                         |
|             | **All Types - Attributes**              | **All Types**                     | -                         |
|             | [name]                                  | name                              | -                         |
|             | [disambiguatingDescription] Scope App   | [mobileDescription]               | -                         |
|             | [description]                           | [description]                     | -                         |  
|             | [channel]                               | [additionalProperty]❓            | -                         |
|             | **Association type** - Verknüfpungen    |                                   | -                         |
|             | [offers]                                | [offers discover]❓               | -                         |
|             | [availableAtOrFrom]                     | [availableAtOrFrom discover]❓    | -                         |
|             | [itemOffered]                           | [itemOffered discover]❓          | -                         |
|             | [itemReviewed]                          | [itemReviewed discover]           | -                         |
|             | [isRelatedTo]                           | [isRelatedTo discover]            | -                         |
|             | [offeredBy]                             | [offeredBy discover]❓            | -                         |
|             | [location]                              | [location discover]❓            | -                         |

[offers]: ../../schema/offers
[availableAtOrFrom]: ../../schema/availableAtOrFrom
[itemOffered]: ../../schema/itemOffered
[itemReviewed]: ../../schema/itemReviewed
[isRelatedTo]: ../../schema/
[offeredBy]: ../../schema/offeredBy
[location]: ../../schema/location

[identifier]: ../../schema/identifier
[avs_id]: ../../schema/avs_id
[validFrom]: ../../schema/validFrom
[validThrough]: ../../schema/validThrough
[HowToDirection]: ../../schema/HowToDirection
[publicTransport]: ../../schema/publicTransport
[parking]: ../../schema/parking
[name]: ../../schema/name
[disambiguatingDescription]: ../../schema/name
[description]: ../../schema/description
[channel]: ../../schema/channel

[additionalProperty discover]: https://docs.discover.swiss/dev/quickstarts/how-to-work-with-traveler-and-itemField/#example-special-additionalproperty
[Place discover]: https://docs.discover.swiss/dev/reference/dataschema/definition/infocenter-classes/Place/

[itemReviewed discover]: https://docs.discover.swiss/dev/reference/dataschema/definition/infocenter-classes/Review/#properties

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
    * [ ] [itemOffered]? --> Verknüpfte Produkte / Service bei discover.swiss?
    * [ ] [availableAtOrFrom]?
    * [ ] [offeredBy]?
- [ ] 


## Beispiele

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

## Demo Inhalt

## Contentdesk.io Demo

- [Tagespass](https://demo.pim.tso.ch/#/enrich/product/74589a84-bfb9-4fcb-a086-a349ba10205d)
  
    * Angebote [Offers]
    
        * [20% Rabatt](https://demo.pim.tso.ch/#/enrich/product/856b935f-05e2-4f26-addc-33894f97b4f9)
        * [Gratis](https://demo.pim.tso.ch/#/enrich/product/8b42f340-85bb-4bd1-b9c5-d0e23887bd94)
        * [Gratis Sauna Eintritt](https://demo.pim.tso.ch/#/enrich/product/345c8f62-f583-4331-9523-af9ed65e0e54)

## discover.swiss

- [Tagespass](https://partner-test.discover.swiss/infocenter/details/Product/ctd_74589a84-bfb9-4fcb-a086-a349ba10205d?tab=0)
    
    * Beziehnung?
    
        * [20% Rabatt](https://partner-test.discover.swiss/infocenter/details/Product/ctd_07314839-1d34-4205-bee2-8615d8e44fa8?tab=0)
        * [Gratis](https://partner-test.discover.swiss/infocenter/details/Product/ctd_562d0dd4-8c33-462b-b166-2242e5779bc8?tab=0)
        * [Gratis Sauna Eintritt](https://partner-test.discover.swiss/infocenter/details/Product/ctd_1e370b67-57ed-4f55-99f5-f7f962aa176c?tab=0)