# Terminology Management for ePI Japan Implementation Guide

This page outlines recommendations for managing terminologies to support the Electronic Product Information (ePI) Japan Implementation Guide (IG), ensuring the transition from the Pharmaceuticals and Medical Devices Agency (PMDA)’s XML-based labeling format to the FHIR ePI standard preserves Japan-specific regulatory terms and aligns with Japanese healthcare systems. The approach addresses PMDA’s section headings (e.g., 効能又は効果, 禁忌), metadata (e.g., revision symbols), and styling cues (e.g., red borders for warnings), as defined in `package_insert-XML.xsd`, `preview.css`, and related XSL files, while integrating with standardized terminologies for interoperability.

## Recommendations for Terminology Management

### 1. Adopt a Hybrid Terminology Approach
- **PMDA-Specific Terms**: Retain Japan-specific terms from PMDA’s XML schema, such as 効能又は効果 (`HDR_IndicationsOrEfficacy`), 禁忌 (`HDR_ContraIndications`), and 用法及び用量 (`HDR_DosageAndAdministration`), to ensure regulatory compliance and familiarity for Japanese stakeholders.
- **Standardized Terminologies**: Map PMDA terms to international standards like SNOMED CT (for clinical concepts), LOINC (for document sections), and EDQM (for pharmaceutical attributes) to support interoperability with Japanese EHR systems.
- **Example**: Map 禁忌 to SNOMED CT’s “Contraindication” (ID: 407563006) in FHIR `Composition.section.code`, while preserving 禁忌 in the narrative text for display, styled with a red border as per `preview.css`’s `.ContraIndications` class.

### 2. Create a Japan-Specific ValueSet for ePI Sections
- Define a FHIR `ValueSet` to codify PMDA’s section headings (e.g., 効能又は効果, 禁忌, 組成・性状) as used in `package_insert-XML.xsd` and styled in `preview.css` (e.g., `.section_header`).
- Use LOINC codes for section types where possible (e.g., LOINC 48768-6 for “Indications”) but prioritize Japanese terms as preferred display names.
- **Example**: A `ValueSet` entry for 効能又は効果 includes LOINC 48768-6, with 効能又は効果 as the display name and a reference to `HDR_IndicationsOrEfficacy`.
- Host the `ValueSet` in this IG, with validation against PMDA guidelines.

### 3. Leverage Code Systems for Metadata and Styling
- **Revision Metadata**: Create a custom `CodeSystem` for PMDA’s revision symbols (e.g., `revisionPrevThis-editor`, `revisionThis-editor` in `preview.css`), defining codes like “Previous”, “Current”, and “Both” for use in FHIR extensions within `Composition`.
- **Styling Cues**: Define a `CodeSystem` for styling-related terms (e.g., “Warning”, “Contraindication”) that trigger visual cues, such as red borders (`preview.css`’s `.Warnings`, `.ContraIndications`), to preserve semantics in FHIR rendering.
- **Example**: A `CodeSystem` code “RedBorderWarning” indicates content requiring `.Warnings` styling, linked to `Composition.section` via an extension.

### 4. Support Multilingual and Regional Metadata
- Use ISO 639-1 two-letter language codes (e.g., `ja` for Japanese, `en` for English) and ISO 3166-1 alpha-2 country codes (e.g., `JP` for Japan) to tag PMDA terms and metadata, supporting bilingual systems and regional compliance, as indicated by `preview_ja.xsl` and `preview_en.xsl`.
- Use FHIR `ConceptMap` to map Japanese terms to English equivalents (e.g., 禁忌 to “Contraindication”) for bilingual EHR displays in Japan, ensuring Japanese terms remain primary.
- **Example**: A `ConceptMap` links 効能又は効果 to “Indications” with language code `en` and country code `JP`.

