# PVCM 7.0 RELN\_1.0C

## 1. Release Overview

PV Case Management 7.0 supports the following new features:

* Case Intake & Processing Automation o Enhanced JSON case intake with additional fields, automated follow-up processing, error mapping, and Intake # traceability
  * Email/S3 intake support with Japanese product encoding and acknowledgment emails o Sending acknowledgement upon acceptance of a case
  * Editable PDF parsing, auto-detection of follow-ups, and sender identification via ML o Parallel and localized Japan case processing workflows
  * Native language handling and product merge during follow-up acceptance
* Follow-up Processing and Difference View o Re-design of Follow-up difference view o Enhanced data merge during follow-up acceptance
* Narratives & AI/ML Capabilities o Auto-narrative generation with multi-language template support o Generative AI-based medical narrative authoring o MedDRA auto-coding using historical data and LLM predictions o ML parsing for Strength, Substance, and Cause Type from AE forms
* Regulatory & PMDA Support o Full Japanese UI, MedDRA J and J Drug Dictionary integration
  * PMDA-specific fields, workflows, DQCRs, and dual-language Translation View o Case versioning, local state handling, and audit log support for Japan o Support for null flavor values. o PMDA-specific DQCRs with multilingual messaging and field-level enforcement o MedDRA recoding support for configurations and MedDRA Japanese.
* Field, DQCR & Workflow Enhancements o Central Field Management via PV Admin
  * Justification tracking for delete/reject/close actions with multilingual support
  * Auto-transition of case state based on workflow rules
  * Auto-calculation of additional fields including Listedness, Product Event Relatedness, and

Categorization o Field edit restrictions applied to finalized or deleted cases. o Data quality checks during bulk transmission, with additional DQCR rules

* Security & Compliance o PII field, blinded data protection and audit trail masking based on user roles o Controlled access to task/query data without case update rights
  * Secondary authentication for non-LDAP user accounts, with added login restrictions for system user and non-LDAP accounts.
* Product & Encoding Support o Device Model Number, Co-packaged product support, and WHO/MFDS drug integration o Auto-population of Product Code fields from config (MFDS/WHO/MPID) o Study browser enhancements with localized Study Program support

## 2. Upgrade Path

The upgrade of 7.0 is supported from 6.2.x.

## 3. RxLogix PV Product Compatibility

| **RxLogix PV Product** | **Version** |
| ---------------------- | ----------- |
| PVD                    | 7.0         |
| PVR                    | 7.0         |
| PVA                    | 7.0         |
| PVS                    | 7.0         |

## 4. Acronyms, Abbreviations and Definitions

Release document relevant acronyms, abbreviations, and terms are listed in the following table.

| **Term** | **Definition**                                     |
| -------- | -------------------------------------------------- |
| AE       | Adverse Event                                      |
| API      | Application Programming Interface                  |
| AWS      | Amazon Web Services                                |
| BCE      | Basic Case Entry                                   |
| FCE      | Full Case Entry                                    |
| CMT      | Configuration Management Tool                      |
| DQCR     | Data Quality Check Report                          |
| FDA      | Food and Drug Administration (U.S.)                |
| FU       | Follow-Up                                          |
| HLGT     | High-Level Group Term (MedDRA hierarchy)           |
| HLT      | High-Level Term (MedDRA hierarchy)                 |
| ICSR     | Individual Case Safety Report                      |
| IME      | Important Medical Event                            |
| **Term** | **Definition**                                     |
| JSON     | JavaScript Object Notation (data format)           |
| LLT      | Lowest Level Term (MedDRA hierarchy)               |
| LLM      | Large Language Model                               |
| MedDRA   | Medical Dictionary for Regulatory Activities       |
| MFDS     | Ministry of Food and Drug Safety (South Korea)     |
| ML       | Machine Learning                                   |
| NLG      | Natural Language Generation                        |
| PII      | Personally Identifiable Information                |
| PMDA     | Pharmaceuticals and Medical Devices Agency (Japan) |
| PT       | Preferred Term (MedDRA hierarchy)                  |
| SOC      | System Organ Class (MedDRA hierarchy)              |
| UI       | User Interface                                     |
| XML      | Extensible Markup Language                         |

### 5.1 Feature: Case List Screen

**5.1.1 Earliest ICSR Due Date**

* **Jira ID:** PVCM-95481
* **Background / Purpose**: The purpose of this field is to enable users to prioritize cases based on Earliest ICSR Due Date and/or Business Due Date (Due Date).
* **Feature Description**: A new field "Earliest ICSR Due Date" is added to the Intake Queue, Case List, and Duplicate Search screens that will always display the Earliest ICSR Due Date (based on configured reporting rules) for a case & corresponding version. This field is not added to the case form. By Default, the field is available under Optional Fields.

![](<.gitbook/assets/Unknown image>)

Figure : Earliest ICSR Due Date on Listing screen

* **Impact on Other Products**: No impact on other products.

**5.1.2 Search filter indicator in Listing screens**

* **Jira ID:** PVCM-86269
* **Background / Purpose**: To ensure users are aware when search filters are applied, a visual indicator has been introduced in the listing screens. This helps prevent confusion by clearly showing that the displayed results are based on specific filter criteria.
* **Feature Description**: A search filter applied icon is displayed on listing screens whenever filters are applied in the search section to refine results. It appears regardless of whether the search section is expanded or collapsed.

![](<.gitbook/assets/Unknown image (1)>)

Figure 1: Search filter applied icon in Intake Queue

* **Impact on Other Products**: No impact on other products.

### 5.2 Case Intake Via JSON

**5.2.1 Additional Fields and Attachment Support for Case Intake via JSON**

* **Jira ID:** PVCM-74040, PVCM-68643
* \*\*Background / Purpose:\*\*To support automation and improve system integration, the application now supports enhanced case intake using structured JSON files
* \*\*Feature Description:\*\*Case JSON Intake now supports the import of additional fields, attachments, and automatic follow-up detection. Any values that cannot be mapped to the corresponding fields are captured in the Additional Notes section.
* **Impact on Other Products**: No impact on other products.

**5.2.2 Intake Error Mapping Report**

* **Jira ID:** PVCM-97009, PVCM-114193
* **Background / Purpose**: The purpose of this enhancement is to support capturing of errors observed during supported case intake processes (e.g., E2B Importer, S3 Intake, JSON Import, etc.). These errors are compiled into a PDF report and attached to the case under the Attachments section within the Case Form.
* **Feature Description**: During case intake processing, all identified issues will be captured in a

PDF document titled "Case Intake Error Report." This report will include key details such as Field Location, Field Name, Description, and Value for each error encountered. The report will be automatically attached to the case under the Attachments section. Common error types include Invalid Codelist Value, Invalid Date, Invalid Date Format, Truncated Field Value, and Missing Source Data. Additionally, users can configure a set of custom tags (e.g.,

, ) under a unified error "Additional Case Intake Information."

![](<.gitbook/assets/Unknown image (2)>)

Figure 2: Case Intake error report attached in Attachment section

* **Impact on Other Products**: No impact on other products.

**5.2.3 Additional JSON Element Support for Device related Fields**

* **Jira ID:** PVCM-105658
* **Background / Purpose**: The purpose of this enhancement is to support additional fields in JSON Intake.
* **Feature Description:** New fields have been added to the PVCM case form in Quality Check, Device Information, and General sections.
* **Impact on Other Products**: No impact on other products.

**5.2.4 Parsing Intake # in API response for case intake via JSON API**

* **Jira ID:** PVCM-91775
* **Background / Purpose**: The system enhanced to includes the Intake Number in the JSON API response during case intake, enabling users to search for cases in PVCM using the Intake #. It also ensures error visibility by indicating case generation failure directly in the API response, improving traceability and error handling.
* \*\*Feature Description:\*\*Enhancement enables the inclusion of the Intake # in the API response for cases created via JSON API.

o Intake # is sourced from the JSON file generated by PVCM. o Users can now search cases in PVCM using the Intake #. o API reflects failure status in case generation issues.

![](<.gitbook/assets/Unknown image (3)>)

Figure 3: API Response on case creation via JSON API

![](<.gitbook/assets/Unknown image (4)>)

Figure 4: Intake # propagated on listing screens

* **Impact on Other Products**: No impact on other products.

### 5.3 Feature: Auto-Narrative

**5.3.1 Multilingual Support for Auto-generation of Text based on Templates**

* **Jira ID:** PVCM-70908
* **Background / Purpose**: The purpose of this enhancement is to extend the system's current capability for template-based Auto-Narratives to support Multi-Lingual Templates.
* **Feature Description**: Auto-Narrative templates can now be explicitly associated with specific languages during configuration. The system ensures that when a user initiates auto-generation for a multilingual field (e.g., Case Narrative in Japanese), only templates associated with the field's language are shown.

![](<.gitbook/assets/Unknown image (5)>)

Figure

5

:

Auto

*

generate template dialog box

![](<.gitbook/assets/Unknown image (6)>)

Figure 6: Auto-Narrative template on selecting language from Language View

* **Impact on Other Products**: No impact on other products.

**5.3.2 Default Auto-generate Narrative Templates for Japanese Language**

* **Jira ID**: PVCM-70909
* \*\*Background / Purpose:\*\*The purpose of this enhancement is to extend out of the box narrative templates for Japanese case processing.
* **Feature Description**: System is now enhanced to support auto-narratives templates in Japanese.

![](<.gitbook/assets/Unknown image (7)>)

Figure 7: Auto-narrative template support in PVCM J

* **Impact on Other Products**: No impact on other products.

**5.3.3 Natural Language Case Narrative Generation**

* **Jira ID**: PVCM-93990
* **Background / Purpose:** The purpose of this enhancement is to support authoring of Medical Narratives in natural language using GenerativeAI.
* \*\*Feature Description:\*\*This enhancement introduces a new Generative AI-based narrative generation capability that leverages case form data and configurable natural language prompts. NLG-based narratives now support all case form fields (excluding operational data) available on Case Form through prompt configuration.

![](<.gitbook/assets/Unknown image (8)>)

Figure 8: Natural Language Generation support in case narratives

![](<.gitbook/assets/Unknown image (9)>)

Figure 9: Natural Language Generation Template in Summary section

* **Impact on Other Products**: No impact on other products.

### 5.4 Feature: Case Entry Form

**5.4.1 Improper Use or Storage Field**

* **Jira ID:** PVCM-109306, PVCM-81230
* **Background / Purpose**: A new field, “Improper Use or Storage,” has been added to the Device Information section under Product(s).
* **Feature Description**: The new codelist field **“Improper Use or Storage”** is added under

Product → Device Information in Full Case Entry (FCE) only with following values o Yes o No

o

Unk (Unknown)

![](<.gitbook/assets/Unknown image (10)>)

Figure 10: Improper Use or Storage field under Device Information section

* **Impact on Other Products:** No impact on other products.

**5.4.2 Product > Device Information > Malfunction Type**

* **Jira ID:** PVCM-81255
* **Background / Purpose**: A new field, "Malfunction Type," has been added to the Device Information section to classify device malfunction.
* **Feature Description**: The field “Malfunction Type” is introduced in the Device Information section as a new codelist field.

![](<.gitbook/assets/Unknown image (11)>)

Figure 11: Malfunction Type field under the Device Information section

* **Impact on Other Products**: No impact on other products.

**5.4.3 New Case Fields for PMDA Japan**

* **Jira ID:** PVCM-66941
* **Background / Purpose**: The purpose of this enhancement is to support capturing additional information required for PMDA case processing & submissions in the Case Entry Form. These enhancements enable reporting of Japan-specific regulatory data.
* **Feature Description**: New fields specific to Japan PMDA reporting have been introduced across various sections of the Case Form. These fields enable the capture of PMDA-specific data and regulatory flags.
  * Fields span across modules such as General, Literature, Study, Product, Event.
  * Few fields (e.g., “First Receipt Date (J)”) are made available in Search Case, Case List & Intake Queue. o A new section “PMDA Information” has been added to Case Form. This is available only for Japanese Users.

![](<.gitbook/assets/Unknown image (12)>)

Figure 12: Field labels in PMDA Japan

* **Impact on Other Products**: No impact on other products.

**5.4.4 Display Granular Product Details in PE Matrix**

* **Jira ID:** PVCM-82345
* **Background / Purpose**: The purpose of this enhancement is to display product header information across the Product, Listedness, and Product Event Matrix sections to maintain consistent product sequencing, supports dynamic updates on sequence changes.
* **Feature Description**:
  * The system enhances product section headers with product name, strength, and formulation. o It synchronizes product sequence across both the sections: Listedness, and Product Event Matrix.
  * This functionality supports real-time updates via a refresh mechanism in the Listedness section, while tracking all changes through audit logs.

Figure : Product sequential

![](<.gitbook/assets/Unknown image (13)>)

Figure

13

:

Listedness

s

ection

![](<.gitbook/assets/Unknown image (14)>)

![](<.gitbook/assets/Unknown image (15)>)

Figure 14: Product event matrix sequential

* **Impact on Other Products**: No impact on other products.

**5.4.5 PVCM Japan UI – Japanese Date Format for Date Fields**

* **Jira ID:** PVCM-43908
* **Background / Purpose:** The purpose of this enhancement is to support Japanese date format in the PVCM user interface, enhancing localization and user experience for Japanese user.
* \*\*Feature Description:\*\*Date fields in the PVCM UI will now display in the Japanese format when the user's language preference is set to Japanese. This enhancement does not impact view of dates by Global Users.

![](<.gitbook/assets/Unknown image (16)>)

Figure 15: Japanese Date format in PVCM Japan

* **Impact on Other Products**: No impact on other products.

**5.4.6 PVCM J | First Receipt Date (J) & Version Receipt Date (J)**

* **Jira ID:** PVCM-90462
* **Background / Purpose:The purpose of this enhancement is to support automation for population of “First Receipt Date (J)” and “Version Receipt Date (J)” that has been added for Japan users.**
* \*\*Feature Description:\*\*This enhancement enables Japan users to manage local receipt dates across various case creation methods including default date population.
  * Fields auto-populate when opened by a Japan user for non-Japan-created cases.
  * Parsing support included for Email, S3, JSON, and E2B intake. o Japan-specific fields are editable, while global receipt dates remain unaffected. o Visible in case form, version information and case exports.

![](<.gitbook/assets/Unknown image (17)>)

Figure 16: First Receipt Date(J) and Version Receipt Date(J)

* **Impact on Other Products**: No impact on other products.

**5.4.7 PVCM Japan – PMDA Number Import**

* **Jira ID:** PVCM-45061
* \*\*Background / Purpose:\*\*A new read-only field, PMDA Number, is now introduced in the PVCM Japan UI. This field automatically captures the identification number received from the PMDA upon successful report transmission.
* \*\*Feature Description:\*\*A new read-only field PMDA Number, corresponding to E2B tag J2.1b, is now available in the PMDA Information section of the PVCM Japan User Interface. The system will auto-populate this field with the value received from the PMDA when an acknowledgment is successfully processed.

o The PMDA Number remains blank for initial submissions, regardless of whether the report is marked complete or incomplete.

![](<.gitbook/assets/Unknown image (18)>)

Figure 17: PMDA Number field in PMDA section

* **Impact on Other Products**: No impact on other products.

**5.4.8 Copy Case operation without Opening the Case Automatically**

* **Jira ID:** PVCM-87380
* **Background / Purpose**: To improve system performance and user control by allowing users to decide whether to open a copied case after the copy operation, preventing unnecessary delays in the case copy process.
* **Feature Description**:
* Upon performing a Copy action on a case, the application does not auto-open the copied case.
* A pop-up message appears on the same screen once the copy operation completes

![](<.gitbook/assets/Unknown image (19)>)

Figure 18: Case Copy Success Pop-Up

* This functionality applies when the Copy operation is performed from:
  * Case Entry Screen
  * Any Case Listing Screen

• **Impact on Other Products**: No impact on other products.

**5.4.9 Restrict Field Editability for Deleted, Rejected, Closed, and Finalized Cases**

* **Jira ID:** PVCM-107529
* **Background / Purpose**: To maintain data integrity and prevent unauthorized modifications to case data that is no longer active, the application now enforces controls on field and section editability for cases in **Deleted**, **Rejected**, **Closed**, and **Finalized** states.
* **Feature** **Description**:
  * Cases in Deleted, Rejected, or Closed states will now be fully displayed in read-only mode within the Case Entry Form, including all sections such as Attachments,

References, Tasks, Follow-up Queries, DQCR, and fields like Assigned Group, Assigned User, and Priority.

*
  * For **Deleted** cases, this read-only behaviour will apply consistently across **all versions** of the case, regardless of their individual status.
  * For Finalized cases, the system supports configurable settings to make the **Attachments** and **Case References** sections non-editable, providing flexibility based on business requirements.
* **Impact on Other Products**: No impact on other products.

**5.4.10 Conversion of “More Info” Field in Lab Test Section to a Dropdown**

* **Jira ID:** PVCM-84804
* \*\*Background / Purpose:\*\*The “More Info” field in the Lab Test(s) section was previously a checkbox, which by default transmitted “false” value when left unchecked—even when the user intended to leave it blank. This behavior led to inaccurate representation of data in downstream ICSR reports. To address this, the field is being updated to a dropdown, allowing a truly blank (unset) value, improving data accuracy and regulatory compliance.
* **Feature** **Description**:
  * The “More Info” checkbox in the Lab Test(s) section has been converted into a dropdown field with three possible values: blank (no selection), Yes, and No. o Legacy cases will be auto-mapped as follows:
    * If the checkbox was unchecked, the dropdown value will be No.
    * If the checkbox was checked, the dropdown value will be Yes.
  * The field supports a blank selection, meaning users can now intentionally leave it unset, and the system will not default to "false" during downstream ICSR transmissions.

Figure

19

:

More Info field as a dropdown

![](<.gitbook/assets/Unknown image (20)>)

* Impact on Other Products:
  * Impacts storage of “More Info” field value in PVD o Impacts the E2B ICSR reports in PVR

**5.4.11 Support for Saving Attachment Notes without Associated fFiles in Case Entry Form**

* **Jira ID**: PVCM-79084
* \*\*Background / Purpose:\*\*Previously, attachment records in the Case Entry Form required an associated file to be retained. As a result, it was not possible to retain or migrate note-only entries (e.g., from legacy systems). This enhancement allows users to save and retain attachment records that only include notes, enabling more flexibility for documentation and smoother data migration from external systems.
* Feature Description:
  * In the **Attachment(s)** section of the **Case Entry Form**, the system will now retain attachment records even if a file is not attached, as long as the **Notes** field contains a value.

![](<.gitbook/assets/Unknown image (21)>)

Figure 20: Attachment record with notes

*
  * A record will only be auto removed during case save/update if both the **Attachment File** and **Notes** fields are blank.
  * **Receipt Date**, **Process Status**, **Include in E2B**, and **Protected** fields will only be **enabled** when a file is selected in the **File Name** column.
  * **Receipt Date** will be auto populated with the **current date** when a file is selected and will remain **blank** by default.
  * The field label **“Attachment Type”** is renamed to **“Type”**. o Fields in Attachment(s) section will now appear in the following order: Case Version, Type, File Name, Receipt Date, Processing Status, Protected, Include in E2B, Notes.
* Impact on Other Products:
  * Impacts the E2B ICSR Reports in PVR

**5.4.12 Prevention of duplicate Name Part Type entries within Product and Drug records**

* **Jira ID**: PVCM-70892
* \*\*Background / Purpose:\*\*Previously, users could assign the same Name Part Type multiple times within a Product or Past Drug History record, which could lead to ambiguity or errors during downstream processing, reporting, or integration. This enhancement introduces validation to prevent duplicate Name Part Type entries within the same Product or Drug, ensuring data clarity and consistency.
* \*\*Feature Description:\*\*In the Name Part(s) section under both Product(s) and Past Drug History (Patient and Parent), the Name Part Type dropdown will now exclude values that have already been selected in other active (non-deleted) Name Part records within the same Product or Drug entry.

Example: If a Past Drug History entry for " Infusion pumps" already has a Name Part Type set to “Device Name”, that option will no longer be listed for selection in another Name Part row under the same " Infusion pumps" record.

* **Impact on Other Products**: No impact on other products.

**5.4.13 Standardization of Field Labels for Gestation Period and Name/Initials**

* **Jira ID**: PVCM-65468
* \*\*Background / Purpose:\*\*To ensure consistency across all modules and products in the PV Suite (such as PVR, PVS), key field labels related to patient initials and gestation periods are being standardized. These changes help eliminate discrepancies in field terminology across various system interfaces, exports, and documentation, aligning with industry standards and improving user clarity.
* \*\*Feature Description:\*\*The following default field labels have been updated across all relevant modules in PVCM. This change ensures consistent naming throughout the application, including UI screens, exports, imports, and supporting tools:
  * Patient > Name / Initials: Patient Initials o Parent > Name / Initials: Parent Initials
  * Products > Exposure Gestation Period: Earliest Exposure Gestation Period
  * Pregnancy Information > Gestation Period at AE Onset: Gestation Period at Earliest AE

Onset o Study Browser > Project Number: Study Program

* **Impact on Other Products**: Impacts field labels displayed in PVR and PVS.

**5.4.14 Standardization of field labels for Product**

* \*\*Jira ID:\*\*PVADMIN-42369,**PVCM-86018**
* \*\*Background / Purpose:\*\*To achieve uniform terminology across the PV Suite the labels for **Product Name** and **Trade/Investigational Name** fields are being harmonized. This ensures consistency across all modules, improves clarity for users, and aligns with regulatory and system documentation expectations.
* \*\*Feature Description:\*\*The following field label changes have been applied across PVCM and PVAdmin:

o

Product Name: Product Set

o

Trade / Investigational Name: Product Name

Figure

21

:

Product Configuration screen

![](<.gitbook/assets/Unknown image (22)>)

![](<.gitbook/assets/Unknown image (23)>)

Figure 22: Study Configuration screen

![](<.gitbook/assets/Unknown image (24)>)

Figure 23: Product Dictionary Browser

* Impact on Other Products: Impacts field labels in PVR and PVS

**5.4.15 Automatic Locking of Local Fields and Datasheets after Local Case Processing Completion**

