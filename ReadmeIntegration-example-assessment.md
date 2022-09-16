
### Assessment Example

[Return](./ReadmeIntegration.md)

```json
{
  "version": "2022-04-01",
  "identity": {
    "trustmarkId": "api-e5b3e97b-b95e-467f-b082-60fcab47ec6d"
  },
  "clientRequestToken" : "4bbccfa6-00a3-448a-a627-84100c20d516",
  "request": {
    "ownerTMLN": "10000",
    "rdSAPFileContent": "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\r\n<RdSAP-Report xmlns ..... <\/RdSAP-Report>",
    "assessorTMLN": "10000",
    "defects": [
      {
        "defectType": "Leaks",
        "comment": "string",
        "severity": "Medium",
        "locations": [
          "Bathroom"
        ],
        "repairCost": 0,
        "resolutionBeforeRetrofit": "Can",
        "destructiveTestsConducted": "string",
        "hasEvidence": true,
        "evidenceImageFileUploadTokens": [
          "string"
        ],
        "yourReference": "ABC"
      }
    ],
    "occupancy": {
      "typicalOccupancy": true,
      "occupancyNotes": "string",
      "numberOccupants": 0,
      "specialConsiderationsApplicable": true
    },
    "ventilation": {
      "existingVentilationProvided": "Yes - Adequate",
      "ventilationType": "Passive Stack Ventillation (PSV)",
      "ventilationNotes": "string",
      "preRetrofitPulseAirTightnessTestRating": 0,
      "preRetrofitBlowerDoorAirTightnessTestRating": 0,
      "suitableBackgroundVentilationPresent": true
    },
    "significance": {
      "appraisalOfHeritage": "string"
    },
    "context": {
        "combustionVentilationAcceptable": "Yes - Adequate",
        "exposureZone": "Moderate",
        "propertyConstruction": [ "Conventional, not high-rise, not protected - cavity wall" ],
        "propertyDetachment": "Detached",

        "planningConstraints": true,
        "planningComments": "string"
    },
    "supportingDocumentAttachments": [
      {
        "fileUploadToken": "rac-0c815e54-429d-40d8-98b5-37f8c7913181t20220426t9959c6afec404be5b28ff57544acb6a2t132954467702961840",
        "documentType": "Assessment report",
        "comments": "string",
        "filename": "TestRA.pdf"
      },
      {
        "fileUploadToken": "rac-0c815e54-429d-40d8-98b5-37f8c7913181t20220426t9959c6afec404be5b28ff57544acb6a2t132954467702961840",
        "documentType": "Advice report",
        "comments": "string",
        "filename": "TestRA.pdf"
      }
    ]
  }
}
```
