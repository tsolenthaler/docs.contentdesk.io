---
tags:
  - concept
hide:
  - navigation
---
# Gästekarte

Produkt mit Angeboten, Leistungen oder Produkten von anderen Leistungsträgern.

Bspw. Tagespass

## Beispiel Tagespass
``` mermaid
graph TD
    Product[Tagespass] -->|offers|Offer[Angebot]

    Offer -->|itemOffered| ProductA["Nusstange"]
    Offer -->|itemOffered| ServiceB["Sauna-Eintritt"]
    Offer -->|itemOffered| EventC["Eintritt ESAF"]
    Offer -->|availableAtOrFrom 0 ... n| PlaceA

    ProductA -->|offers| OfferA
    ServiceB -->|offers| OfferB
    EventC -->|offers| OfferC

    OfferA -->|offeredBy| OrganizationA[Glanerland Tourismus]
    OfferC -->|offeredBy| OrganizationA
    OfferB -->|offeredBy| OrganizationB["ESAF Organisation"]

    OfferA -->|availableAtOrFrom| PlaceA
    OfferA -->|availableAtOrFrom| PlaceB
    OfferA -->|availableAtOrFrom| PlaceC
    OfferB -->|availableAtOrFrom| PlaceB
    OfferC -->|availableAtOrFrom| PlaceA
```

## Schema.org
``` mermaid
graph TD
    Product -->|offers|Offer

    Offer -->|itemOffered| Product
    Offer -->|itemOffered| Service
    Offer -->|itemOffered| Event
    Offer -->|availableAtOrFrom 0 ... n| Place

    Product -->|offers| Offer
    Service -->|offers| Offer
    Event -->|offers| Offer


    Offer -->|offeredBy| Organization
    Offer -->|offeredBy| Person

    Offer -->|availableAtOrFrom| Place
```


## Beispiele

### Nach Schema.org als Offer

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