### 5. Integrate with Pharmaceutical and Japanese Standards
- **EDQM Standard Terms**: Use EDQM for units of presentation (e.g., “tablet”), routes of administration (e.g., “oral”), dose forms (e.g., “film-coated tablet”), packaging types (e.g., “blister pack”), and closure systems (e.g., “child-resistant cap”) to standardize pharmaceutical attributes in `Composition.section`.
- **G-SRS**: Use the Global Substance Registration System (G-SRS) for identifying active ingredients and excipients in `HDR_Composition`, mapped to `Composition.section` with extensions or narrative text, preserving `CompositionAndProperty_table` structure from `preview.css`.
- **UCUM**: Use the Unified Code for Units of Measure (UCUM) for dosing and packaging quantities (e.g., “mg” for milligram, “mL” for milliliter) to ensure machine-readable units.
- **Japanese Standards**: Align with Japan’s Standard Disease Code (標準病名マスター) for diagnoses in relevant sections (e.g., `HDR_IndicationsOrEfficacy`) to ensure compatibility with national EHR systems.
- **Example**: Map 組成 data to G-SRS substance IDs and EDQM dose forms in `Composition.section`, with UCUM units (e.g., “100 mg”) and `CompositionAndProperty_table` formatting.

### 6. Maintain a Terminology Server
- Host terminologies on a FHIR-compliant terminology server (e.g., HAPI FHIR) to manage `CodeSystem`, `ValueSet`, and `ConceptMap` resources, including SNOMED CT, LOINC, EDQM, G-SRS, and UCUM.
- Ensure support for Japanese character sets (e.g., UTF-8 for 游明朝 font) and PMDA metadata (e.g., revision tracking).
- Provide API access to the server via the IG for querying PMDA-specific terms, ISO codes, and standard mappings.

### 7. Validation and Governance
- Establish a governance process with PMDA, Japanese healthcare providers, and FHIR experts to validate and update terminologies, ensuring alignment with EDQM, G-SRS, UCUM, and PMDA guidelines.
- Use FHIR’s `TerminologyCapabilities` to document supported code systems (e.g., SNOMED CT, EDQM) and validation rules.
- Review mappings regularly to reflect updates in PMDA guidelines, EDQM terms, or FHIR ePI standards.

### 8. Documentation and Training
- Document all PMDA terms, standard mappings (e.g., EDQM, G-SRS, UCUM), and usage examples in the IG (e.g., encoding 効能又は効果 in `Composition.section` with LOINC 48768-6).
- Provide training for Japanese implementers on integrating terminologies into EHRs and mobile apps, emphasizing PMDA’s styling (e.g., red borders, table formats in `.VariousForm`) and ISO code usage.

## Example Terminology Mapping
| PMDA Term (Japanese) | PMDA XML Section | FHIR Resource | Standard Code | Display Style |
|----------------------|------------------|---------------|---------------|---------------|
| 効能又は効果 | `HDR_IndicationsOrEfficacy` | `Composition.section` | LOINC 48768-6 | Circle markers (`.SimpleList` in `preview.css`) |
| 禁忌 | `HDR_ContraIndications` | `Composition.section` | SNOMED CT 407563006 | Red border (`.ContraIndications` in `preview.css`) |
| 組成 | `HDR_Composition` | `Composition.section` | G-SRS (substance), EDQM (dose form) | Table format (`.VariousForm` in `preview.css`) |
| 用法及び用量 | `HDR_DosageAndAdministration` | `Composition.section` | EDQM (route), UCUM (unit) | Narrative text, table format (`.VariousForm` in `preview.css`) |

## Additional Notes
- **PMDA Fidelity**: The approach preserves PMDA’s terminology (e.g., 効能又は効果, 禁忌) and styling (e.g., 游明朝 font, red borders) to ensure compliance and user recognition, as seen in `preview.css` and XSL files.
- **Interoperability**: Mapping to SNOMED CT, LOINC, EDQM, G-SRS, UCUM, and ISO standards ensures compatibility with Japanese EHRs and FHIR ecosystems, supporting use cases like pharmacovigilance and structured product details.
- **Scalability**: The terminology server and governance process allow for future PMDA updates, such as new section headings or EDQM term revisions.
- **Implementation Support**: Documentation and training address Japan’s unique needs, including regulatory compliance, mobile app integration, and ISO code usage for metadata.

----------------------------------------


# ePI日本実装ガイドの用語管理

本ページでは、電子製品情報（ePI）日本実装ガイド（IG）の用語管理に関する推奨事項を概説し、医薬品医療機器総合機構（PMDA）のXMLベースの添付文書フォーマットからFHIR ePI標準への移行が日本固有の規制用語を保持し、日本の医療システムと整合することを保証します。このアプローチは、PMDAのセクション見出し（例：効能又は効果、禁忌）、メタデータ（例：改訂記号）、およびスタイルの手がかり（例：警告の赤枠）を、`package_insert-XML.xsd`、`preview.css`、および関連XSLファイルに定義された通りに対処し、相互運用性のための標準化された用語と統合します。

