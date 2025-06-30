# Mapping PMDA XML to FHIR ePI Resources

This table maps elements from the PMDA's XML for Japanese Package Inserts (JPI), based on the provided `package_insert-XML.xsd` and sample XML (`672212_4291012F1022_4_02.xml`) for Aromasin, to FHIR resources compliant with the HL7 FHIR ePI Implementation Guide (version 1.1.0). It addresses Japan-specific requirements (e.g., YJCode, Japanese-language content).

| **PMDA XML Element** | **FHIR Resource/Element** | **Notes** |
|-----------------------|---------------------------|-----------|
| `<PackageInsert>` | `Bundle` | Maps to a `Bundle` of type `document`, encapsulating the ePI with a `Composition` as the entry point. |
| `<ApprovalNumber>` | `RegulatedAuthorization.identifier` | Maps to `identifier` with system `http://pmda.go.jp/approval`. Example: `874291`. Requires Japan-specific extension if not standard. |
| `<RevisionDate>` | `Composition.date` | Maps to the document creation/revision date. Example: `2022-02`. |
| `<Edition>` | `Composition.version` | Maps to the version of the JPI. Example: `第1版`. |
| `<YJCode>` | `MedicinalProductDefinition.identifier` | Maps to `identifier` with system `http://pmda.go.jp/yjcode`. Example: `4291012F1022`. |
| `<TherapeuticCategory>` | `MedicinalProductDefinition.classification` | Maps to a coded classification. Use SNOMED CT (e.g., `386908000` for antineoplastic) or Japan-specific code for “アロマターゼ阻害剤”. |
| `<Brand>` | `MedicinalProductDefinition.name` | Container for brand name details. |
| `<Brand/BrandName>` | `MedicinalProductDefinition.name.productName` | Primary name in Japanese. Example: `アロマシン錠25mg`. Set `language="ja"`. |
| `<Brand/Code>` | `MedicinalProductDefinition.identifier` | Maps to `identifier` for the brand code. Example: `4291012F1022`. Reuse YJCode if identical. |
| `<Brand/BrandNameInEnglish>` | `MedicinalProductDefinition.name.productName` | English name as an additional `name` entry. Example: `Aromasin Tablets 25mg`. Set `language="en"`. |
| `<Brand/Kana>` | `MedicinalProductDefinition.name.productName` | Kana name as an additional `name` entry. Example: `あろましんじょう25mg`. Set `language="ja-kana"`. |
| `<Brand/JAN>` | `PackagedProductDefinition.identifier` | Maps to GS1 barcode identifier. Example: `21400AMY00186`. Use system `http://gs1.org`. |
| `<Brand/ApprovalDate>` | `RegulatedAuthorization.date` | Maps to approval date. Example: `2002-08`. Format as ISO 8601 (`2002-08-01`). |
| `<Brand/StorageCondition>` | `PackagedProductDefinition.storage` | Maps to storage instructions. Example: `室温保存`. Use coded storage conditions if available. |
| `<Brand/ShelfLife>` | `PackagedProductDefinition.shelfLifeStorage` | Maps to shelf life duration. Example: `3年`. Use FHIR `Duration` (e.g., `3 years`). |
| `<Brand/HotCode>` | `PackagedProductDefinition.identifier` | Maps to an additional identifier for hot code. Example: `12`. Use PMDA-specific system URI. |
| `<ActiveIngredients>` | `Ingredient` | Maps to `Ingredient` resource, referenced by `MedicinalProductDefinition`. |
| `<ActiveIngredients/ActiveIngredient>` | `Ingredient.substance.code` | Maps to the active substance. Example: `エキセメスタン`. Use UNII or CAS code if available, else text. |
| `<ContraIndications>` | `ClinicalUseDefinition` | Maps to `ClinicalUseDefinition` of type `contraindication`. Narrative text in `Composition.section`. |
| `<ContraIndications/Item>` | `ClinicalUseDefinition.contraindication` | Each item (e.g., “妊婦又は妊娠している可能性のある女性”) maps to a `contraindication.disease` with text or SNOMED CT codes. Also in `Composition.section.text`. |
| `<Composition>` | `Ingredient` | Maps ingredients to `Ingredient` resources, distinguishing active and inactive ingredients. |
| `<Composition/Item/ActiveIngredient>` | `Ingredient.substance.code` | Maps to active ingredient with strength. Example: `エキセメスタン 25.000mg`. Reference `SubstanceDefinition` if detailed. |
| `<Composition/Item/Amount>` | `Ingredient.strength` | Maps to strength. Example: `25.000mg`. Use UCUM units (`mg`). |
| `<Composition/Item/Excipients>` | `Ingredient.substance.code` | Maps to inactive ingredients as separate `Ingredient` resources with `role="excipient"`. Example: `カルナウバロウ`, etc. |
| `<Property>` | `ManufacturedItemDefinition` | Maps tablet characteristics to `ManufacturedItemDefinition`. |
| `<Property/Item/PropertyDetail>` | `ManufacturedItemDefinition.property` | Maps details like diameter (`6.0mm`), weight (`100mg`), color (`白色～微灰白色糖衣錠`). Use coded properties where possible. |
| `<Property/Item/Code>` | `ManufacturedItemDefinition.identifier` | Maps to tablet code. Example: `7663`. Use PMDA-specific system URI. |
| `<IndicationsOrEfficacy>` | `Composition.section` | Maps to a `Composition.section` with `title="Indications"`. Example: `閉経後乳癌`. Reference `ClinicalUseDefinition` for coded indications (e.g., SNOMED CT `254837009`). |
| `<DosageAndAdministration>` | `Composition.section` | Maps to a `Composition.section` with `title="Dosage and Administration"`. Example: `通常、成人にはエキセメスタンとして1日1回25mgを食後に経口投与する。`. Optionally use `MedicationKnowledge.administrationGuidelines`. |
| `<Precautions>` | `Composition.section` | Maps to a `Composition.section` with `title="Precautions"`. Narrative text in `text.div`. Subsections as nested `section` elements. |
| `<PrecautionsForSpecificPatientPopulations>` | `Composition.section` | Maps to a `Composition.section` with `title="Precautions for Specific Populations"`. Also reference `ClinicalUseDefinition` for coded precautions (e.g., renal/hepatic impairment). |
| `<PrecautionsForPregnant>` | `Composition.section` | Maps to a `Composition.section` with `title="Pregnancy Precautions"`. Link to `ClinicalUseDefinition.contraindication` for pregnancy warnings. |
| `<PrecautionsForLactating>` | `Composition.section` | Maps to a `Composition.section` with `title="Lactation Precautions"`. Link to `ClinicalUseDefinition.contraindication`. |
| `<ContraIndicatedCombinations>` | `ClinicalUseDefinition` | Maps to `ClinicalUseDefinition` of type `interaction`. Narrative in `Composition.section`. Example: `エストロゲン含有製剤`. |
| `<SignificantAdverseEvents>` | `Composition.section` | Maps to a `Composition.section` with `title="Significant Adverse Events"`. Link to `ClinicalUseDefinition` for coded adverse reactions (e.g., `肝炎`). |
| `<OtherAdverseEvents>` | `ClinicalUseDefinition` | Maps structured adverse events (e.g., tables by system organ class) to `ClinicalUseDefinition` with SNOMED CT codes. Narrative in `Composition.section`. |
| `<PrecautionsAtDelivery>` | `Composition.section` | Maps to a `Composition.section` with `title="Precautions at Delivery"`. Example: PTP sheet warnings. |
| `<Carcinogenicity>` | `Composition.section` | Maps to a `Composition.section` with `title="Carcinogenicity"`. Narrative text only, no structured resource unless coded risks are defined. |
| `<Pharmacokinetics>` | `Composition.section` | Maps to a `Composition.section` with `title="Pharmacokinetics"`. Tables/figures as `Binary` if multimedia; otherwise, narrative text. |
| `<ClinicalStudies>` | `Composition.section` | Maps to a `Composition.section` with `title="Clinical Studies"`. Structured trial data may reference `Evidence` (out of scope) or remain narrative. |
| `<Pharmacology>` | `Composition.section` | Maps to a `Composition.section` with `title="Pharmacology"`. Narrative for mechanisms like aromatase inhibition. |
| `<PhysicochemicalInformation>` | `SubstanceDefinition` | Maps to `SubstanceDefinition` for chemical properties (e.g., molecular formula `C20H24O2`, molecular weight `296.40`). |
| `<Packaging>` | `PackagedProductDefinition` | Maps to `PackagedProductDefinition.package.quantity`. Example: `28錠［14錠（PTP）×2］`. |
| `<References>` | `Composition.section` | Maps to a `Composition.section` with `title="References"`. List citations as narrative text or `Citation` resource (out of scope). |
| `<Publisher>` | `Organization` | Maps to `Organization` for the MAH. Example: `ファイザー株式会社`. Referenced by `Composition.author` and `RegulatedAuthorization.holder`. |
| `<Publisher/Address>` | `Organization.address` | Maps to `address`. Example: `東京都渋谷区代々木3-22-7`. Use `country="JP"`. |
| `<Manufacturer>` | `Organization` | Maps to a separate `Organization` for the manufacturer, referenced by `ManufacturedItemDefinition.manufacturer`. Example: `ファイザー株式会社`. |

