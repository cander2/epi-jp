このページでは、ePIの構築と管理方法について段階的な指示を提供します。
 
---

This page provides step-by-step instructions on how to build and manage ePIs.

The following figure shows how the ePI Type 3 resources relate to each other:
<span style="display: inline-block; vertical-align: middle;">
  <img src="epiType3RelationshipDiagram.drawio.svg" alt="Entity relationship diagram of ePI Type 3 resource relationships" style="width: 800px; height: auto;" />
</span>


### Bundle

The Bundle resource serves as the container for the ePI document, aggregating the Composition and all referenced resources into a single, cohesive FHIR document bundle.

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
            <th>FHIR Resource</th>
            <th>FHIR Element</th>
            <th>JP XML/XSD Element</th>
            <th>Notes</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Bundle</td>
            <td>id</td>
            <td>n/a</td>
            <td>The Bundle contains the Composition as the first entry, with other referenced resources.</td>
        </tr>
        <tr>
            <td>Bundle</td>
            <td>meta.versionId</td>
            <td>Document/Revision</td>
            <td>Version identifier based on document revision (e.g., '第1版').</td>
        </tr>
        <tr>
            <td>Bundle</td>
            <td>meta.lastUpdated</td>
            <td>Document/RevisionDate</td>
            <td>Last updated timestamp, mapped from revision date or set to current assembly time.</td>
        </tr>
        <tr>
            <td>Bundle</td>
            <td>identifier</td>
            <td>Document/ProductCode</td>
            <td>Unique identifier for the bundle, possibly using product code or document ID.</td>
        </tr>
        <tr>
            <td>Bundle</td>
            <td>type</td>
            <td>n/a</td>
            <td>Set to 'document' for the ePI Bundle.</td>
        </tr>
        <tr>
            <td>Bundle</td>
            <td>timestamp</td>
            <td>n/a</td>
            <td>Current timestamp when the Bundle is assembled.</td>
        </tr>
        <tr>
            <td>Bundle</td>
            <td>entry</td>
            <td>n/a</td>
            <td>Entries for Composition, Binary (if narrative), Organizations, etc.</td>
        </tr>
    </tbody>
</table>

### Composition

The Composition resource represents the structured content of the electronic Package Insert (ePI), organizing sections such as indications, dosage, and precautions into a human-readable document.

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
            <th>FHIR Resource</th>
            <th>FHIR Element</th>
            <th>JP XML/XSD Element</th>
            <th>Notes</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Composition</td>
            <td>id</td>
            <td>n/a</td>
            <td>Unique identifier for the Composition resource.</td>
        </tr>
        <tr>
            <td>Composition</td>
            <td>status</td>
            <td>n/a</td>
            <td>Typically 'final' for published ePI.</td>
        </tr>
        <tr>
            <td>Composition</td>
            <td>type</td>
            <td>n/a</td>
            <td>Coded as 'Package Insert' or equivalent from value set.</td>
        </tr>
        <tr>
            <td>Composition</td>
            <td>subject</td>
            <td>n/a</td>
            <td>Reference to MedicinalProductDefinition.</td>
        </tr>
        <tr>
            <td>Composition</td>
            <td>date</td>
            <td>Document/RevisionDate</td>
            <td>Maps to the revision date of the document, or Date of Preparation or Revision (作成又は改訂年月).</td>
        </tr>
        <tr>
            <td>Composition</td>
            <td>author</td>
            <td>Document/Manufacturer</td>
            <td>Reference to Organization (manufacturer).</td>
        </tr>
        <tr>
            <td>Composition</td>
            <td>title</td>
            <td>Document/ProductName</td>
            <td>Product name from the XML.</td>
        </tr>
        <tr>
            <td>Composition</td>
            <td>text</td>
            <td>Narrative content from entire XML</td>
            <td>Overall narrative description of the entire document in XHTML format, distinct from title.</td>
        </tr>
        <tr>
            <td>Composition</td>
            <td>language</td>
            <td>Document/Language or default 'ja'</td>
            <td>Language code, e.g., 'ja' for Japanese.</td>
        </tr>
        <tr>
            <td>Composition</td>
            <td>contained</td>
            <td>Reference to Binary for images</td>
            <td>Contained Binary resource for inline images; Binary has id, contentType (e.g., 'image/svg+xml'), and data (base64 encoded SVG).</td>
        </tr>
        <tr>
            <td>Composition</td>
            <td>version</td>
            <td>Document/Revision</td>
            <td>Version of the composition, mapped from document revision (e.g., '第1版').</td>
        </tr>
        <tr>
            <td>Composition</td>
            <td>relatesTo</td>
            <td>n/a</td>
            <td>Relationships to other documents or versions if applicable.</td>
        </tr>
        <tr>
            <td>Composition</td>
            <td>section</td>
            <td>Various sections like Warnings, Indications, etc.</td>
            <td>Each major section in XML maps to a Composition.section, with nested sub-sections. For example, maps to Warnings (警告).</td>
        </tr>
        <tr>
            <td>Composition</td>
            <td>section.id</td>
            <td>n/a</td>
            <td>Unique identifier for the section.</td>
        </tr>
        <tr>
            <td>Composition</td>
            <td>section.title</td>
            <td>Section/Title</td>
            <td>Title of the section from XML.</td>
        </tr>
        <tr>
            <td>Composition</td>
            <td>section.code</td>
            <td>Section/Code</td>
            <td>Coded concept for the section type (e.g., from LOINC or local codes for indications, contraindications).</td>
        </tr>
        <tr>
            <td>Composition</td>
            <td>section.text</td>
            <td>Narrative content from XML sections</td>
            <td>XHTML narrative derived from XML content.</td>
        </tr>
    </tbody>
