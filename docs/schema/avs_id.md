---
tags:
  - property
hide:
  - navigation
---

# avs_id

Akzepttanzstelle ID für die Platform AVS Abrechnungs- und Verwaltungs-Systeme GmbH.

https://www.avs.de/

Attribut im Contentdesk.io

Typ: string


## Beispiel

### Akeneo API
``` json
{
    ...,
    "values":{
        ...
        "avs_id": [
            {
                "locale": null,
                "scope": null,
                "data": "2edda1cc-ce96-4451-9ffc-ab1a100fba99"
            }
        ],
        ...
    }
}
```

### Schema.org JSON-LD
Additional Property
``` json
{
  "@context": "https://schema.org",
  "@type": "Place",
  "name": "Beispielort",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "Musterstraße 1",
    "addressLocality": "Musterstadt",
    "postalCode": "12345",
    "addressCountry": "DE"
  },
  "additionalProperty": {
    "@type": "PropertyValue",
    "name": "avs_id",
    "value": "2edda1cc-ce96-4451-9ffc-ab1a100fba99"
  }
}
```