### Notes
- **Terminology**: Use SNOMED CT (e.g., `386452003` for tablet, `254837009` for breast cancer), LOINC (e.g., `34390-3` for package insert), and UCUM (e.g., `mg` for strength). Japan-specific codes (e.g., YJCode, therapeutic categories) require custom value sets or extensions (e.g., `http://pmda.go.jp/fhir/extension/yjcode`).
- **Extensions**: PMDA-specific elements like `<YJCode>`, `<ApprovalNumber>`, and `<HotCode>` require extensions:
  ```json
  {
    "url": "http://pmda.go.jp/fhir/extension/yjcode",
    "valueString": "4291012F1022"
  }
  ```
- **Narrative Text**: Preserve Japanese narrative content in `Composition.section.text.div` with `language="ja"`. Use XHTML for formatting (e.g., tables in `<OtherAdverseEvents>`).
- **Structured Data**: Map tables (e.g., adverse events, clinical studies) to `ClinicalUseDefinition` where possible, using SNOMED CT or MedDRA codes. Fallback to narrative if coding is infeasible.
- **GS1 Barcode**: `<JAN>` maps to `PackagedProductDefinition.identifier` with `system="http://gs1.org"`, critical for PMDA’s e-labeling system.
- **Language**: Primary content in Japanese (`language="ja"`). English translations (`<BrandNameInEnglish>`) use `language="en"`.
- **Binary**: Use `Binary` for figures (e.g., pharmacokinetic graphs) referenced in `<Pharmacokinetics>`. Example: `<Composition.section.entry>` references a `Binary` resource.
- **Unused Resources**: `MedicationKnowledge` and `AdministrableProductDefinition` have limited use unless structured administration or product form data is extracted. `SubstanceDefinition` is used only for `<PhysicochemicalInformation>`.
- **Regulatory Compliance**: Ensure all mandatory JPI sections (e.g., `<IndicationsOrEfficacy>`, `<ContraIndications>`) are preserved. Validate against PMDA regulations and the Base ePI Profile.