* **Jira ID:PVCM-98848, PVCM-98849**
* \*\*Background / Purpose:\*\*To maintain data integrity in local regulatory workflows, this enhancement restricts further edits to specific local fields and listedness datasheets once local case processing is marked as complete, ensuring compliance with country-specific regulatory requirements.
* **Feature** **Description**:
  * The application supports the configuration of local country field profiles, which determine which local case fields and datasheets remain editable during case processing after the case has been finalized. By default, predefined field profiles for **China** and **Korea** are available in the system.
  * When a case transitions to the Final state, only local fields and listedness (datasheet) values associated with an ICSR profile that has a scheduled report for the case will remain editable. This ensures that such fields are editable only when the case qualifies for submission to the corresponding country. For example, China-specific fields will remain editable if a China ICSR report is scheduled.
  * Once the Local CP Completed checkbox is selected for a local ICSR report (e.g., China), the associated local fields and datasheets will automatically become read-only, ensuring that no further edits are allowed.
* **Impact on Other Products**: Impacts the E2B ICSR reports in PVR

**5.4.16 Parent Case Number in Reference Section when Case is Copied/Split**

* **Jira ID**: PVCM-99884, PVCM-106765
* **Background / Purpose**: The purpose of this enhancement is to provide to automatically populate and manage parent-child case linkages during copy or split case actions in the Reference section. This includes auto-population of other Reference fields, and hyperlink navigation.
* **Feature Description**: System has been enhanced to maintain parent-child case linking between the newly created case/cases and parent case when a case is copied/split. In addition to automated capability, system provide flexibility to manually add the record to maintain the parent-child linkage using default reference types.

![](<.gitbook/assets/Unknown image (25)>)

Figure 24: Reference section on Copy/Split case

* **Impact on Other Products**: No impact on other products.

### 5.5 Feature: Follow-up Case Intake/Amendments

**5.5.1 Accept as Follow Up Operation without Opening the Case Automatically**

* **Jira ID:** PVCM-110811
* **Background / Purpose**: To improve system performance and user control by providing an option to open the follow-up case manually after the follow-up operation, avoiding unnecessary delays caused by automatically opening the case.
* **Feature** **Description**:
  * Existing loader is replaced with a percentage loader during ‘Accept as Follow-Up’ and ‘Create as Follow-Up’ operations.
  * Post-operation, the application displays a pop-up confirmation message with options to:

▪ Open Follow-Up (opens case in same tab)

▪

Return to (closes pop

*

up)

![](<.gitbook/assets/Unknown image (26)>)

Figure 25: Follow Up Case Success Pop-Up

*
  * No automatic redirection to the follow-up case after these operations. o Applied to actions from Follow-Up Duplicate Search Screen, Case Entry Screen, Case List, Intake Queue, Case List and Intake Queue Widget, New Follow-Up option from left panel, and Version Type field.
* **Impact on Other Products**: No impact on other products.

**5.5.2 Ordering of Repeatable Section Records during FU Data Merge**

* **Jira ID:** PVCM-58905
* **Background / Purpose**: To maintain consistency and preserve the original sequence of processed records, the system now prioritizes the ordering of repeatable section data based on the previous case version when a new follow-up is accepted. This enhancement minimizes the need for manual reordering after the follow-up data merge.
* \*\*Feature Description:\*\*When accepting an incoming case as a follow-up to an existing case— either manually or automatically—the system applies the following rules to maintain the sequence of repeatable section records:
  * Records from the previous version (e.g., Events) retain their original order in the follow-up after the data merge. o New records present in the follow-up are appended in sequence after the merged records from the previous version.
  * Example: If the previous version had “Fever” followed by “Headache,” and the follow-up includes a new event “Rash,” the merged follow-up will display the events in the following order: Fever, Headache, Rash.
* **Impact on Other Products**: No impact on other products.

**5.5.3 Auto-merge of Follow-up Case Data on Accept Action**

* **Jira ID:** PVCM-66717
* **Background / Purpose**: The application supports parallel follow-up processing by allowing a follow-up to be created in New state while the previous version is still Active and under processing. With this enhancement, when the New follow-up is accepted after the Active version is finalized, any data added during the previous version’s processing is automatically merged into the follow-up, ensuring data consistency and reducing manual effort.
* **Feature** **Description**:
  * When a follow-up in the New state is accepted using the “Accept” action from the Actions menu, the application now automatically merges data from the previous valid version into the follow-up, similar to the behavior of the “Accept as Follow-up” action
  * To ensure smooth system operation and avoid processing issues, the application displays an error message and prevents selection of more than 10 cases for the “Accept” action through bulk operations if any of the selected cases is a follow-up or amendment in the New state.
* **Impact on Other Products**: No impact on other products.

**5.5.4 Support for Merging Native Language Product Data during Follow-up Acceptance**

* **Jira ID:** PVCM-82020
* **Background / Purpose**: During follow-up acceptance, product data from the previous version is merged into the new follow-up to ensure continuity of the processed data, provided the relevant configuration is enabled. However, native language fields such as localized product names (e.g., Product Name in Chinese) were previously not included in this data merge. This enhancement ensures that localized product data is consistently carried forward into the follow-up, improving data completeness and reducing manual effort.
* **Feature** **Description**:
  * When a new follow-up is accepted and product data is merged from the previous version, native language values for the **Product Name** and **Generic Name** fields are also carried forward into the follow-up. This applies when the application is configured to retain product details from the previous version for matching products.
  * Example: If a case contains a product with the English name “Paracetamol” and a native language value “对乙酰氨基酚” (Chinese for Paracetamol), and the same product is present in the incoming follow-up but without the native language value, the localized entry will be automatically retained and merged into the follow-up version when it is accepted as follow-up.
* **Impact on Other Products**: No impact on other products.

**5.5.5 Retain Product and Drug Information from Previous Version based on Coding**

* **Jira ID:** PVCM-72207
* **Background / Purpose**: Previously, product and past drug history records were merged during follow-up acceptance regardless of their coding status, which could lead to unintended data overwrites. This enhancement refines the merge logic to apply only under specific, controlled conditions based on coding status and source, ensuring more accurate and consistent data handling.
* **Feature Description:** The application now supports conditional carry-forward of product and drug information from the previous version during Accept and Accept as Follow-Up operations. This behavior applies only when records match based on the configured primary identifier (e.g., Product ID).
  * Product information is carried forward to the follow-up version for matching records only if the product is either non-coded or coded via WHO Drug Dictionary in the follow-up being accepted.
  * Example: In the previous version, a product “Atorvastatin” is coded using the Company Product Dictionary. In the follow-up version, the same product (matched by Product ID) is non-coded. During the Accept as Follow-Up operation, the coded information from the previous version will be replaced into the follow-up version.
  * Drug name and related fields are carried forward for matching records in the Past Drug History section only if the drug is non-coded in the follow-up version being accepted.
* **Impact on Other Products**: No impact on other products.

**5.5.6 Accept as Follow Up Support for PVCM J**

* **Jira ID:** PVCM-90515
* **Background / Purpose**: The purpose of this enhancement is to extend the **‘Accept as Follow-Up’** functionality for Japanese cases.
* \*\*Feature Description:\*\*The application has been enhanced to support the "Accept as FollowUp" feature for Japanese cases, aligning its behavior with the existing functionality available for global cases. Users can now manually accept a case as follow-up or leverage the system's automated logic to identify follow-up cases based on key identifiers.
* **Impact on Other Products**: No impact on other products.

### 5.6 Feature: Case Workflow / User Group Assignment

**5.6.1 Default User Group Assignment**

* **Jira ID:** PVCM-109362
* **Background / Purpose**: The purpose of this feature is to automatically assign a default user group to incoming cases based on sender, receiver, or language information. This functionality improves case routing accuracy and efficiency across multiple intake methods, including Email, S3, JSON, and E2B.
* **Feature Description**: The system now supports configurable default user group assignment based on detected or provided language during case intake.

o Case Intake methods:

*
  * **Email (Structured/Unstructured)-** The default user group for Email based on language is configurable via Application config (PV Case Management). In case user group is not configured then by default system will choice “Case Intake”.
  * **S3 Intake -** The default user group based on ML-detected language is configurable via Application config (PV Case Management). In case user group is not configured then by default system will choice “Case Intake”.
  * **E2B and JSON –** The default user group is now configurable for E2B and JSON intake respectively via application config.

![](<.gitbook/assets/Unknown image (27)>)

Figure 26: Default User Group Assignment(E) through different Case intake process

![](<.gitbook/assets/Unknown image (28)>)

Figure 27: Default User Group Assignment(J) through different Case intake process

* **Impact on Other Products**: No impact on other products.

**5.6.2 Local Case Processing**

* **Jira ID:** PVCM-94306
* **Background / Purpose:** The system is now enhanced to support Japanese Local case processing by introducing a Local Case State, Local Due Date, Japan-specific workflow states,

and segregation of Global vs. Local fields. This allows Japan users to independently enter and finalize localized data post-global case finalization while preserving the integrity of global data.

* **Feature Description:** The system has been enhanced to introduce a dedicated Japan case processing workflow, distinct from the global case processing workflow. This new workflow ensures that Japan-specific case processing operates independently, streamlining compliance with local regulatory requirements. For foreign cases to Japan, moved from the global case processing workflow to the Japan case processing workflow, all global fields will be locked to prevent further editing. Only fields required for PMDA reporting, such as PMDA Information, will remain editable in the system to support accurate and efficient regulatory submissions.

![](<.gitbook/assets/Unknown image (29)>)

Figure 28: Local Case State and Local Due Date in PVCM Japan

* **Impact on Other Products**: Impacts the Japan report in PVR.

**5.6.3 Parallel Case Processing**

* **Jira ID:** PVCM-96655
* **Background / Purpose:** The system is now enhanced to support parallel processing of cases for Global and Local Case Versions, allowing local entities (e.g., Japan) to manage localized data workflows independently while the global version continues through its lifecycle.
* **Feature Description:** The application now allows Global and Local Case Versions to be processed in parallel, enabling local users to begin localized workflows (e.g., PMDA submission) even as global case processing continues to process next versions of the same case. The system enforces version control, ensuring the Japan case version can never exceed the Global version.

![](<.gitbook/assets/Unknown image (30)>)

Figure 29: Japan workflows for parallel processing of cases

* **Impact on Other Products**: No impact on other products.

**5.6.4 Automatic Assignment of Case State and Local Case State based on Workflow Rule**

* **Jira ID:** PVCM-82342
* **Background / Purpose:** This feature enables automatic case state and local state transitions when a case is assigned to a workflow group, based on configurations in the associated workflow rule. It includes handling for error conditions, bulk assignment limits, message displays, and ensure validation checks.
* **Feature Description:** The system auto-updates Case State or Local State upon workflow group assignment, based on configured Preferred values in workflow rules. Valid transitions only occur when allowed by system logic. DQCR blocks transitions if errors exist, and detailed user messages support both manual and bulk workflows.

![](<.gitbook/assets/Unknown image (31)>)

Figure 30: Case State and Local Case State changed based on workflow rule

* **Impact on Other Products**: No impact on other products.

**5.6.5 Japan Workflow Eligibility Identification on Listing Screen**

* **Jira ID:** PVCM-111932, PVCM-105965
* **Background / Purpose:** A new field, “To JP Workflow Group,” has been added to the Case Listing screen to indicate eligibility for Japanese Case Processing. Users can now bulk assign eligible cases for transfer to the Japan workflow, enhancing operational efficiency.
* \*\*Feature Description:\*\*A new field “**To JP Workflow Group**” has been introduced in the Case Listing screen. This field displays the next eligible user group based on the case’s routing logic, as configured in PV Admin → Case Workflow. It is particularly useful during bulk assignments by highlighting the appropriate Japan workflow group to which the case should transition next. The field is not shown on the case form and is available under Optional Fields, once a case enters a Japan workflow or reaches a local final state, the evaluation pauses and resumes only if the case returns to a non-Japan workflow.

![](<.gitbook/assets/Unknown image (32)>)

Figure 31: New Field to identify cases which are eligible for Japan Workflow

* **Impact on Other Products**: No impact on other products.

### 5.7 Feature: Generic AE Form Parser

**5.7.1 Support for Editable PDF Parsing in PVCM**

* **Jira ID:PVCM-104646**
* **Background / Purpose:The system has been enhanced to support the parsing of Editable PDFs in PVCM, offering the same functionality as Digital PDFs. This ensures data mapping and supports multilingual inputs.**
* **Feature Description**: Editable PDFs are now supported in PVCM, providing the same capabilities as Digital PDFs.

![](<.gitbook/assets/Unknown image (33)>)

Figure 32: Parsing support of Editable PDFs in PVCM

* **Impact on Other Products**: No Impact to any other module of PVCM.

**5.7.2 ML - Japan Form Intake Support in PVCM**

* **Jira ID**: PVCM-82203
* \*\*Background / Purpose:\*\*This enhancement introduces support for structured AE Intake forms in Japanese (Digital PDF format), allowing the system to automatically extract and encode data fields using a pre-trained ML model.
* **Feature Description**: The system now supports the Digital Japan AE Intake Form as a default pre-trained form for automated extraction of AE data field values, including Japanese fields, using the Machine Learning-based AE Parser. This enhancement enables multilingual case intake by parsing structured native language forms and mapping data into PV Case Management fields.\*\*\*\*
* **Impact on Other Products**: No Impact to any other module of PVCM.

**5.7.3 Populate Sender Name from ML Intake form instead of Email Username**

* **Jira ID**: PVCM-84598
* \*\*Background / Purpose:\*\*The system has been enhanced to intelligently populate the "Sender Name" in the General section of email intake cases. This ensures improved accuracy by prioritizing the most reliable data source during machine learning (ML) form parsing.
* \*\*Feature Description:\*\*The system now supports hierarchical logic to populate the "Sender Name" field in the General section of cases created via email intake.
  * Priority is given to sender names matched via ICSR organization unit configured in PVR. o If unavailable, the parsed text value is used.
  * If both are missing, the email sender's name is used as fallback.

![](<.gitbook/assets/Unknown image (34)>)

Figure 33: Populate Sender Name instead of email username from ML Intake

* **Impact on Other Products**: No impact on other products.

### 5.8 Feature: Case Intake via Email Box

**5.8.1 Encoding of Products for Japanese AE for Email and AWS S3**

* **Jira ID:** PVCM-72277
* **Background / Purpose**: The application now supports automatic detection of the source language during case intake (via Email or AWS S3) and enhanced product auto-coding using the J Drug Dictionary when Japanese is the detected language. This improves localization and reduces manual coding efforts for Japan-specific cases
* **Feature** **Description**:
  * The source language is determined based on the configuration of the AE Intake Email box or AWS S3 folder. If not set, the default is English.
  * When the source language is Japanese, and the J Drug Dictionary is available, the system attempts product auto-coding using defined matching logic with fallback from CDD to J Drug Dictionary.

![](<.gitbook/assets/Unknown image (35)>)

Figure 34: Reported language field detected source language automatically

* **Impact on Other Products**: No impact on other products.

#### 5.8.2 Send an Acknowledgement E-mail when the Case is Accepted

* **Jira ID:** PVCM-106409
* **Background / Purpose:** For cases created via E-mail Intake, acknowledgement e-mails with the assigned Intake # were sent at the time of case creation. This enhancement adds the ability to send an additional acknowledgement notification upon case acceptance, which includes the finalized Case Number to aid accurate reconciliation by senders and partners.
* \*\*Feature Description:\*\*The application now automatically sends an acknowledgement e-mail to the sender when a case received via E-mail Intake is accepted as an initial case, a followup, or merged into an existing active case. These acknowledgement e-mails are sent in the language configured for the receiving mailbox.
* **Impact on Other Products**: No impact on other products.

#### 5.8.3 Email Intake Acknowledgement for PVCM J

* **Jira ID:** PVCM-83301
* **Background / Purpose:** An automated acknowledgment email feature has been implemented for Email Intake. Upon successful case creation, the system sends a confirmation email to the sender with key case details.
* \*\*Feature Description:\*\*The system now sends configurable acknowledgment emails when a case is created through structured or unstructured Email Intake.

o Auto-sends email to sender’s address with key case information o Subject/body content is configurable via metadata o Supports Japanese language and date formatting o Design supports future language and template expansion

![](<.gitbook/assets/Unknown image (36)>)

Figure 35: Automated Email Acknowledgment

* **Impact on Other Products**: No impact on other products.

## 5.9 Feature: Listedness

#### 5.9.1 Undesirable Effects / Datasheet Configuration

* **Jira ID:** PVCM-106408
* **Background / Purpose:** The system has been enhanced for supporting Advanced autolistedness logic to dynamically calculate and justify listedness values based on extended attribute configurations of undesirable effects for configured datasheets.
* **Feature Description**: Advanced listedness now uses configured auto-listedness values for dynamic assessment.
  * System recalculates listedness on Create, Update, or Refresh.

▪ If the case data matches the configured rule, the Listedness value will be flipped (i.e., switched from listed to unlisted or vice versa).

*
  * Auto-populates justification with attribute names and values.
  * Allows manual override and disables further auto-updates.

![](<.gitbook/assets/Unknown image (37)>)

Figure 36: Advanced Auto-Listedness

* **Impact on Other Products**: No impact on other products.

#### 5.9.2 Rename Event Name (Start Date) Column in Listedness Section

* **Jira ID:** PVCM-93180
* **Background / Purpose:** 'Event Name (Start Date)' column in Listedness has been renamed to 'Event Name' to avoid confusion, as it displays both the Event Start Date and the First Receipt Date based on case type.
* **Feature Description**: The 'Event Name (Start Date)' column in the Listedness section has been renamed to 'Event Name’.

![](<.gitbook/assets/Unknown image (38)>)

Figure 37: Listedness Section

*
  * An ‘i’ icon is added after the coding icon in the Event Name column. Hovering over the icon displays:
    * First Receipt Date: If the value is derived from the First Receipt Date field.
    * Event Start Date: If the value is derived from the Event Start Date field.
  * These changes, including the column renaming and date format updates, are also reflected in the case PDF export.
* **Impact on Other Products**: No impact on other products.

## 5.10 Feature: Case Data Translations

#### 5.10.1 Auto-Translation form Local language to English

* **Jira ID:** PVCM-92963, PVCM-92969
* \*\*Background / Purpose:\*\*The purpose of this feature is to allow users to auto-translate supported case fields into the target language, based on system configuration and field eligibility.
* **Feature Description**: A New Auto-Translate Button has been added to the Translation View. The feature supports free-text, MedDRA Reported Descriptions, and non-coded Product Name/Study Number fields. Translations apply only to the current case version and require user confirmation if source data changes after a prior translation. This functionality is available only to users with Translation View access and is governed by system configuration.

![](<.gitbook/assets/Unknown image (39)>)

Figure 38: Auto Translate button

* **Impact on Other Products**: No impact on other products.

#### 5.10.2 Dual Language Translation Screen

* **Jira ID:** PVCM-92953, PVCM-92960
* \*\*Background / Purpose:\*\*A new “Translation View" option has been introduced under the View menu, enabling dual-language display and limited editing functionality of case data in both Source and Target languages (e.g., Japanese ↔ English). This feature supports multilingual case processing and usability for global and local users.
* **Feature Description:** The Translation View feature allows users to view and selectively edit case data side-by-side in the Source Language and the Target Language. It is available across multiple screens: Basic Case Entry, Full Case Entry, Case List and Intake Queue. This functionality is permission-based, available only to users with the “Translation View” role configured in PV Admin or those assigned PVCM Super User role. Source Language view is non-editable by default; Target panes support editing of localized fields only, with switchable edit modes and user warnings. Translation View does not apply to Reporter Web Forms or Follow-Up Diff screens.

![](<.gitbook/assets/Unknown image (40)>)

Figure 39: Translation View feature in PVCM J

* **Impact on Other Products**: No impact on other products.

## 5.11 Feature: Multi-Lingual UI

#### 5.11.1 PV Case Management - Japanese UI

* **Jira ID:** PVCM-72108
* **Background / Purpose:** The application is now enhanced to support complete Japanese language display across the PV Case Management UI when the user’s preferred language is set to Japanese. This ensures a localized experience for Japanese users and aligns with PMDA regulatory requirements.
* **Feature Description**: When a user sets their preferred language to Japanese, the application will display all supported User Interface text elements in Japanese.

o This includes:

*
  * Labels and help text on the Case Form.
  * All field labels and dropdown values (including Optional Fields) on listing screens.

![](<.gitbook/assets/Unknown image (41)>)

Figure 40: PV Case Management UI for Japanese preferred language

* **Impact on Other Products**: No impact on other products.

#### 5.11.2 Multilingual: Japanese Support for Search in Listing S

#### 5.11.3 creens

* **Jira ID**: PVCM-74059
* **Background / Purpose:The system now supports Japanese language which has been introduced for the Follow-up/Duplicate Search, Intake Queue, and Case List screens. This enhancement ensures full localization of field labels, values, date types, and exported content to improve usability and accessibility for Japanese users.**
* **Feature Description**: Support for Japanese localization is enabled across key case listing screens to ensure proper language display and formatting.
  * Field labels and dropdown values are displayed in Japanese.
  * Date types are localized with standard Japanese formats (YYYY/MM/DD).
  * Exported Excel files retain Japanese field labels and values. o Localization applies based on language preferences or source language.

![](<.gitbook/assets/Unknown image (42)>)

Figure 41: Japanese support for search in listing screens

* **Impact on Other Products**: No impact on other products.

#### 5.11.4 PVCM English Code List Values Translation in Japanese

* **Jira ID:PVADMIN-39189**
* **Background / Purpose:The system now supports multilingual display of codelist values in the PVCM UI. When the user's preferred language is set to Japanese, all codelist values (excluding abbreviations) are displayed in Japanese.**
* **Feature Description**: PVCM now displays translated codelist values for Japanese users across the UI for improved accessibility.
  * If user language is set to Japanese, codelist values display in Japanese (excluding abbreviations).
  * English values are shown if Japanese translation is unavailable. o Translations are managed via the CSD with language = JA records. o An Excel file containing all translated values is attached to the story.
* **Impact on Other Products**: No impact on other products.

#### 5.11.5 PVADMIN – PMDA DQCR Rules

