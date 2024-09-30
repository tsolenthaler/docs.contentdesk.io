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
        Angebot --> |itemOffered| Angebot2["Produkt / Service"]
        Angebot --> |areaServed| Ort["Place (POI)"]
    end
    subgraph discover
        direction TB
        Touristcard["Touristcard"] -->|offers| Offer["Produkt mit Angebot"]
        Offer -->|itemOffered| Product["Produkt / Service"]
        Offer -->|areaServed| Place["Place (POI)"]
    end
    subgraph app
        direction TB
        Tagespass --> Leistung
        Leistung --> ProduktApp["Produkt / Service"]
        Leistung --> OrtApp["Place (POI)"]
    end

    avs --> contentdesk
    contentdesk --> discover
    discover --> app
```

#### Table Types

| AVS                           | contentdesk.io        | discover.swiss                                        | App / Binarium            |
| -----------                   | -------------         | -------------                                         | -------------             |   
| Card Typ                      | [GuestCard]           | [Product discover] additonalType GuestCard            | Tagespass                 |
|                               | [Product]             | [Product discover]                                    | Produkt                   |
| Akzeptanzstelle / Leistung?   | [Offer]               | [Offer discover]                                      | Leistung                  |       
|                               | [Place]               | [Place discover]                                      | Place                     |

[GuestCard]: ../../schema/GuestCard
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
        class GuestCard {
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
    GuestCard --> "0..n" Angebot : offers

    Angebot --> "0..n" Produkt : itemOffered
    Angebot --> "0..n" Ort : areaServed

    namespace discover {
        class GuestCardType{
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

        class Place["Place / Product / Event"]

        class Product["Place / Produkt"]
    }

    namespace app {
        class Tagespass {

        }
        class Leistung {

        }
        class OrtApp
        class ProduktApp

        class OrtApp["Place"]
        class ProduktApp["Produkt"]
    }

    Tagespass --> "0..n" Leistung : offers
    Leistung --> "0..n" ProduktApp : itemOffered
    Leistung --> "0..n" OrtApp : areaServed
```

#### Table Properties

| AVS         | contentdesk.io                          | discover.swiss                            | App / Binarium            | Comment |
| ----------- | -------------                           | -------------                             | -------------             |   |
|             | Type **[GuestCard]**                    | Type **GuestCard**                        | -                         |   |
|             | -                                       | [ID discover]                             | -                         |
| -           | [identifier] (ID)                       | [sourceId discover]                       | -                         |
| ID          | [avs_id]                                | [additionalProperty discover] avs_id      | -                         |   |
|             | [validFrom]                             | [validFrom discover]                      | -                         |          
|             | [validThrough]                          | [validThrough discover]                   | -                         |
|             | Type **[Place]**                        | Type **[Place discover]**                 | -                         |
|             | [HowToDirection]                        | [gettingThere]                            | -                         |
|             | [publicTransport]                       | [publicTransport]                         | -                         |
|             | [parking]                               | [parking]                                 | -                         |
|             | **All Types - Attributes**              | **All Types**                             | -                         |
|             | [name]                                  | name                                      | -                         |
|             | [disambiguatingDescription] Scope App   | [mobileDescription]                       | -                         |
|             | [description]                           | [description]                             | -                         |  
|             | [channel]                               | [additionalProperty]❓channel            | -                         |
|             | **Association type** - Verknüfpungen    |                                           | -                         |
|             | [offers]                                | [offers discover]                         | -                         |
|             | [itemOffered]                           | [itemOffered discover]                  | -                         |
|             | [areaServed]                            | [areaServed discover]                   | -                         |

[offers]: ../../schema/offers
[itemOffered]: ../../schema/itemOffered
[areaServed]: ../../schema/areaServed

[availableAtOrFrom]: ../../schema/availableAtOrFrom
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

#### Gästekarte Tagespass
``` mermaid
graph TD
    Product[Product GuestCard]-->|offers|Offer

    Offer-->|itemOffered|Product
    Offer-->|availableAtOrFrom|Place
    Offer-->|offeredBy|Organization
    
    Organization-->|areaServed|Place
    Organization-->|makesOffer|Offer
```

## Offene Punkte / ToDo

- [ ] discover.swiss 
    * [ ] Type [GuestCard] --> Product mit AdditonalTypes GuestCard
    * [x] [Offer] und [offers]
    * [ ] [itemOffered]? --> Verknüpfte Produkte / Service bei discover.swiss?
- [ ] contentdesk.io
    * [ ] Angebote pro Gästekarte (Tagepass) / nicht teilen über mehrere Tagespässe!!
    * [x] offeredBy direkt zu Place! keine Organization dazwischen
    * [ ] Demo Inhalte erfassen 3 Tagespasse mit mehreren Angebote bei itemOffered und Place bei areaServed

## Demo Inhalt

