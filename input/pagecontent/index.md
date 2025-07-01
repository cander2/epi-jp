### Overview

The Electronic Product Information (ePI) Japan Implementation Guide (IG) provides a standardized framework to transition from the Pharmaceuticals and Medical Devices Agency (PMDA)'s custom XML-based labeling format to the Fast Healthcare Interoperability Resources (FHIR) ePI standard. This IG is designed to support the Japanese pharmaceutical labeling ecosystem, ensuring that the structure, content, and regulatory requirements of Japanese package inserts (添付文書) are preserved in the FHIR-based ePI format.

The PMDA's current XML schema, as defined in `package_insert-XML.xsd` and `package_insert-XML-Transitional.xsd`, supports detailed labeling information with specific section headings, metadata, and formatting rules tailored to Japanese regulatory needs. The accompanying XSL transformation files (`preview.xsl`, `preview_ja.xsl`, `preview_en.xsl`) and CSS (`preview.css`) define the presentation of these documents. This IG leverages these existing structures to map PMDA XML elements to FHIR resources, such as `Bundle` and `Composition`, ensuring continuity in content organization, regulatory compliance, and visual presentation.

The ePI Japan IG aligns with the FHIR ePI standard, enabling interoperability within Japanese healthcare systems while accommodating Japan-specific requirements, such as multilingual support (Japanese and English), section-specific styling (e.g., contraindications, warnings), and metadata for revision tracking. By adopting FHIR, this IG aims to enhance accessibility, machine-readability, and integration of Japanese labeling data into Japanese healthcare systems.

### Scope

The scope of this Implementation Guide includes:

- **Mapping PMDA XML to FHIR ePI**: Defining how elements in the PMDA XML schema (e.g., sections like `HDR_IndicationsOrEfficacy`, `HDR_ContraIndications`) are represented using FHIR resources, such as `Bundle` and `Composition`.
- **Preservation of Japanese Labeling Template**: Ensuring that the Japanese labeling template, including section headings (e.g., 効能又は効果, 禁忌), metadata (e.g., revision symbols), and formatting (e.g., red borders for contraindications), is fully supported in the FHIR ePI output.
- **Multilingual Support**: Accommodating both Japanese and English labeling content, as specified in `preview_ja.xsl` and `preview_en.xsl`, to meet regulatory and user needs.
- **Regulatory Compliance**: Adhering to PMDA's metadata rules, such as those for tracking revisions (`revisionPrev-editor`, `revisionThis-editor`), and ensuring that regulatory information is accurately represented in FHIR.
- **Interoperability**: Enabling integration with Japanese healthcare systems through FHIR, supporting use cases such as pharmacovigilance and clinical decision support within Japan.
- **Tooling and Validation**: Providing guidance on tools, profiles, and validation processes to convert PMDA XML to FHIR ePI and validate the resulting FHIR resources against this IG.

This IG does not cover changes to the PMDA's regulatory processes, approval workflows, or the content of labeling information, which remain under the jurisdiction of the PMDA.

### Objectives

The objectives of the ePI Japan Implementation Guide are:

1. **Facilitate Transition to FHIR ePI**: Provide clear mappings and examples to convert PMDA XML-based package inserts to FHIR ePI, minimizing disruption to existing workflows.
2. **Maintain Japan-Specific Requirements**: Ensure that the Japanese labeling template, including section headings, styling (e.g., as defined in `preview.css`), and metadata, is preserved in the FHIR representation.
3. **Enhance Interoperability**: Enable Japanese labeling data to be shared and integrated within Japanese healthcare systems through FHIR, supporting use cases such as pharmacovigilance and clinical decision support.
4. **Support Multilingual Accessibility**: Ensure that both Japanese and English versions of package inserts are accurately represented and styled in FHIR ePI outputs, as per `preview_ja.xsl` and `preview_en.xsl`.
5. **Promote Machine-Readability**: Structure labeling data in FHIR resources to enable automated processing, searchability, and analysis, improving usability for healthcare professionals and systems in Japan.
6. **Provide Implementation Guidance**: Offer detailed profiles, examples, and validation tools to assist implementers in adopting the FHIR ePI standard for Japanese labeling.

### Additional Notes

- **Alignment with PMDA Standards**: The IG respects the PMDA's XML structure, which includes specialized tables (e.g., `ContraIndication_table`, `CompositionAndProperty_table`) and styling (e.g., red borders for warnings, specific font families). These are mapped to FHIR resources with appropriate extensions to maintain fidelity.
- **Revision Tracking**: The PMDA XML includes revision symbols (e.g., `revisionPrevThis-editor`) for tracking changes. This IG will define how such metadata is captured in FHIR, potentially using extensions or annotations.
- **Styling and Presentation**: The `preview.css` file specifies detailed styling, such as margins, fonts, and borders. This IG will provide guidance on how to preserve these in FHIR ePI, possibly through CSS or narrative text in `Composition` resources.
- **Future Extensibility**: While focused on the current PMDA XML schema, the IG is designed to be extensible to accommodate future updates to PMDA requirements or FHIR ePI standards.

For further details, refer to the HL7 Vulcan's [Global ePI Specification](https://build.fhir.org/ig/HL7/emedicinal-product-info/index.html) and the [PMDA Labeling Guidelines](https://www.pmda.go.jp/). Contributions and feedback are welcome via the [GitHub repository](https://github.com/cander2/epi-jp).


----------------------------------------
# 電子製品情報（ePI）日本実装ガイド

## 概要

