
### ECO4 Project PAS2035 [2023] Example

[Return](./ReadmeIntegration.md)

```json
{
  "version": "2022-04-01",
  "identity": {
    "trustmarkId": "[YOUR_API_KEY]"
  },
  "clientRequestToken" : "e9bc274f3-0486-40c1-a2f2-aa61d1cf5525",
  "request": {
    "assessmentReference": "A16063",
    "ownerTMLN": "10000",
    "schemeId": "testscheme",
    "fundingOrganisationName": "string",
    "fundingComment": "string",
    "projectType": "ECO4",
    "yourProjectReference": "example_api_eco4_2023",
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
      "improveManagementOfMoisture": true,
      "improveResilienceToClimateChange": true,
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
            "workTypeCode": "DW-479",
            "product": "string",
            "measureEligibilityStatus": "Eligible",
            "measureInstallationCost": 0,
            "annualFuelCostSaving": 0,
            "lifetimeOfMeasure": 0,
            "potentialEnergyRating": 0,
            "repaymentYears": 0,
            "annualCO2Savings": 0,
            "carbonCostEffectiveness": 0,
            "productInstalledUnitOfMeasure": "Items",
            "productInstalledValue": 1,
            "sapSavings": 1
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
          "improveManagementOfMoisture": true,
          "improveResilienceToClimateChange": true,
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
            "assessmentDefectId": "Vent001",
            "resolution": "string"
          },
          {
            "projectDefectYourReference": "PD01",
            "resolution": "string"
          }
        ],
        "ventilationTreatmentStrategy": "Specific Room",
        "ventilationStrategyNotes": "string"
      }
    ],
    "roles": {
      "installerTMLNs": [
        "string"
      ],
      "evaluatorTMLN": "string"
    },
    "supportingDocumentAttachments": [
      {
        "fileUploadToken": "00000000000000",
        "documentType": "Intended outcomes",
        "comments": "string",
        "filename": "Filename.pdf"
      },
      {
        "fileUploadToken": "00000000000000",
        "documentType": "Improvement option evaluation",
        "comments": "string",
        "filename": "Filename.pdf"
      },
      {
        "fileUploadToken": "00000000000000",
        "documentType": "Medium term improvement plan",
        "comments": "string",
        "filename": "Filename.pdf"
      },
      {
        "fileUploadToken": "00000000000000",
        "documentType": "Retrofit design",
        "comments": "string",
        "filename": "Filename.pdf"
      },
      {
        "fileUploadToken": "00000000000000",
        "documentType": "Pre-Installation Building Inspection",
        "comments": "string",
        "filename": "Filename.pdf"
      }
    ],
    "notes": [
      "string"
    ]
  }
}
```