* **Jira ID:PVADMIN-44188**
* **Background / Purpose:The system has been enhanced to support PMDA-specific DQCR rules through PV Admin, enabling import/export, configuration, and modification of these rules with Japan regulatory requirements.**
* **Feature Description**: PMDA-specific DQCR rule configuration is now supported through the PV Admin Import/Export module.

o Existing feature is extended to include PMDA-specific DQCR rules. o Admin users can import/export and manage PMDA rule configurations. o Existing functionality for DQCR rule modification remains supported. o Enhancements ensure alignment with Japan compliance standards.

* **Impact on Other Products**: No impact on other products.

## 5.12 Feature: Null Flavors

#### 5.12.1 Null Flavor Support in PVCM J

* **Jira ID:** PVCM-82364
* **Background / Purpose**: The application now supports Null Flavor data entry for Japanese fields in the Case Entry screens. This feature supports bi-directional synchronization across English and Japanese Null Flavor fields.
* **Feature** **Description**:

o System allows Null Flavors entry for specific fields, configurable via metadata. o When a Null Flavors is selected in English, the system auto-populates the corresponding Japanese field and vice versa.

![](<.gitbook/assets/Unknown image (43)>)

Figure 42: Configuring Null flavor in PVCM J

* **Impact on Other Products**: No impact on other products.

### 5.13 Feature: Study Browser/ Encoding

**5.13.1 Encoding Studies in PVCM J**

* **Jira ID:** PVCM-92388
* **Background / Purpose**: The system has been enhanced to support the Japanese language, with encoding for Studies added in PVCM. Users with Japanese as their preferred language can now search, select, and code Studies in Japanese across relevant fields.
* **Feature Description**: Users with the Japanese language setting can search and code Studies using Japanese values.
  * Type-ahead and browser search now support Japanese Study Numbers. o Auto-population of values configured in PV Admin i.e. Study Name and Study Type are displayed in Japanese.
  * Deleting coded values triggers cleanup and auto-translation if enabled.

![](<.gitbook/assets/Unknown image (44)>)

Figure 43: Encoded Study in PVCM J

* **Impact on Other Products**: No impact on other products.

### 5.14 Feature: WHO / MFDS Drug / J Drug Browser and Encoding

**5.14.1 Encoding of Products via J Drug Dictionary**

* **Jira ID:** PVCM-46339
* **Background / Purpose**: Support for J Drug Dictionary has been added to enable Japanese users to encode Products and Past Drugs directly from the Japanese drug dictionary.
* **Feature Description**: J Drug Dictionary Browser is introduced for Product and Past Drug fields, available in different case forms.
  * Japanese users can encode Products via J Drug Dictionary.
  * J Drug icon beside the Product Name or Drug Name field instead of the WHO Drug Dictionary appears when preferred language is Japanese.
  * Similar browser layout as the existing WHO Drug Browser for J drug dictionary in Product and Past Drug fields.

![](<.gitbook/assets/Unknown image (45)>)

Figure 44: Product Coded from J Drug Dictionary

* **Impact on Other Products**: No impact on other products.

### 5.15 Feature: Product Browser/ Encoding

**5.15.1 Device Model Number Field**

* **Jira ID:** PVCM-67047
* **Background / Purpose**: A new field is added to the system as Device Model Number field for company device products using PV Admin product configuration, ensuring consistency and minimizing manual data entry.
* **Feature Description:The Device Model Number field in the Device Information section is auto filled from the PV Admin configuration for company products.**
  * Auto populated and non-editable for company products. o Editable for non-company products or when model number is not configured. o Supports both manual encoding and automated intake methods. o Re-coding a product reflects updated configuration values.

Figure

45

:

Device Model Number field in PV

*

Admin

![](<.gitbook/assets/Unknown image (46)>)

Figure

46

:

Device Model Number field in PVCM

![](<.gitbook/assets/Unknown image (47)>)

* Impact on Other Products:
  * Impacts the report on PVR. o Impacts the PVS product on Alerts.

**5.15.2 Configuration Switch | Company Products**

* **Jira ID:** PVCM-88981
* **Background / Purpose:A new configuration switch, “Company Products,” has been introduced to restrict the Product Browser to display only company products during case intake and processing. This enhancement ensures data accuracy and better product selection control for clients that require this level of filtering.**
* \*\*Feature Description:\*\*A configurable switch has been added to enable or disable the display of non-company products in the Product Browser during case creation and processing workflows.
  * The switch is disabled by default for all clients.
  * When enabled, users will only see and select company products (C) in the Product Browser.
  * Product Library and configuration modules remain unaffected.

![](<.gitbook/assets/Unknown image (48)>)

Figure 47: ‘Company Product’ configuration switch

![](<.gitbook/assets/Unknown image (49)>)

Figure 48: Non-Company Products not visible in Product Browser

* **Impact on Other Products**: No impact on other products.

**5.15.3 Auto-population of MFDS Drug Code, WHO Drug Code, and WHO Drug MPID from Product Configuration**

* **Jira ID:** PVCM-66991
* **Background / Purpose**: This enhancement eliminates the need for users to manually enter standard codes such as MFDS Drug Code, WHO Drug Code, and WHO Drug MPID for company products during case data entry. The codes are now auto-populated from product configuration wherever possible, improving data accuracy and efficiency in case processing.
* \*\*Feature Description:\*\*When a product is coded (manually or automatically) in a case using product configuration including selection of study products or during recoding, the system will auto-populate the MFDS Drug Code, WHO Drug Code and WHO Drug MPID field values using the configured values from Product Configuration.
  * Fields remain editable to allow manual entry if auto-population is not possible.
  * On modifying Dosage Form or Strength, the fields are auto refreshed based on the updated combination.
  * WHO Substance Code, MFDS Substance Code and WHO Dict Ver B/C field values are also auto-populated based on the configured WHO Drug and MFDS dictionaries.
* **Impact on Other Products**: No impact on other products.

### 5.16 Feature: MedDRA Browser/Encoding

**5.16.1 PVCM Support MedDRA J Dictionary**

* **Jira ID:** PVCM-89478
* **Background / Purpose**: The system has been enhanced to support encoding via non-current terms in the Japanese MedDRA browser. This enables users to search and select from both current and non-current terms while performing data entry for Japanese language users.
* **Feature Description**: Enhancements have been made to the MedDRA browser for Japanese users to include non-current term search capabilities.
  * A new checkbox, “Include non-Current Terms,” appears for Japanese language users in MedDRA-coded fields.
  * When selected, the browser includes non-current MedDRA terms in the search results. o Non-current terms are marked with an ‘N’ icon. o Both Japanese and English hierarchies are displayed upon selection.

![](<.gitbook/assets/Unknown image (50)>)

Figure 49: Include Non-Current Terms checkbox

* **Impact on Other Products**: No impact on other products.

**5.16.2 Encoding with MedDRA J Dictionary**

* **Jira ID:** PVCM-46338
* **Background / Purpose**: The system has been enhanced to enables users to encode MedDRA fields in the Case Entry screen using the MedDRA J dictionary for Japanese language support when PVCM is configured as the safety system. It ensures bilingual support, correct MedDRA hierarchy display, and consistent user language preferences.
* **Feature** **Description**:
  * Enable encoding of MedDRA fields using the MedDRA J dictionary for Japanese users.
  * Ensure hierarchy (SOC, HLGT, HLT, PT, LLT), auto-translation, language-specific field behaviors, and synchronization with English MedDRA.
  * Rename ‘Translated Event’ to ‘Reported Event (English)’ and manage field visibility as per user language.
* **Impact on Other Products**: No impact on other products.

### 5.17 Feature: Data Quality Check

**5.17.1 DQCR Rules based on Allowed Length of Fields as per ICH E2B R2 and FDA eMDR**

* **Jira ID:** PVCM-83561
* **Background / Purpose**: The field lengths in the Case Form are designed based on ICH/EMA E2B R3 standards. However, regulatory submissions to ICH E2B R2 and FDA eMDR require different length limits for some fields. This enhancement introduces DQCR rules that help users proactively identify and correct any field values exceeding these regulatory limits during case processing.
* **Feature Description**: New DQCR rules have been introduced to validate field lengths specific to ICH E2B R2 and FDA eMDR regulatory profiles. These rules generate errors in the Data Quality Check Report (DQCR) when character counts exceed the permitted limits defined by these regulations.
* **Impact on Other Products**: This enhancement impact is limited to Data Quality Check Report

**5.17.2 DQCR related to PMDA Regulation**

* **Jira ID:** PVCM-96434
* **Background / Purpose**: The PVCM system has been enhanced to support PMDA-specific Data Quality Check Rules (DQCRs). This functionality extends the existing DQCR framework to cater to Japan-specific regulatory requirements while maintaining compatibility with global configurations. Japan users will see both PMDA and global checks (for applicable fields), whereas global users will experience no change.
* **Feature Description**: The system now supports PMDA-specific DQCRs to meet Japan regulatory standards. o PMDA-specific DQCRs will:
  * Be triggered only when the logged-in user is a Japan (PVCMJ) user.
  * Follow the same navigation, display, and error/warning formatting as existing Global DQCRs.
  * Common Field Handling: PVCMJ users will see both PMDA-specific and global DQCRs for fields (based on configuration).
  * The DQCR description will continue to appear in the user’s preferred language, as configured.
* **Impact on Other Products**: No impact on other products.

### 5.18 Feature: Generic AI Form Parser

**5.18.1 ML Form Parsing Extended for Cause Type, Strength and Substance**

* **Jira ID:PVCM-86050, PVCM-112865**
* \*\*Background / Purpose:\*\*The system has been enhanced to support automatic parsing and population of the following fields using machine learning (ML) extracted data during case intake:
  * Death Cause(s) > Cause Type o Product(s) > Strength o Product(s) > Substance(s)
* **Feature Description**: As part of this enhancement, the application now supports ML-based field population using the following logic:
  * \*\*Death Cause(s) > Cause Type:\*\*The **"Cause Type"** field is now auto-populated based on ML-extracted death-related information.
  * **Product(s) > Strength:** System is enhanced to include additional attributes to map incoming products strength and substance(s) for incoming structured forms.

![](<.gitbook/assets/Unknown image (51)>)

Figure 50: ML Form parsing for Cause Type

***

![](<.gitbook/assets/Unknown image (52)>)

Figure 51: ML Form parsing for Substance(s) and Strength

* **Impact on Other Products**: No impact on other products.

### 5.19 Feature: MedDRA Auto-coding

**5.19.1 MedDRA Auto-coding Integration with PVCM**

* **Jira ID:** PVCM-12178, PVCM-12179, PVCM-12183, PVCM-12184
* **Background / Purpose**: This system has enhanced to support intelligent MedDRA autocoding capabilities in PV Case Management. It leverages historical MedDRA-coded data and advanced large language models (LLM) to predict, auto-code, and recommend medical terms for verbatims in Events, Lab Tests, Medical History, and Indications fields. The enhancement supports both auto-created and manual entered cases.
* **Feature Description**: The system now supports auto-coding for cases created via automated channels (e.g., AE Forms, XML, S3) by checking for exact case-insensitive matches in the MedDRA dictionary. If no match is found, the Intelligent MedDRA Coding API predicts top MedDRA LLT matches using historical client data and LLMs, disregarding non-current terms and leaving fields uncoded if results are below threshold. Manual coding is enhanced with an Intelligent Coding icon in the UI for Reported Reaction and Event fields (English), allowing users to select and code predicted terms.
* **Impact on Other Products**: No impact on other products.

### 5.20 Feature: Case Deletion/Nullification

**5.20.1 Standard Justification for Case Actions**

* \*\*Jira ID:\*\*PVCM-92604, PVCM-82325, PVCM-109320
* **Background / Purpose**: Support for configurable standard justifications has been introduced across various case actions, ensuring consistent data capture, multilingual support. A language-specific justification dialog with dropdown-based selection and user-defined entry is now available.
* **Feature Description:** The Justification dialog box has been enhanced to support standard Justification dropdowns along with the ability to capture language-specific justifications based on user selection.
  * Multilingual support for standard justifications across various actions such as delete, reject, close, product deletion, study re-coding, reporting category change from a previous case version, task deletion, and more. o The dialog now offers a list of predefined standard codelist values, support for userdefined input, and a language selection option.
  * Justifications can be captured in both English and the relevant local language(s).
  * The display of the justification dialog is configurable via a CMT parameter. Specific actions can be excluded from requiring justification based on system configuration.

![](<.gitbook/assets/Unknown image (53)>)

Figure 52: Standard Justification dialog box in PVCM

* **Impact on Other Products**: No impact on other products.

**5.20.2 Manage Justification for Multiple Actions**

* \*\*Jira ID:\*\*PVADMIN-45761
* **Background / Purpose**: A new "Justification Details" template has been introduced to standardize and manage reasons provided for key case actions such as deletion, rejection, and data modifications. This multilingual-enabled functionality and supports dynamic configuration via PV Admin and codelist controls.
* **Feature Description:** The system now supports action-based justification prompts through a configurable “Justification Details” template.
  * The template manages justifications per action like delete/reject/update. o It includes groupings for relevant value subsets per action.
  * A new “Justification Actions” codelist and audit logging are enabled. o The feature is multilingual and configurable via PV Admin.
* **Impact on Other Products**: No impact on other products.

### 5.21 Feature: PV Suite – Central Field Management

**5.21.1 Central Field Management**

* **Jira ID:PVADMIN-37860, PVADMIN-43350, PVADMIN-44229,PVCM-65647, PVCM-65648, PVCM-66954, PVCM-86226**
* \*\*Background / Purpose:\*\*This system has enhanced to support label modifications and userdefined fields through PV Admin and reflect admin-managed field settings across security profiles. These updates enable customization of field labels of case form and any other field label across PV Suit without affecting data and provide multilingual support.
* **Feature Description**: Users can now modify field labels and manage user-defined fields in PV Admin, with changes dynamically reflected across PVCM modules, including Case Entry, Case Merge, Copy/Split, and throughout PV Suite. Field labels can be searched and edited in the PV Admin > Field Config console. Modifications, including hiding fields via the display checkbox, take effect in the UI after users log out and log back in, ensuring seamless updates without system restarts. Hidden fields trigger automatic UI adjustments to fill empty spaces. Filtering, sorting, and export functionalities are fully supported for this feature.

Figure

53

:

Central Field Management in PVADMIN

![](<.gitbook/assets/Unknown image (54)>)

![](<.gitbook/assets/Unknown image (55)>)

Figure 54: Field label changed from Type to Attachment Type

* Impact on Other Products:

o Impacts the field labels in PVR. o Impacts the field labels in PVS product.

### 5.22 Feature: Personally Identifiable Information (PII) Protection

**5.22.1 Audit Trail Data Privacy**

* **Jira ID**: PVCM-67046
* \*\*Background / Purpose:\*\*The system has been enhanced to make enforcement of PII data protection in Audit Trail for PV Admin users by extending Privacy Location Access. Unauthorized users, including PV Admin Super Users, are now restricted from viewing protected data, aligning with privacy profiles defined by country-level access control and exemptions.
* **Feature Description**: PV Admin now includes Privacy Location Access settings to control PII visibility. PII fields are masked unless users have authorized access, with audit log rendering respecting this masking logic. Exemptions are applied based on case-level settings, while legacy logs remain unmasked regardless of masking status.

![](<.gitbook/assets/Unknown image (56)>)

Figure 55: Audit Log of User with Privacy Location Access

![](<.gitbook/assets/Unknown image (57)>)

Figure 56: Case Creation for User with no Privacy Location Access

![](<.gitbook/assets/Unknown image (58)>)

Figure 57: Audit Log of User with no Privacy Location Access

* **Impact on Other Products**: No impact on other products.

**5.22.2 PII Field Profile Support for PVCM J**

* **Jira ID:** PVCM-83470
* **Background / Purpose:New fields have been added to the Case Entry Form to support PMDA (Japan) regulatory requirements and Personally Identifiable Information (PII) management in PVCM J. These enhancements ensure compliance with local authority needs and strengthen data security through role-based access, masking, and redaction functionalities.**
* \*\*Feature Description:\*\*Enhancements support PMDA-specific field capture and PII field configuration for PVCM J.
  * New fields added across sections (General, Literature, Study, Product, Event, PMDA

Info).

*
  * Japanese-language-specific field visibility and multilingual support. o Field Profile Management supports PII control with masking and redaction. o UI enhancements like tooltips, validation pop-ups, and security-based access implemented.
* **Impact on Other Products**: No impact on other products.

**5.22.3 PII Security in Data Quality Check Report**

* **Jira ID:** PVCM-12599
* **Background / Purpose:Global users without access to PII data of a case were restricted from generating the Data Quality Check Report (DQCR) for that case, limiting their ability to review or resolve non-PII-related errors and warnings. With this enhancement, they can now generate the report and act on applicable errors and warnings, while all PII-related data remains securely masked.**
* \*\*Feature Description:\*\*Users without access to a case's PII data can now generate the DQCR without restrictions. For any errors or warnings related to PII fields, the Field Location and Value columns in the DQCR will be masked to maintain data privacy.

![](<.gitbook/assets/Unknown image (59)>)

Figure 58: DQCR with PII data masked

* **Impact on Other Products**: No impact on other products.

### 5.23 Feature: Source Document Translations

**5.23.1 Auto-translation of Source Document**

* **Jira ID:PVCM-14546, PVCM-100169, PVCM-95387, PVCM-14547, PVCM-14548**
* \*\*Background / Purpose:\*\*The system has been enhanced to automatically/manually translate foreign language documents into English and attach the translated version in the Attachments section. This enables global users to review case data more effectively using the translated document.
* **Feature Description**: The new Auto-Translation capability enables efficient translation of attachments within the system. An Auto-Translate icon appears in the Attachment Viewer, allowing automatic translation of foreign-language documents into English, with configurable settings. Users with the “Translate Attachment” role can manually initiate translations. The integrated document translation API preserves original formatting, including layout, fonts, colors, headers, footers, and file extension. Translated documents are automatically attached to the case, inheriting key data like Case Version Type and Receipt Date. The Update Attachment functionality extends to translated documents, and a translation history tracks all attempts. Duplicate translations are prevented by checking existing translations for the same language pair.

Figure

59

:

Document

*

translation dialog box

![](<.gitbook/assets/Unknown image (60)>)

![](<.gitbook/assets/Unknown image (61)>)

Figure 60: Attachment section

* **Impact on Other Products**: No impact on other products.

### 5.24 Feature: Case Field Auto-calculations

**5.24.1 Pre-Population Product Event Relatedness**

* \*\*Jira ID:\*\*PVCM-90499
* **Background / Purpose:The system has been enhanced to automatically populate the Source and Method fields in the Case Form based on defined business rules. This enhancement ensures consistent classification across cases using key parameters like Source Type, Study Type, Product Type and Reporter Qualification.**
* \*\*Feature Description:\*\*System allows pre-population of Source and Method fields based on parameters like Source Type, Study Type, Reporter Qualification, and Product Type.

o Supports multiple criteria configured per business rules. o Auto-updated values reflect on related field changes. o It can be enabled / disabled via configuration in PV Admin. o Functionality applies only on company products with coded events in case form.

![](<.gitbook/assets/Unknown image (62)>)

Figure 61: Pre-Population of Source and Method

* **Impact on Other Products**: No impact on other products.

**5.24.2 ML based Auto Case Classifier**

* \*\*Jira ID:\*\*PVCM-87025
* \*\*Background / Purpose:\*\*The system introduces\*\*\*\*an AI-driven case classification engine that supports automatic identification of Adverse Events (AE), Product Quality Complaints (PQC), Medical Inquiries (MI), and Spam cases using local languages. The Case Category field is auto-populated according to this enhancement.

![](<.gitbook/assets/Unknown image (63)>)

Figure 62: Auto-Population of Case Category

* \*\*Feature Description:\*\*AI-based case classification has been introduced for unstructured cases via email or S3 intake.

o Auto-classifies cases into AE, PQC, MI, or Spam using local language. o Populates Case Category field with appropriate value(s). o Applies pre-configured rules to determine or modify category (e.g., Non-Valid AE). o Supports Japanese and other local languages.

* **Impact on Other Products**: No impact on other products.

**5.24.3 Auto-Population of Event Categorization**

* **Jira ID:** PVCM-81229
* \*\*Background / Purpose:\*\*The system introduces\*\*\*\*auto-population logic for Event Category and Seriousness Criteria has been extended beyond Important Medical Events (IME) to support additional categories—Designated Medical Events (DME), Always Serious Terms List (ASTL), and Adverse Events of Special Interest (AESI). The system will now apply auto-categorization and seriousness logic consistently across all configured lists, using the latest categorization data.
* \*\*Feature Description:\*\*The system now auto-populates Event Category based on the latest categorization list and sets Seriousness Criteria to Other Medically Important Condition (OTH) when applicable, per category configuration. For ASTL categories with OTH seriousness, users cannot manually remove these values. Configuration switches for each category (IME, DME, ASTL, AESI) control manual overrides of Event Category and auto-population of OTH seriousness. The system uses the latest categorization list during case book-in, applying all relevant categories for events (e.g., Pyrexia as both IME and ASTL). A new “i” icon in the Product Event Matrix UI displays associated event categories on hover. Event Category values are stored in the PVCM database for downstream use. Configuration updates apply upon the next case save, excluding finalized or closed cases. This enhancement applies only to new cases, leaving legacy cases unaffected.

![](<.gitbook/assets/Unknown image (64)>)

Figure 63: Event Categorization List • **Impact on Other Products**: No impact on other products.

**5.24.4 Auto-Calculation Support for Additional Case Entry Fields based on Source Data**

* **Jira ID:** PVCM-86017
* **Background / Purpose:To reduce manual data entry effort and improve consistency of case data, the system now auto-calculates several additional dependent fields in the Case Entry form. This enhancement streamlines the data entry process, minimizes human error, and ensures accurate capture of derived data.**
* Feature Description:
  * The following new fields are now supported for auto-calculation (on UI and during intake):\*\*\*\*
  * Pregnancy Information > Neonates > Gest Age at Preg Outcome o Patient/Parent > LMP Date o Pregnancy Information > Due Date\*\*\*\*o Auto-Calculation Logic is enhanced for the following fields:
  * Patient > Age o Pregnancy > Gestation Period at Earliest AE Onset o Product > Earliest Exposure Gestation Period o Product > Cumulative Dose to First Reaction o Product Event Matrix > First Dose Interval
  * Product Event Matrix > Last Dose Interval
