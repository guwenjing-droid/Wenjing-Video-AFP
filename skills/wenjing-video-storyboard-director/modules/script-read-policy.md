# Script Read Policy

只接受 manifest 指向、状态 LOCKED、版本与 hash 有效的 `03_script_LOCKED.md`。

每个 sequence/beat/shot 保留 `source_refs[]`，可定位到 Script scene、beat、line、dialogue、knowledge 或 action。不得新增、删减、重排或改写事实与 Dialogue Lock；视觉执行存在歧义时标 `REVIEW_REQUIRED`，若会改变剧本则写 CR 退回 Script Studio。

读取按 sequence/beat 切片进行，禁止每次构建单镜时重读整份 Script。
