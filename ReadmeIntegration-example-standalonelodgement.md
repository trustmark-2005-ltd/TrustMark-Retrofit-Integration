
### Standalone Lodgement Example

[Return](./ReadmeIntegration.md)

```json
{
  "version": "2022-04-01",
  "identity": {
    "trustmarkId": "api-e5b3e97b-b95e-467f-b082-60fcab47ec6d"
  },
  "clientRequestToken" : "e1003e76-fd68-4dd5-ba88-26bd14cda0b4",
  "request": {
    "yourProjectReference": "YourReference",
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
    "paymentReference": "string",
    "trustmarkBusinessId": "string",
    "schemeBusinessId": "string",
    "thirdPartyName": "string",
    "lodgementType": "LICENCEPLUS",
    "ownerRetrofitAccountId": "string",
    "ownerTMLN": "10000",
    "ownerName": "string",
    "workInvoiceTotal": 0,
    "schemeId": "string",
    "schemeName": "string",
    "startingRatingEPC": "D",
    "startingRRNEPC": "0000-0000-0000-0000-0000",
    "completionRatingEPC": "C",
    "completionRRNEPC": "0000-0000-0000-0000-0000",
    "authenticationNumber": "string",
    "confidenceLevel": 0,
    "measures": [
      {
        "improvementOptionEvaluationMeasureReference": "ioem1",
        "workTypeCode": "DW-101",
        "freeTextDetails": "string",
        "percentageMeasureInstalled": "Yes",
        "installerReferenceNumber": "string",
        "installedDate": "2022-04-27",
        "handoverDate": "2022-04-27",
        "workCarriedOutByTMLN": "2337207",
        "workCarriedOutBySchemeId": "trustmark_logo",
        "installerPasCertificateNumber": "string",
        "operativeName": "string",
        "isInnovationMeasure": true,
        "innovationMeasureProduct": "ARP CWI (BBA certificate 89/2294, product sheet 2)",
        "productManufacturer": "string",
        "productModel": "string",
        "productVersion": "string",
        "productSerialNumber": "string",
        "productWarrantyDuration": "string",
        "financialProtectionCategory": "CWI-01",
        "guaranteeName": "CIGA 25 Year Guarantee",
        "guaranteeStartDate": "2022-04-27",
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
      }
    ]
  }
}
```