</table>

### Binary

The Binary will only handle images encoded as Base64 format. This means ePIs are always one XML file since images are embedded in the XML file rather than outside the XML.

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
            <th>FHIR Resource</th>
            <th>FHIR Element</th>
            <th>JP XML/XSD Element</th>
            <th>Notes</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Binary</td>
            <td>id</td>
            <td>n/a</td>
            <td>Identifier for binary content if used (e.g., for images in composition).</td>
        </tr>
        <tr>
            <td>Binary</td>
            <td>contentType</td>
            <td>n/a</td>
            <td>'image/png' or similar for embedded images.</td>
        </tr>
        <tr>
            <td>Binary</td>
            <td>data</td>
            <td>Attached files like images</td>
            <td>Base64 encoded content for images, ensuring inline embedding in the ePI XML.</td>
        </tr>
    </tbody>
</table>

### Organization

The Organization resource describes entities involved in the product lifecycle, such as manufacturers or marketing authorization holders, including their contact and address details.

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
            <th>FHIR Resource</th>
            <th>FHIR Element</th>
            <th>JP XML/XSD Element</th>
            <th>Notes</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Organization</td>
            <td>id</td>
            <td>Document/Manufacturer</td>
            <td>Manufacturer's identifier.</td>
        </tr>
        <tr>
            <td>Organization</td>
            <td>identifier</td>
            <td>Document/Manufacturer/ID</td>
            <td>System-assigned identifier for the organization (e.g., business ID).</td>
        </tr>
        <tr>
            <td>Organization</td>
            <td>name</td>
            <td>Document/Manufacturer/Name</td>
            <td>Name of the manufacturing organization.</td>
        </tr>
        <tr>
            <td>Organization</td>
            <td>contact</td>
            <td>Document/Manufacturer/Contact</td>
            <td>Contact details if available.</td>
        </tr>
        <tr>
            <td>Organization</td>
            <td>contact.telecom.system.email</td>
            <td>Document/Manufacturer/Contact/Email</td>
            <td>Email contact system.</td>
        </tr>
        <tr>
            <td>Organization</td>
            <td>contact.telecom.system.url</td>
            <td>Document/Manufacturer/Contact/URL</td>
            <td>URL or website contact system.</td>
        </tr>
        <tr>
            <td>Organization</td>
            <td>contact.telecom.system.phone</td>
            <td>Document/Manufacturer/Contact/Phone</td>
            <td>Phone contact system.</td>
        </tr>
        <tr>
            <td>Organization</td>
            <td>contact.address.type</td>
            <td>Document/Manufacturer/Address/Type</td>
            <td>Type of address (e.g., postal, physical).</td>
        </tr>
        <tr>
            <td>Organization</td>
            <td>contact.address.text</td>
            <td>Document/Manufacturer/Address/Text</td>
            <td>Full text representation of the address.</td>
        </tr>
        <tr>
            <td>Organization</td>
            <td>contact.address.line</td>
            <td>Document/Manufacturer/Address/Line</td>
            <td>Street address lines.</td>
        </tr>
        <tr>
            <td>Organization</td>
            <td>contact.address.city</td>
            <td>Document/Manufacturer/Address/City</td>
            <td>City part of the address.</td>
        </tr>
        <tr>
            <td>Organization</td>
            <td>contact.address.district</td>
            <td>Document/Manufacturer/Address/District</td>
            <td>District or county part of the address.</td>
        </tr>
        <tr>
            <td>Organization</td>
            <td>contact.address.state</td>
            <td>Document/Manufacturer/Address/State</td>
            <td>State or province part of the address.</td>
        </tr>
        <tr>
            <td>Organization</td>
            <td>contact.address.postalcode</td>
            <td>Document/Manufacturer/Address/PostalCode</td>
            <td>Postal code of the address.</td>
        </tr>
        <tr>
            <td>Organization</td>
            <td>contact.address.country</td>
            <td>Document/Manufacturer/Address/Country</td>
            <td>Country of the address (e.g., Japan).</td>
        </tr>
    </tbody>
