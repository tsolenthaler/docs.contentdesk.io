# Outdooractive


## Types

Typen die von contentdesk.io zu Outdooractive übertragen werden:

| contentdesk.io        | outdooractive             |
| -------------         | -------------             | 
| [Place] - POI ✅      | [poi]                    |
| [Trail]  ❌           | [route]                    | 
| [Event]  ❌           | [event]                    | 
| [Offer]  ❌           | [offer]                    |


## Attribute & Verknüpfungen

Attribute und Verknüpfungen (Association Type) welche zu Outdooractive übertragen werden:

| contentdesk.io                         | outdooractive                        | Bemerkung                         |
| -------------                          | -------------                        | -------------                     | 
| [enabled] ✅                          | [workflow]                            | Status aktive/deaktiviert         |
| [updated] ✅                          | [lastmodified]                        | Letzte aktualisierung             |
| [name] ✅                             | [descriptions][title]                 |                                   |
| [description]  ✅                     | [descriptions][descriptions]          | Beschreibung Mehrsprachig         | 
| [disambiguatingDescription]  ✅       | [descriptions][descriptions]          | Kurzbeschreibung Mehrsprachig     |
| [latitude]  ✅                        | [point]                               | 
| [longitude]  ✅                       | [point]                               |
| [streetAddress]  ✅                   | [contact][address][street]            | 
| [addressLocality]  ✅                 | [contact][address][municipality]      |
| [postalCode]  ✅                      | [contact][address][postalcode]        |
| [telephone]  ✅                       | [contact][tel]                        |
| [email]  ✅                           | [contact][email]                      |
| [url]  ✅                             | [contact][url]                        |
| [starRating]  ✅                      | [attributes][hotelstars]              |
| [image]  ✅                           | [images][image]                       | Hauptbild | 
| [image_01_scope]  ✅                  | [images][image]                       | Galerie-Bild 01-10 | 
| [action_button] ❗                    | [attributes][context][link]           | Call-To-Acton (alte Version) |
| [openingHours] ❌                     |                                       | Öffnungszeiten Text | 
| [OpeningHoursSpecification] ❌        |                                       | Öffnungszeiten (maschinenlesbar) | 