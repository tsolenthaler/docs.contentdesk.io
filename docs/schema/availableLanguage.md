---
tags:
  - property
hide:
  - navigation
---

# availableLanguage
Property

https://schema.org/availableLanguage

## Verwendung
Gibt die Sprachen an, in denen ein Dienst oder ein Angebot verfügbar ist.

## Typische Anwendung
Wird häufig bei Service, Offer, TouristTrip und ähnlichen Typen verwendet.

## Beispiel
Wenn du eine Stadtführung anbietest, die in mehreren Sprachen verfügbar ist, würdest du availableLanguage verwenden, um dies anzugeben.

``` json
{
  "@type": "TouristTrip",
  "name": "Stadtführung",
  "availableLanguage": ["de", "en"]
}
```