This table maps elements from the PMDA's XML for Japanese Package Inserts (JPI) to FHIR resources compliant with the HL7 FHIR ePI Implementation Guide. It addresses Japan-specific requirements (e.g., YJCode, Japanese-language content).

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PMDA XML to FHIR Mapping</title>
    <style>
        table {
            border-collapse: collapse;
            width: 100%;
            margin: 20px 0;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
        }
        th {
            background-color: #f2f2f2;
            font-weight: bold;
        }
        tr:nth-child(even) {
            background-color: #f9f9f9;
        }
        tr:hover {
            background-color: #f5f5f5;
        }
    </style>
</head>
<body>
    <table>
        <thead>
            <tr>
                <th>PMDA XML Element</th>
                <th>FHIR Resource/Element</th>
                <th>Notes</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td><code>&lt;PackageInsert&gt;</code></td>
                <td><code>Bundle</code></td>
                <td>Maps to a <code>Bundle</code> of type <code>document</code>, encapsulating the ePI with a <code>Composition</code> as the entry point.</td>
            </tr>
            <tr>
                <td><code>&lt;ApprovalNumber&gt;</code></td>
                <td><code>RegulatedAuthorization.identifier</code></td>
                <td>Maps to <code>identifier</code> with system <code>http://pmda.go.jp/approval</code>. Example: <code>874291</code>. Requires Japan-specific extension if not standard.</td>
            </tr>
            <tr>
                <td><code>&lt;RevisionDate&gt;</code></td>
                <td><code>Composition.date</code></td>
                <td>Maps to the document creation/revision date. Example: <code>2022-02</code>.</td>
            </tr>
            <tr>
                <td><code>&lt;Edition&gt;</code></td>
                <td><code>Composition.version</code></td>
                <td>Maps to the version of the JPI. Example: <code>第1版</code>.</td>
            </tr>
            <tr>
                <td><code>&lt;YJCode&gt;</code></td>
                <td><code>MedicinalProductDefinition.identifier</code></td>
                <td>Maps to <code>identifier</code> with system <code>http://pmda.go.jp/yjcode</code>. Example: <code>4291012F1022</code>.</td>
            </tr>
            <tr>
                <td><code>&lt;TherapeuticCategory&gt;</code></td>
                <td><code>MedicinalProductDefinition.classification</code></td>
                <td>Maps to a coded classification. Use SNOMED CT (e.g., <code>386908000</code> for antineoplastic) or Japan-specific code for “アロマターゼ阻害剤”.</td>
            </tr>
            <tr>
                <td><code>&lt;Brand&gt;</code></td>
                <td><code>MedicinalProductDefinition.name</code></td>
                <td>Container for brand name details.</td>
            </tr>
            <tr>
                <td><code>&lt;Brand/BrandName&gt;</code></td>
                <td><code>MedicinalProductDefinition.name.productName</code></td>
                <td>Primary name in Japanese. Example: <code>アロマシン錠25mg</code>. Set <code>language="ja"</code>.</td>
            </tr>
            <tr>
                <td><code>&lt;Brand/Code&gt;</code></td>
                <td><code>MedicinalProductDefinition.identifier</code></td>
                <td>Maps to <code>identifier</code> for the brand code. Example: <code>4291012F1022</code>. Reuse YJCode if identical.</td>
            </tr>
            <tr>
                <td><code>&lt;Brand/BrandNameInEnglish&gt;</code></td>
                <td><code>MedicinalProductDefinition.name.productName</code></td>
                <td>English name as an additional <code>name</code> entry. Example: <code>Aromasin Tablets 25mg</code>. Set <code>language="en"</code>.</td>
            </tr>
            <tr>
                <td><code>&lt;Brand/Kana&gt;</code></td>
                <td><code>MedicinalProductDefinition.name.productName</code></td>
                <td>Kana name as an additional <code>name</code> entry. Example: <code>あろましんじょう25mg</code>. Set <code>language="ja-kana"</code>.</td>
            </tr>
            <tr>
                <td><code>&lt;Brand/JAN&gt;</code></td>
                <td><code>PackagedProductDefinition.identifier</code></td>
                <td>Maps to GS1 barcode identifier. Example: <code>21400AMY00186</code>. Use system <code>http://gs1.org</code>.</td>
            </tr>
            <tr>
                <td><code>&lt;Brand/ApprovalDate&gt;</code></td>
                <td><code>RegulatedAuthorization.date</code></td>
                <td>Maps to approval date. Example: <code>2002-08</code>. Format as ISO 8601 (<code>2002-08-01</code>).</td>
            </tr>
            <tr>
                <td><code>&lt;Brand/StorageCondition&gt;</code></td>
                <td><code>PackagedProductDefinition.storage</code></td>
                <td>Maps to storage instructions. Example: <code>室温保存</code>. Use coded storage conditions if available.</td>
            </tr>
            <tr>
                <td><code>&lt;Brand/ShelfLife&gt;</code></td>
                <td><code>PackagedProductDefinition.shelfLifeStorage</code></td>
                <td>Maps to shelf life duration. Example: <code>3年</code>. Use FHIR <code>Duration</code> (e.g., <code>3 years</code>).</td>
            </tr>
            <tr>
                <td><code>&lt;Brand/HotCode&gt;</code></td>
                <td><code>PackagedProductDefinition.identifier</code></td>
                <td>Maps to an additional identifier for hot code. Example: <code>12</code>. Use PMDA-specific system URI.</td>
            </tr>
            <tr>
                <td><code>&lt;ActiveIngredients&gt;</code></td>
                <td><code>Ingredient</code></td>
                <td>Maps to <code>Ingredient</code> resource, referenced by <code>MedicinalProductDefinition</code>.</td>
            </tr>
            <tr>
                <td><code>&lt;ActiveIngredients/ActiveIngredient&gt;</code></td>
                <td><code>Ingredient.substance.code</code></td>
                <td>Maps to the active substance. Example: <code>エキセメスタン</code>. Use UNII or CAS code if available, else text.</td>
            </tr>
            <tr>
                <td><code>&lt;ContraIndications&gt;</code></td>
                <td><code>ClinicalUseDefinition</code></td>
                <td>Maps to <code>ClinicalUseDefinition</code> of type <code>contraindication</code>. Narrative text in <code>Composition.section</code>.</td>
            </tr>
            <tr>
                <td><code>&lt;ContraIndications/Item&gt;</code></td>
                <td><code>ClinicalUseDefinition.contraindication</code></td>
                <td>Each item (e.g., “妊婦又は妊娠している可能性のある女性”) maps to a <code>contraindication.disease</code> with text or SNOMED CT codes. Also in <code>Composition.section.text</code>.</td>
            </tr>
            <tr>
                <td><code>&lt;Composition&gt;</code></td>
                <td><code>Ingredient</code></td>
                <td>Maps ingredients to <code>Ingredient</code> resources, distinguishing active and inactive ingredients.</td>
            </tr>
            <tr>
                <td><code>&lt;Composition/Item/ActiveIngredient&gt;</code></td>
                <td><code>Ingredient.substance.code</code></td>
                <td>Maps to active ingredient with strength. Example: <code>エキセメスタン 25.000mg</code>. Reference <code>SubstanceDefinition</code> if detailed.</td>
            </tr>
            <tr>
                <td><code>&lt;Composition/Item/Amount&gt;</code></td>
                <td><code>Ingredient.strength</code></td>
                <td>Maps to strength. Example: <code>25.000mg</code>. Use UCUM units (<code>mg</code>).</td>
            </tr>
            <tr>
                <td><code>&lt;Composition/Item/Excipients&gt;</code></td>
                <td><code>Ingredient.substance.code</code></td>
                <td>Maps to inactive ingredients as separate <code>Ingredient</code> resources with <code>role="excipient"</code>. Example: <code>カルナウバロウ</code>, etc.</td>
            </tr>
            <tr>
                <td><code>&lt;Property&gt;</code></td>
                <td><code>ManufacturedItemDefinition</code></td>
                <td>Maps tablet characteristics to <code>ManufacturedItemDefinition</code>.</td>
            </tr>
            <tr>
                <td><code>&lt;Property/Item/PropertyDetail&gt;</code></td>
                <td><code>ManufacturedItemDefinition.property</code></td>
                <td>Maps details like diameter (<code>6.0mm</code>), weight (<code>100mg</code>), color (<code>白色～微灰白色糖衣錠</code>). Use coded properties where possible.</td>
            </tr>
            <tr>
                <td><code>&lt;Property/Item/Code&gt;</code></td>
                <td><code>ManufacturedItemDefinition.identifier</code></td>
                <td>Maps to tablet code. Example: <code>7663</code>. Use PMDA-specific system URI.</td>
            </tr>
            <tr>
                <td><code>&lt;IndicationsOrEfficacy&gt;</code></td>
                <td><code>Composition.section</code></td>
                <td>Maps to a <code>Composition.section</code> with <code>title="Indications"</code>. Example: <code>閉経後乳癌</code>. Reference <code>ClinicalUseDefinition</code> for coded indications (e.g., SNOMED CT <code>254837009</code>).</td>
            </tr>
            <tr>
                <td><code>&lt;DosageAndAdministration&gt;</code></td>
                <td><code>Composition.section</code></td>
                <td>Maps to a <code>Composition.section</code> with <code>title="Dosage and Administration"</code>. Example: <code>通常、成人にはエキセメスタンとして1日1回25mgを食後に経口投与する。</code>. Optionally use <code>MedicationKnowledge.administrationGuidelines</code>.</td>
            </tr>
            <tr>
                <td><code>&lt;Precautions&gt;</code></td>
                <td><code>Composition.section</code></td>
                <td>Maps to a <code>Composition.section</code> with <code>title="Precautions"</code>. Narrative text in <code>text.div</code>. Subsections as nested <code>section</code> elements.</td>
            </tr>
            <tr>
                <td><code>&lt;PrecautionsForSpecificPatientPopulations&gt;</code></td>
                <td><code>Composition.section</code></td>
                <td>Maps to a <code>Composition.section</code> with <code>title="Precautions for Specific Populations"</code>. Also reference <code>ClinicalUseDefinition</code> for coded precautions (e.g., renal/hepatic impairment).</td>
            </tr>
            <tr>
                <td><code>&lt;PrecautionsForPregnant&gt;</code></td>
                <td><code>Composition.section</code></td>
                <td>Maps to a <code>Composition.section</code> with <code>title="Pregnancy Precautions"</code>. Link to <code>ClinicalUseDefinition.contraindication</code> for pregnancy warnings.</td>
            </tr>
            <tr>
                <td><code>&lt;PrecautionsForLactating&gt;</code></td>
                <td><code>Composition.section</code></td>
                <td>Maps to a <code>Composition.section</code> with <code>title="Lactation Precautions"</code>. Link to <code>ClinicalUseDefinition.contraindication</code>.</td>
            </tr>
            <tr>
                <td><code>&lt;ContraIndicatedCombinations&gt;</code></td>
                <td><code>ClinicalUseDefinition</code></td>
                <td>Maps to <code>ClinicalUseDefinition</code> of type <code>interaction</code>. Narrative in <code>Composition.section</code>. Example: <code>エストロゲン含有製剤</code>.</td>
            </tr>
            <tr>
                <td><code>&lt;SignificantAdverseEvents&gt;</code></td>
                <td><code>Composition.section</code></td>
                <td>Maps to a <code>Composition.section</code> with <code>title="Significant Adverse Events"</code>. Link to <code>ClinicalUseDefinition</code> for coded adverse reactions (e.g., <code>肝炎</code>).</td>
            </tr>
            <tr>
                <td><code>&lt;OtherAdverseEvents&gt;</code></td>
                <td><code>ClinicalUseDefinition</code></td>
                <td>Maps structured adverse events (e.g., tables by system organ class) to <code>ClinicalUseDefinition</code> with SNOMED CT codes. Narrative in <code>Composition.section</code>.</td>
            </tr>
            <tr>
                <td><code>&lt;PrecautionsAtDelivery&gt;</code></td>
                <td><code>Composition.section</code></td>
                <td>Maps to a <code>Composition.section</code> with <code>title="Precautions at Delivery"</code>. Example: PTP sheet warnings.</td>
            </tr>
            <tr>
                <td><code>&lt;Carcinogenicity&gt;</code></td>
                <td><code>Composition.section</code></td>
                <td>Maps to a <code>Composition.section</code> with <code>title="Carcinogenicity"</code>. Narrative text only, no structured resource unless coded risks are defined.</td>
            </tr>
            <tr>
                <td><code>&lt;Pharmacokinetics&gt;</code></td>
                <td><code>Composition.section</code></td>
                <td>Maps to a <code>Composition.section</code> with <code>title="Pharmacokinetics"</code>. Tables/figures as <code>Binary</code> if multimedia; otherwise, narrative text.</td>
            </tr>
            <tr>
                <td><code>&lt;ClinicalStudies&gt;</code></td>
                <td><code>Composition.section</code></td>
                <td>Maps to a <code>Composition.section</code> with <code>title="Clinical Studies"</code>. Structured trial data may reference <code>Evidence</code> (out of scope) or remain narrative.</td>
            </tr>
            <tr>
                <td><code>&lt;Pharmacology&gt;</code></td>
                <td><code>Composition.section</code></td>
                <td>Maps to a <code>Composition.section</code> with <code>title="Pharmacology"</code>. Narrative for mechanisms like aromatase inhibition.</td>
            </tr>
            <tr>
                <td><code>&lt;PhysicochemicalInformation&gt;</code></td>
                <td><code>SubstanceDefinition</code></td>
                <td>Maps to <code>SubstanceDefinition</code> for chemical properties (e.g., molecular formula <code>C20H24O2</code>, molecular weight <code>296.40</code>).</td>
            </tr>
            <tr>
                <td><code>&lt;Packaging&gt;</code></td>
                <td><code>PackagedProductDefinition</code></td>
                <td>Maps to <code>PackagedProductDefinition.package.quantity</code>. Example: <code>28錠［14錠（PTP）×2］</code>.</td>
            </tr>
            <tr>
                <td><code>&lt;References&gt;</code></td>
                <td><code>Composition.section</code></td>
                <td>Maps to a <code>Composition.section</code> with <code>title="References"</code>. List citations as narrative text or <code>Citation</code> resource (out of scope).</td>
            </tr>
            <tr>
                <td><code>&lt;Publisher&gt;</code></td>
                <td><code>Organization</code></td>
                <td>Maps to <code>Organization</code> for the MAH. Example: <code>ファイザー株式会社</code>. Referenced by <code>Composition.author</code> and <code>RegulatedAuthorization.holder</code>.</td>
            </tr>
            <tr>
                <td><code>&lt;Publisher/Address&gt;</code></td>
                <td><code>Organization.address</code></td>
                <td>Maps to <code>address</code>. Example: <code>東京都渋谷区代々木3-22-7</code>. Use <code>country="JP"</code>.</td>
            </tr>
            <tr>
                <td><code>&lt;Manufacturer&gt;</code></td>
                <td><code>Organization</code></td>
                <td>Maps to a separate <code>Organization</code> for the manufacturer, referenced by <code>ManufacturedItemDefinition.manufacturer</code>. Example: <code>ファイザー株式会社</code>.</td>
            </tr>
        </tbody>
    </table>
</body>
</html>

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