* **Impact on Other Products**: No impact on other products.

### 5.25 Feature: PVCM Security

**5.25.1 New Roles for PV Admin Modules**

* **Jira ID:** PVCM-96963
* \*\*Background / Purpose:\*\*The system has been\*\*\*\*enhanced to access management capabilities in PV Admin modules by introducing new user roles with configurable access levels—Full, View, or No Access. These changes provide role-based access control across the system.
* \*\*Feature Description:\*\*PV Admin roles have been extended to allow granular access control across various modules via Full, View, or No Access types.

o Access governs visibility and permits actions in PV Admin modules. o Import Users supports new access roles.

![](<.gitbook/assets/Unknown image (65)>)

Figure 64: PV Admin Roles with configurable access level

* **Impact on Other Products**: No impact on other products.

**5.25.2 Security Policies for User Account Fields in the PVCM Database**

* **Jira ID:PVCM-109658**
* \*\*Background / Purpose:\*\*To enhance data security and access control by enabling the system to define and enforce security policies for application schema tables and columns containing user account-related fields.
* \*\*Feature Description:\*\*Provides the capability to set security policies on any table or column in the application schema that stores user account-related information (Username, Full Name, Email).
  * Once applied, DB Admin users cannot view or query protected data from these tables or columns.
  * Policies are enforced at the database level during query attempts. o By default, security policies apply to all tables and columns containing user account fields.
* **Impact on Other Products**: Impacts data flow from PVCM PVD to PVR.

**5.25.3 Access to Task and FU Queries without access to case update**

* **Jira ID:** PVCM-94335
* \*\*Background / Purpose:\*\*The system has been\*\*\*\*enhanced to enable users to create, edit, and delete Follow-Up (FU) Queries and Tasks without requiring case update access in PVADMIN for broader permissions.
* \*\*Feature Description:\*\*Users with appropriate roles can now manage FU Queries and Tasks independently of the "Create/Update Case" role.
  * “Create Task” and “Create Follow-up Query” roles renamed to “Create/Manage Tasks” and “Create/Manage Follow-up Queries.”
  * Task and FU Query actions are now accessible in Case Form and Listing screens based on respective roles.
  * Users can perform Add, Edit, and Delete operations without case update access.

![](<.gitbook/assets/Unknown image (66)>)

Figure 65: Roles for managing FU Queries and Tasks

* **Impact on Other Products**: No impact on other products.

**5.25.4 System-defined ‘PVCM Migration User’ for Data Migration Activities**

* **Jira ID:** PVCM-34339
* \*\*Background / Purpose:\*\*To ensure consistent traceability and data lineage during the case migration process, the application requires a dedicated system user account that can be used as the creator or modifier for records migrated into the system. Introducing a pre-defined 'PVCM Migration User' ensures this is handled systematically and uniformly across all environments.
* \*\*Feature Description:\*\*A default non-LDAP user named ‘PVCM Migration User’ will now be provided out of the box in the system. This user is intended only for internal use during case data migration and cannot be used to log in or perform any regular actions. It is pre-configured to support migration activities without affecting normal user operations.
* **Impact on Other Products**: No impact on other products.

**5.25.5 Login Restrictions and User Validation for System and Non-LDAP Accounts**

* **Jira ID:PVCM-107527**
* \*\*Background / Purpose:\*\*To enhance system security, improve user management, and maintain audit accuracy, the application must prevent login through predefined system accounts and allow control over non-LDAP user access. These changes ensure that systemgenerated activities remain clearly segregated from user actions and help enforce user identity integrity through email uniqueness.
* Feature Description:
  * The application will restrict login access for predefined system accounts such as PVCM System User and PVCM Migration User.
  * These system users will be hidden from all user selection lists and will not be available for case or task assignments.
  * A configuration option will be available to enable or disable login for non-LDAP users.
  * The system will enforce unique email addresses across all user accounts, including during bulk user creation.
* **Impact on Other Products**: No impact on other products.

**5.25.6 Email-based Secondary Authentication for Non-LDAP User Login**

* **Jira ID:PVCM-107526**
* \*\*Background / Purpose:\*\*To enhance the security posture of the application, an additional email-based verification step is introduced for non-LDAP user account authentication. This two-step authentication mechanism ensures only authorized users can access the application even if their credentials are compromised.
* **Feature** **Description**:
  * A secondary authentication mechanism has been introduced for non-LDAP user logins via a 6-digit verification code sent to the user's registered email address.
  * Upon successful validation of username and password, the application generates a onetime verification code and emails it to the user. o The user must enter this code within a configurable time limit (default: 5 minutes) on the verification screen to complete the login process.

![](<.gitbook/assets/Unknown image (67)>)

Figure 66: Code Verification for non-LDAP users

*
  * A Resend Code option is provided, which becomes available after a 60-second interval to request a new code.
  * This additional layer of authentication enhances security and is enabled by default. It can be toggled through configuration.
* **Impact on Other Products**: No impact on other products.

**5.25.7 Case PDF Output in Japanese**

* \*\*Jira ID:\*\*PVCM-84547
* \*\*Background / Purpose:\*\*The system has been\*\*\*\*enhanced to access global PDF export functionality by supporting Japanese data and labels, including all relevant fields and formatting requirements for PMDA reporting.
* \*\*Feature Description:\*\*This enhancement extends support for Japanese-language case documentation by enabling Case PDF exports.
  * This functionality includes all Secondary View fields, newly added PMDA-specific fields, and proper sequencing and formatting. o For user’s language preference or source language set to Japanese, the exported PDF will display values and labels in Japanese.
  * Date and time formatting will also follow Japan-specific standards.
* **Impact on Other Products**: No impact on other products.

### 5.26 Feature: Case Intake via E2B Import

**5.26.1 Case Intake via PMDA E2B R3 Import Profile**

* \*\*Jira ID:\*\*PVCM-85849
* \*\*Background / Purpose:\*\*The system now supports automatic case creation via PMDA E2B R3 XML files and Japan-specific JSON intake. Cases are generated using mapped values defined in the E2B importer, including full support for attachments and Null Flavor values. The system also generates and exports acknowledgement files (ACKs) in HL7 format.
* \*\*Feature Description:\*\*The system now automatically creates cases from incoming PMDA E2B R3 XML files, populating fields based on configured E2B Importer mappings. A dedicated folder is used for importing these files, including Null Flavor values. Cases are created via JSON intake in the local language, enabling structured intake of Japan-specific case content through external integrations.
* **Impact on Other Products**: No impact on other products.

**5.26.2 Reply Email Configuration for Case Intake via E2B and JSON Files**

* **Jira ID:** PVCM-90439
* \*\*Background / Purpose:\*\*The system now auto-populates the reply email address for followup (FU) queries based on Vendor and Country for cases created via JSON, E2B, or Mailbox. This ensures replies are directed to the appropriate intake mailbox and enhances case continuity.
* \*\*Feature Description:\*\*Enhancement enables automatic assignment of the reply email for cases created via JSON, E2B, or email intake:
  * Reply address determined by Vendor and Country configuration. o Default mailbox used when no configuration exists. o Supports manually created and reply-based cases.
  * Country auto-populated from latest valid version for follow-up response cases.
* **Impact on Other Products**: No impact on other products.

### 5.27 Feature: ML Parser Confidence Score

**5.27.1 ML Parser Confidence Score – PVCM J**

* **Jira ID:** PVCM-83226
* **Background / Purpose:The system has been enhanced to support Local Language (Japanese) based Unstructured AE Parsing using ML (Machine Learning). The enhancement includes integration of multiple case data fields for ML-based extraction, highlighting extracted values in source documents, confidence score visibility, and user actions (Accept, Reject, Modify).**
* **Feature Description:The enhancement supports the display of Confidence Scores and Ranges for extracted values, along with controls to manage value acceptance based on confidence thresholds. These capabilities are built to extend support to future multi-lingual extraction, beyond Japanese for different fields in case form.**
* **Impact on Other Products**: No impact on other products.

### 5.28 Feature: Audit Log

**5.28.1 PVCM J | Support for Japanese Fields in Audit Log**

* **Jira ID:** PVCM-96512
* \*\*Background / Purpose:\*\*The system has been enhanced to support Audit log for Japanspecific case fields, ensuring full traceability for localized data. This update aligns audit behaviour with global standards while accommodating Japan-specific UI and language requirements.
* \*\*Feature Description:\*\*Audit log support has been extended to Japan-specific fields, ensuring consistent tracking with exceptions for display format and language.

o Field names for Japanese fields are suffixed with “(J)” o Both English and Japanese values are captured where applicable o Dropdown values default to English unless not configured o New Japan fields follow the same audit behavior as existing ones

![](<.gitbook/assets/Unknown image (68)>)

Figure 67: Audit Log- multilingual values

* **Impact on Other Products**: No impact on other products.

### 5.29 Feature: Follow-up Queries

**5.29.1 Support 300,000–Character Length Restriction for FU Query Template Message**

* \*\*Jira ID:\*\*PVCM-83356
* **Background / Purpose:The system now supports Follow-Up (FU) Query messages with an increased character limit of up to 300,000 characters. This enhancement ensures users can input extensive case details without restrictions.**
* \*\*Feature Description:\*\*The system has been enhanced to support FU Query messages up to 300,000 characters in length across all templates and relevant screens.

o Supports actions like Save, Draft, and Preview. o Displays warning message when maximum limit is exceeded.

![](<.gitbook/assets/Unknown image (69)>)

Figure 68: Supporting 300,000-character length for FU Query Template

* **Impact on Other Products**: No impact on other products.

**5.29.2 FU Query Template Support in PVCM J**

* **Jira ID**: PVCM-14693, PVCM-14694, PVCM-87459
* **Background / Purpose:The system has been enhanced with pre-configured Japanese Follow-Up (FU) Query templates. These templates aim to reduce manual effort, ensure consistency in communication, and automatically populate placeholder values in the appropriate local language—aligned with the case's Source Language.**
* **Feature Description:** The system now offers pre-configured Japanese Follow-Up (FU) Query templates, including General FU Query, Product Questionnaire, Pregnancy Follow-Up, and Autopsy Report Enquiry, to enhance localization and streamline communication. These templates dynamically populate case-specific placeholders (e.g., \[Patient Initials]) based on the Case Form’s Source Language, generating output in the local language (e.g., Japanese). Placeholders appear in English for clarity but resolve to the appropriate language during preview or generation, supporting text, dropdown, and multi-select fields. Language-neutral fields like dates and numbers retain consistent formatting. This functionality extends to DQCR rule descriptions and reporter web forms, now supporting Japanese labels.

![](<.gitbook/assets/Unknown image (70)>)

Figure 69: Japanese Follow-up Query Template

* **Impact on Other Products**: No impact on other products.

### 5.30 Feature: Case Attachments and Attachment Viewer

**5.30.1 Display Warning Message on Changing Attachment Protection Status**

* **Jira ID:** PVCM-91815
* **Background / Purpose:The system now supports a warning message when changing the “Protected” status of attachments to prevent unintentional modifications and enhance data security during case editing.**
* \*\*Feature Description:\*\*To reduce errors in toggling attachment protection, a confirmation popup now appears when changing the “Protected” checkbox status during case editing.

o Displays distinct messages when switching between protected and unprotected states. o Provides Cancel and OK buttons with appropriate behavior. o Helps maintain the integrity of attachment protection in the case workflow.

![](<.gitbook/assets/Unknown image (71)>)

Figure 70: Warning message on changing Protection status

* **Impact on Other Products**: No impact on other products.

### 5.31 Feature: E2B Viewer

**5.31.1 Enhancement to E2B Viewer**

* **Jira ID:PVCM-87666, PVCM-107625**
* **Background / Purpose:To enhance the E2B viewer for improved usability, enabling users to view and navigate data more efficiently.**
* **Feature** **Description**:
  * Adds a language drop-down (English/Japanese) in the E2B viewer, displaying header names and code list values based on the selected language. Defaults to English if Japanese names are unavailable.
  * Language drop-down appears only when the user's preferred language is not English.

![](<.gitbook/assets/Unknown image (72)>)

Figure 71: E2B Viewer Language Drop-down

*
  * Displays decoded values for supported null flavor fields (e.g., UNK → Unknown) for all global users.
  * When Japanese is selected, null flavor values display as ‘不明 (Code)’ — e.g., 不明

(UNK), 不明 (MSK), representing 'Unknown' followed by the original code in parentheses. o Displays all multi-select field values in single row. o Product section layout to a parent-child format, displaying complete details for each product sequentially for improved readability and usability.

* **Impact on Other Products**: No impact on other products.

**5.31.2 Display Decoded Values for Date, MedDRA and EDQM Fields in E2B Viewer**

* **Jira ID:** PVCM-81028
* **Background / Purpose**: Users need a readable view of E2B R2/R3 files to easily review case data. Displaying decoded values for dates and medical codes improves usability and accuracy in validation.
* **Feature Description**: The E2B Viewer within the Attachment Viewer now displays humanreadable text values for dates, MedDRA codes, and EDQM codes, making it easier to review and verify case data extracted from E2B R2 and R3 files.
* **Impact on Other Products**: No impact on other products.

### 5.32 Feature: ICSR Management

**5.32.1 ICSR Screen Enhancement and UI Changes Impact on PVCM**

* **Jira ID:PVCM-107086, PVCM-107039, PVCM-107036, PVCM-106489**
* **Background / Purpose:To enhance the PVCM ICSR screen with improved UI, advanced search, preference retention, and enable users to update report status, correct submission/due dates, and enforce user access as per PVR permissions.**
* **Feature** **Description**:
  * PVCM ICSR screen is enhanced to align with the PVR ICSR screen for consistent user experience.
  * Implements improved column stacking for better data organization.

![](<.gitbook/assets/Unknown image (73)>)

Figure 72: ICSR Screen: Column Stacking

*
  * Adds advanced search and filter options across all columns, including multi-select and date range filters.
  * Supports user preference retention for column visibility and selected filters during active sessions. o Introduces access-based controls, ensuring operations are governed by user roles from PVR.
  * Enables users to reverse the "Submission Not Required" status via UI, with mandatory justification and audit logging. o Provides functionality to un-submit reports (except Gateway reports) and move them back to the 'Generated' state.
  * Allows authorized users to update submission and due dates directly through UI actions. o Adds new filters, including a “Ready for Local CP” status filter for easier case tracking. o Supports sorting on stacked columns for efficient data viewing. o Displays overdue and due soon indicators using color coding (Red/Yellow) based on due dates. o Ensures all key actions are audit logged with user, timestamp, and action details for compliance.
  * Maintains secure, role-based case tracking and submission management, aligned with business workflows.
* **Impact on Other Products**: Impacts ICSR Functionality in PVR.

### 5.33 Feature: Case Follow-up Difference Screen

**5.33.1 Display FU Difference View Adjacent to Case Entry Form**

* **Jira ID:PVCM-115172**
* **Background / Purpose:** The FU Difference View, previously shown in a separate screen with a layout similar to the Case Entry Form, is now redesigned to enhance usability, performance, and focus. The new tabular view is displayed alongside the Case Entry Form, enabling users to review case differences while simultaneously referencing the full case data. This layout streamlines follow-up case review by reducing context switching and supporting quicker decision-making.\*\*\*\*
* **Feature** **Description**:
  * Upon opening, FU Difference View will now be displayed to the right of the Case Entry Form in a tabular view. o A new expand/collapse icon allows users to toggle the FU Difference view to full width and back to split view.
  * The Case Entry Form becomes read only when FU Difference View is displayed and becomes editable once the view is closed.
  * If PVCM is configured as an intake system with Safety Case Import enabled, a new menu option “FU Difference with Safety Case” appears below the standard FU Difference View option. This option will display a comparison between the Intake case and the safety case.

![](<.gitbook/assets/Unknown image (74)>)

Figure 73: FU Difference View

* **Impact on Other Products**: No impact on other products.

**5.33.2 FU Difference View in Tabular Format**

* **Jira ID:PVCM-115173**
* **Background / Purpose:** To improve usability and performance during case review, the FU (Follow-Up) Difference View is redesigned to display only differing field and record values between follow-up versions in a concise tabular format. This allows users to focus on critical updates without navigating a separate screen, enhancing visibility and efficiency in case comparison workflows.\*\*\*\*
* **Feature** **Description**:

o The FU Difference View now appears in a side-by-side tabular format next to the Case Entry Form and displays only the fields and repeatable section records that differ between two case versions. The table includes the following columns:

*
  * Field Name: Displays the field label for which differences are displayed.
  * Version Columns: Displays the versions numbers of the case being compared.
  * Reject: This column displays checkboxes that allow to reject the values similar to Reject button in the earlier design of FU Difference View.

![](<.gitbook/assets/Unknown image (75)>)

Figure 74: Differences in tabular view

* Version-specific fields such as Version Receipt Date, Central Receipt Date, Due Date, etc., are excluded from the FU Difference View, even if they contain differences. o Fields displayed are grouped by section and records similar to the Case Entry Form.
* Fields from the Attachments, Tasks, FU Query, ICSR, and Listedness sections are excluded from display in the FU Difference View. o For Repeatable section records, an identifier is displayed. E.g., For reporter section records, an identifier is displayed in format Reporter #1 (First Name, Middle Name, Last Name).
* A new attribute ‘Display Order” is displayed similar to fields to display the differences in sequence of the records.
* Large values that cannot be displayed completely within the tabular view can be viewed by hovering over the value.

![](<.gitbook/assets/Unknown image (76)>)

Figure 75: Large Text field value

* Reject checkbox will be non-editable for field values that are in non-editable state or masked due to PII restrictions, case blinding restrictions or for fields that do not support rejection. Appropriate message is displayed to the user upon hovering over the Reject checkbox for such fields.

• **Impact on Other Products**: No impact on other products.

**5.33.3 Field, Section, Record, and Case-level Rejection in FU Difference View**

* **Jira ID:PVCM-115176, PVCM-82021**
* **Background / Purpose:** The ability to reject data at the field, section, record, and case level was available in the earlier design of the FU Difference View. With the introduction of the new tabular format, this capability is now extended to ensure continuity of functionality. The enhancement enables users to efficiently perform rejection actions within the streamlined tabular view while maintaining the same flexibility and control as the previous layout.\*\*\*\*
* \*\*Feature Description:\*\*The FU Difference View supports multi-level rejection through interactive checkboxes provided at different granular levels.
  * \*\*Section/Record-level Rejection:\*\*Checkboxes are displayed for each section, subsection, and repeatable record. When selected, all eligible fields (excluded disabled/masked ones) within the group are automatically selected.
    * Fields with auto-rejection dependency are automatically selected when their corresponding primary field is selected. E.g., If Product Name is selected, the dependent fields like Dosage Form, Strength etc. are automatically selected including native language field data (E.g., Product Name (Chinese))
    * Fields restricted due to PII or blinding will remain unselected if user does not have access to the data.

![](<.gitbook/assets/Unknown image (77)>)

Figure 76: Reject icon in sections and records

*
  * \*\*Case-Level Rejection:\*\*A checkbox in the Reject column header enables case-level rejection. When selected, all fields, sections, and records in the FU Difference View will be marked for rejection even if individual field checkboxes are disabled or masked.

![](<.gitbook/assets/Unknown image (78)>)

Figure 77: Case level rejection

* **Impact on Other Products**: No impact on other products.

**5.33.4 Save Rejections in FU Difference View**

* **Jira ID:PVCM-115177**
* **Background / Purpose:** The functionality to persist rejections was already supported in the earlier version of the FU Difference View. With the new tabular format, this capability is retained, allowing users to save rejection selections made at the field, section, record, or case level. This enhancement ensures continuity of functionality.\*\*\*\*
* **Feature Description:** The FU Difference View continues to support saving and applying rejections to streamline follow-up data handling.
  * A new Update icon is introduced in the header of the FU Difference View, allowing users to apply selected rejection checkboxes directly to the case.
  * When the update is performed, the selected changes are persisted to the case as follows:
    * Field values selected from the compared version overwrite those in the follow-up version.
    * Non-matching records selected from the current version are removed.
    * Non-matching records from the other version are added to the current version.
    * Auto-calculated fields (e.g., Due Date, Seriousness, Priority, Listedness) are recalculated based on the updated data.
* **Impact on Other Products**: No impact on other products.

**5.33.5 Enhanced Support for Large Text Field Differences in FU Difference View**

* **Jira ID:PVCM-115357**
* **Background / Purpose:** The ability to identify and reject differences in field values has been extended to large text fields in the FU Difference View. This enhancement enables users to view granular differences within large text fields (e.g., narratives or comments) at the word level and selectively reject text changes. The functionality is aligned with the new tabular format of the FU Difference View and is also supported during Case Merge operation.\*\*\*\*
* **Feature Description:** In the FU Difference View (including during Case Merge), large text fields now include an icon next to the Reject checkbox, enabling users to view and manage differences within the text. This icon becomes active once the checkbox for the field is selected.

![](<.gitbook/assets/Unknown image (79)>)

Figure 78: Icon to view differences for large text fields

*
  * Clicking the icon opens a dedicated pop-up window that highlights word-level differences:
    * Text present in the follow-up/current version but not in the previous version is shown with a green background
    * Text present in the previous version but missing in the follow-up/current version is displayed with a red background and strikethrough.

![](<.gitbook/assets/Unknown image (80)>)

Figure 79: Case Narrative – Difference View

*
  * Users can hover over highlighted text to reveal an “X” icon, allowing them to toggle individual word rejections.
  * The following actions are available within the pop-up:
    * Reject All: Applies rejection to all highlighted differences.
    * Clear: Resets all rejection selections to the original difference view.
    * Save: Saves the selected word-level rejections, automatically checks the field’s checkbox, and highlights the icon.
    * Cancel: Closes the pop-up without applying changes.

![](<.gitbook/assets/Unknown image (81)>)

Figure 80: Icon highlighted after rejecting differences

* **Impact on Other Products**: No impact on other products.

**5.33.6 FU Difference and Case Merge Support for PVCM J**

