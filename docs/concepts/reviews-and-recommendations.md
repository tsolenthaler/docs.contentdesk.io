---
tags:
  - concept
hide:
  - navigation
  #- toc
---

# Reviews and recommendations / Empfehlungen

[Dokumentation bei discover.swiss](https://docs.discover.swiss/dev/concepts/reviews-and-recommendations/)


## Schema

``` mermaid
graph TD
    subgraph Products
        direction TB
        Product -->|offers|Offer
    end
    CreativeWork <-.->|inherits|Recommendation
    CreativeWork -->|author|Person
    CreativeWork -->|author|Organization
    Recommendation(Review 
    Recommendation) -->|itemReviewed 0 ... n|Trail
    Recommendation -->|itemReviewed 0 ... n|Place
    Recommendation -->|itemReviewed 0 ... n|Product
    Recommendation -->|isRelatedTo 0 ... 1|Place
    Recommendation -->|isRelatedTo 0 ... 1|Product
    Recommendation -->|isRelatedTo 0 ... 1|Event
    Product -->|availableAtOrFrom 0 ... n|Place

    Offer -->|offeredBy|Organization
    Offer -->|offeredBy|Person
```