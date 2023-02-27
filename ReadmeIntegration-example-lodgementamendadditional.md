
### LodgementAmend Add New Measure Example

[Return](./ReadmeIntegration.md)

```json
{
  "version": "2022-04-01",
  "identity": {
    "trustmarkId": "api-e5b3e97b-b95e-467f-b082-60fcab47ec6d"
  },
  "clientRequestToken" : "e1003e76-fd68-4dd5-ba88-26bd14cda0b4",
  "request": {
    "projectReference": "P1054",
    "lodgementId": "lod-0a506734-32a9-44de-98f2-44c93e607dba",
    "measures": [
      {
        "measureId": "1234-1234-1234-1234",
        "umr": "TBC",
        "workTypeCode": "DW-101",
        "freeTextDetails": "string",
        "installedDate": "2022-04-25",
        "handoverDate": "2022-04-28",
        "workCarriedOutByTMLN": "2337207",
        "workCarriedOutBySchemeId": "trustmark_logo"
      }
    ]
  }
}
```