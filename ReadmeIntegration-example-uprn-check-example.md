
### Example URPN Check

[Return](./ReadmeIntegration.md)

```json
{
  "version": "2022-04-01",
  "identity": {
    "trustmarkId": "api-905d2912-95aa-47a2-8d0d-9c41b9515b52"
  },
  "clientRequestToken": "2bc18df-be32-4177-91a2-f2b0cc2dae9d",
  "request": {
    "assessmentReference": "A5918",
    "ownerTMLN": "1399225",
    "schemeId": "bba",
    "projectType": "ECO4",
    "yourProjectReference": "123_1666688069",
    "tenure": {
      "premisesTenure": "Owner Occupied",
      "residentName": "Test",
      "residentContactNumber": "07889043652",
      "residentAlternativeContactNumber": "07889043651",
      "ownerName": "Alessandro Zerillo",
      "ownerContactNumber": "07889043654",
      "ownerAlternativeContactNumber": "07889043653",
      "ownerEmail": "Alessandro@eco-surv.co.uk"
    },
    "propertyInformation": {
      "propertyType": "House",
      "propertyDetachment": "Semi-detached",
      "propertyAge": "1950-1966",
      "propertyConstruction": ["Conventional, not high-rise, not protected - cavity wall"],
      "propertyBedrooms": "2"
    },
    "fundingOrganisationName": "-",
    "fundingComment": "-",
   "assessmentDefects": [
      {
        "actualRepairCost": 0,
        "toBeAddressedInProject": true,
        "defectId": "string"
      }
    ],
    "projectDefects": [],
    "intendedOutcomes": {
      "reductionEnergyUse": true,
      "reductionInEnergyCosts": false,
      "reductionsInEmissions": false,
      "improvementsInInternalComfort": false,
      "improvementsOfIAQ": false,
      "eliminationDampCondensationMould": false,
      "reduceRiskOverheating": false,
      "improvementsInEnergyRating": false,
      "meetPerformanceStandard": false,
      "improvementsInUsefulnessSustainability": false,
      "protectBuildingAgainstDecay": false,
      "resistanceFloodAndWaterPenetration": false,
      "protectionArchitecturalHeritage": false,
      "integrationEEMSAndOtherImprovements": false,
      "improveManagementOfMoisture": true,
      "improveResilienceToClimateChange": true,
      "otherRelevantIssues": "string",
      "monitoringMethod": "string"
    },
    "improvementOptionEvaluations": [{
        "reference": "",
        "calculationMethodology": "iQ-Engine",
        "householdContribution": 0,
        "measuresEvaluated": [
          {
            "yourReference": "00001",
            "workTypeCode": "DW-143",
            "product": "Loft insulation where there is less than or equal to 100mm pre-existing insulation",
            "measureEligibilityStatus": "Eligible",
            "measureInstallationCost": 1000,
            "annualFuelCostSaving": 560,
            "lifetimeOfMeasure": 12,
            "potentialEnergyRating": 73,
            "repaymentYears": 560,
            "annualCO2Savings": 3206,
            "carbonCostEffectiveness": 4503,
            "sapSavings": 73,
            "productInstalledUnitOfMeasure": "m2",
            "productInstalledValue": 100
          },
          {
            "yourReference": "00002",
            "workTypeCode": "DW-103",
            "product": "Cavity Wall Insulation (0.033)",
            "measureEligibilityStatus": "Eligible",
            "measureInstallationCost": 2400,
            "annualFuelCostSaving": -548,
            "lifetimeOfMeasure": 42,
            "potentialEnergyRating": 79,
            "repaymentYears": -548,
            "annualCO2Savings": 1202,
            "carbonCostEffectiveness": 318,
            "sapSavings": 79,
            "productInstalledUnitOfMeasure": "m2",
            "productInstalledValue": 100
          }
        ],
        "intendedOutcomes": {
          "reductionEnergyUse": true,
          "reductionInEnergyCosts": false,
          "reductionsInEmissions": false,
          "improvementsInInternalComfort": false,
          "improvementsOfIAQ": false,
          "eliminationDampCondensationMould": false,
          "reduceRiskOverheating": false,
          "improvementsInEnergyRating": false,
          "meetPerformanceStandard": false,
          "improvementsInUsefulnessSustainability": false,
          "protectBuildingAgainstDecay": false,
          "resistanceFloodAndWaterPenetration": false,
          "protectionArchitecturalHeritage": false,
          "integrationEEMSAndOtherImprovements": false,
          "improveManagementOfMoisture": true,
          "improveResilienceToClimateChange": true,
          "otherRelevantIssues": "string",
          "monitoringMethod": "string"
        },
        "isMediumTermPlanBase": true
      }
    ],
    "mediumTermImprovementPlan": {
      "reference": "",
      "savingsMoney": 0,
      "savingsSAPPoints": 0,
      "stages": [{
          "sequence": 2,
          "dependentStages": [
            0
          ],
          "savingsMoney": 0,
          "savingsSAPPoints": 1,
          "stageDurationInWeeks": 0,
          "keyEventComments": "",
          "inScopeCurrentProject": true,
          "improvementOptionEvaluationMeasureReferences": ["Array"]
        }
      ]
    },
    "riskAssessment": {
      "declaredProjectRisk": "B",
      "highestRiskCombination": "B"
    },
    "retrofitDesigns": [
      {
        "isRegisteredWithTrustmark": true,
        "designerTMLN": "1399225",
        "designerName": "Rory Nixon",
        "designerQualification": "Stroma",
        "improvementOptionEvaluationMeasureReferences": ["Array"],
        "thermalBridgeTreatment": "Mitigation",
        "thermalBridgeRiskPresent": true,
        "defectResolutions": [],
        "ventilationTreatmentType": "Proportional Intervention",
        "ventilationTreatmentStrategy": "Specific Room",
        "ventilationStrategyNotes": "",
        "supportingDocumentAttachments": [
          {
            "fileUploadToken": "rac-22562bcf-f2ec-4966-a8a1-7838746f0a4ct20221024t6f261fcd3dd74af39334888fadeaeb85t133110932390301445",
            "filename": "Retrofit design.pdf",
            "documentType": "Retrofit design"
          }
        ]
      }
    ],
    "roles":{"installerTMLNs":["234223","234223","1231233"],"evaluatorTMLN":"1399225"},
    "supportingDocumentAttachments": []
  }
}
```

## Response
```json
{
  "message": "UPRN_EXISTS_FIRST_AND_THIRD"
}
```