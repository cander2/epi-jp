### Use Cases for the ePI Japan Implementation Guide

This page outlines Japan-specific use cases for the Electronic Product Information (ePI) Japan Implementation Guide (IG), demonstrating how the transition from the Pharmaceuticals and Medical Devices Agency (PMDA)'s XML-based package insert format to the FHIR ePI standard benefits stakeholders in Japan's healthcare system. These use cases leverage the structured machine-readability of FHIR ePI while preserving Japan-specific requirements (e.g., section headings (Indications or Effects, Contraindications, etc.), styles (red borders for warnings, etc.), metadata (revision symbols, etc.)). These are defined in PMDA's XML schema and style files (package_insert-XML.xsd, preview.css, preview_ja.xsl, preview_en.xsl).

### Pharmacovigilance Reporting and Monitoring

Description: PMDA requires robust pharmacovigilance mandating monitoring of adverse drug reactions (ADRs) nationwide in Japan. FHIR ePI integrates structured package insert data such as adverse event information (e.g., HDR_OtherAdverseEvents) with hospital or pharmacy systems, enabling automation of ADR reporting and improvement of post-marketing surveillance.

Scenario:

- A hospital in Hokkaido uses an EHR system that extracts contraindication data (HDR_ContraIndications) from the FHIR ePI's Composition resource.
- The system detects potential ADRs during prescription checks and generates reports to PMDA's pharmacovigilance database using structured data.
- The machine-readable format of FHIR ePI ensures accurate mapping of adverse event tables, styled according to preview.css (e.g., left-aligned headers for HDR_OtherAdverseEvents).

Benefits:

- Streamlines ADR reporting to PMDA, reducing manual work.
- Improves patient safety through real-time risk identification.
- Preserves PMDA's table structures and metadata for regulatory compliance.

### Clinical Decision Support in Japanese Hospitals

Description: Japanese healthcare providers rely on accurate package insert information for safe prescribing. The structured data of FHIR ePI (e.g., Bundle and Composition resources) integrates with EHR systems to provide real-time clinical decision support on drug interactions and precautions (e.g., HDR_Interactions, HDR_PrecautionsForCombinations).

Scenario:

- A physician in a Tokyo hospital prescribes medication to a patient with known conditions.
- The EHR system queries FHIR ePI resources and retrieves precaution data styled with red borders according to preview.css's .Warnings class.
- Alerts warn the physician of potential drug interactions, preventing inappropriate prescriptions.

Benefits:

- Improves prescription accuracy in Japanese hospitals.
- Reflects PMDA's section-specific styles (e.g., red borders for contraindications) in clinical workflows.
- Enables seamless integration with Japanese EHR systems.

### Regulatory Compliance and Revision Tracking

Description: PMDA requires detailed tracking of package insert revisions to ensure regulatory compliance. FHIR ePI supports structured metadata for documenting changes (e.g., revisionPrevThis-editor, revisionThis-editor), allowing pharmaceutical companies and auditors to efficiently verify updates.

Scenario:

- A Japanese pharmaceutical company updates the package insert to reflect new safety data.
- The updated FHIR ePI's Composition includes revision metadata mapped to FHIR extensions that preserve PMDA's revision symbols (according to preview.css).
- PMDA auditors access the FHIR ePI to confirm changes and ensure compliance with regulatory guidelines.

Benefits:

- Simplifies revision tracking and audit processes for PMDA submissions.
- Preserves PMDA's metadata requirements in a machine-readable format.
- Reduces errors in regulatory documents.

### Patient Education and Mobile Access

Description: Japanese patients are increasingly accessing medical information via mobile apps. FHIR ePI's structured data delivers customized package insert content (e.g., HDR_IndicationsOrEfficacy) to patient-facing apps, preserving Japan-specific styles (e.g., red borders for warnings according to preview.css).

Scenario:

- A patient in Kyoto downloads a PMDA-approved mobile app to learn about their medication.
- The app retrieves FHIR ePI resources and displays simplified Japanese dosing instructions with emphasized warnings (e.g., styles from .Warnings class).
- The patient receives clear, compliant information in a user-friendly format.

Benefits:

- Provides accessible and accurate package insert information to patients.
- Preserves PMDA's visual and structural requirements in digital formats.
- Supports digital health initiatives for patient engagement in Japan.

### Structured Product Details for Regulatory and Supply Chain Management

