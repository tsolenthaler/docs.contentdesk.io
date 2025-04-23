# FAQ

## Schema.org

### Types

* [https://schema.org/FAQPage]
* [https://schema.org/QAPage]
* [https://schema.org/Question]
* [https://schema.org/Answer]

## Links
[https://developers.google.com/search/docs/appearance/structured-data/qapage?hl=de]

[https://honeynjam.com/tools/schema-markup-generators/qapage]

## Konzept
``` mermaid
graph TD
    FAQPage -->|mainEntity| Question1
    FAQPage -->|mainEntity| Question2
    FAQPage -->|mainEntity| Question3
    Question1 --> |acceptedAnswer| Answer1
    Question2 --> |acceptedAnswer| Answer3
    Question3 --> |acceptedAnswer| Answer5
```


## Examples 
``` JSON
{
  "@context": "https://schema.org",
  "@type": "QAPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Was ist Schema.org?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Schema.org ist eine gemeinsame Vokabularsammlung, die von Suchmaschinen verwendet wird, um strukturierte Daten auf Webseiten zu kennzeichnen."
      }
    },
    {
      "@type": "Question",
      "name": "Wie verwende ich JSON-LD?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "JSON-LD kann in den <script> Tags im <head> oder <body> Ihrer HTML-Seite eingebettet werden, um strukturierte Daten bereitzustellen."
      }
    },
    {
      "@type": "Question",
      "name": "Was sind die Vorteile von strukturierten Daten?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Strukturierte Daten helfen Suchmaschinen, den Inhalt Ihrer Seite besser zu verstehen, was zu einer besseren Sichtbarkeit in den Suchergebnissen führen kann."
      }
    }
  ]
}
```

### Question

```
    <script type="application/ld+json">
    {
        "@context": "https://schema.org",
        "@type": "Question",
        "name": "What is attr_accessor in Ruby?",
        "upvoteCount": "196",
        "text": "I am having difficulty understanding Ruby attr_accessors, can someone explain them?",
        "dateCreated": "2010-11-04T20:07Z",
        "author": {
            "@type": "Person",
            "name": "someuser"
        },
        "answerCount": "4",
        "acceptedAnswer": {
            "@type": "Answer",
            "upvoteCount": "1337",
            "text": "(The text of the accepted answer goes here...).",
            "dateCreated": "2010-12-01T22:01Z",
            "author": {
                "@type": "Person",
                "name": "someuser"
            }
        },
        "suggestedAnswer": {
            "@type": "Answer",
            "upvoteCount": "39",
            "text": "(The text of the accepted answer goes here...).",
            "dateCreated": "2010-12-06T21:11Z",
            "author": {
                "@type": "Person",
                "name": "lonelyuser1234"
            }
        }
    }
    </script>
```