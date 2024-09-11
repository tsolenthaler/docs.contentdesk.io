# Glanerland App


## Schema

``` mermaid
graph TD
    Product[Tagespass / Produkt]-->|erhältlich bei oder von|Place[POI/Ort / Place]

    Recommendation[Ausflugstipps / Empfehlung] -->|empfohlene Orte|Place
    Recommendation -->|ist verbunden mit|Product
```

### Types

* Place
* Produkt / Offer
* Recommendation

### Properties

* availableAtOrFrom 0..n - erhältlich bei oder von
* itemReviewed 0..n - empfohlene Orte
* isRelatedTo 0...1 - ist verbunden mit 
* channel
* avs_acceptance_point_id