* **Jira ID:** PVCM-90492
* **Background / Purpose:** The application now supports the FU Difference and Case Merge features for PVCM J cases, ensuring consistency with global case processing workflows. All existing functionalities related to identifying and merging follow-up case data are now available for Japan-specific case processing.\*\*\*\*
* **Feature** **Description**:
  * The FU Difference View allows users to review field-level differences between follow-up and existing case versions and selectively accept or reject changes.
  * Case Merge functionality enables merging of follow-up data into the base case, with proper validation and conflict resolution logic in place for both global and Japan-specific fields.
  * Field weightage and difference thresholds for newly introduced Japanese fields are applied as configured, while existing global field configurations remain unchanged for PVCM J cases.
* **Impact on Other Products**: No impact on other products.

### 5.34 Feature: Case Merge

**5.34.1 Tabular Difference View during Case Merge Operation**

* **Jira ID:PVCM-115180**
* **Background / Purpose:** In the earlier Case Merge, differences between versions were displayed in a layout resembling the Case Entry Form, requiring users to manually select the data to retain in the main version during a merge. With this enhancement, the Difference View during Case Merge is redesigned in line with the Follow up Difference View tabular format, offering a more intuitive and structured comparison. Additionally, since the main case version is now treated as the base version, users no longer need to explicitly select data for retention as the merge process is streamlined and reduces manual effort while improving accuracy.\*\*\*\*
* **Feature Description:** The Case Merge process is enhanced with a tabular Difference View, providing users with a clear and efficient way to review and selectively merge data from an incoming case or follow-up into the active version of a case.
  * When the Case Merge operation is launched, any new or differing data from the incoming version is displayed alongside the Case Entry Form in a structured tabular layout. The Case Entry Form opens in read-only mode, showing data from the base version. A Merge icon appears at the top of the screen to initiate the merge action. o The Difference View table includes the following columns:
    * Field Name: Displays the label of each field with differences.
    * Version Columns: Shows the version number of the base case version and the version number or Intake # of the incoming case or follow-up.
    * Merge: Provides checkboxes to select specific field values or records for merging.

![](<.gitbook/assets/Unknown image (82)>)

Figure 81: Case Merge

By default, merge checkboxes are selected to include all new incoming data in the merge.

*
  * Merge checkboxes are disabled for fields that are non-editable or not supported for merge. When users hover over a disabled checkbox, an appropriate tooltip message is displayed, explaining why merge is not allowed for that field.
  * When users click the Merge icon and proceed with the merge, the selected field values and records from the incoming version are merged into the base case version. A confirmation pop-up appears, allowing users to either open the updated case or return to the screen from where the merge was initiated.
  * Auto-calculated fields (e.g., Due Date, Seriousness, Priority, Listedness) are recalculated based on the updated data.
* **Impact on Other Products**: No impact on other products.

### 5.35 Feature: PV Gateway Integration Options

**5.35.1 PV Gateway Enhancement to Support PMDA Submissions**

* **Jira ID:** PVCM-84834
* **Background / Purpose:PV Gateway has been technically and functionally enhanced to support E2B transmission to the Japanese regulatory authority (PMDA) and receive acknowledgment responses. The system can now import and display the PMDA Number (acknowledgment number) within PV Case Management.**
* **Feature Description:PV Gateway now supports outbound transmission of E2B reports to PMDA and receipt of PMDA acknowledgment responses. Upon successful submission, the PMDA Number from the acknowledgment is automatically imported into the respective case in PV Case Management and displayed in a new read-only PMDA Information section.**

![](<.gitbook/assets/Unknown image (83)>)

Figure 82: PMDA Number imported within PVCM

* **Impact on Other Products**: No impact on other products.

### 5.36 Feature: Case Blinding - Unblinding

**5.36.1 Blind Field Profile Support for PVCM J**

* **Jira ID:** PVCM-83321
* \*\*Background / Purpose:\*\*The system is**enhanced to support the Case Blinding framework of PVCM J in additional fields, language-specific configurations, PMDA section support, and multilingual justification comments during unblinding/re-blinding.**
* \*\*Feature Description:\*\*The system now supports field-level flexibility for blinding either the English, Japanese, or both language versions of a field. Additionally, the system enforces mandatory justification comments when unblinding or re-blinding a case, with multilingual data entry support. The enhancement maintains compatibility with all prior functionalities related to blinding status, study product visibility, role-based access, and audit logging.
* **Impact on Other Products**: No impact on other products.

**5.36.2 Masking Blinded Product Data in Data Quality Check Report**

* **Jira ID:** PVCM-79102
* \*\*Background / Purpose:\*\*Global users without access to blinded data of a case were previously able to view product names in the Data Quality Check Report (DQCR), within errors and warnings related to blinded products. This enhancement ensures that all blinded data remains masked for users without appropriate access, maintaining confidentiality while still allowing them to generate and review the report. \*\*\*\*
* \*\*Feature Description:\*\*Users without access to blinded data will see masked values for blinded product information in the DQCR. The Field Location and Value columns will display masked content for any field configured as blinded, based on the case blinding status, consistent with masking behavior in the Case Form.

![](<.gitbook/assets/Unknown image (84)>)

Figure 83: Blinding in DQCR

* **Impact on Other Products**: No impact on other products.

### 5.37 Feature: Case Finalization

**5.37.1 Renaming “Transmit” Action to “Finalize”**

* **Jira ID:** PVCM-17143
* **Background / Purpose:The term “Transmit” used for finalizing a case did not clearly convey the intent of finalizing a case for submission. To improve usability and align terminology with case state, the action has been renamed to “Finalize”.**
* \*\*Feature Description:\*\*The “Transmit” action has been renamed to “Finalize” across the PVCM application. This change includes action menus, bulk actions, user roles, role descriptions, warning messages, and email notifications.
* **Impact on Other Products**: No impact on other products.

**5.37.2 Automated Data Quality Validation for Bulk and Auto Finalization of Cases**

* **Jira ID:** PVCM-13040
* **Background / Purpose:To maintain data integrity and ensure that only complete and errorfree cases are finalized, the system now enforces Data Quality Checks (DQCR) during bulk and auto-finalization operations. This reduces the risk of transmitting invalid or incomplete case data and provides early error visibility to users before finalization occurs.**
* **Feature** **Description**:
  * When users initiate bulk finalization of cases, the application will run a data quality check (DQCR) in the background. If any cases have unresolved DQCR errors, the system will prompt the user with an option to either proceed with finalizing only the error-free cases or cancel the entire operation.
  * For cases created via intake that are set to auto-finalize, the system will automatically generate a DQCR in the background. If open DQCR errors are detected, the case will not transition to Final state. Instead, an email notification with the error details will be sent to administrators, allowing for timely resolution and maintaining the integrity of case data.
* **Impact on Other Products**: No impact on other products.

### 5.38 Feature: MedDRA Recode

**5.38.1 Enhancements in MedDRA Recode Screens**

* **Jira ID:PVADMIN-45876**
* **Background / Purpose:** The purpose of this enhancement is to improve the clarity, usability, and accuracy of the MedDRA update process by renaming and refining UI elements, labels, and dialog components. This helps ensure better user understanding, aligns terminology with functional goals.\*\*\*\*
* **Feature** **Description**:
  * The ‘MedDRA Upgrade’ section header and related labels have been renamed to ‘MedDRA Recode’ to more accurately reflect the underlying functionality.
  * The ‘Generate’ button has been renamed to ‘Preview’ across all relevant screens, including the main MedDRA Recode section and the MedDRA Recode Preview dialog, to better represent the purpose of the action.

![](<.gitbook/assets/Unknown image (85)>)

Figure 84: MedDRA Recode section

*
  * Options in MedDRA Recode Preview Dialog are updated as below:
    * MedDRA Recode for Cases: This option now includes all non-current term-related data, as the separate non-current term report has been integrated into this report.
    * MedDRA Recode for Product Indications, Datasheet, and Event Categorization Terms: Option is renamed to replace “Upgrade” with “Recode”.
    * Cases Open by Users: Option has been renamed to clearly indicate that it is for generating report with list of cases that are currently open by users.

![](<.gitbook/assets/Unknown image (86)>)

Figure 85: MedDRA Recode Preview

*
  * Existing options in MedDRA Recode Dialog have been renamed as below:
    * Recode all non-current terms to latest PTs

▪

Recode non

*

current terms based on input file

![](<.gitbook/assets/Unknown image (87)>)

Figure 86: MedDRA Recode

* **Impact on Other Products**: No impact on other products.

**5.38.2 Enhancements in MedDRA Recoding for Cases Including Japanese Term Handling**

* **Jira ID:PVCM-107624**
* \*\*Background / Purpose:\*\*The MedDRA Recode functionality, which previously supported recoding based only on English MedDRA terms, has now been enhanced to include Japanese term changes. This enhancement ensures consistent and accurate recoding in cases where Japanese LLT (LLT(J)) differs from the English LLT, addressing hierarchical mismatches and replacing outdated terms in accordance with defined business rules.
* **Feature** **Description**:
  * **MedDRA Japanese Term differences:During MedDRA Recode execution, if there are any changes in the Japanese terms as per the active dictionary, the corresponding MedDRA fields for impacted cases will be recoded.**
* **LLT to PT Conversion for Non-current Terms:** If LLT becomes non-current as per the new MedDRA dictionary, it will continue to be replaced with corresponding PT. If LLT(J) is different from LLT then it shall also be replaced with the PT.

**Note**: This scenario is possible only for case migrated from a source system that allows LLT(J) to be different from LLT(E) and qualifies for MedDRA Recode.

* **LLT and LLT(J) Discrepancies**: In cases where LLT(J) (Japanese) differs from LLT(E) (English) in a MedDRA field, LLT(J) will be replaced with LLT(E) under the following conditions:
  * LLT(J) and LLT(E) now belong to different PTs in the updated MedDRA dictionary.
  * LLT(J) has become non-current in the new dictionary version.
* \*\*Input File for Non-current Terms:\*\*If an Input file is used for recoding of non-current terms, LLT and LLT(J) are updated for matching non-current Terms as per the LLT provided in the input file.
* **Automatic** **Version** **Creation** **for** **Final** **State** **Cases**: The new version that is created when eligible Final versions contain the impacted MedDRA Terms, will now be created with Version Type as “MedDRA Recode” instead of “Amendment”. All Version Receipt Date, Central Receipt Date and Version Disposition records will be copied from the eligible Final version into the new version created.
  * For a case version, if Case state is Final and Local State is Active and it qualifies for MedDRA Recode, then the same version of the case is recoded without creating a new version. The subsequent versions of that case are also recoded as per the new MedDRA dictionary.
* **MedDRA Coding Icon:MedDRA Recoding icon is now displayed in green color instead of orange irrespective of whether the MedDRA version used for coding matches with the latest active dictionary or not.**
* **Impact on Other Products**:
  * Impacts propagation of data to PVD o Impacts ICSRs in PVR

**5.38.3 MedDRA Recoding Support for Product Indications, Datasheets, Advanced Auto-listedness, and Event Categorization Terms**

* **Jira ID:PVADMIN-45875**
* **Background / Purpose:** To ensure consistency and accuracy across product configurations during MedDRA dictionary upgrades, the application is enhanced to automatically update MedDRA hierarchies and terminology for Product Indications, Datasheets, Advanced Autolistedness configurations, and Event Categorization Terms. This automation eliminates the need for manual recoding and ensures all configurations reflect the latest MedDRA hierarchy and term currency. \*\*\*\*
* \*\*Feature Description:\*\*Upon execution of the MedDRA Recode process, the system now automatically recodes the MedDRA terms used in the following configurations:
  * Product Indications and Datasheet Terms:
  * If LLT, PT, HLT, HLGT, or SOC codes or terms (English) differ in the latest active MedDRA dictionary, the complete hierarchy is updated using the Primary SOC path.
  * If LLT has become non-current in the new dictionary, it is replaced with the corresponding PT.
  * All products (except deactivated ones) and datasheet versions (except deactivated ones for standard terms, and all versions for Advanced Autolistedness) are included. o Advanced Autolistedness (Indications and Additional Events):
  * LLT and PT codes or terms are updated using the Primary SOC path if changes are detected in the new MedDRA dictionary.
  * Non-current LLTs are replaced with their corresponding PTs.
  * Event Categorization Terms (IME, DME, ASTL, AESI): o PT terms are replaced if their text differs in the latest MedDRA dictionary.
  * If a PT is demoted or becomes non-current, it is replaced with the PT of the matching LLT, as per the latest dictionary.
* **Impact on Other Products**: No impact on other products.

**5.38.4 Enhancements in MedRA Recode Preview Report for Cases**

* **Jira ID:PVCM-107622**
* **Background / Purpose:** The MedDRA Recode report for cases, which previously supported only English terms, has been enhanced to include Japanese term changes along with additional details like Local State, Assigned Group, and change indicators, enabling a more comprehensive review. Additionally, separate previews for non-current terms have been consolidated into a single unified report, offering a streamlined view of all impacted cases and their corresponding MedDRA term updates. \*\*\*\*
* **Feature** **Description**:
  * The MedDRA Recode preview report for cases has been enhanced to include additional columns such as Local State, Assigned Group, Reported Description, Message, Japanese MedDRA terms, and change indicators at each MedDRA hierarchy level, offering a more detailed and informative view.
  * The report now displays non-current MedDRA LLT terms along with the corresponding replacement PT
* **Impact on Other Products**: No impact on other products.

**5.38.5 Enhancements in MedRA Recode Preview Report for Configurations**

* **Jira** **ID**: PVADMIN-45869, PVADMIN-45870\*\*\*\*
* **Background / Purpose:** To enhance control during MedDRA upgrades, the preview reporting feature, previously limited to IME terms, now includes support for DME, ASTL, and AESI categories. It also extends to Product Indications, Datasheets, and Advanced Auto-listedness configurations, allowing users to proactively review hierarchy and currency changes and make informed decisions before recoding is applied.\*\*\*\*
* **Feature** **Description**:
  * \*\*MedDRA Recode Event Categorization Preview Report:\*\*The existing IME Terms report is enhanced to include impacted terms from additional event categories DME, ASTL, and AESI with new columns such as Trade Name and Message.
  * \*\*MedDRA Recode Product Indications Preview:\*\*The Indications report is updated to include a Message column and display terms that have become noncurrent along with their updated PT hierarchy based on the latest MedDRA dictionary.
  * **MedDRA Recode Product Datasheets Preview:** The Datasheets report is enhanced to include a Message column and list noncurrent terms with the corresponding PT hierarchy from the latest MedDRA version. All versions of the datasheet excluding the deactivated versions are considered for report generation.\*\*\*\*
  * \*\*MedDRA Recode Datasheets Advanced Auto-listedness Preview:\*\*A new report that lists impacted Indications and additional events configured in the Advanced Autolistedness section of product datasheets. It includes LLT and PT changes along with a Message column and displays noncurrent terms with the updated PT hierarchy.

**Note**: As a common change column indicating whether there is a change between old and new terms is included for each MedDRA hierarchy level. Message column in above reports displays additional details/comments for that record.

* **Impact on Other Products**: No impact on other products.\*\*\*\*

### 5.39 Feature: Code List

**5.39.1 Malfunction Type Codelist**

* **Jira ID:PVADMIN-45496**
* \*\*Background / Purpose:\*\*A new codelist, "Malfunction Type," has been introduced to enable configurable and multilingual malfunction types using the PV Admin import/export functionality. This enhancement supports structured data entry, audit tracking, and flexible integration into case entry forms for device-related product cases.
* \*\*Feature Description:\*\*A configurable codelist “Malfunction Type” has been added via PV Admin’s Import module.
  * This codelist enables multilingual support (English, Japanese). o Appears in Full Case Entry under Device Information.
  * Export supported via Import/Export module.
* **Impact on Other Products**No impact on other products.

**5.39.2 Add “Spam” as a New value in Case Category Codelist**

* **Jira ID:PVADMIN-45126**
* **Background / Purpose:A new value, “Spam,” has been added to the Case Category codelist in both English and Japanese to support identification of spam cases during automated case classification.**
* \*\*Feature Description:\*\*The Case Category codelist is updated to include a new value, "Spam," with multilingual support.
  * Applied in both English (“Spam”) and Japanese (“スパム”). o Enabled for auto case classification workflows.
  * Configured under mutable, active values.
* **Impact on Other Products**: No impact on other products.

**5.39.3 Preferred Case State and Local State Configuration in Workflow Rules**

* **Jira ID:PVADMIN-44421**
* **Background / Purpose:The system is now enhanced to allow configuration of “Preferred State” and “Preferred Local State” within workflow rules to enable automatic state transitions during workflow group changes.**
* \*\*Feature Description:\*\*Users can configure workflow rules with either a Preferred State or Preferred Local State to auto-update case states during routing. o New fields added after Workflow Routing Condition. o Optional fields with selectable values: Active or Final. o Only one field (State or Local State) can be selected by the rule.

o Supports import/export and listing customization for workflow rules.

* **Impact on Other Products**: No impact on other products.

**5.39.4 Rename Code List Name from “SENT TO FDA” to “SENT TO REG AUTH”**

* **Jira ID:PVADMIN-41560**
* \*\*Background / Purpose:\*\*The code list “SENT TO FDA” has been renamed to “SENT TO REG AUTH” to provide a more generic label applicable to all regulatory authorities, ensuring consistency and broader regulatory compliance without impacting existing code values or configurations.
* \*\*Feature Description:\*\*The existing code list name “SENT TO FDA” has been updated to “SENT TO REG AUTH” across the application
* The change ensures the terminology is applicable to global regulatory submissions.
* The update affects only the display name; code values, CL\_ID, and value IDs remain unchanged.
* **Impact on Other Products**: No impact on other products.

**5.39.5 Reference Sub-Type | Additional Codelist Values**

* **Jira ID:PVADMIN-45702**
* \*\*Background / Purpose:\*\*Enhancements have been made to the Reference Sub-Type codelist to support automatic parent-child case linking. This includes new values for “Copy Case” and “Split Case,” multilingual support, and configuration flags to establish default linking logic.
* \*\*Feature Description:\*\*Two new values, “Copy Case” and “Split Case,” have been added to the Reference Sub-Type codelist with support in English and Japanese.
* New flags introduced: MASTER REFERENCE TYPE and REFERENCE SUB-TYPE\_FLAG to manage default linkage behavior.
* Reference Type and Sub-Type linkage established via codelist configuration.
* Existing values remain unaffected.
* Validations ensure only one master Reference Type per codelist.
* **Impact on Other Products**: No impact on other products.

**5.39.6 New Column “Relation” for Weight Units and Height Units**

* **Jira ID:PVADMIN-43553**
* \*\*Background / Purpose:\*\*Additional attribute RELATION add in codelist CSD for dynamic calculation of weight and Height units to display the conversions from KGs to Grams and CM to Inches.
* **Feature** **Description**:
  * These updates apply to the WEIGHT, BIRTH\_WEIGHT, and HEIGHT fields.
  * The RELATION attribute (e.g., 1000 for "Kgs") enables the system to allow userdefined/customized entries where applicable.
* **Impact on Other Products**: No impact on other products.

**5.39.7 Event Categorization**

* **Jira ID:PVADMIN-44053**
* \*\*Background / Purpose:\*\*A new “Event Categorization” configuration screen is introduced in PV Admin, enabling users to tag MedDRA PT terms and Trade Names with IME, DME, ASTL, and AESI classifications. This supports efficient identification and management of medically important events across products with enhanced validation, bulk operations, and audit tracking.
* \*\*Feature Description:\*\*A new "Event Categorization" option is added in PV Admin to allow configuration of event classifications using PT terms and Trade Names.
* Supports categorization into IME, DME, ASTL, AESI using toggle controls.
* Allows multi-select, bulk upload, and wild card search for MedDRA PT and Trade Names.
* Includes validation, audit logging, import/export, and sorting/filtering capabilities.
* **Impact on Other Products:** No impact on other products.

**5.39.8 Sub type attribute for Parent Child Case Codelist**

* **Jira ID:PVADMIN-42211**
* \*\*Background / Purpose:\*\*In the existing system, the Parent/Child Case codelist does not provide an explicit way to identify the specific relationship type (such as Mother Case, Father Case, or Child Case) for custom values. This limits the ability of downstream systems and internal processes to interpret and use these values effectively, particularly for autocalculations and automated logic that depend on understanding these relationships. To address this, a new attribute “Subtype” is introduced in the Parent/Child Case codelist. This enhancement ensures clearer data definition and supports consistent processing of Parent/Child relationships across modules and integrations.
* **Feature Description:The Parent/Child Case codelist is enhanced with an additional attribute: Subtype. This attribute specifies the relationship type of each codelist entry, supporting the following values:**
* Mother Case
* Father Case
* Child Case
* **Impact** **on Other Products**: Impacts categorization of pregnancy cases in PVS

### 5.40 Feature: Configuration Export and Import

**5.40.1 Pre-Populate Product Event Relatedness**

* **Jira ID:PVADMIN-44931**
* \*\*Background / Purpose:\*\*The system now supports bulk import/export of Product-Event Relatedness business rules via PV Admin, enabling streamlined configuration of autopopulated relatedness data in the PVCM module.
* **Feature Description**: The system is now enhanced as for PV Admin enable import/export of CSD and non-CSD Product-Event Relatedness rules.
  * Supports bulk configuration and updates using excel templates for configuring rules. o Mandatory fields: Rule Name, Source, Method for implementing the functionality.
  * Pipe delimiter (|) used for multiple values as OR logic in Product Type column.

![](<.gitbook/assets/Unknown image (88)>)

Figure 87: Import / Export of PE Matrix Relatedness template

* **Impact on Other Products**: No impact on other products.

**5.40.2 Codelist - Justification**

* **Jira ID:PVADMIN-45116**
* **Background / Purpose:A new “Justification” codelist has been introduced to support users in selecting standardized reasons for data changes or deletions. The list is configurable, supports import/export, and includes multilingual values with audit tracking.**
* **Feature Description**: A configurable “Justification” codelist is now available for capturing reasons during data changes or deletions.
  * Default justifications (in English and Japanese) are provided. o Users can import/export values through the PV Admin module.
  * Additional justifications can be added as per user needs.
* **Impact on Other Products**: No impact on other products.

### 5.41 Feature: PV Admin Support for Multilingual Specific Requirements

**5.41.1 Product Configuration New Fields for PMDA JAPAN**