## 用語管理の推奨事項

### 1. ハイブリッド用語アプローチの採用
- **PMDA固有の用語**：PMDAのXMLスキーマから日本固有の用語、例えば効能又は効果（`HDR_IndicationsOrEfficacy`）、禁忌（`HDR_ContraIndications`）、用法及び用量（`HDR_DosageAndAdministration`）を保持し、規制順守と日本の関係者にとっての親しみやすさを確保します。
- **標準化された用語**：日本のEHRシステムとの相互運用性をサポートするため、PMDAの用語をSNOMED CT（臨床概念用）、LOINC（文書セクション用）、EDQM（医薬品属性用）などの国際標準にマッピングします。
- **例**：禁忌をFHIR `Composition.section.code`でSNOMED CTの「Contraindication」（ID：407563006）にマッピングし、表示用に禁忌をナラティブテキストで保持し、`preview.css`の`.ContraIndications`クラスに従って赤枠でスタイル設定します。

### 2. ePIセクション用の日本固有のValueSetの作成
- PMDAのセクション見出し（例：効能又は効果、禁忌、組成・性状）を、`package_insert-XML.xsd`で使用され、`preview.css`でスタイル設定された（例：`.section_header`）FHIR `ValueSet`でコード化します。
- 可能であればセクションタイプにLOINCコードを使用します（例：「Indications」のLOINC 48768-6）が、日本語の用語を表示名として優先します。
- **例**：効能又は効果の`ValueSet`エントリにはLOINC 48768-6が含まれ、効能又は効果が表示名として、`HDR_IndicationsOrEfficacy`への参照が含まれます。
- このIG内で`ValueSet`をホストし、PMDAガイドラインに対する検証を行います。

### 3. メタデータおよびスタイル用のコードシステムの活用
- **改訂メタデータ**：PMDAの改訂記号（例：`preview.css`の`revisionPrevThis-editor`、`revisionThis-editor`）用にカスタム`CodeSystem`を作成し、「Previous」、「Current」、「Both」などのコードを定義し、`Composition`内のFHIR拡張で使用します。
- **スタイルの手がかり**：警告や禁忌などのスタイル関連の用語を定義する`CodeSystem`を作成し、赤枠（`preview.css`の`.Warnings`、`.ContraIndications`）などの視覚的な手がかりをトリガーし、FHIRレンダリングでセマンティクスを保持します。
- **例**：`CodeSystem`コード「RedBorderWarning」は、`.Warnings`スタイルが必要なコンテンツを示し、`Composition.section`に拡張を介してリンクします。

### 4. 多言語および地域メタデータのサポート
- ISO 639-1の2文字言語コード（例：日本語の`ja`、英語の`en`）およびISO 3166-1 alpha-2の2文字国コード（例：日本の`JP`）を使用して、PMDAの用語とメタデータをタグ付けし、`preview_ja.xsl`および`preview_en.xsl`で示されるように、バイリンガルシステムと地域のコンプライアンスをサポートします。
- FHIR `ConceptMap`を使用して、日本語の用語を英語の同等語（例：禁忌を「Contraindication」）にマッピングし、日本語の用語を主要なものとして保持しながら、日本のバイリンガルEHR表示で一貫性を確保します。
- **例**：`ConceptMap`は、効能又は効果を言語コード`en`および国コード`JP`で「Indications」にリンクします。

### 5. 医薬品および日本標準との統合
- **EDQM標準用語**：単位提示（例：「錠剤」）、投与経路（例：「経口」）、剤形（例：「フィルムコーティング錠」）、包装タイプ（例：「ブリスターパック」）、および閉鎖システム（例：「チャイルドレジスタントキャップ」）を標準化するために、`Composition.section`でEDQMを使用します。
- **G-SRS**：`HDR_Composition`の有効成分および添加物を特定するためにグローバル物質登録システム（G-SRS）を使用し、`Composition.section`に拡張またはナラティブテキストでマッピングし、`preview.css`の`CompositionAndProperty_table`構造を保持します。
- **UCUM**：投与量および包装数量（例：ミリグラムの「mg」、ミリリットルの「mL」）にUnified Code for Units of Measure（UCUM）を使用して、機械可読な単位を確保します。
- **日本の標準**：関連セクション（例：`HDR_IndicationsOrEfficacy`）の診断に日本の標準病名マスターを使用し、国内EHRシステムとの互換性を確保します。
- **例**：組成データを`Composition.section`でG-SRS物質IDおよびEDQM剤形にマッピングし、UCUM単位（例：「100 mg」）および`CompositionAndProperty_table`の書式を使用します。

