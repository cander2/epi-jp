
Japan began digitizing package insert information for prescription drugs in 1998, targeting healthcare professionals and patients via the internet (Project lead: Takao Orii, MHLW research group). Initially built using SGML, the format was later changed to XML. In November 2018, administrative notices were issued regarding the revision of package insert documentation guidelines and the transition to XML format.

Following amendments to the Pharmaceutical and Medical Device Act, electronic package inserts (ePI) became mandatory from August 1, 2021. Paper inserts were discontinued, and healthcare professionals now access the latest inserts and patient guides via the PMDA website or by scanning GS1 barcodes using the “ePI Navi” smartphone app.

Although Japan was a pioneer in implementing ePI, the format remains a Japan-specific XML standard, which differs from FHIR—the format adopted for electronic health records. This limits its utility in broader digital health applications.

### Expected Benefits of Introducing FHIR for Drug Information in Japan
Adopting FHIR, an international standard, for e-labeling enables integration with widely used web technologies, making it easier to share information via tablets and smartphones. It enhances interoperability and facilitates seamless integration with other systems.

In the future, linking e-labeling with other healthcare and welfare data will allow personalized information delivery tailored to individual patients, improving health management, medication adherence, and treatment understanding. Standardized e-labeling can also support automation in dispensing, contributing to drug and patient safety.

By aligning with EMA and FDA in adopting international standards, Japan can promote regulatory harmonization across Asia, making its ePI more usable as a reference. During global pandemics, international information systems can be leveraged. FHIR-based e-labeling also supports diversity in multilingual environments and helps resolve supply issues by enabling easier drug searches.

Furthermore, transitioning pharmaceutical workflows from PDF to FHIR could lead to new digital processes, enabling content reuse across domains such as labeling, quality, and clinical data, thereby reducing operational burden.

### Conclusion
Despite being a global leader in ePI implementation, Japan’s format remains a proprietary XML. In contrast, the EMA has adopted HL7 FHIR for e-labeling, starting trials in July 2023 and phased implementation from 2024. The FDA has published a draft IG for transitioning from XML to FHIR. HL7 International released a trial-use version of the FHIR e-labeling IG in July 2023 (version 1.0.0 as of October 31, 2023).

While FHIR adoption for electronic health records is confirmed in Japan, as of 2025, there is no confirmed transition of e-labeling to FHIR. Without international harmonization, e-labeling may remain limited in scope. Therefore, to ensure interoperability of digitized drug information and improve accessibility and understanding for healthcare professionals and patients, Japan must develop an HL7 FHIR Implementation Guide for drug package inserts. This will also enhance cost-efficiency, scalability, and international collaboration across the pharmaceutical industry, regulators, and healthcare systems.

---

日本では医療用医薬品添付文書情報（以下、添文情報）のインターネットを利用した電子化（医薬品情報提供システム）を医療従事者、患者を対象とし、1998年（本研究代表者：折井孝男（厚労科研：作業部会長））より開始した。このシステムは現在もPMDAを中心に稼働している。この添文情報の電子化はSGML書式によって構築したが、現在ではXML書式に変更された。現在の添付文書の電子書式の変更（SGMLからXML）においては、平成30年11月22日付行政通知として「医療用医薬品の添付文書等に係る記載要領改訂に伴う添付文書情報の電子化書式の変更について」及び「医療用医薬品の添付文書等に係る記載要領改訂に伴う添付文書情報の電子化書式（XML）の運用について」が発出された。その後、薬機法の改正により、2021年8月1日から医療用医薬品添付文書の電子化 (電子添文) が義務付けられ、従来、製品に添付（同梱）された添付文書（紙）が廃止され、医療従事者はPMDAウェブサイト) で公開されるスキームに移行し、スマートフォンのアプリ「添文ナビ」でGS1バーコードを読み取り、PMDAウェブサイトに掲載されている最新の添付文書、患者向医薬品ガイド等を閲覧すること可能となった。日本は世界に先駆けて添付文書の電子化が実装されたが、そのフォーマットは日本独自規格のXMLであり、電子カルテに導入が決定された規格であるFHIRとは異なるため、デジタルへルス分野への活用においては限定的であることが懸念される。

### 日本において医薬品情報にFHIRを導入することで期待される効果 
e-labelingにおいて国際標準規格であるFHIRを導入することにより、普及しているウェブ技術を活用し、タブレットやスマートフォンなどにより共有しやすく、相互運用性が高いe-labelingの形態で他のシステムと容易に連携が可能となる。将来は、電子添文を含めたe-labelingを他の健康医療介護のデータと連携させることにより、医療従事者が服薬指導する際あるいは患者自身がe-labelingを入手する際、個々の患者に合わせてパーソナライズされた情報提供が可能となり、患者自身の健康管理、服薬遵守、治療の理解の向上に繋がる。また、医療現場においては、e-labelingを標準規格で管理し、調剤の自動化に活用できる可能性があり、医薬品、患者の安全性向上に寄与させることができる。

日本が欧州医薬品庁（European Medical Agency: EMA）及び米国FDAと歩調を合わせながら国際標準規格を導入することで、アジア地域に対して規制調和を促進させ、日本の電子添文をアジア地域においてリファレンスとして使用しやすくなる。そして、世界的なパンデミックの際、国際的な情報提供システムの活用が可能となる。国際的・多言語環境での医療従事者及びおよび患者等を含めた多様性に配慮したe-labelingの利活用が期待される。また、国際的な供給問題の際に適切な薬剤を容易に検索可能にすることで、供給問題解決の一助となる可能性がある。

更に、現在、医薬品の薬事関連の業務ワークフローはPDFで行われているが、それらをFHIR規格で構築・交換できれば、新しいデジタル化された業務方法を創出、例えば、添付文書、品質、臨床等、様々な分野において、コンテンツの再利用により業務削減につながる。

### 結論 
日本は添付文書の電子化を世界に先駆けて実施したにも関わらず、電子化の書式は日本独自のXMLである。欧州では欧州医薬品庁EMAがe-labelingを独自のXML形式ではなく、ヘルスケア領域のデータ交換の国際標準規格であるHL7 FHIRに準拠した形式を導入、2023年7月に試行開始、2024年から段階的に実装している。米国ではFDAが現行の添付文書書式をXMLからFHIRに移行するための実装ガイドの草案を公表した。そして、HL7 Internationalは2023年7月にe-labelingのFHIR国際実装ガイド案を公表した (2023/10/31時点の版はTrial-use 1.0.0) 。このような世界の動きの中で、日本では電子カルテへのFHIRの導入は決定されたものの、2025年時点で、e-LabelingのFHIRへの移行は確認されていない。医療データの交換、統合による利活用が進む中、相互運用性について国際調和がとれていなければ、e-labelingであっても限られた範囲での使用となる。そこで、電子化された医薬品情報の相互運用性を確保し、医療従事者、患者等からよりアクセス及び理解しやすい医薬品情報を提供し、さらに医薬品業界、規制当局、医療システムに対してコスト効率、スケーラビリティ、国際協力を更に向上させるために、日本における医薬品添付文書のHL7 FHIR実装ガイドを作成する。
