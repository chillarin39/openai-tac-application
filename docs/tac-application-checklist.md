# OpenAI TAC / GPT-5.5 Cyber チェックリスト

**対象**: 個人ルート (chatgpt.com/cyber 経由で TAC 有効化 → 段階的に GPT-5.5 Cyber 上位申請)
**最終更新**: 2026-05-30 (Phase C-1 = 運用立ち上げ完了、Phase 1 対話型運用開始)
**Canonical URL**: https://github.com/chillarin39/openai-tac-application/blob/main/docs/tac-application-checklist.md
**参考一次資料**: https://area11.org/Doc/technology/ai/openai-tac-cyber-access/

> **重要 (2026-05-30 発見)**: 個人向け `chatgpt.com/cyber` には詳細な申請フォーム (英文プロファイル / URL リスト / 用途記述) が存在せず、**本人確認 (KYC) を完了するだけで TAC アクセスが即時有効化** される仕組みでした。本チェックリストの Phase A で用意した素材は、当初は申請素材として準備したものの、実際の有効化フローでは使用されていません。現在は「自主公開した個人 TAC 運用ガイドライン」+「GPT-5.5 Cyber 上位申請時の track record」として位置づけています。

---

## Phase A: 申請前準備 (TAC 申請までに完了すべき項目)

### A-1. アカウント保護 (期限あり)

| # | 項目 | 状態 | メモ |
|---|------|------|------|
| A-1-1 | ChatGPT アカウントの Passkey または FIDO2 物理キー登録 (Advanced Account Security) | ☑ | 2026-05 時点で有効化済み (期限 2026-06-01 を前倒し対応) |
| A-1-2 | バックアップ手段 (リカバリコード保管) | ☐ | NAS 暗号化領域に保管推奨 |
| A-1-3 | OAuth 連携アプリの棚卸し (不要連携の削除) | ☐ | |

### A-2. ポリシードキュメント整備

| # | 項目 | 状態 | パス / URL |
|---|------|------|-----------|
| A-2-1 | AI 利用ポリシー (日本語) 作成 | ☑ | [`docs/ai-usage-policy.md`](./ai-usage-policy.md) |
| A-2-2 | 英文プロファイル草稿作成 | ☑ | [`docs/tac-application-profile.en.md`](./tac-application-profile.en.md) |
| A-2-3 | GitHub public repo として publicly accessible にする | ☑ | https://github.com/chillarin39/openai-tac-application |
| A-2-4 | プレースホルダ (`<insert at submission>`) を実値に置換 (提出直前) | ☑ | 2026-05-29 完了、提出版 `docs/submitted/2026-05-29-tac-submission.md` (gitignored) — 実際の有効化フローでは未使用、アーカイブとして保管 |

### A-3. ラボ環境の証憑揃え (Phase 0 進行中)

| # | 項目 | 状態 | 確認方法 |
|---|------|------|---------|
| A-3-1 | `ip_guard.sh` がラボ canonical に存在 | ☑ | 教材ラボワークスペース内 scripts/security/ |
| A-3-2 | `ethics_lint.sh` が pre-commit hook として動作 | ☑ | 同上 |
| A-3-3 | vmbr2 が 3 ノードで設定済 | ☑ | Terraform `network.tf` apply 済 (2026-05-15) |
| A-3-4 | **VMID 701 (kali-edu) Terraform apply** | ☑ | 2026-05-29 apply 完了、cloud-init done、SSH 疎通 + iptables ロード確認済 |
| A-3-5 | **VMID 702 (vuln-web-lab) Terraform apply** | ⚠️ | 2026-05-29 apply 自体は成功 (Resources: 4 added) / VM 起動時 Debian 12 genericcloud で boot-time kernel panic、別途再 provisioning 予定。kali-edu 側の Authorized Target Environment 立証には独立 |
| A-3-6 | kali-edu の iptables OUTPUT DROP ルール検証 | ☑ | [`docs/evidence/2026-05-29-iptables-output.txt`](./evidence/2026-05-29-iptables-output.txt) |
| A-3-7 | 10.20.0.0/16 から 172.16.1.0/24 への到達不能性検証 | ☑ | [`docs/evidence/2026-05-29-unreachability-prod.txt`](./evidence/2026-05-29-unreachability-prod.txt) 全 9 packet 100% loss |
| A-3-8 | 検証結果のスクリーンショット / ログ保管 | ☑ | [`docs/evidence/`](./evidence/) 配下、4 ファイル + README.md |

