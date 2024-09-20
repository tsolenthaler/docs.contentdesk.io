---
tags:
  - concept
hide:
  - navigation
---
# Gästekarte

Produkt mit Angeboten, Leistungen oder Produkten von anderen Leistungsträgern.

Bspw. Tagespass

## Schema.org

``` mermaid
graph TD
    Product -->|offers|Offer

    Offer -->|itemOffered| ProductA
    Offer -->|itemOffered| ServiceB
    Offer -->|itemOffered| EventC
    Offer -->|availableAtOrFrom 0 ... n| PlaceA

    ProductA -->|offers| OfferA
    ServiceB -->|offers| OfferB
    EventC -->|offers| OfferC


    OfferA -->|offeredBy| Organization
    OfferB -->|offeredBy| Person
    OfferC -->|offeredBy| Organization

    OfferA -->|availableAtOrFrom| PlaceA
    OfferA -->|availableAtOrFrom| PlaceB
    OfferA -->|availableAtOrFrom| PlaceC
    OfferB -->|availableAtOrFrom| PlaceB
    OfferC -->|availableAtOrFrom| PlaceA
```


## Beispiel

### Nach Schema.org als Offer

``` json
{
  "@context": "https://schema.org",
  "@type": "Offer",
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