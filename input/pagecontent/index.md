### Overview
The ePI-JP Implementation Guide (IG) provides a standardized framework to support the transition from the Pharmaceuticals and Medical Devices Agency (PMDA)’s custom XML-based package insert format to the FHIR (Fast Healthcare Interoperability Resources) ePI standard. This IG is designed to ensure that the structure, content, and regulatory requirements of Japanese package inserts are fully preserved in the FHIR-based ePI format.

The current PMDA XML schema (defined by package_insert-XML.xsd and package_insert-XML-Transitional.xsd) supports detailed package insert information with specific section headings, metadata, and formatting rules tailored to Japan’s regulatory needs. Associated XSL transformation files (preview.xsl, preview_ja.xsl, preview_en.xsl) and CSS (preview.css) define the visual presentation of these documents. This IG leverages these existing structures and maps PMDA XML elements to FHIR resources (e.g., Bundle and Composition), ensuring continuity in content structure, regulatory compliance, and visual representation.

The ePI-JP IG conforms to the FHIR ePI standard and enables interoperability within Japan’s healthcare system. It also supports Japan-specific requirements such as multilingual support (Japanese and English), section-specific styles (e.g., contraindications and warnings), and metadata for revision tracking. By adopting FHIR, this IG aims to improve accessibility, machine-readability, and integration of package insert data within Japan’s healthcare ecosystem.

### Scope
Included Documents:
- Electronic package inserts (ePI) for prescription drugs in Japan (Japanese and English)
- Patient Information Leaflets

Exclusions:
- This IG does not apply to the regulatory approval of the documents. Regulatory oversight remains under PMDA.

### Purpose
The purpose of this IG is:
- To maximize the value of electronic package inserts as a source of information when converting PMDA XML-based inserts to FHIR ePI, without compromising their current functionality. 
- Enhancing interoperability
- Improving multilingual accessibility
- Promoting machine-readability

To achieve these goals, the IG provides implementation guidance for minimal-effort conversion.

### Goals
The goals of this IG are:
1. To facilitate the transition from PMDA XML to FHIR ePI by providing clear mappings, examples, profiles, and validation tools.
- To define how PMDA XML schema elements (e.g., HDR_IndicationsOrEfficacy, HDR_ContraIndications) are represented using FHIR resources such as Bundle and Composition.
2. To preserve the structure of Japanese ePI templates, including section headings (e.g., Indications, Contraindications), styles (e.g., defined in preview.css), metadata (e.g., revision marks like * or **), and formatting (e.g., red borders for contraindications).
3. To support multilingual presentation of Japanese and English inserts according to preview_ja.xsl and preview_en.xsl.
4. To enable integration with Japanese healthcare professional and healthcare system through improved interoperability and machine-readability, supporting use cases such as pharmacovigilance and clinical decision support.

### Additional Notes
- Alignment with PMDA Standards: This IG respects PMDA’s XML structure (e.g., ContraIndication_table, CompositionAndProperty_table) and styles (e.g., red borders for warnings, specific font families), mapping them to FHIR resources using appropriate extensions.
- Revision Tracking: PMDA XML includes revision metadata (e.g., revisionPrevThis-editor, revisionThis-editor). This IG defines how such metadata is captured in FHIR (e.g., using extensions or annotations).
- Styling and Presentation: The preview.css file specifies detailed styles such as margins, fonts, and borders. This IG provides guidance on preserving these styles in FHIR ePI (e.g., via CSS or narrative text in Composition resources).
- Future Extensibility: While focused on the current PMDA XML schema, this IG is designed to be extensible to accommodate future updates to PMDA requirements and the FHIR ePI standard.

For more details, refer to the FHIR ePI specification and PMDA guidelines. Contributions and feedback are welcome via the GitHub repository.

---

### 概要 
電子製品情報（ePI）日本実装ガイド（IG）は、医薬品医療機器総合機構（PMDA）のカスタムXMLベースの添付文書フォーマットから、FHIR（Fast Healthcare Interoperability Resources）ePI標準への移行を支援する標準化されたフレームワークを提供する。本IGは、日本の医薬品添付文書（添付文書）の構造、内容、および規制要件がFHIRベースのePIフォーマットで完全に保持されるよう設計されている。

