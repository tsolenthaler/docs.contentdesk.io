---
tags:
  - projects
hide:
  - navigation
---

# Glarnerland App

## Konzepte

* Tagespass - [Gästekarte]
* "Empfehlungen"-Liste bspw. Auflugstipps - via Tags bei discover.swiss

[Reviews and recommendations]: ../concepts/reviews-and-recommendations.md
[Gästekarte]: ../concepts/gaestekarte.md

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

### Schnittstellen

#### AVS zu contentdesk.io
Manueller übertrag der AVS ID

#### contentdesk.io zu discover.swiss
Ein mal täglich um ca. 04:00 Uhr

#### discover.swiss zu App Binarium
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
        Gaestekarte["Gästekarte (GuestCard)"] --> |isRelatedTo| Angebot["Angebot (Offer)"]
        Angebot --> |itemOffered| Product2["Produkt / Service (Product)"]
        Angebot --> |areaServed| Ort["POI (Place)"]
        Product2 --> |areaServed| Ort
    end
    subgraph discover
        direction TB
        GuestCard["GuestCard (Product)"] -->|isRelatedTo| Offer["Offer(Product)"]
        Offer -->|itemOffered| Product["Produkt / Service (Product)"]
        Offer -->|areaServed| Place["POI (Place)"]
        Product -->|areaServed| Place["POI (Place)"]
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
| Card Typ                      | [GuestCard]           | [GuestCard discover] (Product)                        | Tagespass                 |
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

##### AVS
``` mermaid
classDiagram
    direction TB
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

```

##### Contentdesk
``` mermaid
classDiagram
    direction TB
        class GuestCard {
            uuid Id
            string Name
            uuid avs_id
            string disambiguatingDescription
            date validFrom
            date validThrough
        }
        class Product {
            uuid Id
            string Name
            string disambiguatingDescription
        }
        class Offer {
            uuid Id
            string Name
            uuid avs_id
            string disambiguatingDescription
        }
        class Place["POI (Place)"] {
            uuid Id
            string Name
            string disambiguatingDescription
            string HowToDirection
            string publicTransport
            string parking
            string leisure
        }
    GuestCard --> "0..n" Offer : isRelatedTo

    Offer --> "0..1" Product : itemOffered
    Offer --> "0..1" Place : areaServed
    
    Product --> "0..1" Place : areaServed
```

##### discover.swiss
``` mermaid
classDiagram
    direction TB
    class GuestCard{
        uuid Id
        string Name
        uuid sourceID
        uuid avs_id
    }
    class Offer{
        uuid Id
        string Name
        uid sourceID
    }

    class Place["POI (Place)"]

    class Offer["Offer (Product)"]

    class Product["Produkt/Service (Product)"]

    GuestCard --> "0..n" Offer : isRelatedTo

    Offer --> "0..1" Product : itemOffered
    Offer --> "0..1" Place : areaServed
    Product --> "0..1" Place : areaServed
```

##### App Binarium
``` mermaid
classDiagram
    direction TB
    class Tagespass {

    }
    class Leistung {

    }
    class OrtApp
    class ProduktApp

    class OrtApp["Place"]
    class ProduktApp["Produkt"]

    Tagespass --> "0..n" Leistung : isRelatedTo
    Leistung --> "0..n" ProduktApp : itemOffered
    Leistung --> "0..n" OrtApp : areaServed
    ProduktApp --> "0..n" OrtApp : areaServed
```

#### Table Properties

