### Overview

The Electronic Product Information (ePI) Japan Implementation Guide (IG) provides a standardized framework to support the transition from the custom XML-based package insert format of the Pharmaceuticals and Medical Devices Agency (PMDA) to the FHIR (Fast Healthcare Interoperability Resources) ePI standard. This IG is designed to ensure that the structure, content, and regulatory requirements of Japanese pharmaceutical package inserts are fully preserved in the FHIR-based ePI format.

PMDA's current XML schema (defined in package_insert-XML.xsd and package_insert-XML-Transitional.xsd) supports detailed package insert information with specific section headings, metadata, and formatting rules tailored to Japan-specific regulatory needs. The accompanying XSL transformation files (preview.xsl, preview_ja.xsl, preview_en.xsl) and CSS (preview.css) define the display format for these documents. This IG leverages these existing structures by mapping PMDA XML elements to FHIR resources (such as Bundle and Composition), ensuring continuity in content organization, regulatory compliance, and visual representation.

The ePI Japan IG complies with the FHIR ePI standard, enabling interoperability within Japan's healthcare system. It also addresses Japan-specific requirements (such as multilingual support for Japanese and English, section-specific styles for contraindications and warnings, and metadata for revision tracking). By adopting FHIR, this IG aims to improve the accessibility, machine-readability, and integration of package insert data in Japan's healthcare system.

### Scope

The scope of this implementation guide is as follows:

- Mapping from PMDA XML to FHIR ePI: Defines methods to represent elements of the PMDA XML schema (e.g., sections like HDR_IndicationsOrEfficacy, HDR_ContraIndications) using FHIR resources (such as Bundle and Composition).
- Preservation of Japanese Package Insert Templates: Fully supports Japanese package insert templates (e.g., section headings like Indications or Effects, Contraindications), metadata (e.g., revision symbols), and formatting (e.g., red borders for contraindications) in FHIR ePI output.
- Multilingual Support: Accommodates Japanese and English package insert content as specified in preview_ja.xsl and preview_en.xsl to meet regulatory and user needs.
- Regulatory Compliance: Adheres to PMDA's metadata rules for revision tracking (e.g., revisionPrev-editor, revisionThis-editor) to ensure regulatory information is accurately represented in FHIR.
- Interoperability: Enables integration with Japan's healthcare system through FHIR, supporting use cases such as pharmacovigilance and clinical decision support within Japan.
- Tools and Validation: Provides guidance on tools, profiles, and validation processes for converting PMDA XML to FHIR ePI and validating the resulting FHIR resources against this IG.

This IG does not apply to PMDA's regulatory processes, approval workflows, or changes to package insert content. These remain under PMDA's jurisdiction.

### Purpose

The purposes of the ePI Japan Implementation Guide are as follows:

1. Facilitate Transition to FHIR ePI: Provides clear mappings and examples for converting PMDA XML-based package inserts to FHIR ePI, minimizing impact on existing workflows.
2. Maintain Japan-Specific Requirements: Ensures that Japanese package insert templates (section headings, styles (e.g., defined in preview.css), metadata, etc.) are preserved in FHIR representations.
3. Improve Interoperability: Enables sharing and integration of package insert data within Japan's healthcare system through FHIR, supporting use cases such as pharmacovigilance and clinical decision support.
4. Support Multilingual Accessibility: Ensures that Japanese and English package inserts are accurately represented and styled according to preview_ja.xsl and preview_en.xsl.
5. Promote Machine-Readability: Builds structured package insert data in FHIR resources to enable automated processing, searchability, and analysis, improving usability for Japanese healthcare professionals and systems.
6. Provide Implementation Guidance: Offers detailed profiles, examples, and validation tools to support implementers adopting the FHIR ePI standard for Japanese package inserts.

### Supplementary Notes

- Alignment with PMDA Standards: This IG respects PMDA's XML structures (e.g., special tables like ContraIndication_table, CompositionAndProperty_table) and styles (e.g., red borders for warnings, specific font families). These are mapped to FHIR resources using appropriate extensions to maintain fidelity.
- Revision Tracking: PMDA XML includes revision symbols for tracking changes (e.g., revisionPrevThis-editor). This IG defines how such metadata is captured in FHIR (e.g., using extensions or annotations).
- Styles and Display: The preview.css file specifies detailed styles such as margins, fonts, and borders. This IG provides guidance on preserving these in FHIR ePI (e.g., via CSS or narrative text in Composition resources).
- Future Extensibility: While focused on the current PMDA XML schema, this IG is designed to be extensible to accommodate future updates to PMDA requirements or the FHIR ePI standard.

For details, please refer to the FHIR ePI specifications and PMDA package insert guidelines. Contributions and feedback are welcome on the GitHub repository.

---
---

### 概要

電子製品情報（ePI）日本実装ガイド（IG）は、医薬品医療機器総合機構（PMDA）のカスタムXMLベースの添付文書フォーマットから、FHIR（Fast Healthcare Interoperability Resources）ePI標準への移行を支援する標準化されたフレームワークを提供します。本IGは、日本の医薬品添付文書（添付文書）の構造、内容、および規制要件がFHIRベースのePIフォーマットで完全に保持されるよう設計されています。