PMDAの現在のXMLスキーマ（package_insert-XML.xsdおよびpackage_insert-XML-Transitional.xsdで定義）では、特定のセクション見出し、メタデータ、および日本固有の規制ニーズに合わせた書式設定ルールを持つ詳細な添付文書情報がサポートされている。付随するXSL変換ファイル（preview.xsl、preview_ja.xsl、preview_en.xsl）およびCSS（preview.css）は、これらの文書の表示形式を定義する。本IGは、これらの既存の構造を活用し、PMDA XML要素をFHIRリソース（BundleおよびCompositionなど）にマッピングすることで、内容の構成、規制順守、および視覚的表現の継続性を確保する。

ePI日本IGは、FHIR ePI標準に準拠し、日本の医療システム内での相互運用性が可能になる。また、日本固有の要件（日本語と英語の多言語サポート、禁忌や警告などのセクション固有のスタイル、改訂追跡のためのメタデータなど）にも対応する。FHIRを採用することで、本IGは日本の医療システムにおける添付文書データのアクセシビリティ、機械可読性、および統合性を向上させることを目指している。

### 適用範囲
本実装ガイドの適用範囲は以下の通り：
- 対象文書：日本の医療用医薬品の電子化された添付文書（略称：電子添文）（日本語及び英語）、患者向医薬品ガイド

適用外：
- 本IGは、対象文書の規制には適用されない。これらは引き続きPMDAの管轄下にある。

### 目的(Purpose)
本実装ガイドの目的は以下の通り：

PMDA XMLベースの添付文書をFHIR ePIに変換するにあたり、現在の電子添文の果たす機能を一切損なうことなく、以下のような観点で、電子添文の情報源としての価値を最大化する。
- 相互運用性の向上
- 多言語アクセシビリティの向上
- 機械可読性の促進

これらを達成するために、最小限の労力で変換するための実装ガイダンスを提供する。

### 目標（Goals）
本実装ガイドの目標は以下の通り：
1.	PMDA XMLベースの添付文書をFHIR ePIに変換するための明確なマッピングと例、プロファイル、検証ツール等を提供することで、FHIR ePIへの移行を促進する。
例えば、PMDA XMLからFHIR ePIへのマッピングはPMDA XMLスキーマの要素（例：HDR_IndicationsOrEfficacy、HDR_ContraIndicationsなどのセクション）を、FHIRリソース（BundleおよびCompositionなど）を使用して表現する方法を定義する。

2.	日本の電子添文テンプレート（セクション見出し（例：効能又は効果、禁忌など）、スタイル（例：preview.cssで定義）、メタデータ（例：改訂記号「*」又は「**」）、および書式設定（例：禁忌の赤枠）など）をFHIR ePIで保持される枠組みを提供する。

3.	多言語サポート：日本語および英語の添付文書が、preview_ja.xslおよびpreview_en.xslに従って正確に表現され、スタイル付けされる枠組みを提供する。規制およびユーザーのニーズを満たすため、preview_ja.xslおよびpreview_en.xslで指定された日本語および英語の添付文書内容に対応する。

4.	相互運用性の向上及び機械可読性の促進により、FHIRを通じて日本の医療システムとの統合を可能にし、日本国内でのファーマコビジランスや臨床意思決定支援などのユースケースをサポートする。それにより、日本の医療専門家およびシステムの利便性を向上させる。

### 補足事項
- PMDA基準との整合性：本IGは、PMDAのXML構造（例：ContraIndication_table、CompositionAndProperty_tableなどの特殊なテーブル）およびスタイル（例：警告の赤枠、特定のフォントファミリー）を尊重する。これらは適切な拡張を使用してFHIRリソースにマッピングされ、忠実性を維持する。
- 改訂追跡：PMDA XMLには変更を追跡するための改訂記号（例：revisionPrevThis-editor又はrevisionThis-editor）が含まれる。本IGは、このようなメタデータがFHIRでどのようにキャプチャされるか（例：拡張又は注釈を使用）を定義する。
- スタイルおよび表示：preview.cssファイルは、マージン、フォント、ボーダーなどの詳細なスタイルを指定します。本IGは、これらをFHIR ePIで保持する方法（例：CSS又はCompositionリソースのナラティブテキストを介して）に関するガイダンスを提供する。
- 将来の拡張性：現在のPMDA XMLスキーマに焦点を当てていますが、本IGはPMDAの要件やFHIR ePI標準の将来の更新に対応できるように拡張可能に設計される。

詳細については、FHIR ePI仕様およびPMDA添付文書ガイドラインを参照してください。貢献やフィードバックはGitHubリポジトリにて歓迎します。


