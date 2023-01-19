
### LADS Project Example

[Return](./ReadmeIntegration.md)

```json
{
  "version": "2022-04-01",
  "identity": {
    "trustmarkId": "api-e5b3e97b-b95e-467f-b082-60fcab47ec6d"
  },
  "clientRequestToken" : "66b174f3-0486-40c1-a2f2-aa61d1cf5525",
  "request": {
    "assessmentReference": "A8037",
    "ownerTMLN": "10000",
    "schemeId": "testscheme",
    "fundingOrganisationName": "string",
    "fundingComment": "string",
    "projectType": "LADS",
    "yourProjectReference": "lads_api_1",
    "localAuthorityProjectPhase": "1b",
    "localAuthorityProjectKey": "P_187",
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
    "propertyInformation": {
      "propertyType": "House",
      "propertyDetachment": "Detached",
      "propertyAge": "B",
      "propertyConstruction": [
        "Conventional, not high-rise, not protected - cavity wall"
      ],
      "propertyBedrooms": "2"
    },
    "assessmentDefects": [
      {
        "actualRepairCost": 0,
        "toBeAddressedInProject": true,
        "defectId": "string"
      }
    ],
    "projectDefects": [
      {
        "yourReference": "PD01",
        "defectType": "Leaks",
        "comment": "string",
        "severity": "Low",
        "locations": [
          "Bedroom"
        ],
        "repairCost": 0,
        "resolutionBeforeRetrofit": "Can",
        "destructiveTestsConducted": "string",
        "hasEvidence": true,
        "actualRepairCost": 0,
        "toBeAddressedInProject": true
      }
    ],
    "intendedOutcomes": {
      "reductionEnergyUse": true,
      "reductionInEnergyCosts": true,
      "reductionsInEmissions": true,
      "improvementsInInternalComfort": true,
      "improvementsOfIAQ": true,
      "eliminationDampCondensationMould": true,
      "reduceRiskOverheating": true,
      "improvementsInEnergyRating": true,
      "meetPerformanceStandard": true,
      "improvementsInUsefulnessSustainability": true,
      "protectBuildingAgainstDecay": true,
      "resistanceFloodAndWaterPenetration": true,
      "protectionArchitecturalHeritage": true,
      "integrationEEMSAndOtherImprovements": true,
      "otherRelevantIssues": "string",
      "monitoringMethod": "string"
    },
    "improvementOptionEvaluations": [
      {
        "reference": "string",
        "calculationMethodology": "string",
        "householdContribution": 0,
        "measuresEvaluated": [
          {
            "yourReference": "ioem1",
            "workTypeCode": "DW-101",
            "product": "string",
            "measureEligibilityStatus": "Eligible",
            "measureInstallationCost": 0,
            "annualFuelCostSaving": 0,
            "lifetimeOfMeasure": 0,
            "potentialEnergyRating": 0,
            "repaymentYears": 0,
            "annualCO2Savings": 0,
            "carbonCostEffectiveness": 0,
            "sapSavings": 0,
            "productInstalledUnitOfMeasure": "Items",
            "productInstalledValue": 1
          }
        ],
        "intendedOutcomes": {
          "reductionEnergyUse": true,
          "reductionInEnergyCosts": true,
          "reductionsInEmissions": true,
          "improvementsInInternalComfort": true,
          "improvementsOfIAQ": true,
          "eliminationDampCondensationMould": true,
          "reduceRiskOverheating": true,
          "improvementsInEnergyRating": true,
          "meetPerformanceStandard": true,
          "improvementsInUsefulnessSustainability": true,
          "protectBuildingAgainstDecay": true,
          "resistanceFloodAndWaterPenetration": true,
          "protectionArchitecturalHeritage": true,
          "integrationEEMSAndOtherImprovements": true,
          "otherRelevantIssues": "string",
          "monitoringMethod": "string"
        },
        "isMediumTermPlanBase": true
      }
    ],
    "mediumTermImprovementPlan": {
      "reference": "string",
      "savingsMoney": 0,
      "savingsSAPPoints": 0,
      "stages": [
        {
          "sequence": 0,
          "dependentStages": [
            0
          ],
          "savingsMoney": 0,
          "savingsSAPPoints": 0,
          "stageDurationInWeeks": 0,
          "keyEventComments": "string",
          "inScopeCurrentProject": true,
          "improvementOptionEvaluationMeasureReferences": [
            "ioem1"
          ]
        }
      ]
    },
    "riskAssessment": {
      "declaredProjectRisk": "A",
      "highestRiskCombination": "Green"
    },
    "retrofitDesigns": [
      {
        "isRegisteredWithTrustmark": true,
        "designerTMLN": "10000",
        "designerName": "",
        "designerQualification": "Architect (ARB)",
        "improvementOptionEvaluationMeasureReferences": [
          "ioem1"
        ],
        "ventilationTreatmentType": "Proportional Intervention",
        "thermalBridgeActionDescription": "string",
        "thermalBridgeTreatment": "Mitigation",
        "thermalBridgeRiskPresent": true,
        "defectResolutions": [
          {
            "assessmentDefectId": "My Ref 1",
            "resolution": "string"
          }
        ],
        "ventilationTreatmentStrategy": "Specific Room",
        "ventilationStrategyNotes": "string"
      }
    ],
    "roles": {
      "installers": [
        {
          "tmln": "string",
          "registeredCompanyName": "string"
        }
      ],
      "evaluator": {
        "tmln": "string",
        "registeredCompanyName": "string"
      }
    },
    "supportingDocumentAttachments": [
      {
        "fileUploadToken": "rac-0c815e54-429d-40d8-98b5-37f8c7913181t20220426t9959c6afec404be5b28ff57544acb6a2t132954467702961840",
        "documentType": "Risk assessment",
        "comments": "string",
        "filename": "TestRA.pdf"
      },
      {
        "fileUploadToken": "rac-0c815e54-429d-40d8-98b5-37f8c7913181t20220426t9959c6afec404be5b28ff57544acb6a2t132954467702961840",
        "documentType": "Intended outcomes",
        "comments": "string",
        "filename": "TestRA.pdf"
      },
      {
        "fileUploadToken": "rac-0c815e54-429d-40d8-98b5-37f8c7913181t20220426t9959c6afec404be5b28ff57544acb6a2t132954467702961840",
        "documentType": "Improvement option evaluation",
        "comments": "string",
        "filename": "TestRA.pdf"
      },
      {
        "fileUploadToken": "rac-0c815e54-429d-40d8-98b5-37f8c7913181t20220426t9959c6afec404be5b28ff57544acb6a2t132954467702961840",
        "documentType": "Medium term improvement plan",
        "comments": "string",
        "filename": "TestRA.pdf"
      },
      {
        "fileUploadToken": "rac-0c815e54-429d-40d8-98b5-37f8c7913181t20220426t9959c6afec404be5b28ff57544acb6a2t132954467702961840",
        "documentType": "Retrofit design",
        "comments": "string",
        "filename": "TestRA.pdf"
      },
      {
        "fileUploadToken": "rac-0c815e54-429d-40d8-98b5-37f8c7913181t20220426t9959c6afec404be5b28ff57544acb6a2t132954467702961840",
        "documentType": "Pre-Design Building Survey",
        "comments": "string",
        "filename": "TestRA.pdf"
      }
    ],
    "notes": [
      "string"
    ]
  }
}
```