</table>

### Ingredient

The Ingredient resource defines the active and inactive components of the medicinal product, including strength specifications for dosing.

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
            <th>FHIR Resource</th>
            <th>FHIR Element</th>
            <th>JP XML/XSD Element</th>
            <th>Notes</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Ingredient</td>
            <td>id</td>
            <td>n/a</td>
            <td>Identifier for the ingredient.</td>
        </tr>
        <tr>
            <td>Ingredient</td>
            <td>identifier</td>
            <td>n/a</td>
            <td>System-assigned identifier for the ingredient.</td>
        </tr>
        <tr>
            <td>Ingredient</td>
            <td>for</td>
            <td>Reference to MedicinalProductDefinition</td>
            <td>Links to the product.</td>
        </tr>
        <tr>
            <td>Ingredient</td>
            <td>role</td>
            <td>n/a</td>
            <td>Coded as 'active' or 'excipient' (e.g., for Active Ingredients or Additives).</td>
        </tr>
        <tr>
            <td>Ingredient</td>
            <td>substance</td>
            <td>ActiveIngredient/Name or IndividualAdditives</td>
            <td>Reference to SubstanceDefinition for the active ingredient or additives (添加剤).</td>
        </tr>
        <tr>
            <td>Ingredient</td>
            <td>strength.presentation</td>
            <td>ActiveIngredient/Amount or ContainedAmount</td>
            <td>Presentation strength details like 25mg (含有量).</td>
        </tr>
        <tr>
            <td>Ingredient</td>
            <td>strength.concentration</td>
            <td>ActiveIngredient/Amount or ContainedAmount</td>
            <td>Concentration strength details.</td>
        </tr>
    </tbody>
</table>

### SubstanceDefinition

