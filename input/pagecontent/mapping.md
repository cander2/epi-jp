### High Level FHIR Resource Mappings to PMDA XML in ePI-JP IG

The following is a high level mapping describing how elements from the PMDA XML schema for Japanese Package Inserts could be translated into the ePI-JP Implementation Guide, based on the core ePI IG. It ensures structured, interoperable representation of product information, with each FHIR resource handling specific aspects of the XML data. 

Below is a high-level overview of the mappings, focusing on major PMDA XML elements like `Document/ProductName`, `Indications`, `DosageForm`, `Document/Manufacturer`, `ActiveIngredient/Name`, `Packaging`, `ApprovalDate`, and `PhysicoChemicalProperties`:

Only the specified FHIR resources are in scope: Bundle, Composition, MedicinalProductDefinition, Ingredient, ManufacturedItemDefinition, AdministrableProductDefinition, PackagedProductDefinition, RegulatedAuthorization, ClinicalUseDefinition (Indication, Contraindication, Interaction, UndesirableEffect subtypes), MedicationKnowledge, Binary, Organization, and SubstanceDefinition.

The table below details the mapping.

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
            <th>FHIR ePI Resource</th>
            <th>PMDA XML Element</th>
            <th>Notes</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan="14">Composition</td>
            <td>Date of preparation</td>
            <td>In Composition.date or extension for preparation date.</td>
        </tr>
        <tr>
            <td>Date of Revision</td>
            <td>In Composition.version or event history.</td>
        </tr>
        <tr>
            <td>Version</td>
            <td>In Composition.version.</td>
        </tr>
        <tr>
            <td>Language</td>
            <td>In Composition.language.</td>
        </tr>
        <tr>
            <td>Warnings</td>
            <td>In Composition.section for warnings/precautions.</td>
        </tr>
        <tr>
            <td>Important precautions</td>
            <td>In Composition.section for precautions.</td>
        </tr>
        <tr>
            <td>Category Name for Free Items</td>
            <td>In Composition.section.title for free text sections.</td>
        </tr>
        <tr>
            <td>Content for Free Items</td>
            <td>In Composition.section.text.</td>
        </tr>
        <tr>
            <td>Title</td>
            <td>In Composition.title or section.title.</td>
        </tr>
        <tr>
            <td>Footer</td>
            <td>In Composition.section.text or extension.</td>
        </tr>
        <tr>
            <td>Precautions</td>
            <td>In section for precautions.</td>
        </tr>
        <tr>
            <td>Clinical use</td>
            <td>In clinical studies section.</td>
        </tr>
        <tr>
            <td>Non-clinical trials</td>
            <td>In non-clinical data section.</td>
        </tr>
        <tr>
            <td>MainLiterature</td>
            <td>In references section.</td>
        </tr>
        <tr>
            <td rowspan="12">MedicinalProductDefinition</td>
            <td>Japanese Standard Commodity Classification Number (Sccj no)</td>
            <td>In MedicinalProductDefinition.classification or identifier.</td>
        </tr>
        <tr>
            <td>Therapeutic Classification Name</td>
            <td>In MedicinalProductDefinition.classification.</td>
        </tr>
        <tr>
            <td>StandardName</td>
            <td>In MedicinalProductDefinition.name.productName or additionalName.</td>
        </tr>
        <tr>
            <td>Regulatory Classification</td>
            <td>In MedicinalProductDefinition.classification.</td>
        </tr>
        <tr>
            <td>GenericName</td>
            <td>In MedicinalProductDefinition.name.productName (generic variant).</td>
        </tr>
        <tr>
            <td>Brand name</td>
            <td>In MedicinalProductDefinition.name.productName.</td>
        </tr>
        <tr>
            <td>YJ code</td>
            <td>In MedicinalProductDefinition.identifier (YJ code system).</td>
        </tr>
        <tr>
            <td>Trademark name (English)</td>
            <td>In MedicinalProductDefinition.name.productName with language code.</td>
        </tr>
        <tr>
            <td>Brand name hiragana</td>
            <td>In MedicinalProductDefinition.name.productName with language variant.</td>
        </tr>
        <tr>
            <td>Brand name</td>
            <td>In MedicinalProductDefinition.name.productName.</td>
        </tr>
        <tr>
            <td>RegulatoryClassificationCode</td>
            <td>In MedicinalProductDefinition.classification.code.</td>
        </tr>
        <tr>
            <td>Drug name</td>
            <td>In name.</td>
        </tr>
        <tr>
            <td rowspan="3">Ingredient</td>
            <td>Composition</td>
            <td>Overall composition in ManufacturedItemDefinition or Ingredient.</td>
        </tr>
        <tr>
            <td>Active ingredient</td>
            <td>In Ingredient.substance.</td>
        </tr>
        <tr>
            <td>Excipients</td>
            <td>In Ingredient for non-active components.</td>
        </tr>
        <tr>
            <td rowspan="6">ManufacturedItemDefinition</td>
            <td>Property</td>
            <td>In ManufacturedItemDefinition.property.</td>
        </tr>
        <tr>
            <td>Physical characteristics (size, colour, shape, flavour, imprint, score, image, text description, Size (diameter, long diameter, short diameter, total length, thickness, area)</td>
            <td>In ManufacturedItemDefinition.property for characteristics like size, color, shape; Binary for images.</td>
        </tr>
        <tr>
            <td>Appearance Surface, back, side, other</td>
            <td>In ManufacturedItemDefinition.property or Binary for images.</td>
        </tr>
        <tr>
            <td>Dose form</td>
            <td>In manufacturedDoseForm</td>
        </tr>
        <tr>
            <td>Odour</td>
            <td>In property.</td>
        </tr>
        <tr>
            <td>Taste</td>
            <td>In property.</td>
        </tr>
        <tr>
            <td rowspan="1">AdministrableProductDefinition</td>
            <td>Dose form</td>
            <td>In AdministrableProductDefinition.formOf or doseForm.</td>
        </tr>
        <tr>
            <td rowspan="3">PackagedProductDefinition</td>
            <td>Storage, Expiration Period</td>
            <td>In PackagedProductDefinition.shelfLifeStorage.</td>
        </tr>
        <tr>
            <td>Shelf life and storage</td>
            <td>In PackagedProductDefinition.shelfLifeStorage.</td>
        </tr>
        <tr>
            <td>packaging</td>
            <td>Primary packaging details.</td>
        </tr>
        <tr>
            <td rowspan="3">RegulatedAuthorization</td>
            <td>Approval Number, Starting Date of Marketing</td>
            <td>In RegulatedAuthorization.identifier (approval number) and RegulatedAuthorization.validityPeriod (start date).</td>
        </tr>
        <tr>
            <td>ApprovalNo</td>
            <td>In RegulatedAuthorization.identifier.</td>
        </tr>
        <tr>
            <td>StartingDateOfMarketing</td>
            <td>In RegulatedAuthorization.validityPeriod.start.</td>
        </tr>
        <tr>
            <td rowspan="1">ClinicalUseDefinition (Indication subtype)</td>
            <td>Indications</td>
            <td>Specific for indications.</td>
        </tr>
        <tr>
            <td rowspan="1">ClinicalUseDefinition (Contraindication subtype)</td>
            <td>Contraindications</td>
            <td>Specific resource for contraindications.</td>
        </tr>
        <tr>
            <td rowspan="2">ClinicalUseDefinition (UndesirableEffect subtype)</td>
            <td>Serious Adverse Events</td>
            <td>For adverse reactions and serious events.</td>
        </tr>
        <tr>
            <td>Undesirable effects</td>
            <td>For adverse effects.</td>
        </tr>
        <tr>
            <td rowspan="2">MedicationKnowledge</td>
            <td>Dose and administration</td>
            <td>In Composition.section for dosage instructions.</td>
        </tr>
        <tr>
            <td>Dosage precautions</td>
            <td>In dosage section precautions.</td>
        </tr>
        <tr>
            <td rowspan="3">Organization</td>
            <td>Manufacturers and Distributors</td>
            <td>Referenced in RegulatedAuthorization.holder or other resources.</td>
        </tr>
        <tr>
            <td>Manufacturer</td>
            <td>For manufacturer organization.</td>
        </tr>
        <tr>
            <td>Reference Request and Contact Information</td>
            <td>In contact section.</td>
        </tr>
        <tr>
            <td rowspan="10">SubstanceDefinition</td>
            <td>Physicochemical Knowledge of Active Ingredients</td>
            <td>In SubstanceDefinition.property for physicochemical info.</td>
        </tr>
        <tr>
            <td>ChemicalName</td>
            <td>In name.</td>
        </tr>
        <tr>
            <td>StructuralFormula</td>
            <td>SubstanceDefinition reference to Binary for structure.</td>
        </tr>
        <tr>
            <td>MolecularFormula</td>
            <td>In molecularFormula.</td>
        </tr>
        <tr>
            <td>MolecularWeight</td>
            <td>In molecularWeight.</td>
        </tr>
        <tr>
            <td>DescriptionOfActiveIngredients</td>
            <td>In description.</td>
        </tr>
        <tr>
            <td>MeltingPoint</td>
            <td>In property.</td>
        </tr>
        <tr>
            <td>PartitionCoefficient</td>
            <td>In property.</td>
        </tr>
        <tr>
            <td>Osmotic Pressure Ratio</td>
            <td>In property extension.</td>
        </tr>
        <tr>
            <td>Mechanism of action</td>
            <td>In MedicationKnowledge.monograph for MoA.</td>
        </tr>
    </tbody>
</table>