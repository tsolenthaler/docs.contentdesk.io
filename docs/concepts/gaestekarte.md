---
tags:
  - concept
hide:
  - navigation
---
# Gästekarte

Eine Gästekarte ist ein Dokument oder eine Karte, die Gäste in bestimmten Urlaubsregionen erhalten, wenn sie dort übernachten. Diese Karte bietet verschiedene Vergünstigungen und kostenlose Angebote, wie z.B. ermäßigte Eintrittspreise für Sehenswürdigkeiten, kostenlose Nutzung öffentlicher Verkehrsmittel oder Rabatte bei Freizeitaktivitäten.

Bspw:

* Glarnerland Pass 
* ZüriCard

## Beispiel Gästekarte
``` mermaid
graph TD
    GuestCard[Gästekarte] --> |bietet| OfferGratisDino[Angebot Gratis Dino Park]
    GuestCard -->|bietet| Offer20RabattHipo[Angebot 20% Rabatt Nationalpark Hipo]
    GuestCard -->|bietet| OfferSauna[Angebot Gratis Sauna Eintritt]
    GuestCard -->|bietet| OfferNusstange[Angebot Gratis Nussstange]

    OfferGratisDino --> |Angebot| OfferDinoPark["Einritt Dino Park"]
    OfferGratisDino --> |erhältlich bei| PlaceDinoPark

    OfferDinoPark -->|erhältlich bei| PlaceDinoPark[Park Dino]

    OfferNusstange --> |Angebot| ProductNusstange[Nusstange]
    OfferNusstange --> |erhältlich bei| PlaceBeck[Bäckerei Beck]
    ProductNusstange --> |erhältlich bei| PlaceBeck

    Offer20RabattHipo --> |Angebot| ProductHipo[Eintritt Hipo Nationalpark]
    Offer20RabattHipo --> |erhältlich bei| PlaceHipo[Nationalpark Hipo]
    ProductHipo --> |erhältlich bei| PlaceHipo[Nationalpark Hipo]

    OfferSauna --> |Angebot| ProductSauna[Eintritt Sauna Hotel Zweistein]
    OfferSauna --> |erhältlich bei| PlaceHotel[Hotel Zweistein]
    ProductSauna --> |erhältlich bei| PlaceHotel[Hotel Zweistein]
```

## Schema.org
``` mermaid
graph TD
    GuestCard -->|isRelatedTo| Offer

    Offer --> |itemOffered| Product[Product / Service / Event]
    Offer --> |areaServed| Place

    Product --> |areaServed| Place
```

### Types

* [GuestCard](../../schema/GuestCard)
* [Offer](../../schema/Offer)
* [Product](../../schema/Product)
* [Place](../../schema/Place)


### Properties

* [offers](../../schema/offers) - Verknüpfung
* [itemOffered](../../schema/itemOffered) - Verknüpfung
* [isRelatedTo](../../schema/isRelatedTo) - Verknüpfung
* [areaServed](../../schema/areaServed) - Verknüpfung

!!! info "Hinweis"

    Diese Properties werden im Contentdesk via Verknüpfungen gepflegt.

!!! warning "Spezifische Properties / Attribut"

    Pro Gästekarte müssen spezifische Properties / Attribute gepflegt werden!
    Bspw. AVS ID, etc.

## Beispiele

## Contentdesk.io Demo

- [Tagespass](https://demo.pim.tso.ch/#/enrich/product/74589a84-bfb9-4fcb-a086-a349ba10205d)
  
    * Angebote [isRelatedTo]
    
        * [20% Rabatt](https://demo.pim.tso.ch/#/enrich/product/856b935f-05e2-4f26-addc-33894f97b4f9)
        * [Gratis](https://demo.pim.tso.ch/#/enrich/product/8b42f340-85bb-4bd1-b9c5-d0e23887bd94)
        * [Gratis Sauna Eintritt](https://demo.pim.tso.ch/#/enrich/product/345c8f62-f583-4331-9523-af9ed65e0e54)

## discover.swiss

- [Tagespass](https://partner-test.discover.swiss/infocenter/details/Product/ctd_74589a84-bfb9-4fcb-a086-a349ba10205d?tab=0)
    
    * Beziehnung?
    
        * [20% Rabatt](https://partner-test.discover.swiss/infocenter/details/Product/ctd_07314839-1d34-4205-bee2-8615d8e44fa8?tab=0)
        * [Gratis](https://partner-test.discover.swiss/infocenter/details/Product/ctd_562d0dd4-8c33-462b-b166-2242e5779bc8?tab=0)
        * [Gratis Sauna Eintritt](https://partner-test.discover.swiss/infocenter/details/Product/ctd_1e370b67-57ed-4f55-99f5-f7f962aa176c?tab=0)
