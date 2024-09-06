# Recommendation

https://schema.org/Recommendation

https://docs.discover.swiss/dev/concepts/reviews-and-recommendations/


## Concepts

``` mermaid
graph TD
    Recommendation -.->|inherits|Review
    Recommendation -->|itemReviewed 0 ... n|Trail
    Recommendation -->|itemReviewed 0 ... n|Place
    Recommendation -->|itemReviewed 0 ... n|Product
    Recommendation -->|isRelatedTo 0 ... 1|Place
    Recommendation -->|isRelatedTo 0 ... 1|Product
    Recommendation -->|isRelatedTo 0 ... 1|Event
    Product -->|availableAtOrFrom 0 ... n|Place
    Product -->|offers|Offer
    Offer -->|offeredBy|Organization
    Offer -->|offeredBy|Person
```