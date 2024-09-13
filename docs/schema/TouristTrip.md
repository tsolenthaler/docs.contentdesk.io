---
tags:
  - type
hide:
  - navigation
---

# TouristTrip
[https://schema.org/TouristTrip](https://schema.org/TouristTrip)

Thing > Intangible > Trip > TouristTrip

Dieser Typ ist speziell für touristische Ausflüge und Führungen gedacht und bietet verschiedene Eigenschaften, um Details wie den Namen der Tour, die Dauer, den Preis und vieles mehr anzugeben1.


## Use-Case / Beispiele

### Führung

#### Schema.org JSON-LD
``` json
{
  "@context": "https://schema.org",
  "@type": "TouristTrip",
  "name": "Stadtführung durch Berg SG",
  "description": "Eine spannende Stadtführung durch Berg SG in verschiedenen Sprachen.",
  "inLanguage": "Deutsch",
  "availableLanguage": ["Deutsch", "Englisch", "Französisch", "Italienisch"],
  "offers": {
    "@type": "Offer",
    "price": "20.00",
    "priceCurrency": "CHF"
  }
}
```
