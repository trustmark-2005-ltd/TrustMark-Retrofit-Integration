### Smart Meter Pledge Project Example

[Return](./ReadmeIntegration.md)

```json
{
  "version": "2022-04-01",
  "identity": {
    "trustmarkId": "api-e5b3e97b-b95e-467f-b082-60fcab47ec6d"
  },
  "clientRequestToken" : "2341716e-23fc-4d6f-b833-f945aa6f5a36",
  "request": {
    "assessmentReference": "A31457",
    "ownerTMLN": "10000",
    "schemeId": "testscheme",
    "fundingOrganisationName": "string",
    "fundingComment": "string",
    "projectType": "ECO4",
    "yourProjectReference": "aug7",
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
    "projectDefects": [
      {
        "yourReference": "DW-489",
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
        "toBeAddressedInProject": true,
        "evidenceImageUrl": [
          {
            "fileUploadToken": "rac-3ed904f7-853c-4975-8d07-afa5b58a5efft20250804t84a1a40b488f40b7b58528eac776a0e2t133987901253989518",
            "filename": "file.pdf"
          }
        ]
      }
    ],
    "intendedOutcomes": {
            "improveResilienceToClimateChange": false,
            "improveManagementOfMoisture": false,
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
            "workTypeCode": "DW-489",
            "product": "string",
            "measureEligibilityStatus": "Eligible",
            "measureInstallationCost": 100,
            "annualFuelCostSaving": 10,
            "lifetimeOfMeasure": 2,
            "potentialEnergyRating": 1,
            "repaymentYears": 2,
            "annualCO2Savings": 2,
            "carbonCostEffectiveness": 1,
                        "productInstalledUnitOfMeasure": "Items",
                        "ProductInstalledValue": 1
          }
        ],
        "intendedOutcomes": {
                    "improveResilienceToClimateChange": false,
                    "improveManagementOfMoisture": false,
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
        "ventilationTreatmentStrategy": "Specific Room",
        "ventilationStrategyNotes": "string"
      }
    ],
    "roles": {
      "installerTMLNs": [
        "10000"
      ],
      "evaluatorTMLN": "10000"
    },
    "supportingDocumentAttachments": [
      {
        "fileUploadToken": "rac-3ed904f7-853c-4975-8d07-afa5b58a5efft20250804t84a1a40b488f40b7b58528eac776a0e2t133987901253989518",
        "documentType": "Intended outcomes",
        "comments": "string",
        "filename": "file.pdf"
      },
                  {
        "fileUploadToken": "rac-3ed904f7-853c-4975-8d07-afa5b58a5efft20250804t84a1a40b488f40b7b58528eac776a0e2t133987901253989518",
        "documentType": "Medium term improvement plan",
        "comments": "string",
        "filename": "file.pdf"
      },
                  {
        "fileUploadToken": "rac-3ed904f7-853c-4975-8d07-afa5b58a5efft20250804t84a1a40b488f40b7b58528eac776a0e2t133987901253989518",
        "documentType": "Improvement option evaluation",
        "comments": "string",
        "filename": "file.pdf"
      },
             {
        "fileUploadToken": "rac-3ed904f7-853c-4975-8d07-afa5b58a5efft20250804t84a1a40b488f40b7b58528eac776a0e2t133987901253989518",
        "documentType": "Retrofit design",
        "comments": "string",
        "filename": "file.pdf"
      }
            
    ],
    "notes": [
      "string"
    ], 
    "highRiskQuestions": [
      {
        "question": "I confirm that I gave the Smart Meter Consumer Pledge to the household",
        "answer": "The consumer accepted the pledge"
      }
    ]
  }
}