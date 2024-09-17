---
tags:
  - type
hide:
  - navigation
---

# Recommendation

[https://schema.org/Recommendation](https://schema.org/Recommendation)


## Konzept

[Review and Recommandtions](../dev/concepts/reviews-and-recommendations.md)

## Properties

* isRelatedTo
* itemReviewed

## Beispiel / Use-Case

### Ausflugstipps

#### Akeneo API
``` json
{
    ...,
    "family": "Recommendation",
    "values": {
        "channel": [
            {
                "locale": null,
                "scope": null,
                "data": [
                    "app",
                    "ecommerce"
                ]
            }
        ],
    }
    ...,
    "associations": {
        ...,
        "isRelatedTo": {
            "products": [
                "74589a84-bfb9-4fcb-a086-a349ba10205d"
            ],
            "product_models": [],
            "groups": []
        },
        ...,
        "itemReviewed": {
            "products": [
                "043aec73-cfa2-4b5c-ad9b-8d3cd4d45a7e",
                "04f93ed5-0c69-453a-92f5-0b36b96ad13e",
                "05cffdbd-5e33-4b47-ad69-b587754d6403",
                "06e9f20f-5db6-4541-b09b-2056c374a263",
                "0a1e30db-a726-4a8f-84f6-b1f66e6b33c6"
            ],
            "product_models": [],
            "groups": []
        },
    }
}
```

#### Schema.org JSON
``` json
{
  "@context": "https://schema.org",
  "@type": "Recommendation",
  "name": "Ausflugstipps",
  "isRelatedTo": {
    "@type": "Offer",
    "name": "Tagespass"
  },
  "itemReviewed": [
    {
        "@type": "Place",
        "name": "Stiftsbezirk St. Gallen"
    },
    {
        "@type": "Product",
        "name": "Taschentuch"
    },
    {
        "@type": "Event",
        "name": "Veranstaltung"
    },
  ]
}
```