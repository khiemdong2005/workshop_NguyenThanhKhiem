---
title: "Amazon Comprehend Medical – extracting data from clinical text"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Amazon Comprehend Medical: Extracting data from clinical text

Clinical information often appears in unstructured notes, discharge summaries, test results, and patient records. In “Patient reports headache and fever. The doctor prescribed Ibuprofen 200 mg every 6 hours,” an application must distinguish symptoms, medication, dosage, and frequency before storing structured data.

Amazon Comprehend Medical is an AWS natural language processing service for clinical text. Its pretrained models detect medical entities and return confidence scores, so developers can build a basic extraction workflow without training their own model.

## Main capabilities

- **Entity detection:** `DetectEntitiesV2` identifies conditions, medications, anatomy, procedures, and related attributes such as dosage or frequency.
- **PHI detection:** `DetectPHI` identifies protected health information such as names, ages, and dates. The application must still implement its own de-identification and data protection workflow.
- **Clinical context:** Traits such as `NEGATION` help distinguish “Patient denies fever” from a positive symptom.
- **Ontology linking:** `InferICD10CM`, `InferRxNorm`, and `InferSNOMEDCT` suggest standardized codes. Suggested codes need review before use in a medical record.

## Processing workflow

1. Receive clinical text and determine how sensitive data will be protected.
2. Call the appropriate API for entity detection, PHI detection, or ontology linking.
3. Read entity offsets, attributes, traits, and confidence scores from the response.
4. Have low-confidence or clinically significant results reviewed before storing them.

The service offers synchronous processing for individual requests and asynchronous processing for document collections in Amazon S3. It can be accessed through the AWS CLI and SDKs.

## Use cases and integrations

Structured clinical data can support record search, case management, clinical research, and medical coding review. For example, medication names and dosages can be extracted into a list for human verification; an extracted result is not itself a prescription.

An application can use Amazon Transcribe Medical first when the input is speech, or Amazon Textract when the input is a scanned document. These are separate integration steps built by the application.

## Limitations and cost

Amazon Comprehend Medical detects entities in **US English** clinical text; it does not directly support Vietnamese. Confidence scores do not replace clinical judgment. AWS states that results used in patient care must be reviewed for accuracy and sound medical judgment by trained professionals.

Clinical text may contain PHI, so access control, encryption, storage, and organizational compliance must be planned. The service's HIPAA eligibility does not make an entire application compliant automatically. API costs vary by task and usage, so check current AWS pricing before deployment.

## References

- [AWS – What is Amazon Comprehend Medical?](https://docs.aws.amazon.com/comprehend-medical/latest/dev/comprehendmedical-welcome.html)
- [AWS – How Amazon Comprehend Medical works](https://docs.aws.amazon.com/comprehend-medical/latest/dev/comprehendmedical-howitworks.html)
- [AWS – Amazon Comprehend Medical pricing](https://aws.amazon.com/comprehend/medical/pricing/)

## Published post

![Amazon Comprehend Medical post in AWS Study Group VN](/images/3-BlogsPosted/comprehend-medical-post.png)