The SubstanceDefinition resource provides detailed information about the chemical or biological substance used in the product, including physico-chemical properties.

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
            <th>FHIR Resource</th>
            <th>FHIR Element</th>
            <th>JP XML/XSD Element</th>
            <th>Notes</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>SubstanceDefinition</td>
            <td>id</td>
            <td>n/a</td>
            <td>Identifier for the substance.</td>
        </tr>
        <tr>
            <td>SubstanceDefinition</td>
            <td>identifier</td>
            <td>n/a</td>
            <td>System-assigned identifier for the substance.</td>
        </tr>
        <tr>
            <td>SubstanceDefinition</td>
            <td>name</td>
            <td>ActiveIngredient/Name or GenericName</td>
            <td>Substance name (e.g., エキセメスタン) or Generic Name (一般的名称).</td>
        </tr>
        <tr>
            <td>SubstanceDefinition</td>
            <td>grade</td>
            <td>n/a</td>
            <td>Grade of the substance if applicable.</td>
        </tr>
        <tr>
            <td>SubstanceDefinition</td>
            <td>molecularWeight</td>
            <td>n/a</td>
            <td>If provided in physico-chemical data.</td>
        </tr>
        <tr>
            <td>SubstanceDefinition</td>
            <td>molecularFormula</td>
            <td>PhysicoChemicalProperties/MolecularFormula</td>
            <td>Molecular formula from physico-chemical properties.</td>
        </tr>
        <tr>
            <td>SubstanceDefinition</td>
            <td>property</td>
            <td>PhysicoChemicalProperties or DescriptionOfActiveIngredients</td>
            <td>Properties like solubility, melting point from XML, or properties of active ingredients (性状).</td>
        </tr>
    </tbody>
</table>

### ManufacturedItemDefinition

The ManufacturedItemDefinition resource describes the physical characteristics of the manufactured product, such as form, size, and appearance.

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
            <th>FHIR Resource</th>
            <th>FHIR Element</th>
            <th>JP XML/XSD Element</th>
            <th>Notes</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>ManufacturedItemDefinition</td>
            <td>id</td>
            <td>n/a</td>
            <td>Identifier for the manufactured item.</td>
        </tr>
        <tr>
            <td>ManufacturedItemDefinition</td>
            <td>identifier</td>
            <td>n/a</td>
            <td>System-assigned identifier for the manufactured item.</td>
        </tr>
        <tr>
            <td>ManufacturedItemDefinition</td>
            <td>name</td>
            <td>Composition/Name</td>
            <td>Name of the manufactured item.</td>
        </tr>
        <tr>
            <td>ManufacturedItemDefinition</td>
            <td>manufacturedDoseForm</td>
            <td>DosageForm</td>
            <td>Coded dose form (e.g., tablet).</td>
        </tr>
        <tr>
            <td>ManufacturedItemDefinition</td>
            <td>unitOfPresentation</td>
            <td>Packaging/Unit</td>
            <td>Unit like 'tablet'.</td>
        </tr>
        <tr>
            <td>ManufacturedItemDefinition</td>
            <td>manufacturer</td>
            <td>Document/Manufacturer</td>
            <td>Reference to Organization.</td>
        </tr>
        <tr>
            <td>ManufacturedItemDefinition</td>
            <td>property</td>
            <td>Composition or Property</td>
            <td>Properties for colour (色調), flavour, shape (外形), score, size (大きさ), surface form, imprint, text, image of the product and pack. Also maps to CompositionAndProperty, PropertyForBrand, etc.</td>
        </tr>
    </tbody>
</table>

### AdministrableProductDefinition

The AdministrableProductDefinition resource specifies how the product is administered to the patient, including dose form and route.

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
            <th>FHIR Resource</th>
            <th>FHIR Element</th>
            <th>JP XML/XSD Element</th>
            <th>Notes</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>AdministrableProductDefinition</td>
            <td>id</td>
            <td>n/a</td>
            <td>Identifier for the administrable form.</td>
        </tr>
        <tr>
            <td>AdministrableProductDefinition</td>
            <td>identifier</td>
            <td>n/a</td>
            <td>System-assigned identifier for the administrable product.</td>
        </tr>
        <tr>
            <td>AdministrableProductDefinition</td>
            <td>description</td>
            <td>DosageForm/Description</td>
            <td>Description of the administrable product.</td>
        </tr>
        <tr>
            <td>AdministrableProductDefinition</td>
            <td>formOf</td>
            <td>Reference to MedicinalProductDefinition</td>
            <td>Links to the product.</td>
        </tr>
        <tr>
            <td>AdministrableProductDefinition</td>
            <td>administrableDoseForm</td>
            <td>DosageForm</td>
            <td>Administrable form (e.g., oral tablet).</td>
        </tr>
        <tr>
            <td>AdministrableProductDefinition</td>
            <td>unitOfPresentation</td>
            <td>Packaging/Unit</td>
            <td>Presentation unit.</td>
        </tr>
        <tr>
            <td>AdministrableProductDefinition</td>
            <td>routeOfAdministration</td>
            <td>AdministrationRoute</td>
            <td>Route like 'oral'.</td>
        </tr>
        <tr>
            <td>AdministrableProductDefinition</td>
            <td>property</td>
            <td>DosageForm/Property</td>
            <td>Properties for colour, flavour, shape, score, size, surface form, imprint, text, image of the product and pack. Maps to PropertyForConstituentUnits, etc.</td>
        </tr>
    </tbody>