> **クリティカルパス**: A-3-4 〜 A-3-8 のうち TAC 申請に必要な核心 (kali-edu 側) は **2026-05-29 すべてクリア**。A-3-5 vuln-web-lab の boot panic は申請後の Phase 0 残務として記録、本申請のスコープ判断には影響しない。

### A-4. 公開実績の整理

| # | 項目 | 状態 | リンク |
|---|------|------|--------|
| A-4-1 | 公開ブログのセキュリティカテゴリ URL 確立 | ☐ | https://chillablog.chillarin39.com/study/security/ (指南書第 0 章公開後) |
| A-4-2 | GitHub プロフィール整備 | ☐ | https://github.com/chillarin39 (README pinned repo 確認) |
| A-4-3 | About ページに連絡先と研究分野 | ☑ | https://chillablog.chillarin39.com/about/ |
| A-4-4 | 個人 Hub の整備 | ☑ | https://chillarin39.com/ |

### A-5. 申請文書の最終チェック

| # | 項目 | 状態 |
|---|------|------|
| A-5-1 | NG ワード (exploit / 制限の少ない / 自由に試したい) が文書に含まれていない | ☑ |
| A-5-2 | 防御目的の言い換え表現に統一されている | ☑ |
| A-5-3 | redteam-lab を **明示的に対象外** と書いている | ☑ |
| A-5-4 | 入力禁止情報リストが具体的 | ☑ |
| A-5-5 | 段階的アプローチ (Phase 1-4) が記述されている | ☑ |
| A-5-6 | ラボ現状 (Phase 0 進行中) を正確に書いている | ☑ |

---

## Phase B: アクセス取得手続き

### B-1. 取得ルートの選択

| 選択肢 | 用途 | 採用 |
|--------|------|------|
| `chatgpt.com/cyber` (個人 TAC) | 個人の防御研究者向け、**KYC 通過のみで即時有効化** | ☑ **第一段階** |
| `openai.com/form/enterprise-trusted-access-for-cyber/` (組織) | 法人登記必要 | ✗ 不採用 |
| GPT-5.5 Cyber 直接申請 | 上位、TAC 実績必要 | ☐ 第二段階 (TAC 運用実績後) |

### B-2. 取得フロー (2026-05-29 実行 → 2026-05-30 有効化確認)

> **想定外発見** (2026-05-30): 個人向け chatgpt.com/cyber には **詳細な申請フォーム (英文プロファイル / URL リスト / 用途記述) が存在しない**。本人確認 (KYC) を完了するだけで TAC アクセスが即時有効化される仕組みだった。我々が用意した英文プロファイル / AI 利用ポリシー / Phase 0 evidence は **「自主公開した個人 TAC 運用ガイドライン」** として位置づけを変更 (透明性 + 自己拘束 + GPT-5.5 Cyber 上位申請時の track record として活用)。

1. ☑ `chatgpt.com/cyber` にアクセス
2. ☑ ChatGPT アカウントでログイン (Passkey 認証)
3. ☑ 本人確認書類アップロード (マイナンバーカード、表面、12 桁個人番号はマスク済)
4. ☑ 同意事項にチェック (利用範囲は防御研究 / 自己所有または明示的認可システムに限る、等)
5. ☑ **KYC 通過確認**: 「確認されました / 本人確認を完了し、信頼されたアクセスが有効になりました。」表示 + 「Codex に移動する」緑ボタン

### B-3. 自主公開素材 (申請フォームには使われなかったが、自主拘束 + track record として価値あり)

| 素材 | 用途 |
|------|-----|
| [`docs/ai-usage-policy.md`](./ai-usage-policy.md) | 自主公開した個人 AI 利用ポリシー (透明性 + 自己監査) |
| [`docs/tac-application-profile.en.md`](./tac-application-profile.en.md) | 当初は申請素材として用意、現在は「個人 TAC 運用方針の自主開示」として位置づけ。GPT-5.5 Cyber 上位申請時に再利用 |
| [`docs/evidence/`](./evidence/) | Phase 0 ラボの物理隔離立証ログ。指南書本編 + 上位申請時の参照素材として活用 |
| [`docs/submitted/2026-05-29-tac-submission.md`](gitignored) | 当初は提出版として用意、提出フォームが無かったため未使用。アーカイブとして保管 |