電子製品情報（ePI）日本実装ガイド（IG）は、医薬品医療機器総合機構（PMDA）のカスタムXMLベースの添付文書フォーマットから、FHIR（Fast Healthcare Interoperability Resources）ePI標準への移行を支援する標準化されたフレームワークを提供します。本IGは、日本の医薬品添付文書（添付文書）の構造、内容、および規制要件がFHIRベースのePIフォーマットで完全に保持されるよう設計されています。

PMDAの現在のXMLスキーマ（`package_insert-XML.xsd`および`package_insert-XML-Transitional.xsd`で定義）では、特定のセクション見出し、メタデータ、および日本固有の規制ニーズに合わせた書式設定ルールを持つ詳細な添付文書情報がサポートされています。付随するXSL変換ファイル（`preview.xsl`、`preview_ja.xsl`、`preview_en.xsl`）およびCSS（`preview.css`）は、これらの文書の表示形式を定義します。本IGは、これらの既存の構造を活用し、PMDA XML要素をFHIRリソース（`Bundle`および`Composition`など）にマッピングすることで、内容の構成、規制順守、および視覚的表現の継続性を確保します。

ePI日本IGは、FHIR ePI標準に準拠し、日本の医療システム内での相互運用性を可能にします。また、日本固有の要件（日本語と英語の多言語サポート、禁忌や警告などのセクション固有のスタイル、改訂追跡のためのメタデータなど）にも対応します。FHIRを採用することで、本IGは日本の医療システムにおける添付文書データのアクセシビリティ、機械可読性、および統合性を向上させることを目指しています。

## 適用範囲

本実装ガイドの適用範囲は以下の通りです：

- **PMDA XMLからFHIR ePIへのマッピング**：PMDA XMLスキーマの要素（例：`HDR_IndicationsOrEfficacy`、`HDR_ContraIndications`などのセクション）を、FHIRリソース（`Bundle`および`Composition`など）を使用して表現する方法を定義します。
- **日本添付文書テンプレートの保持**：日本の添付文書テンプレート（例：効能又は効果、禁忌などのセクション見出し）、メタデータ（例：改訂記号）、および書式設定（例：禁忌の赤枠）をFHIR ePI出力で完全にサポートします。
- **多言語サポート**：規制およびユーザーのニーズを満たすため、`preview_ja.xsl`および`preview_en.xsl`で指定された日本語および英語の添付文書内容に対応します。
- **規制順守**：改訂追跡のためのPMDAのメタデータルール（例：`revisionPrev-editor`、`revisionThis-editor`）を遵守し、規制情報がFHIRで正確に表現されるようにします。
- **相互運用性**：FHIRを通じて日本の医療システムとの統合を可能にし、日本国内でのファーマコビジランスや臨床意思決定支援などのユースケースをサポートします。
- **ツールおよび検証**：PMDA XMLをFHIR ePIに変換し、結果として得られるFHIRリソースを本IGに対して検証するためのツール、プロファイル、および検証プロセスのガイダンスを提供します。

本IGは、PMDAの規制プロセス、承認ワークフロー、または添付文書の内容の変更には適用されません。これらは引き続きPMDAの管轄下にあります。

## 目的

ePI日本実装ガイドの目的は以下の通りです：

1. **FHIR ePIへの移行を促進**：PMDA XMLベースの添付文書をFHIR ePIに変換するための明確なマッピングと例を提供し、既存のワークフローへの影響を最小限に抑えます。
2. **日本固有の要件を維持**：日本の添付文書テンプレート（セクション見出し、スタイル（例：`preview.css`で定義）、メタデータなど）がFHIR表現で保持されることを保証します。
3. **相互運用性の向上**：FHIRを通じて日本の医療システム内での添付文書データの共有と統合を可能にし、ファーマコビジランスや臨床意思決定支援などのユースケースをサポートします。
4. **多言語アクセシビリティのサポート**：日本語および英語の添付文書が、`preview_ja.xsl`および`preview_en.xsl`に従って正確に表現され、スタイル付けされることを保証します。
5. **機械可読性の促進**：FHIRリソースに構造化された添付文書データを構築し、自動処理、検索可能性、および分析を可能にすることで、日本の医療専門家およびシステムの利便性を向上させます。
6. **実装ガイダンスの提供**：日本の添付文書向けにFHIR ePI標準を採用する実装者を支援するための詳細なプロファイル、例、および検証ツールを提供します。

## 補足事項

- **PMDA基準との整合性**：本IGは、PMDAのXML構造（例：`ContraIndication_table`、`CompositionAndProperty_table`などの特殊なテーブル）およびスタイル（例：警告の赤枠、特定のフォントファミリー）を尊重します。これらは適切な拡張を使用してFHIRリソースにマッピングされ、忠実性を維持します。
- **改訂追跡**：PMDA XMLには変更を追跡するための改訂記号（例：`revisionPrevThis-editor`）が含まれます。本IGは、このようなメタデータがFHIRでどのようにキャプチャされるか（例：拡張または注釈を使用）を定義します。
- **スタイルおよび表示**：`preview.css`ファイルは、マージン、フォント、ボーダーなどの詳細なスタイルを指定します。本IGは、これらをFHIR ePIで保持する方法（例：CSSまたは`Composition`リソースのナラティブテキストを介して）に関するガイダンスを提供します。
- **将来の拡張性**：現在のPMDA XMLスキーマに焦点を当てていますが、本IGはPMDAの要件やFHIR ePI標準の将来の更新に対応できるように拡張可能に設計されています。

詳細については、[FHIR ePI仕様](https://www.hl7.org/fhir/)および[PMDA添付文書ガイドライン](https://www.pmda.go.jp/)を参照してください。貢献やフィードバックは[GitHubリポジトリ](https://github.com/cander2/epi-jp)にて歓迎します。