* **Jira ID:PVADMIN-38653**
* \*\*Background / Purpose:\*\*New Japan specific fields have been added to the Product and Study Configuration screens to support PMDA submissions. This includes enhancements to label behavior, field validation, approval number types, multilingual support, and audit logging, for Japanese product data.
* **Feature Description**: Enhancements enable configuration of Japanese values for product details and approval information. Key updates include:
  * New Japanese fields for Product Name, Generic Name and Product Set are introduced.
  * Dynamic multilingual label is enhanced in this functionality. o PMDA-specific approval codes with length constraints. o Audit log support for all changes in Product / Study configuration.

![](<.gitbook/assets/Unknown image (89)>)

Figure 88: New fields added in Product Configuration

* **Impact on Other Products**: No impact on other products.

**5.41.2 Study Configuration New Fields for PMDA JAPAN**

* **Jira ID:PVADMIN-39642**
* **Background / Purpose:The Study Configuration screen has been enhanced with new PMDA-specific fields to support Japan regulatory requirements. This includes multilingual support, updated field placement, and audit logging for studies requiring PMDA submissions.**
* **Feature Description**: New Japan-specific fields have been added to the Study Configuration screen, including CT Notification Number, Target Disease, and Study details in Japanese.
  * Fields support multilingual input via a local language modal.
  * Rearranged layout for improved usability. o Codelist and export support added for study configuration.

![](<.gitbook/assets/Unknown image (90)>)

Figure 89: New fields in Study Configuration

* **Impact on Other Products**: No impact on other products.

**5.41.3 Japanese MedDRA Dictionary Loading**

* **Jira ID:PVADMIN-39424**
* **Background / Purpose:The system has been enhanced to support Japanese MedDRA dictionary loading via the existing interface. This enables multilingual dictionary usage across applications and ensures consistency in dictionary version activation, improving localization and downstream integration.**
* **Feature Description**: Support has been added for loading and activating Japanese MedDRA dictionaries through the MedDRA screen.
  * Includes full UI validation, success/error messages, and versioning logic.
  * Activation applies to all same-version dictionaries across languages. o Enables downstream consumption and maintains historical dictionary data.
* **Impact on Other Products**: No impact on other products.

**5.41.4 J Drug Dictionary & Dosage Formulations Codelist**

* **Jira ID:PVADMIN-39421**
* \*\*Background / Purpose:\*\*The system now supports the loading and activation of the Japanese Drug (J Drug) Dictionary within PV Admin. This enhancement enables users to manage J Drug entries with validations, versioning, and audit logs like WHO MFDS, ensuring data readiness for downstream applications.
* **Feature Description**: Enhancements allow PV Admin users to load and activate J Drug dictionary files via a dedicated interface.
  * A new “J Drug” option is added under the Dictionary menu after WHO MFDS.
  * UI supports file upload, validations, version activation, and success/error notifications. o Activated versions are stored and made available for downstream consumption. o Supports multilingual validations and audit logging.
* **Impact on Other Products**: No impact on other products.

**5.41.5 Codelist Changes for New PMDA Japan Fields**

* **Jira ID:PVADMIN-39695**
* \*\*Background / Purpose:\*\*The system now supports new fields aligned with PMDA Japan requirements by adding or modifying values in the REPORT CATEGORY, ACCESS TO OTC, STUDY PHASE, LITERATURE CLASSIFICATION, APPROVAL NUMBER TYPE, and EVENT CATEGORY codelists.
* **Feature Description**: Enhancements involve updates to six codelists for PMDA-specific fields to support regulatory alignment.
  * New codelist entries added for REPORT CATEGORY, ACCESS TO OTC, STUDY PHASE, and LITERATURE CLASSIFICATION.
  * Modifications made to existing codelists: APPROVAL NUMBER TYPE and EVENT CATEGORY. o Multilingual support included for English and Japanese.
* **Impact on Other Products**: No impact on other products.

#### 5.42 Feature: Product Setup and Configuration

**5.42.1 Device Model Number Field under Approved Product Section**

* **Jira ID:PVADMIN-44234**
* **Background / Purpose:A new field, Device Model Number, has been introduced under the Approved Product section in product configuration to support auto-population in the case entry screen.**
* **Feature Description**: A configurable Device Model Number field is added under Approved Product to enhance case entry accuracy.
  * This field is configured as a text field with 80 alphanumeric characters. o Positioned between Product Code and Device Name fields. o Supports sorting, filtering, import/export, and audit logging. o Blank for legacy product configurations.

![](<.gitbook/assets/Unknown image (91)>)

Figure 90: Device Model Number field under Approved Product section

* **Impact on Other Products**:
  * Impacts the report in PVR o Impacts the PVS product on Alerts

**5.42.2 Configure Multiple Versions of Same Datasheet**

* **Jira ID:PVADMIN-37271**
* **Background / Purpose:The system now supports configuration and versioning of multiple datasheets through Product CSD import. Enhancements allow accurate tracking of datasheet updates using version control, draft creation logic, and validation rules for sequencing and activation.**
* **Feature Description**: Enhancements to Product CSD enable version control for datasheets and undesirable effects:
  * Versioning added in Datasheets and Undesirable Effects tabs. o Draft version auto created based on actions like deactivation or new entry. o Version field supports only sequential numeric values.
  * Audit log tracks version updates and deactivation status.

![](<.gitbook/assets/Unknown image (92)>)

Figure 91: Historical Datasheet Version for single datasheet

* **Impact on Other Products**: No impact on other products.

**5.42.3 Additional Attributes to Calculate Listedness Information**

* **Jira ID:PVADMIN-45769, PVADMIN-44679**
* \*\*Background / Purpose:\*\*A new feature, Advanced Auto-Listedness, has been introduced to streamline the listedness assessment process by allowing configuration of attribute values at both datasheet and undesirable effect levels. This includes rule-based logic, edit/clear capabilities, MedDRA/Product browser support, bulk import/export, and enhancements to listedness.
* **Feature Description**: A dedicated interface supports advanced attribute management and listedness logic:
  * Users can Edit/Clear attributes using MedDRA and Product browsers. o Datasheet- and event-level configurations with rule-based logic (AND/OR). o Bulk import/export via Excel template with pipe-delimited values. o Attributes directly influence real-time listedness calculations.

![](<.gitbook/assets/Unknown image (93)>)

Figure 92: Advanced Auto-Listedness rule table

* **Impact on Other Products**:
  * Impacts the ICSR report in PVR o Impacts the PVS product on Alerts

#### 5.43 Feature: User & User Group Management

**5.43.1 PV Admin Role Configuration**

* **Jira ID:PVADMIN-37278**
* \*\*Background / Purpose:\*\*The system is enhanced through role-based access control for each PV Admin module. Users can now be assigned Full, View, or No Access per module or submodule, enhancing security, visibility, and control. View restrictions are enforced across UI elements, and role assignments are auditable and Excel-import compatible.
* **Feature Description**: The PV Admin application now supports fine-grained access control at module and sub-module levels.
  * Access types include Full, View, and No Access. o Role-based visibility of menus and UI actions is enforced.
  * Role assignments mirror PVCM’s user/group management structure. o Audit logs and Excel imports support these new roles.

![](<.gitbook/assets/Unknown image (94)>)

Figure 93: Access control in PV Admin role configuration

* **Impact on Other Products**: No impact on other products.

#### 5.44 Feature: Configuration Management & Configuration Comparison Module

**5.44.1 PV Admin Role Configuration**

* **Jira ID:PVADMIN-46238, PVADMIN-45850**
* **Background / Purpose:Enhance the Configuration Compare feature to support newly added fields and dual language functionality for both PV Admin and PVCM components.**
* **Feature Description**: The Configuration Compare feature now supports all changes related to dual language support and Central Field Management (CFM) for PV Admin and PVCM components.
* **Impact on Other Products**: No impact on other products.

#### 5.45 Feature: WHO C3 Dictionary Support

**5.45.1 C3 Dictionary Support in PV Admin**

* \*\*Jira ID:\*\*PVADMIN-46361
* \*\*Background / Purpose:\*\*The purpose of this enhancement is to enable the PVADMIN module to support the loading and integration of the WHO Drug Dictionary (WHO C3 format) in both English and Chinese. This functionality will facilitate granular product coding to ensure accurate identification and classification of medicinal products, thereby supporting compliance with local regulatory requirements.
* **Feature Description**: PVADMIN will support loading and activation of the WHO Drug Dictionary (WHO C3 format) in addition to B3 format in both English and Chinese.
  * User can select the language (English or Chinese) at the time of loading the WHO C3 dictionary. The loaded dictionary will be stored with the selected language indicated in the version name (e.g., “GLOBALC3Mar24 (Chinese)” or “GLOBALC3Mar24 (English)”).
  * Users can activate either WHO B3 or WHO C3 dictionaries from a unified dropdown menu. o Activated WHO dictionary (B3 or C3) details will be displayed in the WHO browser in PVCM.

![](<.gitbook/assets/Unknown image (95)>)

Figure 94: C3 Support in PV Admin

* \*\*Impact on Other Products:\*\*No impact on other products.

**5.45.2 MFDS Drug Dictionary Support in Alignment with C3 dictionary**

* \*\*Jira ID:\*\*PVADMIN-46368
* **Background / Purpose**: The purpose of this enhancement is to enable PVADMIN to support Korean users to efficiently select and populate MFDS Drug Code and Substance Code for domestic cases in alignment with the WHO C3 dictionary, supporting compliant Korean E2B(R3) reporting.
* **Feature Description**: PVADMIN will support loading and activation of the LinkKoreaC3 dictionary, similar to LinkKoreaB3, enabling Korean users to populate MFDS Drug Code and Substance Code for domestic cases.
  * LinkKoreaC3 upon loading will be listed in the "Activate Version" dropdown alongside LinkKoreaB3, with only one active at a time.
  * System will prevent activation conflicts between WHO B3 and LinkKoreaC3, and vice versa. If incompatible dictionaries are selected in the MFDS screen, an error will appear.
  * When both WHO C3 and LinkKoreaC3 are activated, MFDS Drug Code info will be shown in the WHO C3 browser (for Korean cases).

![](<.gitbook/assets/Unknown image (96)>)

Figure 95: Dictionary Activation in PV Admin

* **Impact on Other Products**: No impact on other products.

**5.45.3 Encoding of Products via WHO Drug C3 Dictionary in PVCM**

* **Jira ID**: PVCM-63972
* \*\*Background / Purpose:\*\*The purpose of this enhancement is to support encoding of products from the C3 browser to facilitate granular product coding, thereby supporting compliance with local regulatory requirements.
* **Feature Description**: When the WHO C3 dictionary is activated, PVCM will support additional fields such as MPID, Dosage Form, Substance Strength, MAH, and Country, along with enhanced search capabilities to allow more granular product identification and selection.
  * Supports consistent UI behavior across WHO B3 and C3, with dictionary-specific fields shown based on the active version in PV Admin.
  * When a product is selected from the WHO C3 dictionary, key fields including Product Name, Strength, Medicinal Product ID (MPID), and WHO Codes will be automatically populated in the case form.
  * For cases with the case country set as Korea (Republic of), the system will also autopopulate the MFDS Drug Code and MFDS Substance Codes, as per Korean requirements.
  * During intake (e.g., E2B, email), the application performs layered matching logic prioritizing country of incidence and product attributes for accurate encoding.

![](<.gitbook/assets/Unknown image (97)>)

Figure 96: WHO Drug C3 Dictionary Browser

* **Impact** **on Other Products**: No impact on other products.

**5.45.4 C3 Dictionary Support for Product Coded from Company Product Dictionary**

* **Jira ID:** PVCM-111755
* **Background / Purpose**: The purpose of this enhancement is to enable WHO C3 browser lookup for the **MPID** field, allowing users to search and populate limited C3 attributes—such as \*\*MPID, MFDS information, etc.\*\*for products coded from the company product dictionary, in alignment with local regulatory requirements.
* **Feature Description**: A blue browser icon will be added next to the MPID field in the Product section, enabling WHO C3 dictionary lookup. When clicked, it opens the WHO C3 browser to search and select product related information.
  * The icon is conditionally displayed—visible only if the product is coded via the Company Product Dictionary.
  * Upon selection, the system auto-populates WHO Drug MPID, WHO Drug Code, WHO Drug Version (C), and MFDS codes (for Korean cases), without altering other information which is derived from company product dictionary.
  * The feature is configurable, allowing clients to enable/disable the browser and define which fields should be auto-populated.

![](<.gitbook/assets/Unknown image (98)>)

Figure 97: WHO Drug Browser - MPID Field

* **Impact** **on Other Products**: No impact on other products.

**5.45.5 Intelligent Auto population of WHOC3 Attributes for Company Suspect Drugs**

* **Jira ID:** PVCM-110693, PVCM-112074
* **Background / Purpose**: The purpose of this enhancement is to enhance data accuracy and efficiency by implementing intelligent auto-population of C3 attributes—such as MPID, Drug Code, MFDS Code, and WHO C Version—using machine learning for products coded with the company product dictionary.
* **Feature Description**: The system auto-populates C3 related fields in case forms using ML driven capability from historical data and the C3 dictionary when products are coded from the company dictionary.
  * Auto-population is activated only when a product is coded from the company product dictionary, matching attributes from the PVCM Case Form Input field to auto populate the key drug related fields such as MPID, MFDS etc in the case form.
  * A clickable “AI icon” next to MPID will be available and reveal top ranked matches in a configurable table, enabling users to select and auto-populate fields manually if needed.
  * The feature is configurable, allowing clients to enable/disable the feature and also define which fields should be auto populated.
* **Impact** **on Other Products**: No impact on other products.

#### 5.46 Feature: FDA E2B R3 Support

**5.46.1 FDA E2B R3 Support – PV Admin**

* \*\*Jira ID:\*\*PVADMIN-45897
* **Background / Purpose**: The purpose of this enhancement is to update code lists in PVADMIN to support their availability in PVCM and subsequent downstream systems, ensuring compliance with E2B R3 submission requirements as per the FDA E2B R3 profile.
* **Feature Description**: The PV ADMIN codelist values have been enhanced across the Product (additional drug info), Study Registration, Null Flavour sections etc. The FDA-specific codes have been assigned to relevant codelist values to ensure compliance with FDA regulatory requirements.
* **Impact on Other Products:** This enhancement impact the following areas:

o Impacts the E2B ICSR report in PVR

**5.46.2 FDA E2B R3 Support – PVCM**

* \*\*Jira ID:\*\*PVCM-107463
* **Background / Purpose**: This enhancement aims to support Null Flavor for additional PVCM case fields required for case processing, ensuring compliance with FDA E2B R3 requirements.
* **Feature Description**: Additional Null Flavor support has been implemented end-to-end for specific PVCM fields, with the Null Flavor values available for activation based on client requirements. Furthermore, an additional DQCR has been introduced for the Product > Add'l Drug Info field to enforce that only one FDA-specific value can be selected in the field.
* Impact on Other Products:

o Impacts the E2B ICSR report in PVR

#### 5.47 Feature: Patient Initials Auto population based on Patient Name

**5.47.1 Patient Initials Auto population based on Patient Name**

* \*\*Jira ID:\*\*PVCM-107737
* **Background / Purpose**: The purpose of this requirement is to enable the system to automatically populate the patient’s initials. This functionality aims to improve data entry efficiency, ensure consistency, and reduce manual input errors.
* **Feature Description**: Initials are automatically generated in patient initials field using the first letters of the first, middle, and last names of the patient. They are updated automatically upon any name changes.

o The system will allow the Manual overrides of initials if the initials are auto calculated o Auto-calculation is initiated exclusively for global system updates, ensuring synchronization between global and Japan systems, while local Japan-only modifications do not trigger recalculation.

* **Impact** **on Other Products**: No impact on other products

#### 5.48 Feature: Define reportable based on Product Type

**5.48.1 Reportability based on Product Type – PV Admin**

* **Jira ID**: PVADMIN-46396
* **Background / Purpose**: The purpose of this enhancement is to enable additional Version Disposition codelist values specific to product types of **Drug** and **Device**. This capability is essential to accurately determine ICSR scheduling and to prevent over-reporting in scenarios where the information received is applicable only to either the drug or the device component. By introducing these additional disposition values, the system will support more precise and compliant safety reporting, aligned with both business requirements and regulatory obligations.
* **Feature** **Description**:
  * New Code List Values of Drug-Reportable and Device-Reportable will be available in Version Disposition alongside existing values.
  * Values can enabled/disabled per client needs to avoid UI clutter. o All four values will be enabled by default (Reportable, Non-Reportable, Drug Reportable and Device Reportable).
* **Impact** **on** **Other** **Products**:
  * Impacts the E2B ICSR report in PVR

**5.48.2 Reportability based on Product Type – PVCM**

* **Jira ID:** PVCM-107455
* **Background / Purpose**: The purpose of this enhancement is to support reportability based on product type when a case includes product types, such as a drug and a device. The PVCM Version Disposition field will allow users to select disposition values based on reportability needs. This enhancement ensures accurate ICSR scheduling and prevents over-reporting in scenarios when the information is relevant only to one product type.
* **Feature** **Description**:
  * Enhance the Version Disposition field to support additional selection of Drug-Reportable and Device-Reportable values, ensuring correct ICSR reporting for cases consisting of two different product types.
  * Implemented DQCR validation to ensure the selected disposition matches the product type. For example, Drug-Reportable requires at least one drug-type product
  * Default value remains Reportable for a new record; other values are manually selectable unless the mapping is defined.

![](<.gitbook/assets/Unknown image (99)>)

Figure 98: Version Disposition Field

* **Impact** **on Other Products**: Impacts the E2B ICSR report in PVR

#### 5.49 Feature: Co-Packaged Combo Product Support

**5.49.1 System Support for Co-package Combo Product**

* \*\*Jira ID:\*\*PVADMIN-40687
* **Background / Purpose**: The purpose of this enhancement is to enable clear identification, configuration, and management of combo products along with their linked products within the product configuration, ensuring accurate tracking, reporting, and handling of co-packaged products throughout their lifecycle.
* **Feature** **Description**:
  * A new “Combo Product” checkbox is added at the product level in Product Configuration, which when selected enables a multiselect “Linked product(s)” field below the

Trade/Investigational Name that allows choosing only configured products via a lookup browser

*
  * Users can add, remove, and reorder linked products using drag-and-drop or arrow controls, with the system preventing unconfigured entries and supporting scroll/expand functionality for multiple items.
  * The system provides warnings when required linked products are missing, when disabling the Combo Product flag may remove linked data and restricts deletion of linked items with appropriate alerts.

Figure

99

:

Combo Product Icon

![](<.gitbook/assets/Unknown image (100)>)

* **Impact on Other Products**:
  * Impacts the E2B ICSR report in PVR o Impacts the PVS and PVA products

**5.49.2 Co-package Combo Product: Auto population and Support in Case Form**

* \*\*Jira ID:\*\*PVCM-98814
* **Background / Purpose**: The purpose of this enhancement is to support co-packaged combo products by enabling an automatic population of multiple linked products based on selections made in the product browser.
* **Feature Description**:
  * Selecting a co-packaged master product in the Case Entry Form auto-populates all constituent products, displaying them in the specific format.
  * Constituent products have disabled product browser, delete, and copy options; only the master product is editable, and deleting the master product will removes all linked constituents' products.
  * Follow-up difference, merge, and rejection treat the master and constituent products as one unit.

Figure

100

:

Combo Product in Products Section

![](<.gitbook/assets/Unknown image (101)>)

* **Impact on Other Products**:
  * Impacts the E2B ICSR report in PVR o Impacts the PVS and PVA products

#### 5.50 Feature: Split of Sender Name Field (Sender Name Free text as a new field)

**5.50.1 Split Sender Name Field to Capture Structured and Unstructured Data Separately**

* \*\*Jira ID:\*\*PVCM-107762
* **Background / Purpose**: The purpose of this enhancement is to enhance the Sender Name field in the PVCM application by splitting it into two distinct fields—one for structured codelist values and one for unstructured free text input—to improve data control, support compliance tracking, and optimize data incoming matrix.
* **Feature Description**:
  * The existing Sender Name field which accommodates both codelist information and free text information is split into two: a structured typeahead codelist field and a new Sender Name (Free Text) field placed side by side in the General section. o Incoming data (E2B, JSON, Email, Webform, ML) first attempts to match values from the Codelist; if no match, the value is captured in the Free Text field.
  * During upgrade, existing data is auto split into the appropriate fields.

![](<.gitbook/assets/Unknown image (102)>)

Figure 101: Splitted Sender Name Field

* **Impact** **on Other Products**: No impact on other products.

**5.50.2 Codelist Support for Sender Name (codelist) Field and PII Support for New Sender Name (Free Text) Field**

* \*\*Jira ID:\*\*PVADMIN-45937
* **Background / Purpose**: The purpose of this enhancement is to enable clear identification, configuration, and management of combo products along with their linked products within the product configuration, ensuring accurate tracking, reporting, and handling of co-packaged products throughout their lifecycle.
* **Feature Description**:
  * The Sender Name field on the UI will display merged values from both the Sender Name Codelist and Organization Unit Codelist for selection. o The new free text field will be configurable as a PII field in PV Admin, ensuring data privacy and compliance with personal data regulations.
  * All changes to the codelist and the new field will be tracked in audit logs, and the system will handle UI display correctly even if only one codelist is configure.
* **Impact** **on Other Products**: No impact on other products.

#### 5.51 Feature: Multilingual Support for Additional Case form Fields

**5.51.1 Multilingual Support for Additional Case form Fields**

* \*\*Jira ID:\*\*PVCM-111912
* **Background / Purpose**: To implement end-to-end multilingual support for specified fields to ensure accurate and localized data capture. This enhancement will enable seamless integration with downstream systems. It is specifically designed to meet local requirements for some of the authority's requiring information in the local language.
* **Feature Description**:
  * Specific fields across product, patient, event, study, and literature sections to support entry of local Language input, consistent with existing multilingual behavior.
  * All newly supported multilingual fields will show up multilingual box consistent with existing multilingual behavior in terms of display, editing post-finalization, and availability of language icons, with editing post-finalization as configurable feature.
  * Multilingual data to be available end-to-end, including downstream systems and templates (e.g., BCE), ensuring full visibility and usability.
  * Fields configured as Blinded will restrict language icon access with appropriate warnings; all changes will be tracked in audit logs.

