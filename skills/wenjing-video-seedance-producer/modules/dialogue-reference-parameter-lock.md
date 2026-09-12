# Dialogue Reference Parameter Lock

## Dialogue parity

对每个 `dialogue_ref` 比较 Storyboard/Script 原文与 Prompt。逐字符一致；不得润色、翻译、补语气词或调序。模型不支持目标音频方式时标记 capability mismatch。

## Reference parity

`reference_images` 是有序数组。Prompt 中“第 N 个参考”的 order、asset_id、用途、path/url、sha256 必须与请求完全一致；不得用未解析的 `@ImageN` 代替记录。重复资产也要保留每次用途。

`V0_1_DRY_RUN` 且无真实媒体时，`reference_images=[]`，另列 `planned_references[]` 的 asset_id/spec_path/purpose/real_media_status。planned reference 不进入真实调用数组，也不要求伪造 path/hash。

## Parameter parity

逐一比较 Prompt 与请求：model_id、selected_generation_duration、aspect_ratio、resolution、quality、audio_enabled、mode 和 profile 要求的其他字段；同时核对 Storyboard `creative_required_duration` 未被改写，且 selected 值不小于 creative 值。未知/不支持值不能自动改成默认值；无足够档位必须 SPLIT_REQUIRED，不能向下 clamp。

## 结果

三类 parity 全 PASS 才 `READY_TO_SUBMIT`。失败属于 Producer 编译问题时回 P2；源数据冲突时路由属主，不在本件修上游。
