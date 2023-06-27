# TrustMark Retrofit Integration

First Published April 22

> Supporting [Sandbox Swagger](https://api.sandbox.retrofitintegration.data-hub.org.uk/swagger/index.html)

## Introduction

The TrustMark Retrofit.IntegrationApi (RIAPI) allows users to integrate with the new TrustMark Retrofit platform which has been developed in time for ECO4 launch (July 2022).

### Overview
* A Retrofit Project will be created.
* A Retrofit project will require a Retrofit Assessment.
* It will be possible for a Retrofit Assessor to lodge an Assessment or for the Retrofit Coordinator to create it if appropriate.
* Retrofit Assessments will be accompanied with RdSAP xml data.
* Before a Project id can be generated, certain requirements must be met.
* Defects in the property can be recorded at both Assessment and mid Project.
* Designs must indicate who created them, which measures they cover and which property defects are addressed.
* A Project can be completed and lodged in stages.
* Each lodged stage can contain one or more measure.
* To complete a project an updated RdSAP xml must be provided.

Additional supporting documentation such as the Data Dictionary and Structured Data Model will be published at https://www.trustmark.org.uk/data-warehouse
ECO 4 specific information can be found at: https://www.trustmark.org.uk/tradespeople/eco4

### Principles

TrustMark will provide access to a ‘Sandbox’ environment for development and integration testing. Before access to the live environment can be provided you must successfully complete projects into the Sandbox environment that represent a number of core scenarios.

Once TrustMark has validated the test projects a Data Sharing Agreement will be issued and must be signed before the live keys are issued.


### Service Fees

Payable by the party signing the Data Sharing Agreement.

| Service                  | Fee (+VAT)               | Notes                                                            |
| ------------------------ | ------------------------ | ---------------------------------------------------------------- |
| Setup                    | £1500                    |                                                                  |
| Annual Service Charge    | £1500                    |  Annual increase capped at RPI +3%                               |
| Price per activity       | 1.5% of transaction cost |  Calculated monthly based upon lodgement fees payable to TrustMark by the lodging party |


## Key Concepts

### Data

The RIAPI focuses on allowing Assessment, Project and Lodgement data to be submitted at key stages. Sequence numbers (5) and (6) are optional.


| Sequence | Area       | Name     | Description                                                                                | Endpoint         |
| -------- | ---------- | -------- | ------------------------------------------------------------------------------------------ | ---------------- |
| 1        | Assessment | [Submit](#assessmentsubmit)   | Creates a new Retrofit Assessment, generating an AssessmentReference. If you are not a Retrofit Assessor or are using an existing Retrofit Assessment you will need to see [Assessment](#assessment)                       | AssessmentSubmit |
| 2        | Project    | [Start](#projectstart)    | Creates a new Retrofit Project using an AssessmentReference, generating a ProjectReference | ProjectStart     |
| 3        | Lodgement  | [Submit](#lodgementsubmit)   | Create a new Lodgment using a ProjectReference. A lodgement contains one or more measures.                                             | LodgementSubmit  |
| 4        | Project    | [Complete](#projectcomplete) | Completes the existing Project using a ProjectReference                                    | ProjectComplete  |
| (5)      | Project    | [Void](#projectvoid) | Voids an inprogress or draft project using a ProjectReference                                  | ProjectVoid  |
| (6)      | Lodgement  | [Amend](#lodgementamend) | Amends measures in a completed lodgement                              | LodgementAmend  |
| (7)      | Project  | [Amend](#projectamend) | Amends a project final RdSAP file                              | ProjectAmend  |

File uploads can be preloaded and attached during submission of the Assessment, Project, Lodgement and also as a standalone Supporting Document attaching to an existing Project. See [FileUploadToken](#fileuploadtoken)

Lodged Measures can be amended when needed using the [LodgementAmend](#lodgementamend)

### UPRN Check

Before a Project can be Started or Completed checks will be made against the processing project's UPRN. Any existing data within the TrustMark Retrofit Portal held against that UPRN under the same scope of funding will be checked, if any data exists the request will be initially rejected with a 422 response code and a message code. This allows the integrating software provider to notify their user before fully completing their action.

The following message codes exist:
| Code | Description |
| ---- | ----------- |
| UPRN_EXISTS_FIRST | You have created another {{project_type}} project at this property. Ensure that you can meet the eligibility criteria before proceeding. |
| UPRN_EXISTS_THIRD | Another {{project_type}} project exists at this property. Ensure that you can meet the eligibility criteria before proceeding. |
| UPRN_EXISTS_FIRST_AND_THIRD | You and another party have created {{project_type}} projects at this property. Ensure that you can meet the eligibility criteria before proceeding. |

This checking exists for the following project types:
 * GB Insulation Scheme (GBIS)

To accept this message and proceed with the request must be resubmitted with the `acceptUPRNCheck` attribute set to `true`.


### Version

A version value of `2022-04-01` should be supplied.

### ClientRequestToken

A unique token to be provided by you to identify the request, these will expire after 10 minutes.

### Identity

You will need to generate an API Key from the Retrofit Portal. You can do this by accessing your `Account` on the bottom left of the sidebar in the portal and then clicking the `API` tab and following the instructions displayed.

#### Http Header

The `tm-api-key` portion of the API Key needs to be supplied as a http header with each request.

#### Body TrustmarkId

The `trustmarkId` portion of the API Key needs to be supplied in the identity attribute of the request.

```json
{
  "version": "2022-04-01",
  "identity": {
    "trustmarkId": "api-e5b3e97b-b95e-467f-b082-60fcab47ec6d"
  },
  "clientRequestToken" : "2341716e-23fc-4d6f-b833-f945aa6f5a76",
  "request": {
    ...
  }
}
```

#### Third Party Submissions

If you require Third Party Access to submit data on behalf of another TrustMark registered business (TMLN) you will need to ensure they provide permission for you to do so.

You will need to supply your `Retrofit Account ID` to them. You can find your `Retrofit Account ID` by accessing your `Account` on the bottom left of the sidebar in the portal and then clicking the `Details` tab.

The business will then need to log into their account, access `Account` on the bottom left of the sidebar in the portal and then clicking the `Third Party Access` tab, enter your `Retrofit Account ID` and click `Grant Access`.

### Response Codes

TrustMark uses [HTTP response status codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes) to indicate the success or failure of your API requests.

#### 2xx

Success status codes confirm that your request worked as expected.

#### 400 Bad Request

Almost likely that a missing or malformed request has been provided, often due to incorrect data-types being provided. Check your request with the Swagger documentation.

#### 422 Unprocessable Entity

A detailed reason will be provided to indicate how to resolve processing the information provided. For example;

```json
{
  "message": "Ventilation.ExistingVentilationProvided 'string' has an invalid option"
}
```

#### 409 Conflict

The [ClientRequestToken](#clientrequesttoken) has been seen with the timeframe, deeming it a duplicate request.

### 429 Too Many Requests

You have exceeded your usage quota of requests.

### 5xx

Error status codes indicate an error. Whilst in this early stage we would always appreciate feedback and your http request used to cause the error.

## Endpoints

### FileUploadToken

> POST /Data/FileUploadToken

You can upload files to attach to an Assessment, Project or Lodgement. In order to do this you must first request an File Upload Token - this will give you a time bound link to PUT a file to S3.

The body looks like this and all you need to supply in the request is the filename.

```json
{
  "version": "2022-04-01",
  "identity": {
    "trustmarkId": "api-e5b3e97b-b95e-467f-b082-60fcab47ec6d"
  },
  "clientRequestToken" : "8dfb4810-596c-4a52-9910-27de7a1e8bac",
  "request": {
    "filename": "TestRA.pdf"
  }
}
```

The response gives two key pieces back, the first is the `uploadUrl`. You need to do a binary PUT with your file to that url provided, this is limited to 5 minutes before expiring.

```json
{
  "fileUploadToken": "rac-0c815e54-429d-40d8-98b2-37f8c7913181t20220426t9959c6afec404be5b28ff57544acb6a2t132954467702961840",
  "uploadUrl": "https://uat-retrofit-files-api.s3.eu-west-1.amazonaws.com/uploads/rac-0c815e54-429d-40d8-98b5-37f8c7913181/20220401/9959c6afec404be5b28ff57544acb6a2/132954467702961840-TestRA.pdf?X-Amz-Expires=300&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIART62XRCSLHWGUDHO/20220426/eu-west-1/s3/aws4_request&X-Amz-Date=20220426T113930Z&X-Amz-SignedHeaders=host&X-Amz-Signature=8fdd521f0c048e67161430577b3dd46b227481f2f6de4cc3cdf018945907c72c"
}
```

The `fileUploadToken` you will retain and use as part of a future request.


### AssessmentSubmit

> POST /Data/AssessmentSubmit

Allows for a Retrofit Assessment to be submitted, generating an AssessmentReference.

The owner of the Assessment must have enough credit to cover any fees for this transaction.

> If you are not submitting your own assessment and using one already submitted by a Retrofit Assessor see [Assessment](#assessment).

| Field                             | Information                              |
| :-------------------------------- | ---------------------------------------- |
| rdSAPFileContent                  | The full RdSAP xml file content |
| ownerTMLN                         | The TMLN of the owner of this Assessment who lodged the Assessment |
| assessorTMLN                      | The TMLN of the Retrofit Assessor who conducted the Assessment |
| assessorSchemeId                  | A valid SchemeId the assessor is registered with to lodge this Assessment |
| defects []                        | Contains an array of any defects that have been identified |
| - defectType                      | Value from the taxonomy [DefectTypes](#defecttypes) |
| - comment | Optional string       |
| - severity                        | Value from the taxonomy [DefectSeverityTypes](#defectseveritytypes) |
| - locations []                    | Array of values from the taxonomy [DefectLocationTypes](#defectlocationtypes) |
| - repairCost                      |  |
| - resolutionBeforeRetrofit        | Must or Can |
| - destructiveTestsConducted       | Optional string |
| - hasEvidence                     | true / false |
| - evidenceImageFileUploadTokens []| Optional array of strings containing fileUploadToken values |
| - yourReference                   | Optional string to identity this defect
| occupancy                         |  |
| - typicalOccupancy                | true / false |
| - occupancyNotes                  | Optional string |
| - numberOccupants                 | Number |
| - specialConsiderationsApplicable | true / false |
| ventilation                       |  |
| - existingVentilationProvided     | Value from the taxonomy [ExistingVentilationProvidedTypes](#existingventilationprovidedtypes) |
| - ventilationType                 | Value from the taxonomy [VentilationTypes](#ventilationtypes) |
| - ventilationNotes                | Optional string |
| - preRetrofitPulseAirTightnessTestRating |  |
| - preRetrofitBlowerDoorAirTightnessTestRating |  |
| - suitableBackgroundVentilationPresent | true / false |
| significance                      |  |
| - appraisalOfHeritage             | Optional string |
| context                           |  |
| - buildingOrientation             | Optional number 0 - 360 |
| - combustionVentilationAcceptable | Value from the taxonomy CombustionVentilationAcceptableTypes |
| - exposureZone                    | Value from the taxonomy [ExposureZoneTypes](#exposurezonetypes) |
| - planningConstraints             | true / false |
| - planningComments                | Required if planningConstraints is true |
| - propertyConstruction []         | Array of values from the taxonomy [PropertyConstructionTypes](#propertyconstructiontypes) |
| - propertyDetachment              | Value from the taxonomy [PropertyDetachmentTypes](#propertydetachmenttypes) |
| - siteAccessNotes                 | Optional string |
| - statutoryLimitations []         | Array of strings with values from the taxonomy [StatutoryLimitationTypes](#statutorylimitationtypes)  |
| - statutoryLimitationsComment     | Optional string |
| - isPublic     | true / false. False means that the Assesment is only accessible to the TMLN that created it. Public means that it can be retrieved by a Retrofit Coordinator who has been provided with both an assessmentReference and related PostCode  |



### Assessment

> GET /Data/Assessment

Allows you to access and retrieve an existing Retrofit Assessment and starting RdSAP file that has been submitted with the isPublic permission as true by the Assessor.

You must have a valid AssessmentReference and Postcode to successfully pull back an existing Retrofit Assessment.

| Field                             | Information                              |
| :-------------------------------- | ---------------------------------------- |
| assessmentReference               | The Assessment Reference as generated when the assessment was submitted or provided to you by a Retrofit Assessor |
| postcode                          | The Property Postcode from the RdSAP file submitted with the Retrofit Assessment when submitted or provided to you by a Retrofit Assessor |

### ProjectStart

> POST /Data/ProjectStart

Creates a new Retrofit Project using an AssessmentReference, generating a ProjectReference.

The owner of the Project must have enough credit to cover any fees for this transaction.

| Field                             | Information                              |
| :-------------------------------- | ---------------------------------------- |
| assessmentReference | The Assessment Reference to use for this Project. As generated when the assessment was submitted or provided to you by a Retrofit Assessor |
| ownerTMLN | The TMLN of the owner of this Project |
| schemeId | The schemeId of the Scheme Provider which the Project will be submitted under. This must be a value from the schemeId from the taxonomy [SchemeOptions](#schemeoptions), this must also be valid registration with the TMLN |
| fundingOrganisationName |  |
| fundingComment |  |
| projectType | Value from the taxonomy [ProjectTypes](#projecttypes) |
| yourProjectReference | A string containing your unique project reference |
| localAuthorityProjectPhase | Value from the taxonomy [LocalAuthorityProjectsLADS](#LocalAuthorityProjectsLADS) / [LocalAuthorityProjectsSHDF](#LocalAuthorityProjectsSHDF) / [LocalAuthorityProjectsHUG](#LocalAuthorityProjectsHUG) for Local Authority projects only |
| localAuthorityProjectKey | Value from the taxonomy [LocalAuthorityProjectsLADS](#LocalAuthorityProjectsLADS) / [LocalAuthorityProjectsSHDF](#LocalAuthorityProjectsSHDF) / [LocalAuthorityProjectsHUG](#LocalAuthorityProjectsHUG) for Local Authority projects only |
| acceptUPRNCheck | Required to accept UPRN warning of existing records at the same UPRN, see [UPRN Check](#uprn-check) |
| tenure |  |
| - premisesTenure | Value from the taxonomy [TenureTypes](#tenuretypes) |
| - residentName |  |
| - residentContactNumber |  |
| - residentAlternativeContactNumber |  |
| - ownerName |  |
| - ownerContactNumber |  |
| - ownerAlternativeContactNumber |  |
| - ownerEmail | This will be used to distribute certificates |
| propertyInformation |  |
| - propertyType | Value from the taxonomy [PropertyTypes](#propertytypes)  |
| - propertyDetachment | Value from the taxonomy [PropertyDetachmentTypes](#propertydetachmenttypes) |
| - propertyAge | Value from the taxonomy [PropertyAgeTypes](#propertyagetypes) |
| - propertyConstruction [] | Array of values from the taxonomy [PropertyConstructionTypes] |
| - propertyBedrooms | Value from the taxonomy PropertyBedroomTypes |
| assessmentDefects [] | Array of assessment defects being covered in the project |
| - defectId | The defectId as listed in the Assessment |
| - actualRepairCost |  |
| - toBeAddressedInProject | true / false  |
| projectDefects [] | Array of new defects that have been identified at project stage |
| - yourReference | A string reference value |
| - defectType | Value from the taxonomy [DefectTypes](#defecttypes) |
| - comment | Optional string |
| - severity | Value from the taxonomy [DefectSeverityTypes](#defectseveritytypes) |
| - locations [] | Array of values from the taxonomy [DefectLocationTypes](#defectlocationtypes) |
| - repairCost |  |
| - resolutionBeforeRetrofit | Must or Can |
| - hasEvidence | true / false |
| - actualRepairCost |  |
| - toBeAddressedInProject | true / false |
| intendedOutcomes | true / false |
| - reductionEnergyUse | true / false |
| - reductionInEnergyCosts | true / false |
| - reductionsInEmissions | true / false |
| - improvementsInInternalComfort | true / false |
| - improvementsOfIAQ | true / false |
| - eliminationDampCondensationMould | true / false |
| - reduceRiskOverheating | true / false |
| - improvementsInEnergyRating | true / false |
| - meetPerformanceStandard | true / false |
| - improvementsInUsefulnessSustainability | true / false |
| - protectBuildingAgainstDecay | true / false |
| - resistanceFloodAndWaterPenetration | true / false |
| - protectionArchitecturalHeritage | true / false |
| - integrationEEMSAndOtherImprovements | true / false |
| - otherRelevantIssues | Optional string |
| - monitoringMethod | Optional string |
| improvementOptionEvaluations [] | Array of improvement option evaluations, must contain one marked as `isMediumTermPlanBase` |
| - reference | A string reference value |
| - calculationMethodology |  |
| - householdContribution |  |
| - measuresEvaluated [] | |
| -  - yourReference | A string reference value |
| -  - workTypeCode | Value from the taxonomy [MeasureTypes](#measuretypes) |
| -  - product |  |
| -  - measureEligibilityStatus | Value from the taxonomy [MeasureEligibilityStatusTypes](#measureeligibilitystatustypes) |
| -  - measureInstallationCost | Decimal of the install cost |
| -  - annualFuelCostSaving | Decimal of the annual fuel cost saving |
| -  - potentialEnergyRating | Number of the potential energy rating  |
| -  - repaymentYears | Decimal of the number of years to repay |
| -  - annualCO2Savings | Decimal of the CO2 Savings |
| -  - carbonCostEffectiveness | Decimal of the carbon cost effectiveness |
| -  - sapSavings | Decimal range 0-100. Mandatory when the `measureEligibilityStatus` is 'Eligible' |
| -  - productInstalledUnitOfMeasure | 'Items' or 'm2' required when measureEligibilityStatus is 'Eligible' |
| -  - productInstalledValue | Numeric value to indicate how many items or m2 of product evaluated |
| - intendedOutcomes |  |
| - - reductionEnergyUse | true / false |
| - - reductionInEnergyCosts | true / false |
| - - reductionsInEmissions | true / false |
| - - improvementsInInternalComfort | true / false |
| - - improvementsOfIAQ | true / false |
| - - eliminationDampCondensationMould | true / false |
| - - reduceRiskOverheating | true / false |
| - - improvementsInEnergyRating | true / false |
| - - meetPerformanceStandard | true / false |
| - - improvementsInUsefulnessSustainability | true / false |
| - - protectBuildingAgainstDecay | true / false |
| - - resistanceFloodAndWaterPenetration | true / false |
| - - protectionArchitecturalHeritage | true / false |
| - - integrationEEMSAndOtherImprovements | true / false |
| - - otherRelevantIssues | Optional string |
| - - monitoringMethod | Optional string |
| - isMediumTermPlanBase | true if this is the Improvement Option Evaluation to be taken forward for the Medium Term Improvement Plan; otherwise false |
| mediumTermImprovementPlan |  |
| - reference | A string reference value |
| - savingsMoney |  |
| - savingsSAPPoints |  |
| - stages [] |  |
| - - sequence | Number indicating the sequence the stages will be conducted |
| - - dependentStages [] | Optional array containing numbers of stages that will be completed prior to this stage |
| - - savingsMoney |  |
| - - savingsSAPPoints |  |
| - - stageDurationInWeeks |  |
| - - keyEventComments |  |
| - - inScopeCurrentProject |  |
| - - improvementOptionEvaluationMeasureReferences [] | An array of values from `improvementOptionEvaluations.measuresEvaluated.yourReference` from the improvementOptionEvaluation with `isMediumTermPlanBase` is true |
| riskAssessment |  |
| - declaredProjectRisk | Value from the taxonomy [DeclaredProjectRiskTypes](#declaredprojectrisktypes) |
| - highestRiskCombination | Value from the taxonomy [HighestRiskCombinationTypes](#highestriskcombinationtypes) |
| retrofitDesigns [] | |
| - isRegisteredWithTrustmark | true if the designer is registered with TrustMark; otherwise false |
| - designerTMLN | The TMLN of the Designer, required if `isRegisteredWithTrustmark`  |
| - designerName | String required if not `isRegisteredWithTrustmark` |
| - designerQualification | Value from the taxonomy [DesignerQualificationTypes](#designerqualificationtypes)  |
| - improvementOptionEvaluationMeasureReferences [] | An array of values from `improvementOptionEvaluations.measuresEvaluated.yourReference` from the improvementOptionEvaluation with `isMediumTermPlanBase` is true |
| - ventilationTreatmentType | Value from the taxonomy [VentilationTreatmentTypes](#ventilationtreatmenttypes) |
| - thermalBridgeRiskPresent | true / false |
| - thermalBridgeActionDescription | Required if `thermalBridgeRiskPresent` |
| - thermalBridgeTreatment | Value from the taxonomy [ThermalBridgeTreatmentTypes](#thermalbridgetreatmenttypes) |
| - defectResolutions [] | Array of defects resolved with this design |
| - - assessmentDefectId | If an assessment defect, the `defectId` reference |
| - - projectDefectYourReference | If a project defect, the `yourReference` reference |
| - - resolution | String detailing the resolution |
| - ventilationTreatmentStrategy | Value from the taxonomy [VentilationTreatmentStrategyTypes](#ventilationtreatmentstrategytypes) |
| - ventilationStrategyNotes |  |
| roles |  |
| - installerTMLNs [] | Array of any TMLN of installers to be used |
| - evaluatorTMLN | TMLN of the Evaluator |
| supportingDocumentAttachments [] | Array of supporting documents  |
| - fileUploadToken | String as created [FileUploadToken](#fileuploadtoken) |
| - filename | Filename string provided to create the fileUploadToken |
| - documentType | Value from the taxonomy [DocumentTypes](#documenttypes) |
| - comments | Optional string |
| notes [] | Optional array of strings |

### LodgementSubmit

> POST /Data/LodgementSubmit

Create a new lodgement against the project.

The owner of the Project must have enough credit to cover any fees for this transaction.

| Field                             | Information                              |
| :-------------------------------- | ---------------------------------------- |
| projectReference | The project reference of the Project for this Lodgement to be associated with |
| ownerTMLN | The TMLN of the owner of this Project |
| planStageSequence |  |
| measures [] | Array of measures installed |
| - improvementOptionEvaluationMeasureReference | Reference `improvementOptionEvaluations.measuresEvaluated.yourReference` from the improvementOptionEvaluation with `isMediumTermPlanBase` is true |
| - workTypeCode | Value from the taxonomy [MeasureTypes](#measuretypes) |
| - freeTextDetails | String that will appear on the certificate |
| - percentageMeasureInstalled | `Yes` or `No` if 100% measures have been installed |
| - installerReferenceNumber |  |
| - customerContribution            | Decimal |
| - measureCost                     | Decimal |
| - installedDate |  |
| - handoverDate |  |
| - workCarriedOutByTMLN | The TMLN of the registered business that carried out the work |
| - workCarriedOutBySchemeId | The TrustMark Scheme Provider schemeId for the installer of this work |
| - installerPasCertificateNumber |  |
| - operativeName |  |
| - operativeCertificationReference |  |
| - isInnovationMeasure | true / false |
| - innovationMeasureProduct | Value from the taxonomy [InnovationMeasureTypes](#innovationmeasuretypes) |
| - productManufacturer |  |
| - productModel |  |
| - productVersion |  |
| - productSerialNumber |  |
| - productWarrantyDuration |  |
| - financialProtectionCategory |  |
| - guaranteeName | Value from the taxonomy [GuaranteeTypes](#guaranteetypes) |
| - guaranteeStartDate |  |
| - guaranteePolicyReference |  |
| - mcsCertificateReference | Required if the measure is MCS. Will validate the provided value against the MCS database, checking the technology and postcode are correct |
| workInvoiceTotal                  | Decimal |
| customerContribution              | Decimal  |
| supportingDocumentAttachments [] | Array of supporting documents |
| - fileUploadToken | String as created [FileUploadToken](#fileuploadtoken) |
| - filename | Filename string provided to create the fileUploadToken |
| - documentType | Value from the taxonomy [DocumentTypes](#documenttypes) |
| - comments | Optional string |
| - measureReference | Optional string. Map a document directly to a measure by providing the `improvementOptionEvaluationMeasureReference` from the measures array |

### ProjectComplete

> POST /Data/ProjectComplete

Complete an existing retrofit project.

The owner of the Project must have enough credit to cover any fees for this transaction.

| Field                             | Information                              |
| :-------------------------------- | ---------------------------------------- |
| projectReference | The reference of the project generated from the ProjectStart call |
| rdSAPFileContent | The full RdSAP xml file content |
| acceptUPRNCheck | Required to accept UPRN warning of existing records at the same UPRN, see [UPRN Check](#uprn-check) |
| acceptSamePrePostScores | Required to accept warning of same pre and post scores, which will be raised if this POST RdSAP file contains the same or a lower score than the PRE RdSASP file. It could be a valid case so it is not blocking, provide `true` to knowledge and override this warning. This is a precaution to prevent users uploading the incorrect file. Warnings are raised with a 422 response code and response message of `SAME_PRE_AND_POST_SAP_SCORE` or `LOWER_PRE_AND_POST_SAP_SCORE` |
| acceptAddressCheck | Required to accept address check warning, which will be raised if the Address Line 1 in the POST RdSAP file is different to that in the Started Project. It could be a valid case so it is not blocking, provide `true` to knowledge and override this warning. This is a precaution to prevent users uploading the incorrect file. Warnings are raised with a 422 response code and response message of `ADDRESS_LINE_1_DIFFERENT` |

### ProjectVoid

> POST /Data/ProjectVoid

Voids an existing retrofit project.

| Field                             | Information                              |
| :-------------------------------- | ---------------------------------------- |
| projectReference | The reference of the project generated from the ProjectStart call |

Any attempts to void a project on an invalid status will result in a 422 response.

### ProjectUpdatePropertyInformation

> PUT /Data/ProjectUpdatePropertyInformation

Updates property information for an existing retrofit project.

| Field                             | Information                              |
| :-------------------------------- | ---------------------------------------- |
| projectReference | The reference of the project generated from the ProjectStart call |
| propertyType | Value from the taxonomy [PropertyTypes](#propertytypes)  |
| propertyDetachment | Value from the taxonomy [PropertyDetachmentTypes](#propertydetachmenttypes) |
| propertyAge | Value from the taxonomy [PropertyAgeTypes](#propertyagetypes) |
| propertyConstruction [] | Array of values from the taxonomy [PropertyConstructionTypes] |
| propertyBedrooms | Value from the taxonomy PropertyBedroomTypes |

Any attempts to void a project on an invalid status will result in a 422 response.

### ProjectUpdateTenure

> PUT /Data/ProjectUpdateTenure

Updates tenure for an existing retrofit project.

| Field                             | Information                              |
| :-------------------------------- | ---------------------------------------- |
| projectReference | The reference of the project generated from the ProjectStart call |
| premisesTenure | Value from the taxonomy [TenureTypes](#tenuretypes) |
| residentName |  |
| residentContactNumber |  |
| ownerName |  |
| ownerContactNumber |  |
| ownerEmail | This will be used to distribute certificates |

### ProjectAmend

> POST /Data/ProjectAmend

Amend an existing retrofit project.

The owner of the Project must have enough credit to cover any fees for this transaction. Projects can only be amended if there have been no Ofgem queries against it.

| Field                             | Information                              |
| :-------------------------------- | ---------------------------------------- |
| projectReference | The reference of the project generated from the ProjectStart call |
| rdSAPFileContent | The full RdSAP xml file content |
| acceptUPRNCheck | Required to accept UPRN warning of existing records at the same UPRN, see [UPRN Check](#uprn-check) |
| acceptSamePrePostScores | Required to accept warning of same pre and post scores, which will be raised if this POST RdSAP file contains the same or a lower score than the PRE RdSASP file. It could be a valid case so it is not blocking, provide `true` to knowledge and override this warning. This is a precaution to prevent users uploading the incorrect file. Warnings are raised with a 422 response code and response message of `SAME_PRE_AND_POST_SAP_SCORE` or `LOWER_PRE_AND_POST_SAP_SCORE` |
| acceptAddressCheck | Required to accept address check warning, which will be raised if the Address Line 1 in the POST RdSAP file is different to that in the Started Project. It could be a valid case so it is not blocking, provide `true` to knowledge and override this warning. This is a precaution to prevent users uploading the incorrect file. Warnings are raised with a 422 response code and response message of `ADDRESS_LINE_1_DIFFERENT` |

### SupportingDocument

The Supporting Document allows for multiple documents to be associated with a Project or Lodgement in a single call. The ProjectReference sits in the main body and the request accepts an array of pre-loaded files using [FileUploadToken](#fileuploadtoken)

```json
{
  "version": "2022-04-01",
  "identity": {
    "trustmarkId": "api-e5b3e97b-b95e-467f-b082-60fcab47ec6d"
  },
  "clientRequestToken" : "71476ad6-cef7-4615-9ef3-8ce4cd0af745",
  "projectReference": "P1031",
  "request": [
      ...
  ]
}
```

There are two different endpoints for each of these actions.

#### Supported File Extensions

A 403 Forbidden error will be returned if attempting to upload a file with an extension not in the following list:

* jpg
* jpeg
* png
* gif
* pdf
* txt
* doc
* docx
* xls
* xlsx
* xml
* msg

#### Project

> POST /Data/SupportingDocument/Project

Attach a new Supporting Document against the Project.

You will need an existing ProjectReference in order to do this.

| Field                             | Information                              |
| --------------------------------- | ---------------------------------------- |
| fileUploadToken                   | String as created [FileUploadToken](#fileuploadtoken) |
| filename                          | Filename string provided to create the fileUploadToken |
| documentType                      | Value from the taxonomy [DocumentTypes](#documenttypes) |
| comments                          | Optional string |

#### Lodgement

> POST /Data/SupportingDocument/Lodgement

Attach a new Supporting Document against the Lodgement.

You will need an existing LodgementId in order to do this.

| Field                             | Information                              |
| --------------------------------- | ---------------------------------------- |
| fileUploadToken                   | String as created [FileUploadToken](#fileuploadtoken) |
| filename                          | Filename string provided to create the fileUploadToken |
| documentType                      | Value from the taxonomy [DocumentTypes](#documenttypes) |
| comments                          | Optional string |
| lodgementId                       | String containing a valid LodgementId to attach this file to
| MeasureId                         | Optional string to associate the file directly to a measure

#### LodgementAmend

> PUT /Data/LodgementAmend

Performs an amend to existing lodged measures. This will also reissue the certificate and incur charges.

You will need an existing ProjectReference and LodgementId in order to do this.

The owner of the Project must have enough credit to cover any fees for this transaction.

##### Creating a New Measure
This endpoint can also add measures if an existing measure has been submitted with the same TrustMarkTradeCode in the LodgementSubmit call. To do this use the `measureId` of the measure that has the same TrustMarkTradeCode, and the value 'TBC' for `umr`.

| Field                             | Information                              |
| --------------------------------- | ---------------------------------------- |
| projectReference                  | The project reference of the Project for this Lodgement to be associated with |
| lodgementId                       | String containing a valid LodgementId to attach this file to
| measures []                       | Array of measures installed |
| - measureId                       | Measure id reference assigned from the LodgementSubmit call |
| - umr                             | String the measure to amend |
| - workTypeCode                    | Value from the taxonomy [MeasureTypes](#measuretypes) |
| - freeTextDetails                 | String that will appear on the certificate |
| - installedDate                   |  |
| - handoverDate                    |  |
| - workCarriedOutByTMLN            | The TMLN of the registered business that carried out the work |
| - workCarriedOutBySchemeId        | The TrustMark Scheme Provider schemeId for the installer of this work |
| - productManufacturer |  |
| - productModel |  |
| - productVersion |  |

#### StandaloneLodgementSubmit

> POST /Data/StandaloneLodgementSubmit

Creates a project and single lodgement submission in a single API call. This is suitable for TrustMark Licence Plus where all measures are lodged together.

| Field                             | Information                              |
| --------------------------------- | ---------------------------------------- |
| yourProjectReference              | Your reference for the project |
| address                           |  |
| - number                          |  |
| - name                            |  |
| - flatNameNumber                  |  |
| - postcode                        |  |
| - uprn                            |  |
| - address1                        |  |
| - address2                        |  |
| - address3                        |  |
| - city                            |  |
| - county                          |  |
| - country                         |  |
| - town                            |  |
| tenure                            |  |
| - premisesTenure                  | Value from the taxonomy [TenureTypes](tenuretypes) |
| - residentName                    |  |
| - residentContactNumber           |  |
| - residentAlternativeContactNumber |  |
| - ownerName                       |  |
| - ownerContactNumber              |  |
| - ownerAlternativeContactNumber   |  |
| - ownerEmail                      | This will be used to distribute certificates |
| propertyInformation               |  |
| - propertyType                    | Value from the taxonomy [PropertyTypes](#propertytypes)  |
| - propertyDetachment              | Value from the taxonomy [PropertyDetachmentTypes](#propertydetachmenttypes) |
| - propertyAge                     | Value from the taxonomy [PropertyAgeTypes](#propertyagetypes) |
| - propertyConstruction            | Value from the taxonomy [PropertyConstructionTypes](#propertyconstructiontypes) |
| - propertyBedrooms                | Value from the taxonomy PropertyBedroomTypes |
| measures []                       | Array of measures installed |
| - workTypeCode                    | Value from the taxonomy [MeasureTypes](#measuretypes) |
| - freeTextDetails                 | String that will appear on the certificate |
| - percentageMeasureInstalled      | `Yes` or `No` if 100% measures have been installed |
| - installerReferenceNumber        |  |
| - customerContribution            | Decimal |
| - measureCost                     | Decimal |
| - installedDate                   |  |
| - handoverDate                    |  |
| - workCarriedOutByTMLN            | The TMLN of the registered business that carried out the work |
| - workCarriedOutBySchemeId        | The TrustMark Scheme Provider schemeId for the installer of this work |
| - installerPasCertificateNumber   |  |
| - operativeName                   |  |
| - operativeCertificationReference |  |
| - isInnovationMeasure             | true / false |
| - innovationMeasureProduct        | Value from the taxonomy [InnovationMeasureTypes](#innovationmeasuretypes) |
| - productManufacturer             |  |
| - productModel                    |  |
| - productVersion                  |  |
| - productSerialNumber             |  |
| - productWarrantyDuration         |  |
| - financialProtectionCategory     |  |
| - guaranteeName                   | Value from the taxonomy [GuaranteeTypes](#guaranteetypes) |
| - guaranteeStartDate              |  |
| - guaranteePolicyReference        |  |
| - mcsCertificateReference         | Required if the measure is MCS. Will validate the provided value against the MCS database, checking the technology and postcode are correct |
| - whdReplaceWhatMeasure             | Required for lodgementType WHD. Must be a value from taxonomy [WHDReplaceWhatMeasureValues](#whdreplacewhatmeasurevalues) |
| - whdWorkConducted                  | Required for lodgementType WHD. Must be a value from taxonomy [WHDWorkConductedValues](#whdworkconductedvalues) |
| supportingDocumentAttachments []  | Array of supporting documents |
| - fileUploadToken                 | String as created [FileUploadToken](#fileuploadtoken) |
| - filename                        | Filename string provided to create the fileUploadToken |
| - documentType                    | Value from the taxonomy [DocumentTypes](#documenttypes) |
| - comments                        | Optional string |
| startingRatingEPC                 | 'A', 'B', 'C', 'D', 'E', 'F', or 'G' |
| startingRRNEPC                    | 24 character long RRN number including the dashes |
| completionRatingEPC               | 'A', 'B', 'C', 'D', 'E', 'F', or 'G' |
| completionRRNEPC                  | 24 character long RRN number including the dashes |
| schemeId                          | Value from the taxonomy [SchemeOptions](#schemeoptions), this must also be valid registration with the TMLN |
| ownerTMLN                         | The TMLN of the owner of this Lodgement |
| lodgementType                     | 'LICENCEPLUS' or 'LICENCEPLUSWALES' |
| workInvoiceTotal                  | Decimal |
| customerContribution              | Decimal  |
| highRiskQuestions                 | Required for lodgementType WHD. Must contain array of all questions from taxonomy [WHDQuestions](#whdquestions) |
| - question                        | Question string provided by the taxonomy |
| - answer                          | Answer string from the potential answer options provided by the taxonomy |

> To obtain the lodgement certificate use the [LodgementCertificate](#lodgementcertificate) call along with the `RetrofitProjectReference` and `LodgementId` provided from this response.

### ProjectCertificate

> POST /Data/ProjectCertificate

Retrieve the generated certificate for a completed project. Can only be retrieved for projects created using the same identity.

The body looks like this and all you need to supply in the request is the project reference.

```json
{
  "version": "2022-04-01",
  "identity": {
    "trustmarkId": "api-e5b3e97b-b95e-467f-b082-60fcab47ec6d"
  },
  "clientRequestToken" : "8dfb4810-596c-4a52-9910-27de7a1e8bac",
  "request": {
    "projectReference": "P1001"
  }
}
```

The response is the pdf file as Base64 with mime type application/pdf.

### LodgementCertificate

> POST /Data/LodgementCertificate

Retrieve the generated certificate for a completed lodgement. Can only be retrieved for lodgements created using the same identity.

The body looks like this and all you need to supply in the request is the project reference and the lodgementId.

```json
{
  "version": "2022-04-01",
  "identity": {
    "trustmarkId": "api-e5b3e97b-b95e-467f-b082-60fcab47ec6d"
  },
  "clientRequestToken" : "8dfb4810-596c-4a52-9910-27de7a1e8bac",
  "request": {
    "projectReference": "P1001",
    "lodgementId": "lod-00000000-0000-0000-0000-000000000000"
  }
}
```

The response is the pdf file as Base64 with mime type application/pdf.

### ProjectUPRNStatus

> POST /Data/ProjectUPRNStatus

Checks for existing projects under the GBIS fund against the project owner TMLN (The Retrofit Cooridnator who created it) and UPRN provided. See [UPRN Check](#uprn-check)

| Field                      | Information                              |
| -------------------------- | ---------------------------------------- |
| ownerTMLN                  | The TMLN to check                        |
| uprn                       | The UPRN to check                        |

#### Request

```json
{
  "version": "string",
  "identity": {
    "trustmarkId": "string"
  },
  "request": {
    "ownerTMLN": "string",
    "uprn": "string"
  }
}
```

##### Example Request

```json
{
  "version": "2022-04-01",
  "identity": {
    "trustmarkId": "api-e5b3e97b-b95e-467f-b082-60fcab47ec6d"
  },
  "clientRequestToken" : "a4003e76-fd82-a3d5-ba88-26ad1e3da0b4",
  "request": {
    "ownerTMLN": "1399311",
    "uprn": "10008507326"
  }
}
```

#### Response

```json
{
  "uprn": "string",
  "checkedTMLN": "string",
  "checkedFundType": "string",
  "code": "string"
}
```

##### Example Response

```json
{
  "uprn": "10008507326",
  "checkedTMLN": "1399311",
  "checkedFundType": "GBIS",
  "code": "UPRN_EXISTS_FIRST"
}
```

### Taxonomies

#### CombustionVentilationAcceptableTypes

> GET /Taxonomies/CombustionVentilationAcceptableTypes

Returns a list of options for `context.combustionVentilationAcceptable` in the AssessmentStart request.

#### DeclaredProjectRiskTypes

> GET /Taxonomies/DeclaredProjectRiskTypes

Returns a list of options for `riskAssessment.declaredProjectRisk` in the ProjectStart request.

#### DefectLocationTypes

> GET /Taxonomies/DefectLocationTypes

Returns a list of options for `defects.locations` in the AssessmentSubmit request and `projectDefects.locations` in the ProjectStart.

#### DefectTypes

> GET /Taxonomies/DefectTypes

Returns a list of options for `defects.defectType` in the AssessmentSubmit request and `projectDefects.defectType` in the ProjectStart.

#### DefectSeverityTypes

> GET /Taxonomies/DefectSeverityTypes

Returns a list of options for `defects.severity` in the AssessmentSubmit request and `projectDefects.severity` in the ProjectStart.

#### DesignerQualificationTypes

> GET /Taxonomies/DesignerQualificationTypes

Returns a list of options for `retrofitDesigns.designerQualification` in the ProjectStart request.

#### DocumentTypes

> GET /Taxonomies/DocumentTypes

Returns a list of options for `documentType` in the SupportingDocument requests and `supportingDocumentAttachments.documentType` in the AssessmentSubmit and ProjectStart requests.

#### ExistingVentilationProvidedTypes

> GET /Taxonomies/ExistingVentilationProvidedTypes

Returns a list of options for `ventilation.existingVentilationProvided` in the AssessmentSubmit request.

#### ExposureZoneTypes

> GET /Taxonomies/ExposureZoneTypes

Returns a list of options for `context.exposureZone` in the AssessmentSubmit request.

#### GuaranteeTypes

> GET /Taxonomies/GuaranteeTypes

Returns a list of guarantee types for which the `name` value can be used with the `measures.guaranteeName` in the LodgementSubmit request.

#### HighestRiskCombinationTypes

> GET /Taxonomies/HighestRiskCombinationTypes

Returns a list of options for `riskAssessment.highestRiskCombination` in the ProjectStart request.

#### InnovationMeasureTypes

> GET /Taxonomies/InnovationMeasureTypes

Returns a list of innovation measure types for which the `productId` value can be used with the `measures.innovationMeasureProduct` in the LodgementSubmit request.

#### ProjectTypes

> GET /Taxonomies/ProjectTypes

Returns a list of options for `projectType` in the ProjectStart request.

#### PropertyAgeTypes

> GET /Taxonomies/PropertyAgeTypes

Returns a list of options for `propertyInformation.propertyAge` in the ProjectStart request.

#### PropertyConstructionTypes

> GET /Taxonomies/PropertyConstructionTypes

Returns a list of options for `propertyInformation.propertyConstruction` in the ProjectStart request and `context.propertyConstruction` in the AssessmentSubmit request.

#### PropertyDetachmentTypes

> GET /Taxonomies/PropertyDetachmentTypes

Returns a list of options for `propertyInformation.propertyDetachment` in the ProjectStart request.

#### PropertyTypes

> GET /Taxonomies/PropertyTypes

Returns a list of options for `propertyInformation.propertyType` in the ProjectStart request.

#### MeasureEligibilityStatusTypes

> GET /Taxonomies/MeasureEligibilityStatusTypes

Returns a list of options for `improvementOptionEvaluations.measuresEvaluated.measureEligibilityStatus` in the ProjectStart request.

#### MeasureTypes

> GET /Taxonomies/MeasureTypes

Returns a list of options for `improvementOptionEvaluations.measuresEvaluated.workTypeCode` in the ProjectStart request. To filter for ECO4 only check the property eco4Name has a value, or use [MeasureTypesECO4](#measuretypeseco4) instead to get a filtered list.

#### MeasureTypesECO4

> GET /Taxonomies/MeasureTypesECO4

Returns a list of ECO4 only options for `improvementOptionEvaluations.measuresEvaluated.workTypeCode` in the ProjectStart request.

#### SchemeOptions

> GET /Taxonomies/SchemeOptions

Returns a list of options for `schemeId` in the ProjectStart request.

#### StatutoryLimitationTypes

> GET /Taxonomies/StatutoryLimitationTypes

Returns a list of options for `context.statutoryLimitations` in the AssessmentSubmit request.

#### TenureTypes

> GET /Taxonomies/TenureTypes

Returns a list of options for `tenure.premisesTenure` in the ProjectStart request.

#### ThermalBridgeTreatmentTypes

> GET /Taxonomies/ThermalBridgeTreatmentTypes

Returns a list of options for `retrofitDesigns.thermalBridgeTreatment` in the ProjectStart request.

#### VentilationTreatmentStrategyTypes

> GET /Taxonomies/VentilationTreatmentStrategyTypes

Returns a list of options for `retrofitDesigns.ventilationTreatmentStrategy` in the ProjectStart request.

#### VentilationTreatmentTypes

> GET /Taxonomies/VentilationTreatmentTypes

Returns a list of options for `retrofitDesigns.ventilationTreatmentType` in the ProjectStart request.

#### VentilationTypes

> GET /Taxonomies/VentilationTypes

Returns a list of options for `ventilation.ventilationType` in the AssessmentSubmit request.

#### MeasureTypesLADS

> GET /Taxonomies/MeasureTypesLADS

Returns a list of LADS only options for `improvementOptionEvaluations.measuresEvaluated.workTypeCode` in the ProjectStart request.

#### LocalAuthorityProjectsLADS

> GET /Taxonomies/LocalAuthorityProjectsLADS

Returns a list of LADS only options for `localAuthorityProjectPhase` and `localAuthorityProjectKey` in the ProjectStart request.

#### MeasureTypesHUG

> GET /Taxonomies/MeasureTypesHUG

Returns a list of HUG only options for `improvementOptionEvaluations.measuresEvaluated.workTypeCode` in the ProjectStart request.

#### LocalAuthorityProjectsHUG

> GET /Taxonomies/LocalAuthorityProjectsHUG

Returns a list of HUG only options for `localAuthorityProjectPhase` and `localAuthorityProjectKey` in the ProjectStart request.

#### MeasureTypesSHDF

> GET /Taxonomies/MeasureTypesSHDF

Returns a list of SHDF only options for `improvementOptionEvaluations.measuresEvaluated.workTypeCode` in the ProjectStart request.

#### LocalAuthorityProjectsSHDF

> GET /Taxonomies/LocalAuthorityProjectsSHDF

Returns a list of SHDF only options for `localAuthorityProjectPhase` and `localAuthorityProjectKey` in the ProjectStart request.

#### WHDWorkConductedValues

> GET /Taxonomies/WHDWorkConductedValues

Returns options for standalone lodgement type WHD to populate `measure.whdWorkConducted`.

#### WHDReplaceWhatMeasureValues

> GET /Taxonomies/WHDReplaceWhatMeasureValues

Returns options for standalone lodgement type WHD to populate `measure.whdReplaceWhatMeasure`.

#### WHDQuestions

> GET /Taxonomies/WHDQuestions

Returns the list of questions that must be provided for WHD standalone lodgements and the potential answer options.

#### MeasureTypesWHD

> GET /Taxonomies/MeasureTypesWHD

Returns a list of WHD only options for `measure.workTypeCode` in the ProjectStart request.

#### MeasureTypesByProjectType

> POST /Taxonomies/MeasureTypesByProjectType

Returns a list of measures for the requested project type.

| Field                             | Information                              |
| --------------------------------- | ---------------------------------------- |
| projectType                  | The project type to filter the measure types on, e.g. ECO4, LADS, HUG, WHD, SHDF, LicencePlus |

## RdSAP Files

RdSAP files are required at Assessment and Project Completion stages. The xml content of the file must be supplied in the fields, if you are exploring the API and need an online tool to escape characters then https://www.freeformatter.com/json-escape.html works well.

TrustMark is not responsible for external websites and their functionality or security, we advise that only non-personal test data is used with any of the tools listed.

## MCS Measures and Testing

In order to use MCS measures you must provide an MCS Certificate Reference that can be validated. Therefore, the certificate reference must exist in the MCS Testing Database and the returned certificate must have a matching property postcode and technology.

`MCS-01109079-R` is a valid testing mcsCertificateReference value and must match against a postcode of `IP7 6RL` and an MCS technology of `2`, for example `DW-305` would be a valid measure type.

## Visualising

If you'd like to visualise the data [JSON Visio (jsonvisio.com)](https://jsonvisio.com/editor) illustrates data on graphs well and can help with the understanding of the Assessment, Project and Lodgement requests.

* [Assessment Example](./ReadmeIntegration-example-assessment.md)

* [Project Example](./ReadmeIntegration-example-project.md)

* [GBIS Project Example](./ReadmeIntegration-example-project-gbis.md)

* [GBIS Lodgement Example](./ReadmeIntegration-example-lodgement-gbis.md)

* [LADS Project Example](./ReadmeIntegration-example-project-lads.md)

* [HUG Project Example](./ReadmeIntegration-example-project-hug.md)

* [SHDF Project Example](./ReadmeIntegration-example-project-shdf.md)

* [Lodgement Example](./ReadmeIntegration-example-lodgement.md)

* [LodgementAmend Example](./ReadmeIntegration-example-lodgementamend.md)

* [LodgementAmend Add Measure Example](./ReadmeIntegration-example-lodgementamendadditional.md)

* [StandaloneLodgement Example](./ReadmeIntegration-example-standalonelodgement.md)

* [WHD StandaloneLodgement Example](./ReadmeIntegration-example-whd-standalonelodgement.md)

* [ProjectVoid Example](./ReadmeIntegration-example-projectvoid.md)

* [ProjectUpdateTenure Example](./ReadmeIntegration-example-projectupdatetenure.md)

* [ProjectUpdatePropertyInformation Example](./ReadmeIntegration-example-projectupdatepropertyinformation.md)

* [ProjectAmend Example](./ReadmeIntegration-example-projectamend.md)

* [UPRN Check Example](./ReadmeIntegration-example-uprn-check-example.md)

## Postman Examples

An example collection is available to import, copy this link `https://www.getpostman.com/collections/5507b8404d64566f477c` and use the 'Import From Link' feature in Postman. Once imported update the variables in the API Collection with your own tm-api-key as mentioned in [Identity](#identity)

If you don't have Postman installed, you can get a copy here https://www.postman.com

## Certificates

Certificates will be returned as Base64 - https://base64.guru/converter/decode/file and when decoded a PDF.

## Integration Testing

Before access to live API keys can be granted, integrators must sign a Data Sharing Agreement and successfully complete testing of their integration.
The document below provides an overview of core testing scenarios and includes the declarations that must be built into your application and evidenced.
http://trustmark.org.uk/docs/default-source/data-warehouse/retrofit-api-testcases

## Third Party Lodgement Permission
To lodge work as a Software Provider on behalf on a TrustMark Registered Business they must give you permission to lodge on their behalf. This can be achieved by:
- Logging into your retrofit portal account and retrieving your Retrofit Account Id.
- Providing it to the TrustMark Business
- They log into their portal and enter the Retrofit Account Id in the 'Third Party Access' tab and 'Grant Access'

## TrustMark Licence (TMLN) TradeCheck

You can request an API Key to use the `TradeCheck Service` provided by TrustMark that will enable you to request trades that a TMLN is registered for.

### Endpoints

UAT Swagger: https://api.trades.data-hub.org.uk/swagger/index.html

Production Swagger: https://api.trades.data-hub.org.uk/swagger/index.html

#### Sample Request

```json
{
  "publicId": 3033827
}
```

#### Sample Response

```json
{
  "success": true,
  "tmln": "3033827",
  "trades": [
    {
      "tradeCode": 89,
      "tradeDescription": "Cavity Wall Internal Insulation [B8 - 2019]",
      "registered": [
        {
          "fromDate": "2023-03-27T00:00:00+00:00",
          "toDate": null,
          "certificateId": null,
          "schemeId": "trustmark_logo"
        }
      ]
    },
    {
      "tradeCode": 103,
      "tradeDescription": "Room in Roof Insulation [B12 - 2019]",
      "registered": [
        {
          "fromDate": "2023-03-27T00:00:00+00:00",
          "toDate": null,
          "certificateId": null,
          "schemeId": "trustmark_logo"
        }
      ]
    }
  ],
  "schemes": [
    "trustmark_logo"
  ],
  "organisationRegisteredName": "FPTestLAP1",
  "rcInfo": {
    "isRC": false,
    "isRA": false,
    "apiOnlyRC": false,
    "apiOnlyRA": false,
    "rcSchemeIds": [],
    "apiOnlyRCSchemeIds": [],
    "apiOnlyRASchemeIds": []
  },
  "lastUpdated": "27/03/2023 14:35",
  "licenceStatus": "Active"
}
```