### 6. 用語サーバーの維持
- `CodeSystem`、`ValueSet`、および`ConceptMap`リソース（SNOMED CT、LOINC、EDQM、G-SRS、UCUMを含む）を管理するために、FHIR準拠の用語サーバー（例：HAPI FHIR）をホストします。
- 日本語の文字セット（例：游明朝フォント用のUTF-8）およびPMDAメタデータ（例：改訂追跡）のサポートを確保します。
- PMDA固有の用語、ISOコード、および標準マッピングをクエリするためのAPIアクセスをIGを通じて提供します。

### 7. 検証およびガバナンス
- PMDA、日本の医療提供者、FHIR専門家と協力して用語を検証および更新し、EDQM、G-SRS、UCUM、およびPMDAガイドラインとの整合性を確保するガバナンスプロセスを確立します。
- FHIRの`TerminologyCapabilities`を使用して、サポートされているコードシステム（例：SNOMED CT、EDQM）および検証ルールを文書化します。
- PMDAガイドライン、EDQM用語、またはFHIR ePI標準の更新を反映するために、マッピングを定期的にレビューします。

### 8. 文書化およびトレーニング
- PMDAの用語、標準マッピング（例：EDQM、G-SRS、UCUM）、および使用例（例：`Composition.section`での効能又は効果のエンコーディング、LOINC 48768-6を使用）をIGで文書化します。
- 日本の実装者向けに、EHRおよびモバイルアプリへの用語統合に関するトレーニングを提供し、PMDAのスタイル（例：赤枠、`.VariousForm`のテーブル書式）およびISOコードの使用を強調します。

## 用語マッピングの例
| PMDA用語（日本語） | PMDA XMLセクション | FHIRリソース | 標準コード | 表示スタイル |
|-------------------|-------------------|-------------|-----------|-------------|
| 効能又は効果 | `HDR_IndicationsOrEfficacy` | `Composition.section` | LOINC 48768-6 | 丸記号（`preview.css`の`.SimpleList`） |
| 禁忌 | `HDR_ContraIndications` | `Composition.section` | SNOMED CT 407563006 | 赤枠（`preview.css`の`.ContraIndications`） |
| 組成 | `HDR_Composition` | `Composition.section` | G-SRS（物質）、EDQM（剤形） | テーブル書式（`preview.css`の`.VariousForm`） |
| 用法及び用量 | `HDR_DosageAndAdministration` | `Composition.section` | EDQM（投与経路）、UCUM（単位） | ナラティブテキスト、テーブル書式（`preview.css`の`.VariousForm`） |

## 補足事項
- **PMDAの忠実性**：このアプローチは、PMDAの用語（例：効能又は効果、禁忌）およびスタイル（例：游明朝フォント、赤枠）を保持し、`preview.css`およびXSLファイルに見られるように、コンプライアンスとユーザーの認識を確保します。
- **相互運用性**：SNOMED CT、LOINC、EDQM、G-SRS、UCUM、およびISO標準へのマッピングは、日本のEHRおよびFHIRエコシステムとの互換性を確保し、ファーマコビジランスや構造化製品詳細などのユースケースをサポートします。
- **スケーラビリティ**：用語サーバーおよびガバナンスプロセスは、新しいセクション見出しやEDQM用語の改訂など、将来のPMDA更新に対応します。
- **実装サポート**：文書化およびトレーニングは、規制コンプライアンス、モバイルアプリ統合、ISOコードの使用を含む日本の独自のニーズに対応します。

詳細については、[FHIR ePI仕様](https://www.hl7.org/fhir/)、[PMDA添付文書ガイドライン](https://www.pmda.go.jp/)、[EDQM標準用語](https://www.edqm.eu/)、[G-SRS](https://www.fda.gov/)、および[UCUM](https://ucum.org/)を参照してください。貢献およびフィードバックは[GitHubリポジトリ](https://github.com/cander2/epi-jp)にて歓迎します。