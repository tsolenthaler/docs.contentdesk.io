# Reviews and recommendations

Dokumentation bei discover.swiss
https://docs.discover.swiss/dev/concepts/reviews-and-recommendations/


## Schema

``` mermaid
graph LR
    subgraph Product
        direction TB
        Product -->|offers|Offer
    end
    Recommendation -.->|inherits|Review
    Recommendation -->|itemReviewed 0 ... n|Trail
    Recommendation -->|itemReviewed 0 ... n|Place
    Recommendation -->|itemReviewed 0 ... n|Product
    Recommendation -->|isRelatedTo 0 ... 1|Place
    Recommendation -->|isRelatedTo 0 ... 1|Product
    Recommendation -->|isRelatedTo 0 ... 1|Event
    Product -->|availableAtOrFrom 0 ... n|Place
    
    Offer -->|offeredBy|Organization
    Offer -->|offeredBy|Person
```