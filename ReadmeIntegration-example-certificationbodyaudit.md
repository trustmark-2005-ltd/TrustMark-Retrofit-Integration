
### CertificationBodyAuditSubmit Example

[Return](./ReadmeIntegration.md)

```json
{
  "version": "2022-04-01",
  "identity": {
    "trustmarkId": "api-e5b3e97b-b95e-467f-b082-60fcab47ec6d"
  },
  "clientRequestToken": "a1f3e76c-1234-5678-abcd-26bd14cda0b4",
  "request": {
    "retrofitProjectId": "rpj-d0aa61a0-ec95-4d6c-a39f-24e092076718",
    "certificationBodyAuditType": "Certification Body Audit"
  }
}
```

## 2. CertificationBodyAuditAmend

[Return](./ReadmeIntegration.md)

```json
{
  "version": "2022-04-01",
  "identity": {
    "trustmarkId": "api-e5b3e97b-b95e-467f-b082-60fcab47ec6d"
  },
  "clientRequestToken": "b2e4f87d-2345-6789-bcde-37ce25edb1c5",
  "request": {
    "retrofitProjectId": "rpj-d0aa61a0-ec95-4d6c-a39f-24e092076718",
    "certificationBodyAuditId": "cba-6c47b15d-92cb-4c8b-a2df-398ecdea1a91",
    "certificationBodyAuditType": "Certification Body Audit",
    "status": "In Progress",
    "measures": [
      {
        "lodgementId": "lod-704774e9-f675-4d38-bb9d-4e8b46a860eb",
        "umr": "P24923GFBY",
        "installerTMLN": "2403100",
        "installerBusinessName": "1st Rate Electrical Services Limited",
        "installerSchemeId": "napit",
        "measureType": "Smart thermostat (no pre-existing programmer and room thermostat)",
        "auditAppointmentStatus": "Booked",
        "inspectionDate": "2026-04-01T09:00:00Z"
      }
    ],
    "evidenceUploads": []
  }
}
```
## 3. CertificationBodyAudit (Get Single)

[Return](./ReadmeIntegration.md)

```json
{
  "version": "2022-04-01",
  "identity": {
    "trustmarkId": "api-30b1aa54-4b9a-4e98-a05a-f17051bea61f"
  },
  "clientRequestToken": "d4061090-4567-89ab-def0-59e047afd3e7",
  "request": {
    "retrofitProjectId": "rpj-d0aa61a0-ec95-4d6c-a39f-24e092076718",
    "certificationBodyAuditId": "cba-6c47b15d-92cb-4c8b-a2df-398ecdea1a91"
  }
}
```
## 4. CertificationBodyAudits (Get All for Project)

[Return](./ReadmeIntegration.md)

```json
{
  "version": "2022-04-01",
  "identity": {
    "trustmarkId": "api-30b1aa54-4b9a-4e98-a05a-f17051bea61f"
  },
  "clientRequestToken": "e5172101-5678-9abc-ef01-60f158afe4f8",
  "request": {
    "retrofitProjectId": "rpj-d0aa61a0-ec95-4d6c-a39f-24e092076718"
  }
}
```

## 5. CertificationBodyAuditDelete

[Return](./ReadmeIntegration.md)
```json
{
  "version": "2022-04-01",
  "identity": {
    "trustmarkId": "api-30b1aa54-4b9a-4e98-a05a-f17051bea61f"
  },
  "clientRequestToken": "f6283212-6789-abcd-f012-71a269ahf5a9",
  "request": {
    "retrofitProjectId": "rpj-d0aa61a0-ec95-4d6c-a39f-24e092076718",
    "certificationBodyAuditId": "cba-6c47b15d-92cb-4c8b-a2df-398ecdea1a91"
  }
}
```