| AVS         | contentdesk.io                          | discover.swiss                            | App / Binarium            | Comment |
| ----------- | -------------                           | -------------                             | -------------             |   |
|             | **Type [GuestCard]**                    | **Type GuestCard**                        | -                         |   |
|             | -                                       | [ID discover]                             | -                         |
| -           | [identifier] (ID)                       | [sourceId discover]                       | -                         |
| ID          | [avs_id]                                | [additionalProperty discover] avs_id      | -                         |   |
|             | [validFrom]                             | [validFrom discover]                      | -                         |          
|             | [validThrough]                          | [validThrough discover]                   | -                         |
|             | **Type [Place]**                        | **Type [Place discover]**                 | -                         |
|             | [HowToDirection]                        | [gettingThere]                            | -                         |
|             | [publicTransport]                       | [publicTransport]                         | -                         |
|             | [parking]                               | [parking]                                 | -                         |
|             | **All Types - Attributes**              | **All Types**                             | -                         |
|             | [name]                                  | name                                      | -                         |
|             | [disambiguatingDescription] Scope App   | [mobileDescription]                       | -                         |
|             | [description]                           | [description]                             | -                         |  
|             | **Association type** - Verknüfpungen    |                                           | -                         |
|             | [itemOffered]                           | [itemOffered discover]                  | -                         |
|             | [areaServed]                            | [areaServed discover]                   | -                         |
|             | [isRelatedTo]                           | [isRelatedTo discover]                   | -                         |

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

## Offene Punkte / ToDo

- [ ] discover.swiss 
    * [x] Type [GuestCard] --> Product mit AdditonalTypes GuestCard
    * [x] [isRelatedTo] --> Beziehung von GuestCard zu Offer 
    * [x] [Offer] - Angebote
    * [x] [itemOffered] --> Verknüpfte Produkte / Service bei discover.swiss?
    * [x] [areaServed] --> Verknüfpung von Offer zu Place
    * [x] Empfehlungen --> via Tags - muss definiert werden welche genutzt werden sollen!
    * [x] Zuweistung an Projekt bspw. vgl-app
    * [x] Tags für 20% oder Gratis, etc. bei discover.swiss pflegen
    * [x] Kampagnen-Tags für Empfehlung-Liste --> definieren der Tags notwendig (Bspw. Ausflugsziele (life-excursions))
    * [ ] Klassifikation / Kategorie werde nicht übernommen
    * [ ] Öffnungszeiten mit Zeitzonen werden nicht korrekt übernommen
    * [x] Call to Action Button und Link für App (+ Webseite) übernehmen
    * [ ] Skilifte testen
    * [ ] Langlaufloipen testen --> Poi mit Pfad/Strecke/Weg

- [ ] contentdesk.io
    * [x] Angebote pro Gästekarte (Tagepass) / nicht teilen über mehrere Tagespässe!!
    * [x] offeredBy direkt zu Place! keine Organization dazwischen
    * [x] Demo Inhalte erfassen 3 Tagespasse mit mehreren Angebote bei itemOffered und Place bei areaServed
    * [x] Demo Inhalte für 3 Empfehlungen (bspw. Ausflugstipps)
    * [x] Zugang Connect ---> discover.swiss
    * [x] [offers] mit [isRelatedTo] ersetzen
    * [x] Produtke und Angebote immer mit Datum gütlig von und gültig bis (Pflichtfelder)
    * [x] Freizeittypen bei Produkt und Angebot
    * [ ] sitios / ginto läuft über discover.swiss (Tags?)
    * [x] discount (Rabatt in Prozenz) bei Angebot möglich? gemäss Schema.org - Abklären (vorerst einfach via Tags bei discover.swiss)
    * [ ] Freizeittyp (leisure) Discover.swiss Kateogiren an discover.swiss übergeben
    * [x] isAccessibleForFree und publicAccess - Demo Inhalt
    * [x] publicTransport und parking
    * [x] AVS Object ID avs_object_id --> Number bspw. 32
    * [x] Attributes Options Übersetzungen mit Tags bspw. PreisKategorien, und paymentAccepted
   

## Demo Inhalt