</table>

### PackagedProductDefinition

The PackagedProductDefinition resource details the packaging of the medicinal product, including container type, quantity, and storage conditions.

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
            <th>FHIR Resource</th>
            <th>FHIR Element</th>
            <th>JP XML/XSD Element</th>
            <th>Notes</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>PackagedProductDefinition</td>
            <td>id</td>
            <td>n/a</td>
            <td>Identifier for the package.</td>
        </tr>
        <tr>
            <td>PackagedProductDefinition</td>
            <td>identifier</td>
            <td>n/a</td>
            <td>System-assigned identifier for the package.</td>
        </tr>
        <tr>
            <td>PackagedProductDefinition</td>
            <td>packageFor</td>
            <td>Reference to MedicinalProductDefinition</td>
            <td>Links to the product.</td>
        </tr>
        <tr>
            <td>PackagedProductDefinition</td>
            <td>containedItem</td>
            <td>Reference to ManufacturedItemDefinition</td>
            <td>Points to a manufactured item.</td>
        </tr>
        <tr>
            <td>PackagedProductDefinition</td>
            <td>manufacturer</td>
            <td>Document/Manufacturer</td>
            <td>Reference to Organization (manufacturer).</td>
        </tr>
        <tr>
            <td>PackagedProductDefinition</td>
            <td>type</td>
            <td>Packaging/Type</td>
            <td>Type of packaging.</td>
        </tr>
        <tr>
            <td>PackagedProductDefinition</td>
            <td>description</td>
            <td>Packaging/Description</td>
            <td>Description of the package.</td>
        </tr>
        <tr>
            <td>PackagedProductDefinition</td>
            <td>packaging</td>
            <td>Packaging</td>
            <td>Details like PTP sheets, bottle size (包装).</td>
        </tr>
        <tr>
            <td>PackagedProductDefinition</td>
            <td>shelfLifeStorage</td>
            <td>StorageConditions or ShelfLife</td>
            <td>Storage instructions and shelf life (貯法、有効期間).</td>
        </tr>
    </tbody>
</table>

### RegulatedAuthorization

The RegulatedAuthorization resource captures regulatory approval details for the product, including marketing authorization and holder information.

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
            <th>FHIR Resource</th>
            <th>FHIR Element</th>
            <th>JP XML/XSD Element</th>
            <th>Notes</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>RegulatedAuthorization</td>
            <td>id</td>
            <td>n/a</td>
            <td>Identifier for the authorization.</td>
        </tr>
        <tr>
            <td>RegulatedAuthorization</td>
            <td>subject</td>
            <td>Reference to MedicinalProductDefinition</td>
            <td>The authorized product.</td>
        </tr>
        <tr>
            <td>RegulatedAuthorization</td>
            <td>type</td>
            <td>n/a</td>
            <td>'Marketing Authorization'.</td>
        </tr>
        <tr>
            <td>RegulatedAuthorization</td>
            <td>region</td>
            <td>n/a</td>
            <td>Japan (JP).</td>
        </tr>
        <tr>
            <td>RegulatedAuthorization</td>
            <td>status</td>
            <td>ApprovalStatus</td>
            <td>Approved or similar.</td>
        </tr>
        <tr>
            <td>RegulatedAuthorization</td>
            <td>date</td>
            <td>ApprovalDate or StartingDateOfMarketing</td>
            <td>Date of approval or starting date of marketing (承認番号、販売開始年月).</td>
        </tr>
        <tr>
            <td>RegulatedAuthorization</td>
            <td>holder</td>
            <td>Document/Manufacturer</td>
            <td>Reference to Organization (MAH).</td>
        </tr>
        <tr>
            <td>RegulatedAuthorization</td>
            <td>identifier</td>
            <td>ApprovalAndLicenseNo</td>
            <td>Approval number (承認番号).</td>
        </tr>
    </tbody>
