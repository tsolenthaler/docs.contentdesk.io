---
tags:
  - type
hide:
  - navigation
---

# Place

https://schema.org/Place

https://docs.discover.swiss/dev/reference/dataschema/definition/infocenter-classes/Place/

## Properties

| Name                        | Type             | Beschreibung             |
| --------------------------- | ---------------- | ------------------------ |
| [name]                      | Text             | Bezeichnung des Objekts  |
| [disambiguatingDescription] | Textarea         | Kurzbeschreibung         |
| [description]               | Textarea         | Beschreibung des Objekts |
| [image]                     | Image            | Hauptbild des Objekts    |
| [license]                   | Einfache-Auswahl | Lizenz des Objekts       |

## Use-Case / Beispiele

### Empfehlungen (Recommandation)

### contentdesk.io API

```json
{
  ...,
  "associations": {
    ...
    "Recommendation": {
            "products": [],
            "product_models": [],
            "groups": []
      },
    ...
  }
}

```

### Weitere Orte (containedInPlace)

```json
{
  "@context": "https://schema.org",
  "@type": "Place",
  "name": "Stiftsbibliothek St. Gallen",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "Klosterhof 6D",
    "addressLocality": "St. Gallen",
    "postalCode": "9000",
    "addressCountry": "Schweiz"
  },
  "containedInPlace": {
    "@type": "Place",
    "name": "Stiftsbezirk St. Gallen"
  }
}
```

### containsPlace

```json
{
  "@context": "https://schema.org",
  "@type": "Place",
  "name": "Stiftsbibliothek St. Gallen",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "Klosterhof 6D",
    "addressLocality": "St. Gallen",
    "postalCode": "9000",
    "addressCountry": "Schweiz"
  },
  "containsPlace": [
    {
      "@type": "Place",
      "name": "Lesesaal"
    },
    {
      "@type": "Place",
      "name": "Ausstellungsraum"
    }
  ]
}
```

### event

### Videos
