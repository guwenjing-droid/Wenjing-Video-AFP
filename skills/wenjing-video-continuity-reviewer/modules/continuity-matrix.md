# Continuity Matrix

逐 shot 与 neighbor 记录 expected/observed/evidence/result：

- identity 与角色数量；
- wardrobe/state；
- scene、time/light、空间布局；
- prop ownership/location/state；
- blocking、screen direction、eyeline、entry/exit；
- action start/end 与 match-on-action；
- dialogue speaker/order、VO、环境声/SFX/BGM intent；
- transition buffer。

PREFLIGHT 的 observed 是计划字段；POSTGEN 的 observed 必须来自媒体。不要把两个证据层混在同一 PASS。
