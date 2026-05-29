# AI 利用ポリシー（個人版）

**対象**: chillarin39 個人が、OpenAI TAC / GPT-5.5 Cyber 等の高度 AI モデルをサイバーセキュリティ研究・教材執筆・教材ラボ運用に用いる際の自己宣言ポリシー。
**版数**: v1.0
**最終更新**: 2026-05-29
**Canonical URL**: https://github.com/chillarin39/openai-tac-application/blob/main/docs/ai-usage-policy.md

---

## 1. 目的

本ポリシーは、OpenAI の Trusted Access for Cyber (TAC) および GPT-5.5 Cyber を含む高度 AI モデルの利用申請にあたり、申請者の利用目的・統制範囲・禁止事項を明文化することを目的とします。OpenAI の "Cybersecurity Disclosure and Use Policy" および TAC 申請審査論点 9 項目に整合させた構成です。

## 2. 申請者情報

- **氏名**: 非公開 (申請時のみ本人確認書類で提示)
- **ハンドル**: chillarin39
- **公開ブログ**: https://chillablog.chillarin39.com/
- **公開連絡先**: https://chillablog.chillarin39.com/about/
- **GitHub**: https://github.com/chillarin39
- **個人 Hub**: https://chillarin39.com/
- **役割**: 個人セキュリティ研究者・教材執筆者・自宅検証ラボ運営者

## 3. 利用目的 (許可される用途のみ列挙)

1. **教材コンテンツ執筆支援**: OWASP Top 10 / MITRE ATT&CK / NIST CSF 2.0 等のフレームワーク解説、CVE 影響範囲調査、検知ルール (Snort / Suricata / Sigma) の妥当性検証
2. **隔離教材ラボ内での PoC 再現**: 意図的脆弱ターゲット (DVWA / Juice Shop / Metasploitable2 / vulhub) に対する攻撃手法の再現性確認、および対応する防御策の検証
3. **セキュアコードレビュー**: 自プロジェクトの PR レビュー、IaC レビュー
4. **インシデント対応訓練**: ログ分析 (auth.log / syslog / Suricata eve.json) のトリアージ、IOC 抽出補助
5. **教材記事執筆**: 攻撃手法と防御策の両面を一貫した粒度で記述するための文章添削、図解設計補助

## 4. 利用対象環境 (明示的許可範囲)

### 4.1 許可対象 (educational lab segment のみ)

- **物理隔離セグメント**: `10.20.0.0/16` (Proxmox VE クラスタ上の vmbr2、slaveless internal bridge、ノード間通信不可)
- **教材 VM 群** (VMID 701-705、全て Proxmox node `nuc2` に集約予定):
  - 701 = kali-edu (Kali Linux 2026.x、2 NIC 構成、本番方向への新規接続は iptables OUTPUT で DROP)
  - 702 = vuln-web-lab (Debian 12 + Docker、DVWA / Juice Shop / vulhub ホスト)
  - 703 = metasploitable2
  - 704 = blue-lab (Ubuntu 22.04、検知側演習)
  - 705 = lab-router (任意、ARP Spoof 等 L2 演習用)
- **公開済み読者配布教材**: Vagrantfile / docker-compose (DVWA / Juice Shop / Kali / Metasploitable2)

> **現状 (2026-05-30)**: vmbr2 / VMID 701 (kali-edu) は Terraform で apply 済み + 物理隔離立証 ([Phase 0 evidence](./evidence/)) 完了。VMID 702 (vuln-web-lab) は boot panic で再 provisioning 待ち、703-705 は後続フェーズ。TAC アクセスは 2026-05-30 に KYC 通過で有効化済 (個人ルートでは詳細申請フォーム非経由)。本ポリシーは TAC 有効化と同時点から効力を持つ。

### 4.2 明示的に対象外 (利用禁止)

- **自宅本番ネットワーク** (`172.16.1.0/24` Proxmox / VM、`10.1.1.0/24` ネットワーク機器、`192.168.1.0/24` NAS)
- **インターネット上の第三者システム** (本人の明示的書面許可がない一切のターゲット)
- **個人検証ライン (redteam-lab)** — 自宅本番ネットワークを対象とするため、TAC/Cyber 利用対象から除外