### Contentdesk.io Demo
``` mermaid
graph TD
    Tagespass[<a href='https://demo.pim.tso.ch/#/enrich/product/74589a84-bfb9-4fcb-a086-a349ba10205d' target='_blank'>Gästekarte Tagespass</a>]
    Tagespass -->|isRelatedTo| OfferGratisDino["Gratis Dino Park Eintritt"]
    Tagespass -->|isRelatedTo| OffeGartisSauna["Gratis Sauna Eintritt Hotel Zweistein"]
    Tagespass -->|isRelatedTo| OffeBergbahn["20% Rabatt auf Bergbahn-Fahrt auf den Sitzberg"]
    Tagespass -->|isRelatedTo| OffeGratisKaffe["Gratis Kaffe von Restaurant Vegi"]
    Tagespass -->|isRelatedTo| OffeGratisNusstange["Gratis Nusstange vom Beck"]

    OfferGratisDino -->|areaServed| PlaceDino["Park Dino"]
    OfferGratisDino -->|itemOffered| ProductDinoEintritt["Eintritt Dino Park"]

    OffeGartisSauna -->|areaServed| PlaceHotelZweistein["Hotel Zweistein"]
    OffeGartisSauna -->|itemOffered| ProductSaunaEintritt["Eintritt Sauna Hotel Zweistein"]
```

#### Gästekarte
- [Gästekarte Tagespass](https://demo.pim.tso.ch/#/enrich/product/74589a84-bfb9-4fcb-a086-a349ba10205d)
    * [isRelatedTo]
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

#### Empfehlung

Via Tags in Discover.swiss pflegen.
Definieren welche Tags für welche Empfehlungs-Liste genutzt wird.
Eigene können im Interface erstellt werden.

### discover.swiss

- [Gästekarte Tagespass](https://partner-test.discover.swiss/infocenter/details/Product/ctd_74589a84-bfb9-4fcb-a086-a349ba10205d?tab=0)
    
    * Angebote via [isRelatedTo]
    
        * [20% Rabatt](https://partner-test.discover.swiss/infocenter/details/Product/ctd_07314839-1d34-4205-bee2-8615d8e44fa8?tab=0)
        * [Gratis](https://partner-test.discover.swiss/infocenter/details/Product/ctd_562d0dd4-8c33-462b-b166-2242e5779bc8?tab=0)
        * [Gratis Sauna Eintritt](https://partner-test.discover.swiss/infocenter/details/Product/ctd_1e370b67-57ed-4f55-99f5-f7f962aa176c?tab=0)


### Design App

[Design figma](https://www.figma.com/design/OcvSQlgOO70u17wXhO8EJO/Glarnerland?node-id=1156-26321&node-type=frame)


## Datenpflege

### Bei Contentdesk.io

* Gästekarte

    * AVS ID
    * Preis
    * Freizeittyp (Discover.swiss Kategorie) (leisure)
    * Gültig von 
    * Gültig bis
    * Preis-Informationen (offers) - (Bedingungen bei discover.swiss und im Beschreibungs-Text!)
    * Verknüpfungen

        * ist verbunden mit [isRelatedTo] (mehrere Angebot)
        * Angebot, wo es bezogen werden kann [areaServed]


* Angebot

    * AVS ID
    * Freizeittyp (Discover.swiss Kategorie) (leisure)
    * Preis
    * Gültig von 
    * Gültig bis
    * Preis-Informationen (offers) / (Bedingungen bei discover.swis)
    * Verknüpfungen

        * enthaltene Angebote [itemOffered] (nur 1 Angebot zu 1 Produkt)
        * Angebot, wo es bezogen werden kann [areaServed] (nur 1 Angebot zu 1 Standort)


### Bei discovers.swiss

* Gästekarte

    * ???

* Angebot

    * Tags für Bspw. Gratiseintritte (reduction-free) oder Reduktion mit Tourismuskarte (reduction-citycard)
    * Kampagnen-Tags von VGL: 5 %(vgl_glp-5)


* Empfehlungsliste

    * definierte Tags setzten bei gewünschten Objekte (bspw. Place) - bspw. Tag Ausflugsziele (life-excursions)
    * Kampagnen-Tags von VGL definiert: Home_3 (vgl_home-3), Home_1 (vgl_home-1), Home_2 (vgl_home-2)