</table>

### MedicinalProductDefinition

The MedicinalProductDefinition resource provides a comprehensive definition of the medicinal product, including name, classification, and references to related resources like packaging and ingredients.

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
            <th>FHIR Resource</th>
            <th>FHIR Element</th>
            <th>JP XML/XSD Element</th>
            <th>Notes</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>MedicinalProductDefinition</td>
            <td>id</td>
            <td>Document/ProductCode</td>
            <td>Product identifier like 4291012F1022.</td>
        </tr>
        <tr>
            <td>MedicinalProductDefinition</td>
            <td>identifier</td>
            <td>Sccj</td>
            <td>System-assigned identifier for the product, or Japanese Standard Commodity Classification Number (日本標準商品分類番号).</td>
        </tr>
        <tr>
            <td>MedicinalProductDefinition</td>
            <td>name</td>
            <td>Document/ProductName or StandardName or GenericName</td>
            <td>Product name (e.g., アロマシン錠25mg), Standard Name (基準名), or Generic Name (一般的名称).</td>
        </tr>
        <tr>
            <td>MedicinalProductDefinition</td>
            <td>domain</td>
            <td>n/a</td>
            <td>'Human use'.</td>
        </tr>
        <tr>
            <td>MedicinalProductDefinition</td>
            <td>status</td>
            <td>n/a</td>
            <td>Active.</td>
        </tr>
        <tr>
            <td>MedicinalProductDefinition</td>
            <td>type</td>
            <td>n/a</td>
            <td>Type of medicinal product.</td>
        </tr>
        <tr>
            <td>MedicinalProductDefinition</td>
            <td>version</td>
            <td>Document/Revision</td>
            <td>Version of the product definition.</td>
        </tr>
        <tr>
            <td>MedicinalProductDefinition</td>
            <td>combinedPharmaceuticalDoseForm</td>
            <td>DosageForm</td>
            <td>Combined form like 'film-coated tablet'.</td>
        </tr>
        <tr>
            <td>MedicinalProductDefinition</td>
            <td>indication</td>
            <td>Indications</td>
            <td>Text from indications section.</td>
        </tr>
        <tr>
            <td>MedicinalProductDefinition</td>
            <td>classification</td>
            <td>TherapeuticClassification</td>
            <td>ATC or Japanese classification (薬効分類名).</td>
        </tr>
        <tr>
            <td>MedicinalProductDefinition</td>
            <td>description</td>
            <td>Document/ProductDescription</td>
            <td>Description of the medicinal product.</td>
        </tr>
        <tr>
            <td>MedicinalProductDefinition</td>
            <td>route</td>
            <td>AdministrationRoute</td>
            <td>Route of administration.</td>
        </tr>
        <tr>
            <td>MedicinalProductDefinition</td>
            <td>packagedMedicinalProduct</td>
            <td>Packaging</td>
            <td>Reference to PackagedProductDefinition.</td>
        </tr>
        <tr>
            <td>MedicinalProductDefinition</td>
            <td>marketingStatus</td>
            <td>MarketingStatus</td>
            <td>Status in Japan.</td>
        </tr>
        <tr>
            <td>MedicinalProductDefinition</td>
            <td>legalStatusOfSupply</td>
            <td>RegulatoryClassification</td>
            <td>Regulatory classification (規制区分).</td>
        </tr>
    </tbody>
</table>

### ClinicalUseDefinition (Indication subtype)

