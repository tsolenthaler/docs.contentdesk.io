---
tags:
  - property
hide:
  - navigation
---

# availableAtOrFrom
[https://schema.org/availableAtOrFrom](https://schema.org/availableAtOrFrom)

Verknüpfung

## Definition
Dieses Attribut wird verwendet, um anzugeben, wo ein Produkt oder eine Dienstleistung verfügbar ist. Es kann sich um eine physische Adresse, eine URL oder einen anderen Ort handeln, an dem das Produkt oder die Dienstleistung erworben werden kann.

## Beispiele

### Produkt ist bei folgenden POI(Place) verfügbar
```mermaid
flowchart LR
    Product(Produkt) -->|availableAtOrFrom| Place(POI)
```

``` json
{
  "@context": "https://schema.org",
  "@type": "Offer",
  "name": "Tagespass",
  "price": "20.00",
  "priceCurrency": "CHF",
  "availableAtOrFrom": {
    "@type": "Place",
    "name": "Freizeitpark Berg",
    "address": {
      "@type": "PostalAddress",
      "streetAddress": "Hauptstrasse 1",
      "addressLocality": "Berg",
      "addressRegion": "SG",
      "postalCode": "9305",
      "addressCountry": "CH"
    }
  }
}

```

## Ähnliche Verknüpfungen

[areaServed](/schema/areaServed)

## Hinweise

!!! info "Hinweis"
    Bei wird areaServed statt availableAtOrFrom für die Verknüpfung der Produkte mit einem POI verwendet.
    https://docs.discover.swiss/dev/concepts/offers/