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

* [itemOffered](../../schema/itemOffered) - Verknüpfung
* [isRelatedTo](../../schema/isRelatedTo) - Verknüpfung
* [areaServed](../../schema/areaServed) - Verknüpfung

!!! info "Hinweis"

    Diese Properties werden im Contentdesk via Verknüpfungen gepflegt.

!!! warning "Spezifische Properties / Attribute"

    Pro Gästekarte müssen spezifische Properties / Attribute gepflegt werden!
    Bspw. AVS ID, etc.

## Beispiele

### Contentdesk.io Demo

- [Gästekarte Tagespass](https://demo.pim.tso.ch/#/enrich/product/74589a84-bfb9-4fcb-a086-a349ba10205d)

### discover.swiss

- [Gästekarte Tagespass](https://partner-test.discover.swiss/infocenter/details/Product/ctd_74589a84-bfb9-4fcb-a086-a349ba10205d?tab=0)


## Verwendet in Projekten

* [Glarnerland App]

[Glarnerland App]: ../projects/glarnerlandApp.md