![](<.gitbook/assets/Unknown image (103)>)

Figure 102: Multi-lingual Supported Fields

* **Impact on Other Products**: Impacts the E2B ICSR report in PVR.

## 6. Issues Addressed in this Release (Bug Fixes)

| **S. No.** | **JIRA ID** | **Issue Description**                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ---------- | ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.         | PVCM-101209 | Multiple issues were noted with user operations. OTP emails were sometimes triggered more than once when accessing the webform. In the full case entry template, product questionnaires were not accessible. Follow-up cases showed missing auto-populated fields, and webform submissions failed when multiple reporters were involved. \[Additional Jira reference ID includes: PVCM-46574, PVCM-86175, PVCM-13592, PVCM-110681, PVCM77794, PVCM-68675] |
| 2.         | PVCM-103632 | Inconsistencies were observed in attachment handling after the upgrade, where some files were missing, inaccessible, or could not be modified across cases and versions. In certain situations, related audit log entries were not recorded, making it difficult to trace the attachment. \[Additional Jira reference ID includes: PVCM-98015, PVCM-103922, PVCM-96427, PVCM-124247]                                                                      |
| 3.         | PVCM-87626  | Discrepancies were noted in the E2B R2 viewer where linked report numbers, parent medical history, and route information were not displayed correctly. Attachments occasionally appeared in the wrong language, and redactions were visible only after a manual refresh. \[Additional Jira reference ID includes: PVCM-95595, PVCM-82438, PVCM-77193, PVCM-91758]                                                                                         |
| 4.         | PVCM-100994 | Issues were noted with case handling during copy or split follow-up operations. Attachments were sometimes missing, and version information displayed in duplicate or incorrect entries. \[Additional JIRA reference ID includes: PVCM-87546]                                                                                                                                                                                                             |
| 5.         | PVCM-95347  | Users experienced multiple issues in the PVCM Case form, including truncation of data in certain fields, limitations on field lengths, restrictions on how information is displayed, and failures during case transmission. These problems cause delays and inconsistencies in the information captured. \[Additional Jira reference ID includes: PVCM-105743, PVCM-73931, PVCM-62563]                                                                    |
| 6.         | PVCM-119284 | Delays and failures were observed in ICSR and XML file generation, with some cases remaining in the scheduled state without producing any output and causing processing interruptions. \[Additional Jira reference ID includes: PVCM-84345, PVADMIN-46391, PVCM-124590, PVCM-106352, PVCM-109756]                                                                                                                                                         |

| **S. No.** | **JIRA ID** | **Issue Description**                                                                                                                                                                                                                                                                                                                                                                                                           |
| ---------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 7.         | PVCM-98846  | Issues were observed in PVCM related to reporters and events, including updates not being applied correctly, restrictions on removal, duplicate entries, and occasional errors during parsing or data handling. \[Additional Jira reference ID includes: PVCM-106769, PVCM-118587, PVCM-64218]                                                                                                                                  |
| 8.         | PVCM-44472  | In PVCM, users experienced unnecessary screen refreshes, occasional incorrect warning messages, and inconsistent behavior between tabs, which sometimes disrupted navigation and made it harder to view or update case information efficiently. \[Additional Jira reference ID includes: PVCM-124305, PVCM-86168, PVCM-58783, PVCM-31771]                                                                                       |
| 9.         | PVCM-117142 | Delays were observed during ACK imports, causing postponed case processing. Users also faced partner case rejections, multiple downloads of the same case, and incorrect default values being applied during E2B imports, affecting workflow consistency. \[Additional Jira reference ID includes: PVCM-114443, PVCM-96847, PVADMIN-44178, PVCM-80160, PVCM-96612, PVCM-98831, PVCM-96721, PVCM89251, PVCM-113819, PVCM-117444] |
| 10.        | PVCM-117739 | Parsing issues were observed in Lab Follow-Up terms, causing incorrect data interpretation. Additionally, the Case Country field was sometimes populated incorrectly, leading to inaccurate case details in PVCM records. \[Additional Jira reference ID includes: PVCM-100046]                                                                                                                                                 |
| 11.        | PVCM-116359 | In PVCM, the submission date sometimes does not appear correctly in the Case List. Additionally, autocomplete updates the Case State incorrectly, and both bulk and individual case transmit operations fail intermittently. \[Additional Jira reference ID includes: PVCM-95341, PVCM-96916]                                                                                                                                   |
| 12.        | PVCM-100993 | Inconsistencies were observed in PVCM, including occasional incorrect case lock warnings, unexpected transmission failures during routine operations, and limits on comment length validation that may affect how they are displayed within the system. \[Additional Jira reference ID includes: PVCM-79083, PVCM-66963]                                                                                                        |
| 13.        | PVCM-73936  | Some fields in the Case PDF were displayed incorrectly, and the timestamp for the First Receipt Date did not match the expected value, requiring adjustment for consistent presentation in generated documents.                                                                                                                                                                                                                 |

| **S. No.** | **JIRA ID**   | **Issue Description**                                                                                                                                                                                                                                                                                                                                                                                  |
| ---------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
|            |               | \[Additional Jira reference ID includes: PVCM-49626]                                                                                                                                                                                                                                                                                                                                                   |
| 14.        | PVCM-106481   | Duplicate entries of Version 2 were observed in cases, with some records marked as 'Initial' and certain new records displaying version numbers that do not align with the expected sequence. \[Additional Jira reference ID includes: PVCM-100045]                                                                                                                                                    |
| 15.        | PVCM-91734    | Inconsistencies were observed in case assignment and user group functionality, including occasional mismatches in workflow due dates and incomplete or delayed assignment logs, which may affect how assignment details are displayed or tracked in the system. \[Additional Jira reference ID includes: PVCM-82341, PVCM-78004, PVCM-98054, PVCM-101249, PVCM83581, PVCM-109465, PVCM-72026]          |
| 16.        | PVADMIN-47915 | The disabled code continues to appear in the Sender Name dropdown, allowing users to select incorrect or inactive entries. To address this, the system has been updated to deactivate the decoding of the Sender Name and remove all associated contact entries.                                                                                                                                       |
| 17.        | PVADMIN-45189 | The system lacks proper mapping between Approval Type and Authorization Type, resulting in inconsistencies while determining whether the approval belongs to a Marketed or Investigational Drug/Device/Vaccine. To resolve this, mapping between Approval Type and Authorization Type has been maintained in the code list so that the correct authorization number can be generated for ICSR reports. |
| 18.        | PVCM-90582    | The Reference Sub-Type field was displayed twice in the Full Case Entry screen, causing a minor duplication in the user interface without affecting other case details or functionality.                                                                                                                                                                                                               |
| 19.        | PVCM-97762    | Some fields in the Case Entry Form display values that are incorrect or appear in addition to the expected entries in the system.                                                                                                                                                                                                                                                                      |
| 20.        | PVADMIN-46859 | In PV Admin, some system entries with restricted keywords or configuration key values containing special characters were not updated consistently, leading to minor inconsistencies in displayed data across the interface. \[Additional Jira reference ID includes: PVADMIN- 46908]                                                                                                                   |
| 21.        | PVCM-103767   | The Follow-Up Difference feature in PVCM does not consistently display complete comparisons between case versions. Users also experience difficulties while creating, accepting, rejecting, or merging follow-up versions for certain cases, with some actions not working as expected for legacy or existing cases.                                                                                   |

| **S. No.** | **JIRA ID** | **Issue Description**                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ---------- | ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|            |             | \[Additional Jira reference ID includes: PVCM-113033, PVCM-104613, PVCM-99040, PVCM-96566, PVCM- 74090, PVCM-79762, PVCM-63236, PVCM-61231]                                                                                                                                                                                                                                                                                                  |
| 22.        | PVCM-106282 | Data quality checks in the system showed inconsistencies, such as unexpected rule behaviors, occasional incorrect triggers, and some workflow routing not following the intended path, requiring attention during review. \[Additional Jira reference ID includes: PVCM-103806, PVCM-99831, PVCM-112120, PVCM-105875, PVCM87549, PVCM-104692, PVCM-100038]                                                                                   |
| 23.        | PVCM-87664  | In E2B(R3), the event date view displayed inconsistently, and some fields that should remain inactive were not greyed out. A few display variations were noted during regular case review. \[Additional Jira reference ID includes: PVCM-87581]                                                                                                                                                                                              |
| 24.        | PVCM-123310 | Follow-up emails and queries are not consistently identified within the PVCM intake system. In some cases, the information is not captured as expected, leading to occasional variations in intake processing. \[Additional Jira reference ID includes: PVCM-96488]                                                                                                                                                                          |
| 25.        | PVCM-103896 | Cases occasionally encounter issues during creation, editing, or saving. Some records displayed incomplete details, and a few instances showed irregular behavior while transmitting case-related information. \[Additional Jira reference ID includes: PVCM-102768, PVCM-117655, PVCM-97655, PVCM-89494, PVCM- 124332, PVCM-118477, PVCM-102699, PVCM85995, PVCM-98388, PVCM-109752, PVCM-96539, PVCM-105630, PVCM-87617]                   |
| 26.        | PVCM-96915  | In PVCM UI, product details occasionally appear as 'Deprecated', and several auto-calculated fields, task completion dates, and date-time values display inconsistently. These inconsistencies are visible until cases are refreshed, updated, or revisited by the user. \[Additional Jira reference ID includes: PVCM-109340, PVCM-87556, PVCM-72175, PVCM-62656, PVCM124342, PVCM-83374, PVCM-79592, PVCM-103755, PVCM-112095, PVCM-96180] |
| 27.        | PVCM-91820  | Product dictionary includes missing entries, incorrect strength and indication of info display, and incomplete strength population. \[Additional Jira reference ID includes: PVCM-109269, PVCM-84538]                                                                                                                                                                                                                                        |
| 28.        | PVCM-68599  | Some parsing variations were noted across sections such as CIOMS text, event coding, spam entries, and unstructured content, with a few inconsistencies occurring during information processing.                                                                                                                                                                                                                                             |

| **S. No.** | **JIRA ID**   | **Issue Description**                                                                                                                                                                                                                                                                                                                                |
| ---------- | ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|            |               | \[Additional Jira reference ID includes: PVCM-47653, PVCM-56928, PVCM-87496]                                                                                                                                                                                                                                                                         |
| 29.        | PVCM-93136    | Variations were noted in data mapping and field outputs, with occasional gaps in Chinese results and comments. A few records showed incomplete values, creating minor inconsistencies in application views and reports. \[Additional Jira reference ID includes: PVCM-93004, PVCM-100936]                                                            |
| 30.        | PVCM-102616   | Some intake-related inconsistencies were noted, including occasional misrouted assignments, a few missing or duplicate case records, and certain instances where case details were not displayed as expected. \[Additional Jira reference ID includes: PVCM-101642, PVCM-57389, PVCM- 24912]                                                         |
| 31.        | PVCM-97805    | Inconsistencies were observed in PV Admin audit logs, such as unchanged privacy location updates and occasional missing blinding profile entries. A few duplicate or inaccurate records were also noticed. \[Additional Jira reference ID includes: PVCM-86236, PVCM-93007, PVCM-96454, PVCM-88063, PVCM87511, PVCM-13690]                           |
| 32.        | PVCM-87636    | Inconsistencies were observed in V3 listedness, such as occasional incorrect IB version display and intermittent missing datasheets in certain scenarios. \[Additional Jira reference ID includes: PVCM-107437, PVCM-87573, PVCM-91832]                                                                                                              |
| 33.        | PVCM-58782    | Minor inconsistencies were noted in ML Parser confidence and unstructured parsing, including occasional empty fields, unexpected highlights, and display variations during processing. \[Additional Jira reference ID includes: PVCM-49610, PVCM-15789]                                                                                              |
| 34.        | PVADMIN-44915 | Irregularities were noted in MedDRA coding, including occasional duplicate records, minor download interruptions, and intermittent pop-up issues. A few coding entries did not appear as expected during review. \[Additional Jira reference ID includes: PVADMIN44913, PVCM-99999, PVCM-68607]                                                      |
| 35.        | PVCM-102743   | Multilingual product fields in PVCM were observed to be non-editable in certain cases, and the application occasionally did not respond when the browser language was set to Japanese, limiting user interaction.                                                                                                                                    |
| **S. No.** | **JIRA ID**   | **Issue Description**                                                                                                                                                                                                                                                                                                                                |
|            |               | \[Additional Jira reference ID includes: PVCM-60088]                                                                                                                                                                                                                                                                                                 |
| 36.        | PVCM-90443    | During fresh installation, the E2B Importer component failed as S3 bucket creation in the us-east-1 region failed due to AWS S3 library limitations; additionally, support for Instance Metadata Service (IMDSv2) is required. \[Additional Jira reference ID includes: PVCM-95269]                                                                  |
| 37.        | PVCM-77876    | System issues identified where product/event updates are not reflected, and the PEM section fails to load due to sequencing errors as per event section. \[Additional Jira reference ID includes: PVCM-72052, PVCM-125243, PVCM-115660, PVCM-102632]                                                                                                 |
| 38.        | PVCM-89339    | In PV Admin and PVCM, some inconsistencies were observed in study product management, including irregular ordering of study products and occasional missing study type information during coding. Additional Jira reference ID includes: PVCM-87329, PVCM-86264, PVADMIN-45689]                                                                      |
| 39.        | PVCM-69478    | Case assignment logs sometimes show null values for users who have been disabled, and there are occasional issues when adding new user groups, affecting assignment tracking visibility. \[Additional Jira reference ID includes: PVCM-91872]                                                                                                        |
| 40.        | PVCM-83341    | Multiple PVI functional and validation issues observed, including case duplication, incorrect field handling, auto-calculation failures, attachments, and display inconsistencies. \[Additional Jira reference ID includes: PVCM-94175, PVCM-97840, PVCM-90732, PVCM-35568, PVCM90617, PVCM-115188, PVCM-96691, PVCM-114257, PVCM-18884, PVCM-20114] |

**NOTE:**\[PVCM-124247, PVCM-79762 and PVCM-89494] - These three issues are considered non-valid as part of the PVCM 7.0 release due to the implementation of new functionalities.

## 7. List of Patches Merged

| **S. No.** | **Product Name**   | **Version No#** |
| ---------- | ------------------ | --------------- |
| 1          | PV Case Management | 6.1.0.8         |
| 2          | PV Case Management | 6.1.0.9         |
| 3          | PV Case Management | 6.1.0.10        |
| 4          | PV Case Management | 6.2.0.6         |
| 5          | PV Case Management | 6.2.0.7         |
| 6          | PV Case Management | 6.2.0.8         |
| 7          | PV Case Management | 6.2.0.9         |

## 8. New/Modified Code Lists Introduced

| **CodeListID** | **Code List\*\*\*\*Name** | **New/Modified Code List ID** | **New/Modified\*\*\*\*Code List Name** | **Purpose**                                                                                                   | **Values**                                   |
| -------------- | ------------------------- | ----------------------------- | -------------------------------------- | ------------------------------------------------------------------------------------------------------------- | -------------------------------------------- |
| N/A            | N/A                       | 136                           | LAB TEST MORE INFORMATION              | Codelist has been added to indicate if more information is held by the sender about the test and test result. | Below values are added: Yes No               |
| N/A            | N/A                       | 137                           | PREFERRED WORKFLOW STATE               | Codelist has been added to indicate the preferred workflow state.                                             | Below values are added: Active Final         |
| N/A            | N/A                       | 138                           | MALFUNCTION TYPE                       | Codelist has been added to define the category that describes the malfunction.                                | Below values are added: CIRM Not CIRM        |
| N/A            | N/A                       | 200                           | REPORT CATEGORY                        | Codelist has been added to select the reporting category for PMDA reporting.                                  | Please refer to 7.0 CSD values.              |
| N/A            | N/A                       | 201                           | ACCESS TO OTC                          | Codelist has been added to select the reason for a drug to be made available as an Over the Counter.          | Please refer to 7.0 CSD values.              |
| N/A            | N/A                       | 202                           | LITERATURE CLASSIFICATION              | Codelist has been added to classify literature.                                                               | Please refer to 7.0 CSD values.              |
| N/A            | N/A                       | 203                           | J DRUG DOSAGE FORMULATION              | Codelist has been added to select J dosage form and formulation.                                              | Please refer 7.0 CSD for values              |
| N/A            | N/A                       | 204                           | PATIENTS UNDER TREATMENT               | Codelist has been added to indicate patient is under treatment or not.                                        | Below values are added: Yes No               |
| N/A            | N/A                       | 205                           | APPROVAL CATEGORY                      | Codelist has been added to define the type of                                                                 | Please refer 7.0 CSD for values              |
| **CodeListID** | **Code List\*\*\*\*Name** | **New/Modified Code List ID** | **New/Modified\*\*\*\*Code List Name** | **Purpose**                                                                                                   | **Values**                                   |
|                |                           |                               |                                        | license or registration category for the product.                                                             |                                              |
| N/A            | N/A                       | 206                           | OTC DRUG RISK CATEGORY                 | Codelist has been added to provide the risk of drug category.                                                 | Please refer 7.0 CSD for values              |
| N/A            | N/A                       | 208                           | BMI GROUP                              | Codelist has been added to define BMI group based on BMI(KG/M^2)                                              | Please refer 7.0 CSD for values              |
| N/A            | N/A                       | 210                           | YNU States                             | Codelist has been added to generically represent Yes/No values.                                               | Below values are added: Yes No               |
| N/A            | N/A                       | 211                           | JUSTIFICATION ACTIONS                  | Codelist has been added to display actions for which justification dialog box will appear.                    | Please refer 7.0 CSD for values              |
| 126            | REFERENCE SUB TYPE        | 126                           | REFERENCE SUB TYPE                     | Added additional reference sub-type to maintain parent-child linkage in copied/split cases.                   | Below values are added: Copy Case Split Case |
| 68             | LANGUAGES                 | 68                            | LANGUAGES                              | New languages are added to support document translation.                                                      | Please refer 7.0 CSD for values              |
| 46             | DOSAGE FORMS              | 46                            | DOSAGE FORMS                           | New values added as per updated list of EDQMs                                                                 | Please refer 7.0 CSD for values              |
| 6              | ADMINISTRATI ON ROUTES    | 6                             | ADMINISTRATION ROUTES                  | New values added as per updated list of EDQMs                                                                 | Please refer 7.0 CSD for values              |

**NOTE**: - Each codelist value now includes its respective J-value. Detailed information is available in section 7.0 of the CSD.

## 9. List of DB Changes