Description: Japan's regulatory and supply chain systems require detailed structured product information such as active ingredients, excipients, and packaging details (e.g., HDR_Composition, HDR_Property). FHIR ePI represents this data in a machine-readable format, facilitating regulatory submissions, inventory management, and quality control.

Scenario:

- A pharmaceutical manufacturer in Osaka submits a new drug application to PMDA including structured ingredient data from the FHIR ePI's Composition resource.
- PMDA reviews the structured data mapped to FHIR (e.g., CompositionAndProperty_table) to ensure compliance with composition and packaging standards.
- Pharmacy chains use the same FHIR ePI data to verify packaging details (e.g., vial sizes, storage conditions) for inventory management, styled according to preview.css (e.g., table formats in .VariousForm).

Benefits:

- Simplifies regulatory submissions by providing PMDA-compliant structured product data.
- Improves supply chain efficiency through machine-readability of ingredient and packaging details.
- Preserves PMDA's formatting and metadata (e.g., table structures, revision symbols) in FHIR ePI.

### Supplementary Notes

- Japan-Specific Context: These use cases address Japan's unique regulatory environment, including PMDA's strict metadata and style rules, healthcare infrastructure (e.g., EHR adoption), and supply chain needs (e.g., structured product data).
- Alignment with FHIR: Each use case leverages FHIR's Bundle and Composition resources to ensure interoperability within Japan's healthcare system, in line with the IG's objectives.
- Integration with PMDA: The use cases reflect PMDA's XML structures (e.g., special tables like ContraIndication_table, CompositionAndProperty_table) and styles (e.g., YuMincho font), ensuring fidelity in the FHIR ePI transition.
- Extensibility: The use cases are designed to accommodate future PMDA requirements, such as updates to product data standards or enhanced revision tracking.

For details on implementing these use cases, please refer to the FHIR ePI specifications and PMDA package insert guidelines. Feedback and contributions are welcome on the GitHub repository.

---
---

### ePI日本実装ガイドのユースケース

本ページでは、電子製品情報（ePI）日本実装ガイド（IG）の日本特有のユースケースを概説し、医薬品医療機器総合機構（PMDA）のXMLベースの添付文書フォーマットからFHIR ePI標準への移行が日本の医療システムの関係者にどのように利益をもたらすかを示します。これらのユースケースは、FHIR ePIの構造化された機械可読性を活用し、日本固有の要件（例：セクション見出し（効能又は効果、禁忌など）、スタイル（警告の赤枠など）、メタデータ（改訂記号など））を保持します。これらはPMDAのXMLスキーマおよびスタイルファイル（package_insert-XML.xsd、preview.css、preview_ja.xsl、preview_en.xsl）に定義されています。

### ファーマコビジランス報告およびモニタリング

説明：PMDAは、日本全国での副作用（ADR）の監視を義務付ける強固なファーマコビジランスを要求します。FHIR ePIは、副作用情報（例：HDR_OtherAdverseEvents）などの構造化された添付文書データを病院や薬局のシステムと統合し、ADR報告の自動化と市販後監視の向上を可能にします。

シナリオ：

•	北海道の病院が、FHIR ePIのCompositionリソースから禁忌データ（HDR_ContraIndications）を抽出するEHRシステムを使用します。

•	システムは処方チェック中に潜在的なADRを検出し、構造化データを使用してPMDAのファーマコビジランスデータベースに報告を生成します。

•	FHIR ePIの機械可読フォーマットは、副作用テーブルの正確なマッピングを保証し、preview.cssに従ってスタイル設定されます（例：HDR_OtherAdverseEventsの左揃えヘッダー）。

利点：

•	PMDAへのADR報告を効率化し、手作業を削減。

•	リアルタイムのリスク特定により患者の安全性を向上。

•	PMDAのテーブル構造とメタデータを規制順守のために保持。

### 日本の病院での臨床意思決定支援

説明：日本の医療提供者は、安全な処方のために正確な添付文書情報に依存します。FHIR ePIの構造化データ（例：BundleおよびCompositionリソース）は、EHRシステムと統合され、薬物相互作用や注意事項（例：HDR_Interactions、HDR_PrecautionsForCombinations）に関するリアルタイムの臨床意思決定支援を提供します。

シナリオ：

•	東京の病院の医師が、既知の疾患を持つ患者に薬を処方します。

•	EHRシステムはFHIR ePIリソースを照会し、preview.cssの.Warningsクラスに従って赤枠でスタイル設定された注意データを取得します。

•	アラートが医師に潜在的な薬物相互作用を警告し、不適切な処方を防ぎます。