The ClinicalUseDefinition resource with Indication subtype specifies the approved indications or uses of the medicinal product.

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
            <th>FHIR Resource</th>
            <th>FHIR Element</th>
            <th>JP XML/XSD Element</th>
            <th>Notes</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>ClinicalUseDefinition (Indication subtype)</td>
            <td>id</td>
            <td>n/a</td>
            <td>Identifier for indication.</td>
        </tr>
        <tr>
            <td>ClinicalUseDefinition (Indication subtype)</td>
            <td>identifier</td>
            <td>n/a</td>
            <td>System-assigned identifier for the indication.</td>
        </tr>
        <tr>
            <td>ClinicalUseDefinition (Indication subtype)</td>
            <td>type</td>
            <td>n/a</td>
            <td>'indication'.</td>
        </tr>
        <tr>
            <td>ClinicalUseDefinition (Indication subtype)</td>
            <td>subject</td>
            <td>Reference to MedicinalProductDefinition</td>
            <td>The product.</td>
        </tr>
        <tr>
            <td>ClinicalUseDefinition (Indication subtype)</td>
            <td>indication.diseaseSymptomProcedure</td>
            <td>Indications</td>
            <td>Coded or text indication (e.g., 閉経後乳癌).</td>
        </tr>
        <tr>
            <td>ClinicalUseDefinition (Indication subtype)</td>
            <td>indication.intendedEffect</td>
            <td>n/a</td>
            <td>Therapeutic effect.</td>
        </tr>
    </tbody>
</table>

### ClinicalUseDefinition (Contraindication subtype)

The ClinicalUseDefinition resource with Contraindication subtype lists conditions or patient groups where the product should not be used.

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
            <th>FHIR Resource</th>
            <th>FHIR Element</th>
            <th>JP XML/XSD Element</th>
            <th>Notes</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>ClinicalUseDefinition (Contraindication subtype)</td>
            <td>id</td>
            <td>n/a</td>
            <td>Identifier for contraindication.</td>
        </tr>
        <tr>
            <td>ClinicalUseDefinition (Contraindication subtype)</td>
            <td>identifier</td>
            <td>n/a</td>
            <td>System-assigned identifier for the contraindication.</td>
        </tr>
        <tr>
            <td>ClinicalUseDefinition (Contraindication subtype)</td>
            <td>type</td>
            <td>n/a</td>
            <td>'contraindication'.</td>
        </tr>
        <tr>
            <td>ClinicalUseDefinition (Contraindication subtype)</td>
            <td>subject</td>
            <td>Reference to MedicinalProductDefinition</td>
            <td>The product.</td>
        </tr>
        <tr>
            <td>ClinicalUseDefinition (Contraindication subtype)</td>
            <td>contraindication.diseaseSymptomProcedure</td>
            <td>Contraindications</td>
            <td>Coded or text (e.g., 妊婦又は妊娠している可能性のある女性). Maps to 禁忌.</td>
        </tr>
    </tbody>
</table>

### ClinicalUseDefinition (Interaction subtype)

The ClinicalUseDefinition resource with Interaction subtype describes drug-drug or drug-food interactions that may affect the product's efficacy or safety.

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
            <th>FHIR Resource</th>
            <th>FHIR Element</th>
            <th>JP XML/XSD Element</th>
            <th>Notes</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>ClinicalUseDefinition (Interaction subtype)</td>
            <td>id</td>
            <td>n/a</td>
            <td>Identifier for interaction.</td>
        </tr>
        <tr>
            <td>ClinicalUseDefinition (Interaction subtype)</td>
            <td>identifier</td>
            <td>n/a</td>
            <td>System-assigned identifier for the interaction.</td>
        </tr>
        <tr>
            <td>ClinicalUseDefinition (Interaction subtype)</td>
            <td>type</td>
            <td>n/a</td>
            <td>'interaction'.</td>
        </tr>
        <tr>
            <td>ClinicalUseDefinition (Interaction subtype)</td>
            <td>subject</td>
            <td>Reference to MedicinalProductDefinition</td>
            <td>The product.</td>
        </tr>
        <tr>
            <td>ClinicalUseDefinition (Interaction subtype)</td>
            <td>interaction.interactant</td>
            <td>Interactions/Drug</td>
            <td>Interacting substance or class (e.g., エストロゲン含有製剤). Maps to 相互作用.</td>
        </tr>
        <tr>
            <td>ClinicalUseDefinition (Interaction subtype)</td>
            <td>interaction.type</td>
            <td>Interactions/Type</td>
            <td>Interaction type.</td>
        </tr>
        <tr>
            <td>ClinicalUseDefinition (Interaction subtype)</td>
            <td>interaction.effect</td>
            <td>Interactions/Effect</td>
            <td>Description of effect.</td>
        </tr>
    </tbody>
