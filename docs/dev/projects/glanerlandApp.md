# Glanerland App


## Schema

``` mermaid
graph TD
    Offer[Tagespass]-->|availableAtOrFrom 0 ... n|Place[POI/Ort]

    Recommendation[Ausflugstipps] -->|itemReviewed 0 ... n|Place[POI/Ort]
    Recommendation -->|isRelatedTo 0 ... 1|Offer
```