# Secure AI SaaS for Partners ワークショップ（全6回構成）

> 本リポジトリは **SI / SDC / ISV パートナー向け**の「AI SaaS セキュリティ基礎～実践」学習資産です。  
> エンドユーザー最終利用者向け（運用現場教育等）ではなく、**自社ソリューションに安全性・信頼性を組み込む担当者**（Dev / AppSec / Arch / SRE / プロダクト企画）が対象です。  
> 「SDC セキュリティシリーズ：AI時代のサイバーディフェンス」と整合し、**CAF（Cloud Adoption Framework）× WAF（Well-Architected Framework）× Zero Trust × DevSecOps × Responsible AI** を “小さく始め再利用できる” 形で体験・内製化することを目的としています。

公式シリーズページ:  
[ISV/SDC セキュリティシリーズ：AI時代のサイバーディフェンス](https://www.microsoft.com/ja-jp/securityforsdcseries/)

---

## 🎯 全体ゴール

| 観点 | ゴール |
|------|--------|
| 再現性 | 各回で得た成果物（チェックリスト / 設計票 / パイプライン / 監視クエリ）をそのまま自社 PoC / MVP に移植可能 |
| 段階学習 | L100（用語・概念把握）→ L150-200（設計観点）→ L200+（最小実装と運用） |
| コスト配慮 | 単一テナント / 単一サブスクリプション / 最小 SKU・無料/試用枠を優先 |
| 安全性 | 多テナント境界 / データ分類 / 秘匿・鍵管理 / 開発供給網 / 実行時ガードレール |
| 運用性 | ログ・評価メタデータ → 検知 → 初動 → 改善ループを “過剰実装せず” 体験 |
| 組織浸透 | 参加後 “自社で語れる・意思決定を支援できる” 成果を持ち帰る |

---

## 🧭 学習パス（全6回 / 推奨順）

1. 基礎（用語・俯瞰）
2. 設計（フレームワーク適用）
3. 境界（Zero Trust / Identity）
4. 実装パイプライン（DevSecOps）
5. 活用と生成AI利用安全（Copilot）
6. 監視・検知（運用ループの起動）

各回は「座学（Why）→ ガイド付きハンズオン（How）→ 共有（So What）→ 成果物（Asset）」で構成。

---

## 📅 各回詳細

### ① 安全な AI SaaS の基礎（2時間）
**目的**: “AI SaaS を守る” ための構成要素と主要脅威を俯瞰し、Azure の基本防御レイヤを理解。  
**学習アウトカム**:
- 主要リスク（多テナント・秘匿情報・モデル濫用）を説明できる
- Landing Zone を最小構成で語れる
- Portal で基礎的ガードレール（アクセス制御 / NSG / Defender 推奨）に触れる

**アジェンダ**  
1. オープニング / ゴール共有 (10)  
2. AI SaaS の仕組みと主要脅威 (20)  
3. マルチテナント環境の課題 (15)  
4. Azure セキュリティ機能サマリ (15)  
5. ハンズオン (40)  
6. まとめ / Q&A (20)

**ハンズオン**  
- リソース グループ作成 & RBAC 付与  
- NSG で最小イン/アウト設定  
- Defender for Cloud（Security Center）推奨事項 1件改善  
- “どこが脆弱化しやすいか” ディスカッション

**成果物**  
- “基礎用語＆脅威メモ”  
- “最小 Azure リソース配置サンプル”  
- “初学者向けセキュリティ確認リスト v1”

---

### ② セキュリティ設計入門（2時間）
**目的**: CAF / WAF / Zero Trust の観点で “設計レビュー” を行う型を習得。  
**アウトカム**:
- 設計時の質問テンプレを自力で作れる
- 脅威→対策のマッピングをチームで議論できる

**アジェンダ**  
1. オープニング (10)  
2. セキュリティ設計フレームワーク (20)  
3. Zero Trust と DevSecOps の接点 (15)  
4. 製品設計時のチェックポイント (15)  
5. グループ演習 (40)  
6. まとめ / Q&A (20)

**ハンズオン**  
- サンプルアーキ図を脅威分解  
- “脅威 / 対策 / 設計注意” 付箋出し → 集約  
- “自社ならどう設計始めるか” ミニ発表  
- 最終: “設計時セキュリティ質問リスト v1” 作成

**成果物**  
- 設計レビュー質問 30項目（初期ドラフト）  
- 脅威モデル表（リスク分類列付き）

---

### ③ ゼロトラスト入門 for ISV（2時間）
**目的**: ID / アクセス制御の原則を体験し、運用に耐える最小ポリシー設計を理解。  
**アウトカム**:
- Conditional Access / MFA の適用例を説明できる
- “顧客データ境界” の基本モデルを言語化できる

**アジェンダ**  
1. オープニング (10)  
2. Zero Trust 基本概念 (20)  
3. Entra ID 基本設定 (15)  
4. ISV にとっての重要性 (15)  
5. ハンズオン (40)  
6. まとめ / Q&A (20)

**ハンズオン**  
- ユーザー追加 & グループ分離（管理 / 開発 / 監視）  
- 条件付きアクセス：MFA + リスクベース基本テンプレ  
- MFA 有効化テスト  
- “導入ステップ 30/60/90 日案” ブレスト

**成果物**  
- Zero Trust 適用ミニロードマップ  
- 最小 CA ポリシー定義書（YAML / 表形式）  
- ID ガバナンス初期チェックリスト

---

### ④ DevSecOps 入門（2時間）
**目的**: 供給網（Supply Chain）リスク低減と自動ゲートの最小構成を体感。  
**アウトカム**:
- CI/CD における SAST / 依存性 / Secret / IaC スキャンの位置付けを説明
- “失敗を価値化する” パイプライン観点（改善ループ）を語れる

**アジェンダ**  
1. オープニング (10)  
2. DevSecOps とは (20)  
3. CI/CD セキュリティ基本 (15)  
4. Azure DevOps でできること (15)  
5. ハンズオン (40)  
6. まとめ / Q&A (20)

**ハンズオン**  
- サンプルリポジトリ Fork  
- YAML にスキャン（例: CodeQL / Trivy / OWASP ZAP / Secret Scan）追加  
- ビルド失敗条件と通知（Teams / Email）  
- “優先度付けルール” と “初期 SLA” のドラフト

**成果物**  
- セキュリティゲート付き YAML テンプレ  
- 脆弱性トリアージ基準表（Critical/High/Medium/Low）  
- 初期パイプライン運用 SOP

---

### ⑤ Copilot 体験とセキュリティ（2時間）
**目的**: AI アシスト活用時のデータ/プロンプト安全とガバナンス初期設計。  
**アウトカム**:
- “危険なプロンプト例” を判断できる
- 利用ログ / 監査の意義と運用フローを説明できる

**アジェンダ**  
1. オープニング (10)  
2. Copilot 概要 / 価値例 (20)  
3. ユーザーデータ保護の基礎 (15)  
4. AI 利用時の注意点 (15)  
5. ハンズオン (40)  
6. まとめ / Q&A (20)

**ハンズオン**  
- Copilot で要約 / コード生成 / ドキュメント整形  
- “リダクションすべき情報” ラベル付け演習  
- 危険プロンプト（情報漏えい / 誤誘導）評価  
- “社内利用ガイド” スケルトン作成

**成果物**  
- プロンプト安全ガイド（Do / Don’t 形式）  
- 監査ログ確認手順メモ  
- Copilot 利用ポリシー初期ドラフト

---

### ⑥ AI アプリの脅威検出・監視基礎（2時間）
**目的**: アプリ / アイデンティティ / 生成 AI 利用ログを用いた “見る→判断→初動” の最小体験。  
**アウトカム**:
- Defender / ログ活用の優先度を説明
- 初期 MTTR 改善サイクルの設計骨子を語れる

**アジェンダ**  
1. オープニング (10)  
2. AI アプリ脅威の類型 (20)  
3. Microsoft Defender 概要 (15)  
4. 監視 / 防御 基本 (15)  
5. ハンズオン (40)  
6. まとめ / Q&A (20)

**ハンズオン**  
- Defender for Cloud アラート確認  
- インシデント対応シナリオ（役割分担：分析 / 判断 / 報告）  
- 簡易レポート（対象 / 影響 / 対応 / 学び）作成  
- 監視運用ガイド “初期 10項目” 作成

**成果物**  
- KQL 例（リスクサインイン / 境界越えアクセス / プロンプト異常）  
- インシデント初動 Runbook（T+0～T+60分）  
- 監視運用ミニポリシー

---

## 📦 成果物・資産（回横断）

| 種別 | 例 |
|------|----|
| チェックリスト | 設計質問 / Zero Trust CA / パイプライン導入 / Copilot 利用 / 監視運用 |
| テンプレ | 脅威モデル表 / YAML パイプライン / CA ポリシー / インシデントレポート / プロンプト安全ガイド |
| クエリ | Defender / Log Analytics / 評価メタデータ 解析用 KQL |
| ドキュメント | 最小 LZ Lite 指針 / データ分類メモ / 改善ループ計画 |
| ガイド | “30/60/90 日” 強化ロードマップ / トリアージ基準 / SLA 草案 |

---

## 📁 推奨フォルダ構成（本リポジトリ）

```
/workshops
├── 01_foundation/                # 回①：基礎（用語・脅威・最小リソース）
│   ├── agenda.md
│   ├── hands-on-guide.md
│   └── checklist_basic-security.md
├── 02_design/                    # 回②：設計フレームワーク
│   ├── threat-model-template.md
│   ├── design-review-questions.md
│   └── architecture-sample.png
├── 03_zero-trust/                # 回③：ID/アクセス制御
│   ├── ca-policy-min.yaml
│   ├── zero-trust-roadmap.md
│   └── id-governance-checklist.md
├── 04_devsecops/                 # 回④：CI/CD & Supply Chain
│   ├── pipeline-secure-template.yml
│   ├── triage-criteria.md
│   └── devsecops-sop.md
├── 05_copilot/                   # 回⑤：生成AI活用安全
│   ├── prompt-safety-guide.md
│   ├── copilot-usage-policy-draft.md
│   └── audit-log-howto.md
├── 06_monitoring/                # 回⑥：監視・検知
│   ├── kql-samples/
│   │   ├── prompt-anomaly.kql
│   │   ├── cross-tenant-access.kql
│   │   └── risk-signin.kql
│   ├── incident-runbook.md
│   └── monitoring-policy.md
└── common
    ├── 00_glossary.md
    ├── 90_lz-lite-setup.md       # 最小ポリシー / 命名 / タグ / 予算警告
    ├── 91_sample-data/           # 疑似ログ / サンプル分類
    └── 99_refs.md                # CAF / WAF / Zero Trust / DevSecOps / Responsible AI 参照
```

> 既存（旧 A-secure-app / B-mini-soc / C-agent-marketplace）構造から段階学習型へ再整理。必要に応じて `C-agent-marketplace` の資産は今後「拡張編」として別ブランチへ移動検討。

---

## ✅ 受講前提 & 推奨準備

| 項目 | 推奨内容 |
|------|----------|
| Azure アカウント | 検証用サブスクリプション 1つ（Pay-As-You-Go / Visual Studio 等） |
| 権限 | Owner 1名 + Contributor / Security Reader 分離（演習用） |
| ID | Entra ID（テストユーザー 2～3名） |
| 端末要件 | ブラウザ最新版 / VS Code（DevSecOps回で使用可） |
| 事前資料 | 用語集(00_glossary) / LZ Lite セットアップ手順 |

---

## 📊 KPI（例）

| フェーズ | KPI 例 | 測定タイミング |
|----------|--------|---------------|
| 設計 | 設計質問リスト活用率（レビュー会議記録数） | 回②終了後～ |
| ゲート | パイプライン失敗→修復平均時間 | 回④後 2週間 |
| 利用安全 | 危険プロンプト検出率 / 誤用報告件数 | 回⑤後 1ヶ月 |
| 監視 | インシデント初動手順 準拠率 | 回⑥後演習 |
| 継続改善 | “改善ループ” チケットクローズ率 | 四半期 |

---

## 🔁 改善ループ設計（Cross-Cutting）

| ステップ | 具体例 | 生成物 |
|----------|--------|--------|
| 観測 | ログ / 評価メタ（プロンプト / 応答分類） | kql-samples |
| 分析 | 異常アクセス / モデル逸脱 | 分析メモ |
| 判断 | トリアージ基準 / 影響評価 | triage-criteria |
| 対応 | パイプライン修正 / CA 強化 / ポリシー改訂 | 変更PR |
| 学習 | レトロスペクティブ 30日サイクル | meeting-notes |

---

## 🔐 原則（Policy Snippets）

```text
[Least Privilege] 役割は “作成 / 運用 / 監査” を分離
[Data Boundary] 機微データはタグ + Key Vault 管理キー + 最小ログ保持
[Shift Left] 脆弱性検知を “検出→修復時間” 指標化し週次レビュー
[Observable AI] プロンプト/応答の評価メタを匿名化収集し逸脱検知
[Cost Awareness] 30日保持→アーカイブ→削除ポリシーを宣言し例外承認必須
```

---

## 🧪 ライセンス / 利用条件

- 本資材は学習・社内展開を目的としたテンプレートです。実運用投入時は **法務 / セキュリティ審査 / 契約条件** を再確認してください。
- サンプルコード・クエリは “参考実装” であり完全性・完全な無害性を保証しません。

---

## 🤝 フィードバック

改善 Issue / PR 歓迎:  
- 追加希望モジュール  
- 演習ステップの不明点  
- 新たな Azure / Defender 機能の反映提案

---

## 🗺 今後の拡張（ロードマップ例）

| 検討 | 内容（案） |
|------|-----------|
| 拡張編 | Marketplace / エージェント公開（旧 C-agent-marketplace 資産再編） |
| 自動化 | IaC（Bicep / Terraform）化オプション |
| 評価 | LLM 出力安全性自動メトリクス収集パッケージ |
| ガバナンス | Purview / DLP / 情報保護 ライト版演習 |
| RAI | Responsible AI チェックリスト連携（スコアリング） |

---

## 📚 参考リンク（抜粋）

- CAF / ALZ: Azure Cloud Adoption Framework
- WAF: Azure Well-Architected Framework
- Zero Trust: Microsoft Zero Trust Guidance
- DevSecOps: GitHub Advanced Security / Azure DevOps
- Responsible AI: Microsoft Responsible AI Standard
- Defender for Cloud / Entra ID / Azure Monitor Docs

（詳細は `common/99_refs.md` を参照）

---

> 次のアクション: `workshops/01_foundation/hands-on-guide.md` から開始し、成果物を自社向けにカスタマイズして Issue 化 / パイプライン化してください。

---
© 2025 Secure AI SaaS for Partners（Draft / Internal Enablement Template）
