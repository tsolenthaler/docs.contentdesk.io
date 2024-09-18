---
tags:
  - concepts
hide:
  - navigation
---
# Führungen

* Gruppenführungen
* Stadtführungen


## Beispiel

### Schema.org

``` json
{
  "@context": "https://schema.org",
  "@type": "TouristTrip",
  "name": "Geführte Museumstour",
  "description": "Eine spannende Führung durch die Highlights des Museums.",
  "touristType": "Group",
  "offers": {
    "@type": "Offer",
    "price": "20.00",
    "priceCurrency": "EUR",
    "availability": "https://schema.org/InStock",
    "validFrom": "2024-09-18",
    "validThrough": "2024-12-31",
    "url": "https://example.com/buchung"
  },
  "startDate": "2024-09-18T10:00:00+02:00",
  "endDate": "2024-09-18T12:00:00+02:00",
  "location": {
    "@type": "Place",
    "name": "Museum Beispiel",
    "address": {
      "@type": "PostalAddress",
      "streetAddress": "Museumsstraße 1",
      "addressLocality": "Berlin",
      "postalCode": "10117",
      "addressCountry": "DE"
    }
  }
}
```