</table>

### ClinicalUseDefinition (UndesirableEffect subtype)

The ClinicalUseDefinition resource with UndesirableEffect subtype documents potential adverse effects or side effects of the product.

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
            <th>FHIR Resource</th>
            <th>FHIR Element</th>
            <th>JP XML/XSD Element</th>
            <th>Notes</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>ClinicalUseDefinition (UndesirableEffect subtype)</td>
            <td>id</td>
            <td>n/a</td>
            <td>Identifier for undesirable effect.</td>
        </tr>
        <tr>
            <td>ClinicalUseDefinition (UndesirableEffect subtype)</td>
            <td>identifier</td>
            <td>n/a</td>
            <td>System-assigned identifier for the undesirable effect.</td>
        </tr>
        <tr>
            <td>ClinicalUseDefinition (UndesirableEffect subtype)</td>
            <td>type</td>
            <td>n/a</td>
            <td>'undesirable-effect'.</td>
        </tr>
        <tr>
            <td>ClinicalUseDefinition (UndesirableEffect subtype)</td>
            <td>subject</td>
            <td>Reference to MedicinalProductDefinition</td>
            <td>The product.</td>
        </tr>
        <tr>
            <td>ClinicalUseDefinition (UndesirableEffect subtype)</td>
            <td>undesirableEffect.symptomConditionEffect</td>
            <td>AdverseReactions</td>
            <td>Coded adverse effect (e.g., 肝炎). Maps to 副作用, SeriousAdverse, OtherAdverseEvent.</td>
        </tr>
        <tr>
            <td>ClinicalUseDefinition (UndesirableEffect subtype)</td>
            <td>undesirableEffect.frequencyOfOccurrence</td>
            <td>AdverseReactions/Frequency</td>
            <td>Frequency like '頻度不明'.</td>
        </tr>
    </tbody>
</table>

### MedicationKnowledge

The MedicationKnowledge resource is only used for structured dosing.

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
            <th>FHIR Resource</th>
            <th>FHIR Element</th>
            <th>JP XML/XSD Element</th>
            <th>Notes</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>MedicationKnowledge</td>
            <td>id</td>
            <td>n/a</td>
            <td>Identifier for medication knowledge.</td>
        </tr>
        <tr>
            <td>MedicationKnowledge</td>
            <td>identifier</td>
            <td>n/a</td>
            <td>System-assigned identifier for the medication knowledge.</td>
        </tr>
        <tr>
            <td>MedicationKnowledge</td>
            <td>status</td>
            <td>n/a</td>
            <td>Active.</td>
        </tr>
        <tr>
            <td>MedicationKnowledge</td>
            <td>indicationGuideline.indication</td>
            <td>Indications</td>
            <td>Indication guidelines from indications section.</td>
        </tr>
        <tr>
            <td>MedicationKnowledge</td>
            <td>indicationGuideline.dosingGuideline.dosage</td>
            <td>DosageAndAdministration or InfoDoseAdmin</td>
            <td>Dosing guidelines including dosage instructions (用法及び用量).</td>
        </tr>
        <tr>
            <td>MedicationKnowledge</td>
            <td>indicationGuideline.dosingGuideline.patientCharacteristic</td>
            <td>Precautions/PatientCharacteristic</td>
            <td>Patient characteristics for dosing, from precautions or similar (特定の背景を有する患者に関する注意).</td>
        </tr>
    </tbody>
</table>