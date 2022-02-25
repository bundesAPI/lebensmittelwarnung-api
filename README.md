# Lebensmittelwarnung API

Das Bayerische Staatsministerium für Umwelt und Verbraucherschutz ermöglicht über die hier dokumentierte API die Information von Verbraucher\*innen zu Lebensmittel- und Produktwarnungen.


## Anfragen

**URL:** https://megov.bayern.de/verbraucherschutz/baystmuv-verbraucherinfo/rest/api/warnings/merged

Anfragen sind als POST-request zu formulieren. Dabei ist folgendes zu beachten:
- "Authorization" muss als header, query parameter oder cookie mit folgendem Inhalt gesendet werden: "baystmuv-vi-1.0 os=ios, key=9d9e8972-ff15-4943-8fea-117b5a973c61"; 
- als ASCII-data ist ein JSON-Objekt mit den Elementen "food" (ein Objekt mit den Eigenschaften "rows", "sort", "start" und "fq") und "products" (ebenfalls ein Objekt mit den Eigenschaften "rows", "sort", "start" und "fq") zu senden.


**Eigenschaft:** *rows* 

Anzahl zu ladender Einträge (z.B. 500).


**Eigenschaft:** *sort* 

Vorgaben zur Sortierung zu ladender Einträge (z.B. publishedDate desc, title asc)


**Eigenschaft:** *start* 

Start-Index der zu ladenden Einträge (z.B. 11).


**Eigenschaft:** *fq* 

Array zur Eingrenzung zu ladender Einträge (z.B. ["publishedDate > 1630067654000"]).


### Beispiel:

```bash
warnings=$(curl -X 'POST' \
  'https://megov.bayern.de/verbraucherschutz/baystmuv-verbraucherinfo/rest/api/warnings/merged' \
  -H 'accept: application/json' \
  -H 'Authorization: baystmuv-vi-1.0 os=ios, key=9d9e8972-ff15-4943-8fea-117b5a973c61' \
  -H 'Content-Type: application/json' \
  -d '{
  "food": {
    "rows": 500,
    "sort": "publishedDate desc, title asc",
    "start": 11,
    "fq": [
      "publishedDate > 1630067654000"
    ]
  },
  "products": {
    "rows": 500,
    "sort": "publishedDate desc, title asc",
    "start": 11,
    "fq": [
      "publishedDate > 1630067654000"
    ]
  }
}')
```
