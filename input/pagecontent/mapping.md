This table maps elements from the PMDA's XML for Japanese Package Inserts (JPI) to FHIR resources compliant with the HL7 FHIR ePI Implementation Guide. It addresses Japan-specific requirements (e.g., YJCode, Japanese-language content).

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
        <tr>
            <th>PMDA XML Element/Path</th>
            <th>FHIR ePI Mapping</th>
            <th>Notes</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>package_insert/@id</td>
            <td>MedicinalProductDefinition.identifier</td>
            <td>Maps to the unique identifier for the product in MedicinalProductDefinition.</td>
        </tr>
        <tr>
            <td>package_insert/@code</td>
            <td>MedicinalProductDefinition.identifier</td>
            <td>PMDA code; could also map to PackagedProductDefinition.identifier for packaging specifics.</td>
        </tr>
        <tr>
            <td>package_insert/revision_info/date</td>
            <td>Composition.date or Composition.extension:revisionDate</td>
            <td>Represents the revision date of the package insert document.</td>
        </tr>
        <tr>
            <td>package_insert/revision_info/edition</td>
            <td>Composition.version</td>
            <td>Edition or version number of the document.</td>
        </tr>
        <tr>
            <td>package_insert/pmda_code</td>
            <td>MedicinalProductDefinition.identifier</td>
            <td>PMDA-specific code for the medicinal product.</td>
        </tr>
        <tr>
            <td>package_insert/therapeutic_category</td>
            <td>MedicinalProductDefinition.classification</td>
            <td>Maps to ATC code or therapeutic classification in MedicinalProductDefinition.</td>
        </tr>
        <tr>
            <td>package_insert/brand/name</td>
            <td>MedicinalProductDefinition.name.productName</td>
            <td>Brand name of the product.</td>
        </tr>
        <tr>
            <td>package_insert/brand/product_code</td>
            <td>MedicinalProductDefinition.identifier</td>
            <td>Product-specific code (YJ code or similar).</td>
        </tr>
        <tr>
            <td>package_insert/brand/english_name</td>
            <td>MedicinalProductDefinition.name.namePart (type: 'invented') with language extension</td>
            <td>English brand name; use FHIR language extensions for multilingual support.</td>
        </tr>
        <tr>
            <td>package_insert/brand/kana_name</td>
            <td>MedicinalProductDefinition.name.namePart (type: 'invented') with language extension</td>
            <td>Kana (phonetic) name; Japanese-specific, may require custom extension.</td>
        </tr>
        <tr>
            <td>package_insert/brand/hot_code</td>
            <td>MedicinalProductDefinition.identifier</td>
            <td>HOT code for reimbursement or regulatory purposes.</td>
        </tr>
        <tr>
            <td>package_insert/brand/approval_date</td>
            <td>RegulatedAuthorization.validityPeriod.start</td>
            <td>Approval date from PMDA.</td>
        </tr>
        <tr>
            <td>package_insert/brand/storage</td>
            <td>PackagedProductDefinition.shelfLifeStorage</td>
            <td>Storage conditions (e.g., room temperature).</td>
        </tr>
        <tr>
            <td>package_insert/brand/expiration</td>
            <td>PackagedProductDefinition.shelfLifeStorage.periodDuration</td>
            <td>Shelf life/expiration period.</td>
        </tr>
        <tr>
            <td>package_insert/brand/pack_size</td>
            <td>PackagedProductDefinition.package.packaging.quantity</td>
            <td>Number of units per pack (e.g., 28 tablets).</td>
        </tr>
        <tr>
            <td>package_insert/active_ingredient/name</td>
            <td>MedicinalProductDefinition.ingredient.substance.name</td>
            <td>Active ingredient name (e.g., Exemestane).</td>
        </tr>
        <tr>
            <td>package_insert/contraindication/item</td>
            <td>Composition.section (code: 'contraindication')</td>
            <td>Section for contraindications; text in Composition.section.text.</td>
        </tr>
        <tr>
            <td>package_insert/precaution/item</td>
            <td>Composition.section (code: 'precaution')</td>
            <td>Precautions for use; may nest under warnings.</td>
        </tr>
        <tr>
            <td>package_insert/indication</td>
            <td>Composition.section (code: 'indication') or MedicinalProductDefinition.indication</td>
            <td>Disease or condition for which the product is indicated (e.g., postmenopausal breast cancer).</td>
        </tr>
        <tr>
            <td>package_insert/dosage</td>
            <td>Composition.section (code: 'dosage')</td>
            <td>Dosage and administration instructions.</td>
        </tr>
        <tr>
            <td>package_insert/warning/item</td>
            <td>Composition.section (code: 'warning')</td>
            <td>General warnings and precautions.</td>
        </tr>
        <tr>
            <td>package_insert/interaction/item</td>
            <td>Composition.section (code: 'interaction') or ClinicalUseDefinition.type='interaction'</td>
            <td>Drug interactions; may reference Interaction resources.</td>
        </tr>
        <tr>
            <td>package_insert/adverse_reaction/item</td>
            <td>Composition.section (code: 'adverse-reaction') or ClinicalUseDefinition.type='undesirable-effect'</td>
            <td>Adverse reactions, including frequencies.</td>
        </tr>
        <tr>
            <td>package_insert/pharmacokinetics</td>
            <td>Composition.section (code: 'pharmacokinetics')</td>
            <td>PK data, including absorption, distribution, etc.</td>
        </tr>
        <tr>
            <td>package_insert/clinical_study</td>
            <td>Composition.section (code: 'clinical-study')</td>
            <td>Summary of clinical trials.</td>
        </tr>
        <tr>
            <td>package_insert/pharmacology</td>
            <td>Composition.section (code: 'pharmacology')</td>
            <td>Mechanism of action and pharmacodynamics.</td>
        </tr>
        <tr>
            <td>package_insert/physicochemical/name</td>
            <td>MedicinalProductDefinition.name (scientific) or Ingredient.substance.name</td>
            <td>Chemical name.</td>
        </tr>
        <tr>
            <td>package_insert/physicochemical/formula</td>
            <td>Ingredient.substance.molecularFormula</td>
            <td>Molecular formula (e.g., C20H24O2).</td>
        </tr>
        <tr>
            <td>package_insert/physicochemical/weight</td>
            <td>Ingredient.substance.molecularWeight</td>
            <td>Molecular weight.</td>
        </tr>
        <tr>
            <td>package_insert/physicochemical/description</td>
            <td>Ingredient.substance.description</td>
            <td>Physical description (e.g., white powder).</td>
        </tr>
        <tr>
            <td>package_insert/physicochemical/structure</td>
            <td>Ingredient.substance.structure</td>
            <td>Chemical structure if represented.</td>
        </tr>
        <tr>
            <td>package_insert/package</td>
            <td>PackagedProductDefinition.package</td>
            <td>Packaging details (e.g., 28 tablets PTP).</td>
        </tr>
        <tr>
            <td>package_insert/reference/item</td>
            <td>Composition.section (code: 'reference') or Citation</td>
            <td>References to literature or studies.</td>
        </tr>
        <tr>
            <td>package_insert/contact</td>
            <td>Organization.contact (for manufacturer)</td>
            <td>Contact information for inquiries.</td>
        </tr>
        <tr>
            <td>package_insert/manufacturer</td>
            <td>MedicinalProductDefinition.manufacturer or Organization</td>
            <td>Manufacturer details.</td>
        </tr>
        <tr>
            <td>package_insert/composition/item</td>
            <td>MedicinalProductDefinition.ingredient</td>
            <td>Composition including excipients (e.g., carnauba wax).</td>
        </tr>
        <tr>
            <td>package_insert/property/item</td>
            <td>ManufacturedItemDefinition.property</td>
            <td>Tablet properties (e.g., size, color).</td>
        </tr>
        <tr>
            <td>package_insert/non_clinical/toxicity</td>
            <td>Composition.section (code: 'non-clinical')</td>
            <td>Non-clinical data like toxicity studies.</td>
        </tr>
        <tr>
            <td>package_insert/overdosage</td>
            <td>Composition.section (code: 'overdosage')</td>
            <td>Overdose information (not explicitly in sample, but schema supports).</td>
        </tr>
        <tr>
            <td>package_insert/pediatric</td>
            <td>Composition.section (code: 'pediatric-use')</td>
            <td>Pediatric precautions (not in sample).</td>
        </tr>
        <tr>
            <td>package_insert/geriatric</td>
            <td>Composition.section (code: 'geriatric-use')</td>
            <td>Elderly use precautions.</td>
        </tr>
        <tr>
            <td>package_insert/pregnancy</td>
            <td>Composition.section (code: 'pregnancy')</td>
            <td>Pregnancy and lactation warnings.</td>
        </tr>
        <tr>
            <td>package_insert/lactation</td>
            <td>Composition.section (code: 'lactation')</td>
            <td>Breastfeeding warnings.</td>
        </tr>
        <tr>
            <td>package_insert/driving</td>
            <td>Composition.section (code: 'driving')</td>
            <td>Effects on ability to drive/operate machinery.</td>
        </tr>
        <tr>
            <td>package_insert/excipient</td>
            <td>MedicinalProductDefinition.ingredient (role: 'excipient')</td>
            <td>List of excipients in composition.</td>
        </tr>
        <tr>
            <td>package_insert/marketing_holder</td>
            <td>RegulatedAuthorization.holder</td>
            <td>Marketing authorization holder (e.g., Pfizer).</td>
        </tr>
    </tbody>
</table>