### B-4. 想定される後続 (Codex 側で運用ポリシー要求が出る可能性)

Codex 側に移動した時に追加の同意 / ポリシー記述要求が出る可能性。出た時の準備:

| 想定質問 | 用意した回答素材 |
|---------|----------------|
| 「教材ラボの物理隔離証明は？」 | vmbr2 が slaveless internal bridge である旨 + Terraform `network.tf` の構成 + Phase 0 evidence directory |
| 「公開ブログで攻撃手法を解説するリスクは？」 | 文章レビュー (anti-ai-slop-check / study-prose-check) 経由、抽象化ルール (RFC 5737) |
| 「本番環境と教材ラボの分離は技術的にどう保証？」 | 4 層 (vmbr2 物理隔離 / iptables OUTPUT / ip_guard.sh / ethics_lint.sh commit hook) |
| 「日本語以外のドキュメントは？」 | 英文プロファイル URL を提示 |

---

## Phase C: 利用開始後の運用立ち上げ (KYC 通過 = 即時有効化のため Phase B 直後に着手)

### C-1. 即時実施 (TAC 有効化 1 週間以内) — 2026-05-30 完了 (PR #4)

| # | 項目 | 状態 |
|---|------|------|
| C-1-1 | `docs/usage-log.md` を新設、月次サマリ運用開始 | ☑ 2026-05-30 ([`docs/usage-log.md`](./usage-log.md)、PR #4) |
| C-1-2 | 利用フェーズ (Phase 1) を README に記載 | ☑ 2026-05-30 (README「現在の運用 (Phase 1: 対話型)」、PR #4) |
| C-1-3 | system-dashboard の systems.yaml に "openai-tac-application" 項目追加 | ☑ 2026-05-30 (phase=deployed、dev_projects グループ) |
| C-1-4 | TAC 有効化を ナレッジ DB に記録 | ☑ 2026-05-30 (3 件: KYC 有効化仕様 / 体感差 / 運用マイルストーン) |

### C-2. 1〜3ヶ月運用 (Phase 1-2)

- ☐ 月次で `docs/usage-log.md` 更新 (利用回数 / 用途カテゴリ別件数)
- ☐ ポリシー逸脱の有無を自己監査
- ☐ Cyber 上位申請に向けた "実績証拠" として記録蓄積

### C-3. Cyber 上位申請判断基準 (3〜6ヶ月後)

以下が揃ったタイミングで Cyber 上位申請を検討:

- ☐ TAC を 3 ヶ月以上、ポリシー逸脱なしで運用
- ☐ 卒業課題ラボ (指南書第 12 章) 着手準備完了
- ☐ redteam-lab Phase 4 設計確定 (本 repo の TAC 利用範囲外として整理が完了していること)
- ☐ 公開記事 5 本以上で TAC 活用実績

---

## Phase D: 記事化計画 (オプション)

申請プロセス自体をブログ記事として公開する場合:

| # | 項目 | 状態 |
|---|------|------|
| D-1 | `blog_article_index.md` に「個人セキュリティ研究者の TAC 取得記 + GPT-5.5 Cyber 上位申請判断」登録 (S-79) | ☑ |
| D-2 | 取得プロセスのうち公開可能な範囲 = この repo 自体が公開素材 (KYC のみで有効化される実態 + 自主公開した運用ガイドラインの設計過程を含む) | ☑ |
| D-3 | content-publishing-flow に基づく有料コンテンツ化判断 | ☐ TAC 運用 3 ヶ月後 |

---

## 参考

- 元記事: https://area11.org/Doc/technology/ai/openai-tac-cyber-access/
- AI 利用ポリシー: [`docs/ai-usage-policy.md`](./ai-usage-policy.md)
- 英文プロファイル: [`docs/tac-application-profile.en.md`](./tac-application-profile.en.md)
