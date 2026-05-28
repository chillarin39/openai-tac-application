# OpenAI TAC / GPT-5.5 Cyber 申請前チェックリスト

**対象**: 個人申請ルート (chatgpt.com/cyber 経由で TAC 取得 → 段階的に Cyber 上位申請)
**最終更新**: 2026-05-29
**Canonical URL**: https://github.com/chillarin39/openai-tac-application/blob/main/docs/tac-application-checklist.md
**参考一次資料**: https://area11.org/Doc/technology/ai/openai-tac-cyber-access/

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
| A-2-3 | GitHub public repo として publicly accessible にする | ☐ | https://github.com/chillarin39/openai-tac-application |
| A-2-4 | プレースホルダ (`<insert at submission>`) を実値に置換 (提出直前) | ☐ | 英文プロファイル §10、提出版は `docs/submitted/` に保管 (gitignored) |

### A-3. ラボ環境の証憑揃え (Phase 0 進行中)

| # | 項目 | 状態 | 確認方法 |
|---|------|------|---------|
| A-3-1 | `ip_guard.sh` がラボ canonical に存在 | ☑ | 教材ラボワークスペース内 scripts/security/ |
| A-3-2 | `ethics_lint.sh` が pre-commit hook として動作 | ☑ | 同上 |
| A-3-3 | vmbr2 が 3 ノードで設定済 | ☑ | Terraform `network.tf` apply 済 (2026-05-15) |
| A-3-4 | **VMID 701 (kali-edu) Terraform apply** | ☐ | **未着手 — 申請提出の必須前提** |
| A-3-5 | **VMID 702 (vuln-web-lab) Terraform apply** | ☐ | **未着手 — 申請提出の必須前提** |
| A-3-6 | kali-edu の iptables OUTPUT DROP ルール検証 | ☐ | `ssh kali-edu sudo iptables -L OUTPUT -n -v` で確認 |
| A-3-7 | 10.20.0.0/16 から 172.16.1.0/24 への到達不能性検証 | ☐ | `ssh kali-edu ping -c 1 172.16.1.1` が失敗することを確認 |
| A-3-8 | 検証結果のスクリーンショット / ログ保管 | ☐ | `docs/evidence/` に保存 (次フェーズで新設) |

> **クリティカルパス**: A-3-4 〜 A-3-8 が揃わないと TAC 申請の核心根拠 (Authorized Target Environment) が「計画段階」のままになる。提出前に必ずクリア。

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
| A-5-1 | NG ワード (exploit / 制限の少ない / 自由に試したい) が文書に含まれていない | ☐ |
| A-5-2 | 防御目的の言い換え表現に統一されている | ☐ |
| A-5-3 | redteam-lab を **明示的に対象外** と書いている | ☑ |
| A-5-4 | 入力禁止情報リストが具体的 | ☑ |
| A-5-5 | 段階的アプローチ (Phase 1-4) が記述されている | ☑ |
| A-5-6 | ラボ現状 (Phase 0 進行中) を正確に書いている | ☑ |

---

## Phase B: 申請手続き

### B-1. 申請ルートの選択

| 選択肢 | 用途 | 採用 |
|--------|------|------|
| `chatgpt.com/cyber` (個人 TAC) | 個人の防御研究者向け | ☑ **第一段階** |
| `openai.com/form/enterprise-trusted-access-for-cyber/` (組織) | 法人登記必要 | ✗ 不採用 |
| GPT-5.5 Cyber 直接申請 | 上位、TAC 実績必要 | ☐ 第二段階 (TAC 取得後) |

### B-2. 申請提出フロー

1. ☐ `chatgpt.com/cyber` にアクセス
2. ☐ ChatGPT アカウントでログイン (Passkey 認証)
3. ☐ 申請フォームに以下を貼付:
   - 英文プロファイル §1〜§10 の本文
   - AI 利用ポリシー URL (https://github.com/chillarin39/openai-tac-application/blob/main/docs/ai-usage-policy.md)
   - GitHub URL (https://github.com/chillarin39)
   - 公開ブログ URL (https://chillablog.chillarin39.com/)
   - 個人 Hub URL (https://chillarin39.com/)
4. ☐ 本人確認書類アップロード (パスポート or 運転免許証 or マイナンバーカード)
5. ☐ 禁止用途の不使用宣言にチェック
6. ☐ 提出版を `docs/submitted/YYYY-MM-DD-tac-submission.md` に保存 (gitignored)
7. ☐ 提出
8. ☐ 提出日と参照番号を `docs/usage-log.md` に記録 (Phase C で新設)

### B-3. 想定される追加質問への準備回答

| 想定質問 | 用意した回答素材 |
|---------|----------------|
| 「教材ラボの物理隔離証明は？」 | vmbr2 が slaveless internal bridge である旨 + Terraform `network.tf` の構成 |
| 「公開ブログで攻撃手法を解説するリスクは？」 | 文章レビュー (anti-ai-slop-check / study-prose-check) を経由、抽象化ルール (RFC 5737) |
| 「本番環境と教材ラボの分離は技術的にどう保証？」 | 4 層 (vmbr2 物理隔離 / iptables OUTPUT / ip_guard.sh / ethics_lint.sh commit hook) |
| 「日本語以外のドキュメントは？」 | 英文プロファイル URL を提示 |

---

## Phase C: 承認後の運用立ち上げ

### C-1. 即時実施 (TAC 承認 1 週間以内)

| # | 項目 | 状態 |
|---|------|------|
| C-1-1 | `docs/usage-log.md` を新設、月次サマリ運用開始 | ☐ |
| C-1-2 | 利用フェーズ (Phase 1) を README に記載 | ☐ |
| C-1-3 | system-dashboard の systems.yaml に "openai-tac-application" 項目追加 | ☐ |
| C-1-4 | TAC 取得を ナレッジ DB に記録 | ☐ |

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
| D-1 | `blog_article_index.md` に「個人セキュリティ研究者の GPT-5.5 Cyber 申請記」登録 (S-79) | ☑ |
| D-2 | 申請内容のうち公開可能な範囲 = この repo 自体が公開素材 | ☑ |
| D-3 | content-publishing-flow に基づく有料コンテンツ化判断 | ☐ TAC 運用 3 ヶ月後 |

---

## 参考

- 元記事: https://area11.org/Doc/technology/ai/openai-tac-cyber-access/
- AI 利用ポリシー: [`docs/ai-usage-policy.md`](./ai-usage-policy.md)
- 英文プロファイル: [`docs/tac-application-profile.en.md`](./tac-application-profile.en.md)
