---
tags:
  - property
hide:
  - navigation
---

# accommodationFloorPlan
Property

[https://schema.org/accommodationFloorPlan](https://schema.org/accommodationFloorPlan)

Verknüpfung

## Verwendet für diese Typen
[Accommodation](/schema/Accommodation) via [accommodationFloorPlan](/schema/accommodationFloorPlan) 

## Beispiel

```mermaid
flowchart LR
    Accommodation(Unterkunft) -->|accommodationFloorPlan| FloorPlan(Grundriss / Raumplan)
```

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
  "accommodationFloorPlan": {
    "@type": "FloorPlan",
    "url": "https://example.com/grundriss.pdf",
    "name": "Grundriss des Beispielorts",
    "description": "PDF-Dokument mit dem Grundriss des Beispielorts"
  }
}
```