## Contentdesk.io Demo
``` mermaid
graph TD
    Tagespass[<a href='https://demo.pim.tso.ch/#/enrich/product/74589a84-bfb9-4fcb-a086-a349ba10205d' target='_blank'>Gästekarte Tagespass</a>]
    Tagespass -->|offers| OfferGratisDino["Gratis Dino Park Eintritt"]
    Tagespass -->|offers| OffeGartisSauna["Gratis Sauna Eintritt Hotel Zweistein"]
    Tagespass -->|offers| OffeBergbahn["20% Rabatt auf Bergbahn-Fahrt auf den Sitzberg"]
    Tagespass -->|offers| OffeGratisKaffe["Gratis Kaffe von Restaurant Vegi"]
    Tagespass -->|offers| OffeGratisNusstange["Gratis Nusstange vom Beck"]

    OfferGratisDino -->|areaServed| PlaceDino["Park Dino"]
    OfferGratisDino -->|itemOffered| ProductDinoEintritt["Eintritt Dino Park"]

    OffeGartisSauna -->|areaServed| PlaceHotelZweistein["Hotel Zweistein"]
    OffeGartisSauna -->|itemOffered| ProductSaunaEintritt["Eintritt Sauna Hotel Zweistein"]
```

### Gästekarte
- [Gästekarte Tagespass](https://demo.pim.tso.ch/#/enrich/product/74589a84-bfb9-4fcb-a086-a349ba10205d)
    * Angebote via [offers]
        * [Gratis Dino Park Eintritt](https://demo.pim.tso.ch/#/enrich/product/03274851-da78-4793-bf8d-3f6d7b85345a)
            *  Angebot, wo es bezogen werden kann [areaServed]
                * [Park Dino](https://demo.pim.tso.ch/#/enrich/product/57bba700-bac4-4b83-8038-74efd93032ca)
            * Enthaltene Angebote [itemOffered]
                * [Eintritt Dino Park](https://demo.pim.tso.ch/#/enrich/product/887a664e-4734-4a7e-aab7-5f30bfada107)
        * [Gratis Sauna Eintritt Hotel Zweistein](https://demo.pim.tso.ch/#/enrich/product/345c8f62-f583-4331-9523-af9ed65e0e54)
            * Angebot, wo es bezogen werden kann  [areaServed]
                * [Hotel Zweistein](https://demo.pim.tso.ch/#/enrich/product/631b73f9-15dd-461e-a3f6-e706c9f30630)
            * Enthaltene Angebote [itemOffered]
                * [Sauna Eintritt Hotel Zweistein](https://demo.pim.tso.ch/#/enrich/product/1afc2025-cb65-4b05-9297-ec9ee51a87f3)
        * [20% Rabatt auf Bergbahn-Fahrt auf den Sitzberg](https://demo.pim.tso.ch/#/enrich/product/856b935f-05e2-4f26-addc-33894f97b4f9)
            *  Angebot, wo es bezogen werden kann [areaServed]
                * [Sitzberg](https://demo.pim.tso.ch/#/enrich/product/ed6a836c-943f-4ad9-a9bf-6cbe8021bf49)
            * Enthaltene Angebote [itemOffered]
                * [Bergfahrt auf den Sitzberg](https://demo.pim.tso.ch/#/enrich/product/291e6b23-3e43-4a78-a1d8-14be12e57249)
        * [Gratis Kaffe von Restaurant Vegi](https://demo.pim.tso.ch/#/enrich/product/8b42f340-85bb-4bd1-b9c5-d0e23887bd94)
            *  Angebot, wo es bezogen werden kann [areaServed]
                * [Restaurant Vegi](https://demo.pim.tso.ch/#/enrich/product/12387058-735d-48b2-86fc-068ce39efa0d)
            * Enthaltene Angebote [itemOffered]
                * [Kaffe von Restaurant Vegi](https://demo.pim.tso.ch/#/enrich/product/8894485f-38ac-4f10-94d8-fd507801c1b5)
        * [Gratis Nusstange vom Beck](https://demo.pim.tso.ch/#/enrich/product/e188459d-1260-4fe5-b538-7effedc46b68)
            *  Angebot, wo es bezogen werden kann [areaServed]
                * [Bäckerei Beck](https://demo.pim.tso.ch/#/enrich/product/dab66e16-f9de-4fb0-ab7c-d96853174712)
            * Enthaltene Angebote [itemOffered]
                * [Nussstange](https://demo.pim.tso.ch/#/enrich/product/a627ea92-fcf6-4bf7-9a44-1271bce41f3d)

## discover.swiss

- [Tagespass](https://partner-test.discover.swiss/infocenter/details/Product/ctd_74589a84-bfb9-4fcb-a086-a349ba10205d?tab=0)
    
    * Beziehnung?
    
        * [20% Rabatt](https://partner-test.discover.swiss/infocenter/details/Product/ctd_07314839-1d34-4205-bee2-8615d8e44fa8?tab=0)
        * [Gratis](https://partner-test.discover.swiss/infocenter/details/Product/ctd_562d0dd4-8c33-462b-b166-2242e5779bc8?tab=0)
        * [Gratis Sauna Eintritt](https://partner-test.discover.swiss/infocenter/details/Product/ctd_1e370b67-57ed-4f55-99f5-f7f962aa176c?tab=0)