利点：

•	日本の病院での処方精度を向上。

•	PMDAのセクション固有のスタイル（例：禁忌の赤枠）を臨床ワークフローに反映。

•	日本のEHRシステムとのシームレスな統合を可能に。

### 規制順守および改訂追跡

説明：PMDAは、規制順守を確保するために添付文書の改訂の詳細な追跡を要求します。FHIR ePIは、変更を文書化するための構造化メタデータ（例：revisionPrevThis-editor、revisionThis-editor）をサポートし、製薬会社や監査者が更新を効率的に検証できるようにします。

シナリオ：

•	日本の製薬会社が新しい安全性データを反映して添付文書を更新します。

•	更新されたFHIR ePIのCompositionには、PMDAの改訂記号（preview.cssに従って）を保持するFHIR拡張にマッピングされた改訂メタデータが含まれます。

•	PMDAの監査者はFHIR ePIにアクセスして変更を確認し、規制ガイドラインへの準拠を確保します。

利点：

•	PMDA提出のための改訂追跡と監査プロセスを簡素化。

•	PMDAのメタデータ要件を機械可読フォーマットで保持。

•	規制文書でのエラーを削減。

### 患者教育およびモバイルアクセス

説明：日本の患者は、医療情報をモバイルアプリでアクセスする傾向が増しています。FHIR ePIの構造化データは、患者向けアプリにカスタマイズされた添付文書内容（例：HDR_IndicationsOrEfficacy）を配信し、日本固有のスタイル（例：preview.cssに従った警告の赤枠）を保持します。

シナリオ：

•	京都の患者が、PMDA承認のモバイルアプリをダウンロードして薬について学びます。

•	アプリはFHIR ePIリソースを取得し、警告が強調表示された（例：.Warningsクラスのスタイル）日本語の簡略化された投与指示を表示します。

•	患者は、ユーザーフレンドリーな形式で明確かつ準拠した情報を受け取ります。

利点：

•	患者にアクセスしやすく正確な添付文書情報を提供。

•	デジタル形式でPMDAの視覚的および構造的要件を保持。

•	日本の患者エンゲージメントのためのデジタルヘルスイニシアチブをサポート。

### 規制およびサプライチェーン管理のための構造化製品詳細

説明：日本の規制およびサプライチェーンシステムは、有効成分、添加物、包装詳細（例：HDR_Composition、HDR_Property）などの詳細な構造化製品情報を要求します。FHIR ePIは、このデータを機械可読フォーマットで表現し、規制提出、インベントリ管理、品質管理を促進します。

シナリオ：

•	大阪の製薬メーカーが、FHIR ePIのCompositionリソースから構造化された成分データを含む新薬申請をPMDAに提出します。

•	PMDAは、FHIRにマッピングされた構造化データ（例：CompositionAndProperty_table）を確認し、組成および包装基準への準拠を確保します。

•	薬局チェーンは、同じFHIR ePIデータを使用して包装詳細（例：バイアルサイズ、保存条件）をインベントリ管理のために検証し、preview.cssに従ってスタイル設定されます（例：.VariousFormのテーブル書式）。

利点：

•	PMDA準拠の構造化製品データを提供することで規制提出を簡素化。

•	成分および包装詳細の機械可読性によりサプライチェーンの効率を向上。

•	FHIR ePIでPMDAの書式およびメタデータ（例：テーブル構造、改訂記号）を保持。

### 補足事項

•	日本特有のコンテキスト：これらのユースケースは、PMDAの厳格なメタデータおよびスタイル規則、日本の医療インフラ（例：EHRの採用）、サプライチェーンのニーズ（例：構造化製品データ）など、日本の独自の規制環境に対応します。

•	FHIRとの整合性：各ユースケースは、IGの目標に沿って、日本の医療システム内での相互運用性を確保するためにFHIRのBundleおよびCompositionリソースを活用します。

•	PMDAとの統合：ユースケースは、PMDAのXML構造（例：ContraIndication_table、CompositionAndProperty_tableなどの特殊なテーブル）およびスタイル（例：游明朝フォント）を反映し、FHIR ePI移行における忠実性を確保します。

•	拡張性：ユースケースは、製品データ基準の更新や改訂追跡の強化など、将来のPMDA要件に対応できるように設計されています。

これらのユースケースの実装に関する詳細は、FHIR ePI仕様およびPMDA添付文書ガイドラインを参照してください。フィードバックおよび貢献はGitHubリポジトリにて歓迎します。