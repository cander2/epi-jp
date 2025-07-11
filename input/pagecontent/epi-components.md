This page provides an overview of the FHIR resources utilized in the ePI-JP Implementation Guide, which adapts the HL7 FHIR ePI IG for Japanese Package Inserts (JPI) from PMDA XML data. The table below details each resource and its specific purpose in supporting structured, queryable ePI content compliant with Japanese regulatory requirements.

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

<table>
<thead>
<tr><th>FHIR Resource</th><th>Purpose in ePI-JP Context</th></tr>
</thead>
<tbody>
<tr><td><strong>Bundle</strong></td><td>Serves as the container for the entire ePI document in Japan, typically of type "document". It bundles the Composition (the core ePI content) with supporting resources like MedicinalProductDefinition, ensuring the package insert XML data (e.g., from PMDA sources) is structured as a cohesive, queryable FHIR document compliant with Japanese regulatory formats.</td></tr>
<tr><td><strong>Composition</strong></td><td>Represents the structured package insert (添付文書) document. It organizes sections such as AdministrativeInfo, ProductInfo, Indications (効能・効果), DosageAndAdministration (用法・用量), ContraIndications (禁忌), AdverseReactions (副作用), and others from the Japanese XML schema. Each section uses narrative text (xhtml) for human-readable content, with references to other resources for coded data, supporting bilingual (Japanese/English) previews via XSL transformations.</td></tr>
<tr><td><strong>MedicinalProductDefinition</strong></td><td>Defines the medicinal product details, including name (ブランド名, e.g., アロマシン錠25mg), product code (YJコード, e.g., 4291012F1022), therapeutic category (治療分類, e.g., アロマターゼ阻害剤), and physicochemical properties. It maps to ProductInfo and PhysicochemicalProperties sections in the Japanese XML, enabling standardized product identification and cross-referencing with PMDA databases.</td></tr>
<tr><td><strong>Ingredient</strong></td><td>Details the active and inactive ingredients (組成・性状), including strength (e.g., エキセメスタン 25mg) and excipients (e.g., カルナウバロウ). Corresponds to the Composition section in the XML, supporting safety checks and allergy/intolerance queries in Japanese clinical systems.</td></tr>
<tr><td><strong>ManufacturedItemDefinition</strong></td><td>Describes the specific manufactured item (e.g., the tablet form of アロマシン錠25mg), including unit of presentation, manufacturing details, and references to ingredients. Maps to Composition and Property sections in the XML, providing a link between the medicinal product and its physical manufactured characteristics for quality and regulatory compliance in Japan.</td></tr>
<tr><td><strong>AdministrableProductDefinition</strong></td><td>Describes the form and administration route (e.g., 錠剤, oral), including shape, size, color, and imprint (e.g., diameter 6.0mm, imprint "7663"). Maps to Property and visual identification details in the XML, aiding in patient education and counterfeit detection in Japan.</td></tr>
<tr><td><strong>PackagedProductDefinition</strong></td><td>Captures packaging information (包装), such as pack sizes (e.g., 28錠 PTP) and storage conditions (保存条件, e.g., 室温保存). Aligns with Packaging section in the XML, ensuring compliance with Japanese distribution and stability requirements.</td></tr>
<tr><td><strong>RegulatedAuthorization</strong></td><td>Represents regulatory approvals, including approval date (承認日, e.g., 2002-08), holder (製造販売元, e.g., ファイザー株式会社), and edition/revision details (版数, e.g., 第1版). Maps to AdministrativeInfo and ApprovalDate in the XML, facilitating PMDA regulatory tracking and updates.</td></tr>
<tr><td><strong>ClinicalUseDefinition</strong> (Indication subtype)</td><td>Defines indications (効能・効果, e.g., 閉経後乳癌). Provides coded and narrative details, supporting decision support in Japanese EHRs for appropriate prescribing.</td></tr>
<tr><td><strong>ClinicalUseDefinition</strong> (Contraindication subtype)</td><td>Specifies contraindications (禁忌, e.g., 妊婦, 授乳婦, 過敏症). Uses coded risks and populations, mapping to ContraIndications section for safety alerts in prescribing systems.</td></tr>
<tr><td><strong>ClinicalUseDefinition</strong> (Interaction subtype)</td><td>Details drug interactions (相互作用, e.g., with エストロゲン含有製剤). Supports interaction checks, corresponding to Interactions or Precautions sections in the XML.</td></tr>
<tr><td><strong>ClinicalUseDefinition</strong> (UndesirableEffect subtype)</td><td>Lists adverse reactions (副作用, e.g., 肝炎, 悪心) with frequencies (e.g., 5%以上). Maps to AdverseReactions section, enabling pharmacovigilance reporting in Japan via PMDA.</td></tr>
<tr><td><strong>MedicationKnowledge</strong></td><td>Outlines dosage and administration (用法・用量, e.g., 1日1回25mg 食後). Provides structured dosing instructions, including precautions for use, for integration into Japanese CPOE systems.</td></tr>
<tr><td><strong>Binary</strong></td><td>Handles base64 encoded versions of images (e.g., tablet photos), where the FHIR XML or JSON Binary object contains the base64 data. Used for visual previews in Japanese/English, ensuring accessibility of insert visuals without separate files.</td></tr>
<tr><td><strong>Organization</strong></td><td>Represents manufacturers/distributors (製造販売元, e.g., ファイザー株式会社) and contact info (e.g., 製品情報センター). Maps to Manufacturer section, supporting supply chain and inquiry management in Japan.</td></tr>
</tbody>
</table>