## 5. 禁止用途 (OpenAI Cybersecurity Policy に準拠)

以下の用途には本 AI モデルを一切利用しません:

- 認可されていない第三者システムへの攻撃、偵察、スキャン
- 資格情報窃取の自動化、フィッシング、ソーシャルエンジニアリング
- ステルス技術、永続化、回避技術、権限昇格の悪用
- マルウェア配布、C2 (Command and Control) 構築、ボットネット運用
- 横展開、データ窃取、ランサムウェア、DDoS
- 公開ブログ記事における具体的攻撃ターゲット情報の暴露 (IP / ドメイン / 認証情報)

## 6. 入力データの取り扱い

### 6.1 入力禁止事項

- 本番認証情報 (パスワード / API キー / SSH 秘密鍵)
- 自宅本番ネットワークの実 IP / ホスト名 / サービス名 (記事化前は伏字、記事化後は抽象化)
- 顧客情報・個人情報 (該当する取扱いなし)
- 本番ログの生データ (匿名化 / 合成例に置換してから入力)

### 6.2 マスキング・匿名化の運用

- 自宅本番セグメントの IP は記事執筆時 `192.0.2.x` / `198.51.100.x` (RFC 5737 documentation prefix) に置換
- ドメインは `example.com` 系に置換
- credentials は `<REDACTED>` 表記または合成値

## 7. アカウント保護

- ChatGPT アカウントは **Passkey または FIDO2 物理セキュリティキー** で保護 (2026-06-01 以降の OpenAI 個人 TAC 必須要件「Advanced Account Security」準拠、2026-05 時点で有効化済み)
- パスワード単体での認証は使用しない
- セッショントークンの第三者への共有・漏洩防止

## 8. ログ・監査

### 8.1 利用ログの保存

- ChatGPT 会話履歴 (OpenAI 側保存、必要に応じてエクスポート保管)
- 教材ラボ側の認証ログ (`/var/log/auth.log`)、Suricata `eve.json`、bash history は VM スナップショット時点で保全
- 重要な利用記録は [`docs/usage-log.md`](./usage-log.md) に月次サマリで記録 (2026-05-30 新設、TAC 有効化と同日に運用開始)

### 8.2 監査可能性

- 全 PoC スクリプトは `ip_guard.sh` (教材ラボ canonical 配下) を必ず source、`10.20.0.0/16` 以外への実行を実行時にブロック
- リポジトリへの commit 前 hook `ethics_lint.sh` で本番 IP/ドメインの混入を検出
- 公開ブログ記事は文章レビュー (anti-ai-slop-check / brand-voice-check / study-prose-check) を経て main マージ

## 9. 段階的アクセス運用 (Phase 1 → 4)

OpenAI TAC ガイドラインに沿い、以下の段階で機能拡張を進めます:

| Phase | 利用形態 | 統制 |
|-------|--------|------|
| 1 | 対話型 (記事執筆補助、CVE 調査、検知ルール添削) | TAC 取得直後はここに留める |
| 2 | 読み取り中心 (Git PR レビュー、IaC レビュー) | 書き込み権限を AI に渡さない |
| 3 | 限定 HTTP 接続 (10.20.0.0/16 内 DVWA/Juice Shop への偵察補助) | MCP 化検討、ip_guard で対象限定 |
| 4 | 隔離環境演習 (卒業課題ラボ ACME 演習) | 完全隔離 vmbr2 内、承認フロー必須 |

## 10. ポリシー逸脱時の対応

- 本ポリシーに反する利用が判明した場合、即時に対象アクセスを停止し、OpenAI へ報告
- 公開ブログ記事内で本ポリシー違反が発見された場合、該当記事を即時非公開化
- 教材ラボ内で意図しない本番方向への通信が発生した場合、即時 VM 停止 + iptables ルール検証

## 11. 改版履歴

- v1.0 (2026-05-29): 初版作成。OpenAI TAC / GPT-5.5 Cyber 申請に向けた基盤ポリシー
