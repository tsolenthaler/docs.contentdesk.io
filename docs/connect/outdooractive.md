# Outdooractive

## Zyklus

Um 12 Uhr und ca. ab 19 Uhr werden die Daten übertragen.

## Types

Typen die von contentdesk.io zu Outdooractive übertragen werden:

| contentdesk.io        | outdooractive             |
| -------------         | -------------             | 
| [Place] - POI ✅      | [poi]                    |
| [Trail]  ❌           | [route]                  | 
| [Event]  ❌           | [event]                  | 
| [Offer]  ❌           | [offer]                  |


## Attribute & Verknüpfungen

Attribute und Verknüpfungen (Association Type) welche zu Outdooractive übertragen werden:

| contentdesk.io                         | outdooractive                        | Bemerkung                                 |
| -------------                          | -------------                        | -------------                             | 
| [enabled] ✅                          | [workflow]                            | Status aktive/deaktiviert                 |
| [updated] ✅                          | [lastmodified]                        | Letzte aktualisierung                     |
| [name] ✅                             | [descriptions][title]                 |                                           |
| [description]  ✅                     | [descriptions][descriptions]          | Beschreibung Mehrsprachig                 | 
| [disambiguatingDescription]  ✅       | [descriptions][descriptions]          | Kurzbeschreibung Mehrsprachig             |
| [latitude]  ✅                        | [point]                               | Koordinaten                               |
| [longitude]  ✅                       | [point]                               | Koordinaten                               |
| [streetAddress]  ✅                   | [contact][address][street]            | Strasse                                   |
| [addressLocality]  ✅                 | [contact][address][municipality]      | Ort                                       |
| [postalCode]  ✅                      | [contact][address][postalcode]        | PLZ                                       |
| [telephone]  ✅                       | [contact][tel]                        | Telefon                                   |
| [email]  ✅                           | [contact][email]                      | E-Mail                                    |
| [url]  ✅                             | [contact][url]                        | Webseite                                  |
| [starRating]  ✅                      | [attributes][hotelstars]              | Sterneklassifikation bei Unterkünften     |
| [image]  ✅                           | [images][image]                       | Hauptbild                                 | 
| [image_01_scope]  ✅                  | [images][image]                       | Galerie-Bild 01-10                        | 
| [action_button] ❗                    | [attributes][context][link]           | Call-To-Acton (alte Version)              |
| [openingHours] ❌                     |                                       | Öffnungszeiten Text                       | 
| [OpeningHoursSpecification] ❌        |                                       | Öffnungszeiten (maschinenlesbar)          | 