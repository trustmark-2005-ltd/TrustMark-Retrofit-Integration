
### Assessment PAS2035 [2023] Example

[Return](./ReadmeIntegration.md)

```json
{
  "version": "2022-04-01",
  "identity": {
    "trustmarkId": "[YOUR_API_KEY]"
  },
  "clientRequestToken": "e4cdcb2515-fd19-4dd2-b014-f807ae36b49d",
  "request": {
    "pasVersion": "PAS2035 [2023]",
    "ownerTMLN": "10000",
    "rdSAPFileContent": "<?xml version=\"1.0\" encoding=\"UTF-8\"?><RdSAP-Report xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://www.epcregister.com/xsd/rdsap\" xsi:schemaLocation=\"http://www.epcregister.com/xsd/rdsap http://www.epcregister.com/xsd/RdSAP/Templates/RdSAP-Report.xsd\"> ... </RdSAP-Report>",
    "assessorTMLN": "10000",
    "assessorSchemeId": "testscheme",
    "defects": [
      {
        "defectType": "Ventilation Defect",
        "yourReference": "Vent001",
        "comment": "Test mandatory defect"
      }
    ],
    "occupancy": {
      "typicalOccupancy": true,
      "occupancyNotes": null,
      "numberOccupants": 4,
      "specialConsiderationsApplicable": false
    },
    "ventilation": {
      "existingVentilationProvided": "Yes - Inadequate",
      "ventilationType": "Continuous Mechanical Extract Ventilation (CMEV)",
      "ventilationNotes": null,
      "preRetrofitPulseAirTightnessTestRating": 0,
      "preRetrofitBlowerDoorAirTightnessTestRating": 0,
      "suitableBackgroundVentilationPresent": false
    },
    "significance": {
      "areaSignificanceIdentified": true
    },
    "context": {
      "buildingOrientation": 0,
      "statutoryLimitationsComment": null,
      "statutoryLimitations": [],
      "siteAccessNotes": null,
      "propertyDetachment": "Mid-terrace",
      "propertyConstruction": [
        "Traditional, not protected - solid wall"
      ],
      "floorAreaM2": 0,
      "buildingServicesHeating": null,
      "buildingServicesHeatingControls": null,
      "buildingServicesHotWater": null,
      "buildingServicesVentilation": null,
      "buildingServicesElectricity": null,
      "buildingServicesGas": null,
      "planningComments": null,
      "planningConstraints": false,
      "exposureZone": "Moderate",
      "combustionVentilationAcceptable": "Yes - Adequate"
    },
    "supportingDocumentAttachments": [
      {
        "fileUploadToken": "00000000000000",
        "documentType": "Full Property Assessment",
        "comments": "string",
        "filename": "Filename.pdf"
      },
      {
        "fileUploadToken": "00000000000000",
        "documentType": "Significance survey",
        "comments": "string",
        "filename": "Filename.pdf"
      },
      {
        "fileUploadToken": "00000000000000",
        "documentType": "Condition report",
        "comments": "string",
        "filename": "Filename.pdf"
      },
      {
        "fileUploadToken": "00000000000000",
        "documentType": "Occupancy assessment",
        "comments": "string",
        "filename": "Filename.pdf"
      },
      {
        "fileUploadToken": "00000000000000",
        "documentType": "Ventilation Assessment Checklist",
        "comments": "string",
        "filename": "Filename.pdf"
      },
      {
        "fileUploadToken": "00000000000000",
        "documentType": "Ventilation Assessment",
        "comments": "string",
        "filename": "Filename.pdf"
      },
      {
        "fileUploadToken": "00000000000000",
        "documentType": "Heritage Impact Assessment",
        "comments": "string",
        "filename": "Filename.pdf"
      }
    ],
    "isPublic": false
  }
}
```