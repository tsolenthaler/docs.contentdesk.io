---
tags:
  - concept
hide:
  - navigation
---
# Gästekarte

Eine Gästekarte ist ein Dokument oder eine Karte, die Gäste in bestimmten Urlaubsregionen erhalten, wenn sie dort übernachten. Diese Karte bietet verschiedene Vergünstigungen und kostenlose Angebote, wie z.B. ermäßigte Eintrittspreise für Sehenswürdigkeiten, kostenlose Nutzung öffentlicher Verkehrsmittel oder Rabatte bei Freizeitaktivitäten.

Bspw. Tagespass Glarnerland

## Beispiel Gästekarte
``` mermaid
graph TD
    Product[Gästekarte] -->|bietet|OfferGratis[Angebot Gratis]
    Product -->|bietet|Offer20Rabatt[Angebot 20% Rabatt]
    Product -->|bietet|OfferSauna[Angebot Gratis Sauna Eintritt]

    OfferGratis -->|Angebote| OfferDinoPark["Einritt Dino Park"]
    OfferGratis -->|Angebote| ProductKaffee["Kaffee"]
    OfferGratis -->|Angebote| ProductNusstange["Nusstange"]

    OfferDinoPark -->|erhältlich bei| PlaceDinoPark[Park Dino]

    ProductNusstange -->|erhältlich bei|PlaceBeck

    Offer20Rabatt -->|Angebote| ServiceB["Sauna-Eintritt"]

    Offer20Rabatt -->|erhältlich bei| PlaceOstPark[Alpine Abenteuerpark Ostschweiz]
    Offer20Rabatt -->|erhältlich bei| PlaceHipo[Nationalpark Hipo]
    Offer20Rabatt -->|erhältlich bei| PlaceSuperland[Superland Park]

    OfferSauna -->|erhältlich bei| PlaceHotelC[Sternenhotel]
    OfferSauna -->|erhältlich bei| PlaceHotelB[Hotel Zweistein]
```

## Schema.org
``` mermaid
graph TD
    Product -->|offers|Offer

    Offer -->|itemOffered| Product
    Offer -->|itemOffered| Service
    Offer -->|itemOffered| Event
    Offer -->|availableAtOrFrom 0 ... n| Place

    Service -->|offers| Offer
    Event -->|offers| Offer

    Offer -->|offeredBy| Organization
    Offer -->|offeredBy| Person

    Offer -->|availableAtOrFrom| Place
```

### Types

* [Product](../../schema/Place.md)
* [Offer](../../schema/Offer.md)

### Properties

* [offers](../../schema/offers.md)
* [itemOffered](../../schema/itemOffered.md)
* [availableAtOrFrom](../../schema/availableAtOrFrom.md)
* *[offeredBy](../../schema/offeredBy.md)

## Beispiele

## Contentdesk.io Demo

- [Tagespass](https://demo.pim.tso.ch/#/enrich/product/74589a84-bfb9-4fcb-a086-a349ba10205d)
  
    * Angebote [Offers]
    
        * [20% Rabatt](https://demo.pim.tso.ch/#/enrich/product/856b935f-05e2-4f26-addc-33894f97b4f9)
        * [Gratis](https://demo.pim.tso.ch/#/enrich/product/8b42f340-85bb-4bd1-b9c5-d0e23887bd94)
        * [Gratis Sauna Eintritt](https://demo.pim.tso.ch/#/enrich/product/345c8f62-f583-4331-9523-af9ed65e0e54)

## discover.swiss

- [Tagespass](https://partner-test.discover.swiss/infocenter/details/Product/ctd_74589a84-bfb9-4fcb-a086-a349ba10205d?tab=0)

## Schema.org

### mit unterschiedlichen Preisen

``` json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Tagespass",
  "description": "Ein Tagespass mit verschiedenen Angeboten und Produkten von Partnerorganisationen.",
  "offers": [
    {
      "@type": "Offer",
      "itemOffered": {
        "@type": "Service",
        "name": "Gratis Sauna Eintritt"
      },
      "price": "0",
      "priceCurrency": "CHF"
    },
    {
      "@type": "Offer",
      "itemOffered": {
        "@type": "Product",
        "name": "Gratis Nussstange"
      },
      "price": "0",
      "priceCurrency": "CHF"
    }
  ]
}
```
### Mit mehrere Gratis Angebote
``` json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Tagespass",
  "description": "Ein Tagespass mit verschiedenen Angeboten und Produkten von Partnerorganisationen.",
  "offers": {
    "@type": "Offer",
    "price": "0",
    "priceCurrency": "CHF",
    "itemOffered": [
      {
        "@type": "Service",
        "name": "Gratis Sauna Eintritt"
      },
      {
        "@type": "Product",
        "name": "Gratis Nussstange"
      }
    ]
  }
}
```