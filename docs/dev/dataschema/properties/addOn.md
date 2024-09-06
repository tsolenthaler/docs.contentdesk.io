# addOn



https://schema.org/addOn


Verknüpfung / Association-type

## Schema
``` mermaid
graph LR
    Offer(Angebot) -->|addOn|Offer
    Offer -->|addOn|Offer
```

!!! example

## Beispiele

### Zuschläge
``` json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Beispielprodukt",
  "offers": {
    "@type": "Offer",
    "price": "100.00",
    "priceCurrency": "CHF",
    "addOn": [
      {
        "@type": "Offer",
        "name": "Sonntagszuschlag",
        "price": "10.00",
        "priceCurrency": "CHF"
      },
      {
        "@type": "Offer",
        "name": "Feiertagszuschlag",
        "price": "15.00",
        "priceCurrency": "CHF"
      }
    ]
  }
}
```