# openai-tac-application

OpenAI Trusted Access for Cyber (TAC) および GPT-5.5 Cyber を**個人申請ルート**で取得するための公開リポジトリです。

申請の核心根拠となる「AI 利用ポリシー」「英文プロファイル草稿」「申請前後チェックリスト」を全て公開し、申請プロセスの透明性を確保することを目的としています。

## なぜ公開するのか

1. **OpenAI 審査の透明性確保**: 申請時に「公開ポリシー URL」として直接参照可能
2. **日本語圏での事例公開**: 国内で TAC/Cyber を申請する個人研究者がほぼおらず、申請プロセスの事例提供
3. **自己拘束**: 公開された運用ルールは破りにくい。AI エージェント運用 5 原則 (原則 4「AI 丸投げ禁止、説明責任は人間」) に沿った設計

## ドキュメント

| ファイル | 役割 | 公開状態 |
|---------|------|---------|
| [docs/ai-usage-policy.md](docs/ai-usage-policy.md) | 個人版 AI 利用ポリシー (日本語、申請時に URL 提示) | public |
| [docs/tac-application-profile.en.md](docs/tac-application-profile.en.md) | 英文プロファイル草稿 (提出時にプレースホルダ実値置換) | public |
| [docs/tac-application-checklist.md](docs/tac-application-checklist.md) | Phase A〜D 4 段階の申請前/申請時/承認後/記事化チェックリスト | public |

## 関連リポジトリ・プロジェクト

- **教材ラボ環境** (申請の核心根拠): プライベートワークスペース内 `study-contents` のサイバーセキュリティ指南書ライン。VMID 701-705、vmbr2 / 10.20.0.0/16 隔離セグメント
- **倫理装置**: `ip_guard.sh` (10.20.x.x 以外実行ブロック) + `ethics_lint.sh` (本番 IP commit 前検出)
- **redteam-lab**: 自宅本番 172.16.1.0/24 を対象とする個人検証ライン。**TAC/Cyber 利用範囲外** として明示除外
- **公開ブログ**: https://chillablog.chillarin39.com/ (`/study/security/` セクションで指南書配信)

## 申請ステータス

| Phase | 状態 | 着手予定 |
|-------|------|---------|
| Phase A: 申請前準備 | in progress | 2026-05-29〜 |
| Phase B: TAC 申請提出 | not started | ラボ証憑揃い後 |
| Phase C: TAC 承認後運用 (Phase 1-2) | not started | 承認後 |
| Phase D: Cyber 上位申請判断 | not started | TAC 運用 3〜6 ヶ月後 |

詳細は [docs/tac-application-checklist.md](docs/tac-application-checklist.md) 参照。

## ライセンス

ドキュメントは [CC BY 4.0](LICENSE) で公開。引用・再利用歓迎。
