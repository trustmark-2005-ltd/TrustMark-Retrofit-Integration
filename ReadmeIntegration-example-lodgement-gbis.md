
### Lodgement Example

[Return](./ReadmeIntegration.md)

```json
{
  "version": "2022-04-01",
  "identity": {
    "trustmarkId": "api-70232d27-eccc-488e-9501-624296e91f1e"
  },
  "clientRequestToken" : "a4003e76-fd82-a3d5-ba88-26ad1e3da0b4",
  "request": {
    "projectReference": "P6579",
    "ownerTMLN": "10000",
    "planStageSequence": 0,
    "measures": [
      {
        "improvementOptionEvaluationMeasureReference": "ioem1",
        "workTypeCode": "DW-101",
        "freeTextDetails": "string",
        "percentageMeasureInstalled": "Yes",
        "installerReferenceNumber": "string",
        "installedDate": "2022-04-16",
        "handoverDate": "2023-04-18",
        "workCarriedOutByTMLN": "2337207",
        "workCarriedOutBySchemeId": "trustmark_logo",
        "installerPasCertificateNumber": "string",
        "operativeName": "string",
        "productManufacturer": "string",
        "productModel": "string",
        "productVersion": "string",
        "productSerialNumber": "string",
        "productWarrantyDuration": "string",
        "financialProtectionCategory": "CWI-01",
        "guaranteeName": "Qualitymark Protection / GDGC - Insurance Backed Guarantee (IBG)",
        "guaranteeStartDate": "2022-04-27",
        "guaranteeTerm": "string",
        "guaranteePolicyReference": "string",
        "measureCost": 800
      }
    ],
    "workInvoiceTotal": 800,
    "customerContribution": 100,
    "supportingDocumentAttachments": [
      {
        "fileUploadToken": "rac-0c815e54-429d-40d8-98b5-37f8c7913181t20220426t9959c6afec404be5b28ff57544acb6a2t132954467702961840",
        "documentType": "Claim of compliance PAS2030",
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
      },
      {
        "fileUploadToken": "rac-0c815e54-429d-40d8-98b5-37f8c7913181t20220426t9959c6afec404be5b28ff57544acb6a2t132954467702961840",
        "documentType": "Pre-Installation Building Inspection",
        "comments": "string",
        "filename": "TestRA.pdf"
      }
    ]
  }
}
```