## 🔗 このリポジトリと「SDC セキュリティシリーズ」の関係 / Relation to the SDC Security Series
本リポジトリは **SI/SDC パートナー向け**の AppDev 優先ワークショップ資材です。  
「**SDC セキュリティシリーズ**」の以下テーマと整合し、学んだ原則を実践するためのワークショップを提供します。

> 公式ページ（公開）:  
> **ISV/SDC セキュリティシリーズ：AI時代のサイバーディフェンス**  
> [https://www.microsoft.com/ja-jp/securityforisvseries/](https://www.microsoft.com/ja-jp/securityforsdcseries/)

**Note:** 本リポジトリは **パートナー（SI/SDC）向け**です。**エンドユーザー向けではありません**。

# AI SaaS 向けワークショップ設計書（AppDev優先・低コスト版）

> **前提**：AppDev 優先／準備とコストの障壁を最小化／NDA不要／検証レベルSKU。

---

## 0. 目的と設計ポリシー

- **目的**：AI SaaS における 安全設計→実装→評価→運用 を、CAF（Cloud Adoption Framework）とWAF（Well-Architected Framework）に準拠し再現性のあるワークショップとして利用できるようにする。PoCだけで留まらないようワークフロー統合と継続学習（評価→修正のループ）を成果物に組み込む。
- **対象者**：Dev / AppSec / SRE などを主対象とする。SecOpsについては後半のワークショップで対象とする。
- **障壁最小**：単一テナント＋単一サブスクリプション、無料/低単価機能を優先、ログやデータはサンプルで代替。

---

## 1. 事前準備（最小・低コスト構成）

### 1.1 テナント／サブスクリプション

- **Microsoft Entra ID**：検証用 **単一テナント**（既存の社内検証テナントで可）。
- **Azure サブスクリプション**：**1つ**（Pay-As-You-Go / Visual Studio サブスク等）。
- **リソース グループの最小分割**：
  - `rg-platform`（ネットワーク/監視/Key Vault 等）
  - `rg-app`（アプリ/API/ベクトルDB 等）
  - `rg-secops`（ログ分析/Mini SOC 等）

> **理由**：CAF の **Azure Landing Zone（ALZ）設計領域**（Identity / Network / Security / Governance / Management）を、**小さく始めて後から拡張**できる分割で踏襲。

### 1.2 推奨SKUとサービス（検証レベル優先）

- **アプリ層**：Azure App Service / Azure Functions（小規模プラン）、Azure Storage、**Key Vault**（Secrets/Keys）
- **AI**：Azure OpenAI（**小トラフィック向け**モデル・SKU）
- **ベクトルDB**：Azure AI Search（ベクタ化対応）または軽量OSS（コンテナ）
- **セキュリティ/ガバナンス**：
  - **Microsoft Purview**：**監査/分類/DLP**を最小スコープで有効化（サンプル分類・限定スキャン）
  - **Defender for Cloud**：**無料CSPM**＋必要箇所だけスポットで有料評価（推奨→PR自動修復の体験まで）
  - **Entra 条件付きアクセス（CA）**：MFA/高リスク遮断の基本テンプレのみ
- **運用・可観測性**：Application Insights / Log Analytics（取り込み上限と保持日数は短期設定）
- **Mini SOC（任意）**：Sentinel相当は**最小ログ**で概念体験（Data Tiers/最適化の設計原則は座学＋サンプル）

> **コスト抑制（WAF: Cost）**：**必要データのみ**短期保持＋**安価層**へ退避、**未活用データ**を特定・除外。

---

## 2. ワークショップ構成

> **順番**：  
> ① **安全なAIアプリ開発ハンズオン**  
> ② **AI SOC 実践ラボ**  
> ③ **Agent開発・Marketplace公開ワークショップ**

### 2.1 ワークショップA：安全なAIアプリ開発ハンズオン

**目標（学習後の状態）**
- **要件→安全設計→実装→評価→運用**の**反復プロセス**を、**WAF**の5柱視点で説明・実装・記録できる。
- **CAF-ALZ**の設計領域と**多テナント境界**（論理/鍵/権限/データ）の**最小実装**をテンプレ化できる。

**モジュール（アウトライン）**
1. **AI脅威モデル & データ分類**  
   - OWASP LLM リスクに沿ったユースケース棚卸し  
   - **Purview** で機微タグ（サンプル）と**監査**の最小有効化（出力逸脱の可視化）
2. **多テナント境界の最小パターン**  
   - 顧客別キー/ストレージ分離、RBAC、Managed Identity、Private Link  
   - **CAF-ALZ**の **Identity / Resource 組織 / Network**を“**LZ Lite**”として適用（管理グループ/ポリシーは必須最小）
3. **DevSecOps / 供給網**  
   - GitHub Advanced Security（SAST/依存関係/Secret Scanning）と署名  
   - **Defender for Cloud**の推奨→**PR自動修復**（スポット体験）
4. **実行時ガードレール**  
   - **DLP/ラベル適用**、**実行時ブロック/マスク**（設計観点）  
   - **評価メタデータ**（プロンプト/応答の評価ログ）収集パターン（サンプルコード導入は任意）
5. **WAFレビュー & ゲーティング**  
   - **Security / Operational Excellence / Cost / Reliability / Performance**で設計レビュー  
   - **CI/CDゲート**にレビュー票と自動テスト（lint/scan/負荷ミニ試験）を組み込んで**“学習ループ”**を開始

**成果物**
- **方針ブループリント（Markdown）**：データ分類、鍵管理、境界、評価観点  
- **Promptbook（Markdown）**：安全性・機密性評価チェック込み  
- **CI/CD テンプレ**：SAST/依存/Secret/Infrastructure scan、簡易負荷試験  
- **WAFレビュー票**：5柱×設計判断×トレードオフの記録（根拠リンク付）

**KPI（例）**
- **漏えいインシデント 0**（テストでの逸脱検出 0）  
- **評価Pass率↑**（安全性・品質ゲート）  
- **修復リードタイム↓**（Defender 推奨→PRマージまで）

---

### 2.2 ワークショップB：AI SOC 実践ラボ

**狙い**：Aの成果（ログ/評価メタデータ）を**可観測化**し、**検知→調査→（一部）自動化**を**低コスト**で体験。Aで作った“学習ループ”を**運用**へ接続。

**モジュール（アウトライン）**
1. **可観測化の最小セット**  
   - App Insights / Log Analytics（プロンプト/応答の評価指標、異常HTTP、Key Vaultアクセス）  
   - Entra サインイン/CA のリスクシグナル（高リスクはフラグのみ）
2. **検知ユースケース（軽量）**  
   - **プロンプト注入/脱走の兆候**（異常なツール呼出、過大出力）  
   - **多テナント境界逸脱**（顧客跨ぎアクセス）  
   - **IDリスク**（高リスクサインイン／MFA回避）
3. **調査と半自動化**  
   - チケット化（Webhook/Logic Apps）／**例外申請テンプレ**  
   - **コスト最適化の基本**：短期保持＋**非活用ログの特定**（座学）

**成果物**
- **KQLサンプル**（ハンティング/アラート雛形）  
- **Runbook**（初動SOPと判断基準）  
- **最小Playbook**（通知→CA強化/タグ付→アサイン）

**KPI（例）**
- **有効検知率↑ / 誤検知率↓**  
- **MTTR短縮**（簡易測定でOK）  
- **自動化率↑**（通知/初動）

### 2.3 Agent開発・Marketplace公開ワークショップ

**狙い**
- SDC/SIパートナーがMicrosoft 365 CopilotやAzure上でエージェントを開発し、Marketplace公開までの流れを実践的に体験。
- Marketplace公開に必要なセキュリティ・ガバナンス設計（Certification Policies/Responsible AIチェック/データ保護/認証/監査）を開発フローに組み込むテンプレートを提供。
- Partner Center提出～審査～Listing最適化までの流れを、Microsoft Learn/Partner Centerの最新ガイドラインに沿って体験。

**モジュール（アウトライン）**
1. エージェントの定義と方式選定（Azure/Copilot/MCP連携）
2. Agents Toolkit/SDKによるカスタムエージェント開発（VS Code/CLI/サンドボックス）
3. Copilot Studioによる宣言的エージェント構築（複数チャネル配布）
4. Marketplace公開のためのセキュリティ設計（Certification Policies/Responsible AI/Offer Type選定）
5. Partner Center提出・審査・公開フロー（Listing要件/バリデーション/エビデンスパック作成）
6. 公開後のListing最適化と成長（Marketplace Rewards/営業・マーケ連動

**成果物**
- Agent Scaffolds（Toolkit/Studio両系統のサンプル）
- Security & Compliance Pack（Certification Policies対応チェックリスト、Responsible AIセルフチェック、データ/認証/ログ設計テンプレ）
- Partner Center提出パッケージ（マニフェスト/説明文/画像/キーワード雛形）
- Ops・改善ループ（レビュー/テスト/提出/差し戻し対応フロー）

---

## 3. GenAI Divide を跨ぐための実装ガイド

- **ワークフロー統合**：成果物は**ドキュメントではなく運用資産**（Policy/CIゲート/監査クエリ/Runbook）として提供。**レビューと計測**が続く仕組みに埋め込む。  
- **CAF×WAFの継続適用**：  
  - **CAF-ALZ**で**同一の設計原則**（Identity/Network/Security/Governance/Management）を新規案件にも再適用。  
  - **WAF 5柱**で**定期レビュー**（設計変更・コスト・SLO・回復性・性能）→**トレードオフ票**を更新。

---

## 📁 成果物フォルダ構成
```
/workshop
├── A-secure-app
│   ├── 01_policy-blueprint.md            # データ分類・鍵管理・境界・評価観点の方針
│   ├── 02_promptbook.md                  # 安全性・機密性評価チェック
│   ├── 03_cicd-templates/                # SAST/依存/Secret/IaCスキャン・負荷試験テンプレ
│   └── 04_waf-review-checklist.md        # WAF 5柱レビュー票
│
├── B-mini-soc
│   ├── 10_kql-samples/                   # ハンティング/アラート用KQLサンプル
│   ├── 11_runbook.md                     # 初動SOP・判断基準
│   └── 12_playbooks/                     # 通知・CA強化・タグ付け等の自動化プレイブック
│
├── C-agent-marketplace
│   ├── 20_agent-toolkit-sample/          # Agents Toolkit/SDKによるカスタムエージェントサンプル
│   ├── 21_agent-studio-sample/           # Copilot Studio宣言的エージェントサンプル
│   ├── 22_certification-policies-checklist.md # Marketplace Certification Policies対応チェックリスト
│   ├── 23_responsible-ai-selfcheck.md    # Responsible AIセルフチェック
│   ├── 24_partnercenter-package/         # マニフェスト/説明文/画像/キーワード雛形
│   └── 25_ops-improvement-loop.md        # レビュー/テスト/提出/差し戻し対応フロー
│
└── common
    ├── 90_env-setup-min.md               # LZ Lite（最小ポリシー/命名/タグ/予算警告）
    ├── 91_data-sample/                   # 疑似ログ/サンプル分類
    └── 99_refs.md                        # 参考リンク（CAF/WAF/Marketplace/Agents/Certification Policies等）
```
