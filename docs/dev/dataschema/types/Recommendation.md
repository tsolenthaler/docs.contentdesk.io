# Recommendation

https://schema.org/Recommendation

https://docs.discover.swiss/dev/concepts/reviews-and-recommendations/


## Concepts

``` mermaid
graph LR
    Recommendation -.->|inherits|Review
    Recommendation -->|itemReviewed 0 ... n|Trail
    Recommendation -->|itemReviewed 0 ... n|Place
    Recommendation -->|itemReviewed 0 ... n|Product
    Product -->|availableAtOrFrom 0 ... n|Place
    Product -->|offers|Offer
    Offer -->|offeredBy|Organization
    Offer -->|offeredBy|Person
```