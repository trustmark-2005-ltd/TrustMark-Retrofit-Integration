
### Standalone WHD Lodgement Example

[Return](./ReadmeIntegration.md)

```json
{
  "version": "2022-04-01",
  "identity": {
    "trustmarkId": "api-e5b3e97b-b95e-467f-b082-60fcab47ec6d"
  },
  "clientRequestToken" : "e1003e76-fd68-4dd5-ba88-26bd14cda0b4",
  "request": {
    "lodgementType": "WHD",
    "ownerTMLN": "10000",
    "schemeId": "testscheme",
    "yourProjectReference": "whd_api_3",
    "highRiskQuestions": [
      {
        "question": "High rise (more than 12M or 4 storeys?",
        "answer": "No"
      },
      {
        "question": "Park home?",
        "answer": "No"
      },
      {
        "question": "In both a protected area and of traditional construction?",
        "answer": "No"
      },
      {
        "question": "Are you fitting a new or replacing a Central Heating system?",
        "answer": "No"
      }
    ],
    "address": {
      "number": "string",
      "name": "string",
      "flatNameNumber": "string",
      "postcode": "string",
      "uprn": "string",
      "address1": "string",
      "address2": "string",
      "address3": "string",
      "city": "string",
      "county": "string",
      "country": "string",
      "town": "string"
    },
    "propertyInformation": {
      "propertyType": "House",
      "propertyDetachment": "Detached",
      "propertyAge": "B",
      "propertyConstruction": [
        "Conventional, not high-rise, not protected - cavity wall"
      ],
      "propertyBedrooms": "2"
    },
    "tenure": {
      "premisesTenure": "Owner Occupied",
      "residentName": "string",
      "residentContactNumber": "string",
      "residentAlternativeContactNumber": "string",
      "ownerName": "string",
      "ownerContactNumber": "string",
      "ownerAlternativeContactNumber": "string",
      "ownerEmail": "string"
    },
    "workInvoiceTotal": 0,
    "startingRatingEPC": "D",
    "startingRRNEPC": "0000-0000-0000-0000-0000",
    "completionRatingEPC": "C",
    "completionRRNEPC": "0000-0000-0000-0000-0000",
    "authenticationNumber": "string",
    "confidenceLevel": 0,
    "measures": [
      {
        "whdReplaceWhatMeasure": "Gas boiler",
        "whdWorkConducted": "Repair",
        "workTypeCode": "DW-385",
        "freeTextDetails": "string",
        "percentageMeasureInstalled": "Yes",
        "installerReferenceNumber": "string",
        "installedDate": "2023-01-20",
        "handoverDate": "2023-01-20",
        "workCarriedOutByTMLN": "2337207",
        "workCarriedOutBySchemeId": "trustmark_logo",
        "installerPasCertificateNumber": "string",
        "operativeName": "string",
        "productManufacturer": "string",
        "productModel": "string",
        "productVersion": "string",
        "productSerialNumber": "string",
        "productWarrantyDuration": "string",
        "financialProtectionCategory": "RMI-01",
        "guaranteeName": "TrustMark Framework Section 10 Compliant",
        "guaranteeStartDate": "2023-01-20",
        "guaranteeTerm": "string",
        "guaranteePolicyReference": "string"
      }
    ],
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
      },
      {
        "fileUploadToken": "rac-0c815e54-429d-40d8-98b5-37f8c7913181t20220426t9959c6afec404be5b28ff57544acb6a2t132954467702961840",
        "documentType": "Evidence of submission to CPS",
        "comments": "string",
        "filename": "TestRA.pdf"
      },
      {
        "fileUploadToken": "rac-0c815e54-429d-40d8-98b5-37f8c7913181t20220426t9959c6afec404be5b28ff57544acb6a2t132954467702961840",
        "documentType": "Handover documents for client",
        "comments": "string",
        "filename": "TestRA.pdf"
      },
      {
        "fileUploadToken": "rac-0c815e54-429d-40d8-98b5-37f8c7913181t20220426t9959c6afec404be5b28ff57544acb6a2t132954467702961840",
        "documentType": "Claim of compliance PAS2035",
        "comments": "string",
        "filename": "TestRA.pdf"
      },
      {
        "fileUploadToken": "rac-0c815e54-429d-40d8-98b5-37f8c7913181t20220426t9959c6afec404be5b28ff57544acb6a2t132954467702961840",
        "documentType": "Insurance guarantee",
        "comments": "string",
        "filename": "TestRA.pdf"
      }
    ]
  }
}
```