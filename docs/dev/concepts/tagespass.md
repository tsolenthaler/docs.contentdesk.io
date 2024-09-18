---
tags:
  - property
hide:
  - navigation
---
# Tagespass


Produkt mit Angeboten, Leistungen, Produkten von anderen Leistungsträgern.


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