### Example FHIR Snippet
For `<Brand>` and `<IndicationsOrEfficacy>`:
```json
{
  "resourceType": "Bundle",
  "type": "document",
  "entry": [
    {
      "resource": {
        "resourceType": "Composition",
        "status": "final",
        "type": {
          "coding": [{ "system": "http://loinc.org", "code": "34390-3", "display": "Package Insert" }]
        },
        "date": "2022-02-01",
        "title": "アロマシン錠25mg Package Insert",
        "section": [
          {
            "title": "Indications",
            "code": {
              "coding": [{ "system": "http://snomed.info/sct", "code": "254837009", "display": "Breast cancer" }]
            },
            "text": { "status": "generated", "div": "<div xmlns='http://www.w3.org/1999/xhtml'>閉経後乳癌</div>" }
          }
        ]
      }
    },
    {
      "resource": {
        "resourceType": "MedicinalProductDefinition",
        "identifier": [
          { "system": "http://pmda.go.jp/yjcode", "value": "4291012F1022" }
        ],
        "name": [
          { "productName": "アロマシン錠25mg", "language": "ja" },
          { "productName": "Aromasin Tablets 25mg", "language": "en" },
          { "productName": "あろましんじょう25mg", "language": "ja-kana" }
        ]
      }
    }
  ]
}
```