PMDAの現在のXMLスキーマ（package_insert-XML.xsdおよびpackage_insert-XML-Transitional.xsdで定義）では、特定のセクション見出し、メタデータ、および日本固有の規制ニーズに合わせた書式設定ルールを持つ詳細な添付文書情報がサポートされています。付随するXSL変換ファイル（preview.xsl、preview_ja.xsl、preview_en.xsl）およびCSS（preview.css）は、これらの文書の表示形式を定義します。本IGは、これらの既存の構造を活用し、PMDA XML要素をFHIRリソース（BundleおよびCompositionなど）にマッピングすることで、内容の構成、規制順守、および視覚的表現の継続性を確保します。

ePI日本IGは、FHIR ePI標準に準拠し、日本の医療システム内での相互運用性を可能にします。また、日本固有の要件（日本語と英語の多言語サポート、禁忌や警告などのセクション固有のスタイル、改訂追跡のためのメタデータなど）にも対応します。FHIRを採用することで、本IGは日本の医療システムにおける添付文書データのアクセシビリティ、機械可読性、および統合性を向上させることを目指しています。

### 適用範囲

本実装ガイドの適用範囲は以下の通りです：

- PMDA XMLからFHIR ePIへのマッピング：PMDA XMLスキーマの要素（例：HDR_IndicationsOrEfficacy、HDR_ContraIndicationsなどのセクション）を、FHIRリソース（BundleおよびCompositionなど）を使用して表現する方法を定義します。
- 日本添付文書テンプレートの保持：日本の添付文書テンプレート（例：効能又は効果、禁忌などのセクション見出し）、メタデータ（例：改訂記号）、および書式設定（例：禁忌の赤枠）をFHIR ePI出力で完全にサポートします。
- 多言語サポート：規制およびユーザーのニーズを満たすため、preview_ja.xslおよびpreview_en.xslで指定された日本語および英語の添付文書内容に対応します。
- 規制順守：改訂追跡のためのPMDAのメタデータルール（例：revisionPrev-editor、revisionThis-editor）を遵守し、規制情報がFHIRで正確に表現されるようにします。
- 相互運用性：FHIRを通じて日本の医療システムとの統合を可能にし、日本国内でのファーマコビジランスや臨床意思決定支援などのユースケースをサポートします。
- ツールおよび検証：PMDA XMLをFHIR ePIに変換し、結果として得られるFHIRリソースを本IGに対して検証するためのツール、プロファイル、および検証プロセスのガイダンスを提供します。

本IGは、PMDAの規制プロセス、承認ワークフロー、または添付文書の内容の変更には適用されません。これらは引き続きPMDAの管轄下にあります。

### 目的

ePI日本実装ガイドの目的は以下の通りです：

1. FHIR ePIへの移行を促進：PMDA XMLベースの添付文書をFHIR ePIに変換するための明確なマッピングと例を提供し、既存のワークフローへの影響を最小限に抑えます。
2. 日本固有の要件を維持：日本の添付文書テンプレート（セクション見出し、スタイル（例：preview.cssで定義）、メタデータなど）がFHIR表現で保持されることを保証します。
3. 相互運用性の向上：FHIRを通じて日本の医療システム内での添付文書データの共有と統合を可能にし、ファーマコビジランスや臨床意思決定支援などのユースケースをサポートします。
4. 多言語アクセシビリティのサポート：日本語および英語の添付文書が、preview_ja.xslおよびpreview_en.xslに従って正確に表現され、スタイル付けされることを保証します。
5. 機械可読性の促進：FHIRリソースに構造化された添付文書データを構築し、自動処理、検索可能性、および分析を可能にすることで、日本の医療専門家およびシステムの利便性を向上させます。
6. 実装ガイダンスの提供：日本の添付文書向けにFHIR ePI標準を採用する実装者を支援するための詳細なプロファイル、例、および検証ツールを提供します。

### 補足事項

- PMDA基準との整合性：本IGは、PMDAのXML構造（例：ContraIndication_table、CompositionAndProperty_tableなどの特殊なテーブル）およびスタイル（例：警告の赤枠、特定のフォントファミリー）を尊重します。これらは適切な拡張を使用してFHIRリソースにマッピングされ、忠実性を維持します。
- 改訂追跡：PMDA XMLには変更を追跡するための改訂記号（例：revisionPrevThis-editor）が含まれます。本IGは、このようなメタデータがFHIRでどのようにキャプチャされるか（例：拡張または注釈を使用）を定義します。
- スタイルおよび表示：preview.cssファイルは、マージン、フォント、ボーダーなどの詳細なスタイルを指定します。本IGは、これらをFHIR ePIで保持する方法（例：CSSまたはCompositionリソースのナラティブテキストを介して）に関するガイダンスを提供します。
- 将来の拡張性：現在のPMDA XMLスキーマに焦点を当てていますが、本IGはPMDAの要件やFHIR ePI標準の将来の更新に対応できるように拡張可能に設計されています。

詳細については、FHIR ePI仕様およびPMDA添付文書ガイドラインを参照してください。貢献やフィードバックはGitHubリポジトリにて歓迎します。