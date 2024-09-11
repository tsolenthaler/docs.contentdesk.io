# Glanerland App


## Schema

``` mermaid
graph TD
    Offer[Tagespass]-->|erhältlich bei oder von|Place[POI/Ort]

    Recommendation[Ausflugstipps] -->|empfohlene Orte|Place[POI/Ort]
    Recommendation -->|ist verbunden mit|Offer
```

### Properties

* availableAtOrFrom 0..n - erhältlich bei oder von
* itemReviewed 0..n - empfohlene Orte
* isRelatedTo 0...1 - ist verbunden mit 
* channel
* avs_acceptance_point_id