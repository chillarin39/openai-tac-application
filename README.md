# openai-tac-application

OpenAI Trusted Access for Cyber (TAC) を**個人ルート**で取得した記録と、有効化後の運用ポリシー / 物理隔離ラボの構成証憑をまとめた公開リポジトリです。

GPT-5.5 Cyber (上位) への将来申請に向けた track record の役割も担います。

> **注記 (2026-05-30)**: 当初は「個人 TAC は詳細な申請フォーム経由」と想定していましたが、`chatgpt.com/cyber` の実際の経路は **本人確認 (KYC) 通過のみで TAC を即時有効化** する仕組みでした。本リポジトリの英文プロファイル / AI 利用ポリシー / Phase 0 evidence は、当初は申請素材として用意したものの、実際の TAC 有効化フローでは使用されていません。現在は **「自主公開した個人 TAC 運用ガイドライン」** として位置づけ、自己拘束 + 透明性 + 将来の GPT-5.5 Cyber 上位申請時の track record として活用します。

## なぜ公開するのか

1. **自己拘束**: 公開された運用ルールは破りにくい。AI エージェント運用 5 原則 (原則 4「AI 丸投げ禁止、説明責任は人間」) に沿った設計
2. **日本語圏での事例公開**: 国内で TAC を個人取得した研究者がほぼおらず、有効化までの経路 (KYC のみ) と運用ルールの設計事例として参考になる可能性がある
3. **GPT-5.5 Cyber 上位申請時の track record**: 上位申請では詳細審査が想定されるため、TAC 期間中の運用ポリシー + ラボ証憑 + 利用ログを継続蓄積しておく

## ドキュメント

| ファイル | 役割 | 公開状態 |
|---------|------|---------|
| [docs/ai-usage-policy.md](docs/ai-usage-policy.md) | 個人版 AI 利用ポリシー (日本語、自主公開) | public |
| [docs/tac-application-profile.en.md](docs/tac-application-profile.en.md) | 英文運用プロファイル (当初は申請素材、現在は自主公開の個人運用方針) | public |
| [docs/tac-application-checklist.md](docs/tac-application-checklist.md) | Phase A〜D の取得前/取得時/運用/上位申請判断チェックリスト | public |
| [docs/evidence/](docs/evidence/) | Phase 0 ラボの物理隔離立証ログ (iptables / 到達不能性) | public |
| `docs/submitted/` | 当初の提出版コピー (KYC のみで有効化されたため未使用、アーカイブ) | gitignored |

## 関連リポジトリ・プロジェクト

- **教材ラボ環境** (運用根拠): プライベートワークスペース内 `study-contents` のサイバーセキュリティ指南書ライン。VMID 701-705、vmbr2 / 10.20.0.0/16 隔離セグメント
- **倫理装置**: `ip_guard.sh` (10.20.x.x 以外実行ブロック) + `ethics_lint.sh` (本番 IP commit 前検出)
- **redteam-lab**: 自宅本番 172.16.1.0/24 を対象とする個人検証ライン。**TAC/Cyber 利用範囲外** として明示除外
- **公開ブログ**: https://chillablog.chillarin39.com/ (`/study/security/` セクションで指南書配信)

## ステータス

| Phase | 状態 | 日付 |
|-------|------|------|
| Phase A: 取得前準備 | ✅ 完了 | 2026-05-29 |
| Phase B: TAC 有効化 (KYC 経由) | ✅ 有効化済 | 2026-05-30 |
| Phase C: 利用開始後の運用立ち上げ | 🟡 着手中 | 2026-05-30〜 |
| Phase D: GPT-5.5 Cyber 上位申請判断 | ⏳ TAC 運用 3〜6 ヶ月後 | 未定 |

詳細は [docs/tac-application-checklist.md](docs/tac-application-checklist.md) 参照。

## ライセンス

ドキュメントは [CC BY 4.0](LICENSE) で公開。引用・再利用歓迎。