[PVCM 7.0 Release Database Changes](https://rxlogix.sharepoint.com/validation/Shared%20Documents/Forms/Docs.aspx?viewid=397dba77%2D9e04%2D4b6b%2Da4ea%2D0603c5e5c084\&id=%2Fvalidation%2FShared%20Documents%2FPV%20Case%20Management%2F7%2E0%2F10%20RELN%2FWord%2FPVCM%207%2E0%20Release%20Notes%20Database%20Changes%2Epdf\&parent=%2Fvalidation%2FShared%20Documents%2FPV%20Case%20Management%2F7%2E0%2F10%20RELN%2FWord)

## 10. Deprecated Features

No features are deprecated in this release.

## 11. Known Issues

| **S. No** | **JIRA ID** | **Issue Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | **Business Justification**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --------- | ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1         | PVCM-127048 | The system encountered multiple issues within the assigned group workflow, including incorrect reassignment of groups after case refresh, failure in user assignment, missing or inaccurate soft messages, and improper handling of case state transitions. These issues resulted in in inconsistent group ownership, incomplete user assignments, and irregular workflow progression during case processing. \[Additional Jira reference ID includes: PVCM-127029, PVCM127013, PVCM-127005, PVCM- 126937, PVCM-126881, PVCM118544]          | The identified issues are restricted to specific, non-critical scenarios, such as the display of warning messages in workflow management or false warnings appearing in rare cases — for example, when changing the assigned group for cases already in an active state. These issues are primarily related to the visibility and behavior of soft toast messages or other minor user interface elements. While they may cause minimal impact to user experience, they do not affect underlying system functionality or performance. In addition, certain issues are confined to the Bulk Assignment functionality within the Case List screen and occur only under specific conditions. These behaviors are isolated and have no adverse effect on other system features or overall operations. Given the limited scope and low impact, the issues have been classified as low impact, with resolution planned for a future release. |
| 2         | PVCM-126878 | The DQCRs are not functioning as expected in certain cases, resulting in issues that affect field validations, where specific data fields are not being validated correctly according to defined rules. Additionally, some custom DQC rules are not executing as intended, leading to inconsistencies in data quality checks. The problem also impacts the display of Personally Identifiable Information (PII), where visibility or masking behavior may not align with configuration settings, and soft deleted DQC rules are displayed in | The issue, where certain DQCRs are not being raised correctly, is confined to specific validation scenarios and some are specific to custom DQCRs. In these cases, the system may not trigger the expected data quality checks, but core functionality and overall case processing workflow remain unaffected. Workarounds have been provided to mitigate the mentioned issues, including updated deployment steps and an updated configuration file,                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |

| **S. No** | **JIRA ID** | **Issue Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | **Business Justification**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| --------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|           |             | export. Furthermore, Data quality report generation in PVCM is affected in some specific scenarios. \[Additional Jira reference ID includes: PVCM-126827, PVCM119300, PVCM-127160, PVCM116803]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | ensuring that users can continue operations without disruption. These DQCR-related issues are isolated, minor, and limited in scope, with no impact on system stability or critical operations. Given their low operational impact, resolution is planned for a future release.                                                                                                                                                                                                                                                                                                               |
| 3         | PVCM-126861 | Issues have been observed in case entry related to product information, including instances of missing or incorrect substance codes, and inaccurate population of MPID where the system fails to capture or display the correct codes for products. There are also strength mismatches, where the recorded product strength does not align with the expected values, and version conflicts, which occur when different versions of product data create inconsistencies during case entry. Additionally, validation errors have been noted during Intelligent Product Coding, preventing certain products from being coded correctly and impacting the accuracy of product information within the system. \[Additional Jira reference ID includes: PVCM-126860, PVCM126859, PVCM-126762, PVCM- 101023, PVCM-127220, PVCM127219] | Product coding issues include MFDS code auto-population in specific cases, MFDS–WHO C3 version mismatches, Strength field issues in B3, and intelligent coding of \_MPID.\_These issues are limited to specific scenarios and do not affect core system functionality, overall stability, or regulatory compliance. While they may cause minor disruptions during product coding, workarounds have been suggested wherever applicable to ensure continuity of operations. Given their isolated nature and low operational impact, resolution of these issues is planned for a future release. |
| 4         | PVCM-126751 | Issues are observed in PVCM listing and task screens, including incorrect ICSR due date calculation and task screen field labels are displayed in English instead of Japanese. \[Additional Jira reference ID includes: PVCM-125836]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | The issue specific to the Earliest ICSR Due Date column in the listing screen occurs only for cases transitioned from the global workflow to the Japan workflow. Additionally, on Japanese task screen, labels visible in English instead of Japanese. The mentioned issues are scenario-specific, low-impact, and do not compromise system performance, functionality, or                                                                                                                                                                                                                    |

| **S. No** | **JIRA ID** | **Issue Description**                                                                                                                                                                                                                                                                                                                                          | **Business Justification**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --------- | ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|           |             |                                                                                                                                                                                                                                                                                                                                                                | regulatory compliance. Effective workarounds are available and provided. Therefore, deferring these issues to future release.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| 5         | PVCM-126816 | Issues observed in the case intake process via import methods, including incorrect handling of some PMDA E2B importer tags, unexpected display of additional labels in patient history sections, and default values not populating for Source and Product role in JSON cases. \[Additional Jira reference ID includes: PVCM-126567, PVCM- 103729, PVCM-103725] | The issue is specific to a few fields where incorrect data is not displayed in the _Case Intake Error Report_. The issue is limited to the default value of population for _Source_ and _Product Role_ fields in cases created via JSON intake. A workaround exists where users can manually select the appropriate values for these fields. The mentioned issue does not impact system performance or compliance, as cases continue to be processed correctly through the JSON intake channel. The behavior observed is limited to a non-functional display aspect and does not affect workflow operations. Considering the issues are scenario specific and not related to a major business use case, the fix will be planned in a future release. |
| 6         | PVCM-125688 | Follow-up cases encounter minor inconsistencies such as delays during case merge/ Accept as follow-up,incorrect product ordering within case data, and generation of duplicate case reference numbers. \[Additional Jira reference ID includes: PVCM-120372, PVCM118534, PVCM-110681, PVCM81245, PVCM-120181]                                                  | Minor inconsistencies were observed in follow-up cases, during case merge or acceptance, including delay in rare scenarios, incorrect product ordering, and duplicate case reference generation. Additional non-critical issues include limited product visibility, manual entry of sender details due to autopopulation failure, and behaviour specific to cases created via the email intake channel. All identified issues are scenariospecific and do not impact system functionality, performance, or regulatory compliance. Workarounds are available where necessary,                                                                                                                                                                         |

| **S. No** | **JIRA ID** | **Issue Description**                                                                                                                                                                                                                                                                                                                                                                                          | **Business Justification**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --------- | ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|           |             |                                                                                                                                                                                                                                                                                                                                                                                                                | ensuring continued operational stability until resolution in a future release.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| 7         | PVCM-118579 | Minor audit log issues observed, including incorrect field labels, workflow group changes, and redundant entries. \[Additional Jira reference ID includes: PVCM-123416, PVCM126958, PVCM-126616, PVCM127045]                                                                                                                                                                                                   | Minor issues have been identified related to field name and label visibility. In certain scenarios, updates to the Sender Na&#x6D;_**e**_ field are not captured correctly. Additionally, renaming a user group or updating autotranslated labels may impact name visibility. Similar visibility issues were also observed for some updated field labels within the Task and Follow-up sections. As these issues occur only in rare cases where field labels' names are updated or renamed, their business impact is minimal. They do not affect overall system functionality, performance, or compliance. Therefore, the resolution has been scheduled for a future release to prioritize higher-impact enhancements in the current cycle. |
| 8         | PVCM-122709 | Issues observed in the dual translation screen include incorrect handling of null flavor fields, lack of synchronization between source and target views on check/uncheck, issue in display of confidence score for deleted records and unsaved data not properly retained when navigating back after confirmation. \[Additional Jira reference ID includes: PVCM-122708, PVCM110437, PVCM-127038, PVCM122604] | The identified issue is limited to the translation screen and confidence score calculation during translation,confidence score is calculated for deleted records and does not affect the integrity of the underlying data stored for the respective fields. Users can manually review and validate the system-translated fields prior to submission, ensuring data accuracy and continuity of operations. Since the issue does not impact system performance, functionality, or regulatory compliance, it has been classified as low priority and scheduled for resolution in a future release to allow focus on higher-impact and compliancecritical enhancements in the current cycle                                                     |

| **S. No** | **JIRA ID** | **Issue Description**                                                                                                                                                                                                                              | **Business Justification**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| --------- | ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 9         | PVCM-126920 | Cases created via import may require manual refresh to display auto-calculated listedness, and product sequences in the Product Event Matrix may misalign when some products are ineligible. \[Additional Jira reference ID includes: PVCM-123504] | This issue is limited to the AutoListedness functionality for cases created via E2B\_R2/R3 and JSON formats. In certain scenarios, a manual refresh in the Listedness section is required for the auto-calculated listedness to display accurately. Additionally, product sequences in the Product Event Matrix may appear misaligned when some products are ineligible; however, this is restricted to a visibility impact only. A workaround is available, and the issue does not affect system performance, functionality, or regulatory compliance. Given its limited scope and low business impact, the fix has been deferred to a future release to prioritize high-impact and compliancecritical enhancements in the current development cycle. |
| 10        | PVCM-91872  | Unable to add a user to a user group manually in the Production environment.                                                                                                                                                                       | This issue occurs only in a specific scenario where the number of users in a single group exceeds the acceptable limit. Such cases are rare, typically involving groups with thousands of users. A workaround is available—by limiting the number of active users and removing disabled or deleted users to reduce the overall count. As the issue is limited in scope and does not affect a major business use case, it has been classified as low impact and is planned for resolution in a future release to allow prioritization of higher-value enhancements in the current cycle.                                                                                                                                                                |
| 11        | PVCM-126844 | In the AE parsing form, the Additional Notes field is being auto-                                                                                                                                                                                  | In the AE Parsing form, the Additional Notes field is being                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |

| **S. No** | **JIRA ID** | **Issue Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | **Business Justification**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| --------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|           |             | populated unexpectedly, and data is not correctly parsed for certain fields, including Reference Type, Continuing, Report Source, Dose field, and the Summary section. Additionally, some fields are not capturing some values from the ML response, leading to incomplete data population during unstructured AE parsing. Minor inconsistencies have also been observed in one of the fields of the Product section. \[Additional Jira reference ID includes: PVCM-124609, PVCM127235, PVCM-127161, PVCM- 23335, PVCM-121327, PVCM121328] | auto-populated unexpectedly, and some data in Reference Type, Continuing, Report Source, Dose, and the Summary fields aren’t being parsed correctly. Additionally, some minor issues have been observed in one of the fields, and some fields are not capturing some values from the ML response, leading to incomplete data population during unstructured AE parsing. This issue only affects one out-of-thebox Japanese structured form, specifically the Summary section, and does not impact system performance, overall data integrity, or compliance. Clientspecific structured forms can still be updated during implementation to ensure accurate data mapping. Since the issue is limited in scope and has no operational or compliance impact, it will be addressed in a future release. Deferring this fix allows the team to focus on higher-priority improvements while ensuring that client-specific forms continue to work as expected. |
| 12        | PVCM-123244 | ML-parsed fields are not colorcoded during unstructured email intake for global cases, and supported entities are not highlighted in the Japanese UI for local cases when processing Japanese narratives. \[Additional Jira reference ID includes: PVCM-123243]                                                                                                                                                                                                                                                                            | The issue is limited to the colour coding used to highlight parsed fields in the system. Additionally, issue is limited to supported entities are not highlighted in the Japanese UI for local cases when processing Japanese narratives. It does not affect the actual parsing of data, system performance, or compliance in any way. Given its limited impact, this issue has been deferred to a future release. Addressing it later allows the team to prioritize higher-impact enhancements and critical fixes while ensuring                                                                                                                                                                                                                                                                                                                                                                                                                       |

| **S. No** | **JIRA ID** | **Issue Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | **Business Justification**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| --------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|           |             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | that ongoing operations and compliance remain unaffected.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| 13        | PVCM-102731 | First Receipt Date Japan and Version Receipt Date Japan are not visible in Case E2B in case information display.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | The issue is limited to the Case E2B feature in the case entry form, which is planned for deprecation and will be addressed as part of the new functionality. It does not impact overall system performance, compliance, or critical functionality. As the issue is limited to specific feature which does not impact overall system performance, compliance, or critical functionality. This has been scheduled for a future release to prioritize the other items.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| 14        | PVCM-126843 | Issues observed in local cases, including transmission failures for Japan cases, where certain case data is not successfully transmitted; incorrect label language, causing some field labels to display in the wrong language for localized forms; a disabled or incorrectly colored Auto-Translate button, which may affect visibility and usability of the translation feature; and mismatched State/Province field display, where the data shown does not consistently correspond to the selected region or follow the expected formatting and incorrect error message display on finalizing case. \[Additional Jira reference ID includes: PVCM-126817, PVCM126774, PVCM-111820, PVCM127203] | The issues identified are confined to specific and isolated scenarios and do not have any impact on overall system performance or regulatory compliance. These are minor, localized issues that affect only certain user interface elements or individual field values without compromising the core functionality of the system. Several of the issues are related to the Japan case transmission feature, where certain cases may not be transmitted as expected under very specific conditions. Other issues involve the naming of particular labels, where labels may display in an unexpected language or format, and visual indicators, such as the color of icons denoting translation-inprogress status, which may not reflect the current state accurately. Additionally, some issues occur with data received from global cases for specific fields and incorrect error message display on case finalizing; in these situations, users can apply an existing |

| **S. No** | **JIRA ID** | **Issue Description**                                                                                                                                                                                                                                                                                                                                                                                                                                  | **Business Justification**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|           |             |                                                                                                                                                                                                                                                                                                                                                                                                                                                        | workaround to manage the affected data. While these issues are minor in nature and do not impact critical operations or compliance, they have been documented to ensure future enhancements and fixes. Given their low operational impact and limited scope, resolution of these issues is scheduled for a future releas**e**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| 15        | PVCM-126855 | Minor issues observed in PVCM include ICSR section data not loading warning messages, Intelligent MedDRA coding not matching synonyms correctly, and translated records ‘protected’ checkbox functionality not behaving as expected in global cases, extra suffix in case PDF and the More Info field displaying the value ‘Select’ in a specific scenario. \[Additional Jira reference ID includes: PVCM-126549, PVCM119666, PVCM-127049, PVCM125277] | The identified issues are limited to a few specific scenarios, including message display inconsistencies within the ICSR section, unexpected behaviour of the Protected checkbox, and one isolated case in Intelligent MedDRA coding where the system is unable to encode a term that matches a synonym, extra suffix of ‘.0’ in numeric value is observed in Case PDF. Additionally, More Info field is showing ‘select’ instead of ‘No’ value for specific scenario. These occurrences are confined to narrow use cases and do not impact overall system performance, compliance, or the functionality of other critical features. While these issues may cause minor effects on user experience—such as an incorrect or unclear message display, or an inability to encode a specific term in a rare instance—they do not compromise system functionality, data integrity, or regulatory compliance. Considering the complexity and development effort required to implement these fixes, along with the fact that all other related scenarios are functioning as expected, these issues have been classified as minor. |

| **S. No** | **JIRA ID** | **Issue Description**                                                                                                                                                                                       | **Business Justification**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| --------- | ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|           |             |                                                                                                                                                                                                             | Resolution is therefore planned for a future release.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| 16        | PVCM-126428 | Minor issues observed on the FU Difference screen, including improper functioning of the edit lock feature and incorrect display of product ordering. \[Additional Jira reference ID includes: PVCM-123418] | The issue is specific to the edit lock functionality within the Follow-Up Difference and visibility of certain products on the Follow-Up Difference screen, where some products may intermittently not display as expected. This behavior is limited in scope and does not impact overall system performance, regulatory compliance, data accuracy, or the functionality of other system components. While it may cause a minor impact on user experience, it does not affect critical operations or system integrity. Given that the issue is isolated, low-impact, and occurs only in specific scenarios, it has been classified as minor. The resolution will be planned for a future release. |
| 17        | PVCM-125914 | Mismatch in reported date and acknowledgement date.                                                                                                                                                         | The issue is restricted to a specific configuration setting for a specific client, for which a workaround exists (“Update the configuration”). It does not impact overall system performance, functionality, or compliance. The issue is minor and limited in scope, and while it may require user attention in certain scenarios, it does not affect core operations. As such, the fix will be planned for a future release.                                                                                                                                                                                                                                                                     |
| 18        | PVCM-126874 | Justification pop-ups for First Receipt Date and Version Receipt Date are not appearing for Global and Local users.                                                                                         | The issue is restricted to specific scenarios involving the First Receipt Date and Version Receipt Date justification popups in global and local cases. These scenarios do not impact overall system performance or compliance. While they may                                                                                                                                                                                                                                                                                                                                                                                                                                                    |

| **S. No** | **JIRA ID** | **Issue Description**                                                                                                                                                                                     | **Business Justification**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --------- | ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|           |             |                                                                                                                                                                                                           | slightly affect user experience in these cases, they do not compromise core system functionality or regulatory requirements. Given that the issue is minor and confined to a limited context, the fix will be planned for a future release.                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| 19        | PVCM-66853  | Minor data visibility issues observed in the Attachment Viewer, where deleted attachments from previous case versions reappear upon screen refresh. \[Additional Jira reference ID includes: PVCM-123420] | The issue is limited to the rendering of Word documents containing tables in the Attachment Viewer. A workaround exists whereby using a licensed version of Microsoft Office installed alongside the Attachment Viewer ensures proper display of the content. Additionally, another issue has been observed where deleted records from previous case versions reappear upon screen refresh. These scenarios are restricted to a specific use case and does not affect overall system performance or compliance. While it may minimally impact user experience, it does not compromise system functionality. As the issue is minor and isolated, the resolution will be planned for a future release. |
| 20        | PVCM-110723 | Study ID fails to code correctly during force merging.                                                                                                                                                    | The issue is limited to coding a single field in the study section during accept as follow up operations. This specific scenario does not affect overall system performance or compliance. Work around exists by recoding the product post accept as follow up operation. The impact is restricted and does not compromise core functionality. Given the limited scope and minimal user impact, the                                                                                                                                                                                                                                                                                                  |

| **S. No** | **JIRA ID**  | **Issue Description**                                                          | **Business Justification**                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| --------- | ------------ | ------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|           |              |                                                                                | resolution of this issue will be planned for a future release.                                                                                                                                                                                                                                                                                                                                                                                                                           |
| 21        | PVADMIN48316 | Duplicate notifications occur when WHO C3 Version is activated.                | The issue is confined to the WHO notification functionality and occurs only in multi-node environments, leading to the generation of duplicate notifications in certain cases. It does not affect any core processing, case workflow, or regulatory compliance, and its impact on overall system performance is minimal. Since the occurrence is limited to a specific configuration and does not hinder normal user operations, the resolution will be planned in a subsequent release. |
| 22        | PVADMIN48214 | Sequencing issues observed in Configuration comparison.                        | The issue is limited to the sequencing and nomenclature within the snapshot configuration comparison sheet. Issue listed is non-critical, scenario specific. Workaround available, ensuring continued operational stability. Deferring these issues to upcoming releases allows prioritization of other issues.                                                                                                                                                                          |
| 23        | PVADMIN46811 | Bulk import of new language fields is not allowed when the UID already exists. | The identified issue is limited to a specific scenario involving the bulk import of users when the UID already exists. As the issue occurs only under rare conditions and has no effect on normal operations it is considered minor in nature. The issue has been deferred considering the impact and will be considered in future release for fixing.                                                                                                                                   |
| 24        | PVCM-125060  | Error log fails to capture duplicate email IDs during bulk user import.        | The issue is limited to a specific scenario where the system does not correctly capture the duplicate email error message. However, this does not impact                                                                                                                                                                                                                                                                                                                                 |

| **S. No** | **JIRA ID** | **Issue Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | **Business Justification**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| --------- | ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|           |             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | overall system performance, as the system already prevents users from entering duplicate email IDs. Since the impact is minor and limited to error message handling, the resolution will be planned for a future release.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| 25        | PVCM-126967 | Issues have been identified in the MedDRA recode functionality. These include instances where user full names are missing in export files, leading to incomplete user attribution in recoding reports; duplicate records appearing in case-open reports, which may cause confusion in case tracking; and report generation failures in specific scenarios. Additionally, users have received failure notifications even when recoding operations were completed successfully, creating inconsistency between system notifications and actual processing status. Additionally, a minor visual issue occurs where the MedDRA hierarchy icon appears orange on the Follow-Up/Duplicate Search screen when accessed from Case Entry. \[Additional Jira reference ID includes: PVCM-126754, PVCM127058, PVCM-127003, PVCM- 127231, PVADMIN-48397, PVCM127346] | The identified issues are limited to specific non-critical scenarios within the MedDRA recoding and MedDRA report functionalities. These include the generation of duplicate records in the _Case Open by Users_ file, false failure notifications appearing during MedDRA recoding despite successful operations, and partial visibility of usernames in export files. In addition, certain issues are observed in previous MedDRA versions and in the generation of success and error reports during the recoding process. Additionally, a minor visual issue limited to the MedDRA hierarchy icon incorrectly appears orange on the Follow-Up/Duplicate Search screen when accessed from the Case Entry screen. These issues are isolated to specific use cases and do not impact overall system performance, data integrity, or MedDRA recoding process. Workarounds are available where necessary to ensure continued usability and reporting accuracy. Given the minimal impact and the fact that these issues are confined to user interface and report generation aspects, the fixes have been classified as low priority and will be planned for implementation in a future release. |

| **S. No** | **JIRA ID**  | **Issue Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | **Business Justification**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| --------- | ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 26        | PVADMIN48201 | Issues observed in Central Field Management include incorrect labeling of signal comments and Process Status. \[Additional Jira reference ID includes: PVADMIN-48346]                                                                                                                                                                                                                                                                                                                                                                                                                                                  | The issue is restricted to a single field in the case form, for which a workaround is available. Users can modify the field label through field configuration in PVADMIN. This issue does not impact overall system performance, functionality, or regulatory compliance. Given the limited scope and the availability of a workaround, the issue is considered minor. The fix will be planned in a future release.                                                                                                                                                                                                                                                                                                                                                      |
| 27        | PVCM-103637  | PVCM Application went down for a specific environment URL.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | The issue is limited to specific client environment, for which a workaround is available. User can restart the one of the PVCM Component (follow-up API) to bring the application up. This is one of instance and can be mitigated by following the above steps. Given the limited scope and the availability of a workaround, the issue is considered minor. The fix will be planned in a future release.                                                                                                                                                                                                                                                                                                                                                               |
| 28        | PVCM-118407  | Issues have been identified where cases are not visible on listing screens under specific scenarios, including after case indexing during MedDRA upgrades and within the Intake Queue, Case List, or other listing screens. \[Additional Jira reference ID includes: PVCM-82468, PVCM52127]                                                                                                                                                                                                                                                                                                                            | The issue is limited to specific client environment, for which a workaround is available. This is one of instance and can be mitigated easily by quick workaround. Given the limited scope and the availability of a workaround, the issue is considered minor. The fix will be planned in a future release.                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| 29        | PVCM-126550  | Listing Screen issues: issues have been identified affecting case listing functionality. Cases are                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | The identified issues affecting case listing functionality are scenario-specific and do not                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| **S. No** | **JIRA ID**  | **Issue Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | **Business Justification**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|           |              | sometimes visible to users who do not have access to the constituent product. User and user group assignment from listing screens is incorrectly enabled for cases in the final state linked to deleted versions. Additionally, non-current MedDRA terms are not searchable in Follow-Up/Duplicate searches, and users are able to add Tasks or Follow-Up Queries from the matching cases list inappropriately. Additionally, the window autocomplete feature is incorrectly populating information in the Case State field. \[Additional Jira reference ID includes: PVCM-119705, PVCM122112, PVCM-113641, PVCM77806] | compromise overall system performance, stability, case processing operation. Cases being visible to users without access to the constituent product, incorrect enabling of user and user group assignment for cases in the final state linked to deleted versions, inability to search non-current MedDRA terms, inappropriate addition of Tasks or Follow-Up Queries from the matching cases list, and window autocomplete incorrectly populating the Case State field are all limited to specific workflows and user interactions. While these behaviors may cause minor disruptions to user experience, they do not impact core system operations or data integrity. Given their low operational impact, these issues are planned for resolution in a future release. |
| 1         | PVCM-125828  | Issues have been identified where the Preferred Case Entry field appears blank, and the audit log displays ‘null’ for the allowed case entry template when the FCE template is hidden for user groups with FCE, BCE, and FCE (Custom) templates.                                                                                                                                                                                                                                                                                                                                                                       | The identified issue is limited to a specific scenario involving system logic handling for preferred case entry selection when one of the associated templates (FCE) is made invisible. The application does not automatically reassign a default template (BCE) in such cases, resulting in the field appearing blank. As this issue arises only during manual backend operations and does not affect standard configurations or case processing, it is considered minor in nature. The issue has been deferred considering its limited impact and will be addressed in a future release.                                                                                                                                                                               |

***

## 12. Supported Software / Environment

#### 12.1 Technical Stack

***

| **Component**                          | **Supported Version(s)** |
| -------------------------------------- | ------------------------ |
| Operating System of Application Server | Amazon Linux             |
| Oracle Database                        | 19.23 Standard Edition   |
| Spotfire                               | NA                       |
| Apache Tomcat                          | 9.x                      |
| ARGUS Safety                           | NA                       |

## 13. Any Other Information

All information related to the release is captured in the above section.

## 14. APPENDICES

#### 14.1 Appendices- A- Supporting Documents

Please refer to the attached document.

| **Template ID** | **Template Name**                     |
| --------------- | ------------------------------------- |
| RxL-TMP-VAL-032 | New Feature, Enhancements & Bug Fixes |
