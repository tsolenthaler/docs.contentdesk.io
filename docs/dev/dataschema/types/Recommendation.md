# Recommendation

https://schema.org/Recommendation

https://docs.discover.swiss/dev/concepts/reviews-and-recommendations/


## Concepts

``` mermaid
graph LR
  A[Start] --> B{Error?};
  B -->|Yes| C[Hmm...];
  C --> D[Debug];
  D --> B;
  B ---->|No| E[Yay!];
```