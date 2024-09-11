# Glanerland App


## Schema

``` mermaid
graph TD
    Offer[Tagespass]-->|erhältlich bei oder von (availableAtOrFrom 0 ... n)|Place[POI/Ort]

    Recommendation[Ausflugstipps] -->|empfohlene Orte (itemReviewed 0 ... n)|Place[POI/Ort]
    Recommendation -->|ist verbunden mit (isRelatedTo 0 ... 1)|Offer
```

### Properties

* availableAtOrFrom
* itemReviewed
* isRelatedTo
* channel
* avs_acceptance_point_id