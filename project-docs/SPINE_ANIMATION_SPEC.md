# Spine 动画制作清单与规则

本文档给 Spine 美术/动画协作者使用，也是后续 Cocos Creator 接入时的验收标准。请严格按这里的命名、导出和性能规则制作资源。

## 1. 项目目标

游戏名：百分百空手接白刃

目标平台：微信小游戏，Cocos Creator 3.8.8，竖屏 750 x 1334。

当前角色表现方案：

- 猫：使用 Spine 骨骼动画。
- 武士：使用 Spine 骨骼动画。
- 木剑：不要作为武士 Spine 里的可见玩法物体。木剑由 Cocos 代码创建独立节点控制长度、旋转、落点和碰撞时机。

这样做是为了保证“刀不会变长、不会跳帧、不会和判定错位”。Spine 只负责角色身体、手、表情、受击等视觉表现。

## 2. 资源目录

美术交付建议放在以下目录：

```text
D:\workspace\百分百空手接白刃\art_delivery\spine\cat\
D:\workspace\百分百空手接白刃\art_delivery\spine\samurai\
D:\workspace\百分百空手接白刃\art_delivery\spine_exports\cat\
D:\workspace\百分百空手接白刃\art_delivery\spine_exports\samurai\
```

Cocos 项目最终导入目录由程序侧检查后再放入：

```text
D:\workspace\百分百空手接白刃\cocos-client\assets\spine\cat\
D:\workspace\百分百空手接白刃\cocos-client\assets\spine\samurai\
```

## 3. 文件命名

运行时文件名禁止使用中文，统一小写英文。

猫：

```text
cat.spine
cat.skel
cat.atlas
cat.png
```

武士：

```text
samurai.spine
samurai.skel
samurai.atlas
samurai.png
```

每个角色目录需要附带一个 `README.md`，写清楚动画名、循环方式、特殊注意事项。

## 4. 角色比例与站位

- 猫的整体高度约为武士的三分之二。
- 两个角色都是横向侧视，面对面。
- 双脚踩在同一条地面线上。
- 角色根节点建议放在双脚中心的地面位置，方便 Cocos 按同一地线对齐。
- 猫不能有整体前移接刀动作，身体位置要稳定。
- 猫可以有手臂、手掌、头部、表情动作。
- 为了让玩家看清猫的双手，双手可以做轻微错位显示，即使不完全符合真实透视也可以。
- 猫准备姿势时，双手必须已经举到头顶附近，不要从身体前方大幅移动到头顶。

## 5. 木剑规则

木剑是关键玩法物体，请严格遵守：

- 不要把木剑做成武士 Spine 里的可见玩法物体。
- 武士 Spine 可以保留握剑手势。
- 如果需要在 Spine 内做预览参考，可以做一个隐藏参考槽，命名为 `ref_sword_hidden`，但导入游戏后默认不可见。
- 木剑长度、角度、落点、命中猫头、被猫手接住，都由 Cocos 的 `bladeNode` 控制。
- 猫接刀不是必须接刀尖，猫的双手只需要夹住木剑中段或靠近前段的位置。

## 6. 猫动画清单

所有动画名必须完全一致。

| 动画名 | 循环 | 建议时长 | 用途 | 要求 |
| --- | --- | --- | --- | --- |
| `cat_idle_prepare` | 是 | 0.6 - 1.0 秒 | 默认准备 | 双手在头顶附近，身体不前移，轻微呼吸即可 |
| `cat_ready_hold` | 是 | 0.4 - 0.8 秒 | 刀下落前紧张状态 | 双手保持头顶附近，姿态更紧张 |
| `cat_catch_success` | 否 | 0.18 - 0.28 秒 | 成功接住 | 双手夹住木剑中段，不要让头和剑重叠 |
| `cat_catch_perfect` | 否 | 0.25 - 0.4 秒 | 完美接住 | 可在成功基础上加一点更稳的姿态，但不要夸张位移 |
| `cat_fail_hit` | 否 | 0.25 - 0.45 秒 | 晚点失败，被敲头 | 木剑自然落到头上，头上起大包，身体可以小幅震动 |
| `cat_early_fail` | 否 | 0.25 - 0.45 秒 | 提前出手失败 | 手先动但没接住，身体不前移 |
| `cat_result_win_idle` | 是 | 0.6 - 1.0 秒 | 成功结果待机 | 可选，保持接住后的轻微动作 |
| `cat_result_fail_idle` | 是 | 0.6 - 1.0 秒 | 失败结果待机 | 可选，头上大包，委屈/晕乎 |

## 7. 武士动画清单

所有动画名必须完全一致。

| 动画名 | 循环 | 建议时长 | 用途 | 要求 |
| --- | --- | --- | --- | --- |
| `samurai_idle_hold` | 是 | 0.6 - 1.0 秒 | 起手举剑待机 | 武士不出屏，双手保持握剑姿势 |
| `samurai_warning` | 否 | 0.3 - 0.5 秒 | 攻击前蓄力 | 可选，轻微蓄力，不要大幅位移 |
| `samurai_slash_down` | 否 | 0.5 - 0.8 秒 | 挥剑下劈 | 只做身体和手臂下劈，木剑可见物体由 Cocos 控制 |
| `samurai_recover` | 否 | 0.3 - 0.5 秒 | 攻击后回收 | 成功/失败后可回到稳定姿势 |
| `samurai_idle_after` | 是 | 0.6 - 1.0 秒 | 结果待机 | 可选 |

## 8. 程序状态映射

程序侧会按下面逻辑播放 Spine：

| 游戏状态 | 猫动画 | 武士动画 | 木剑 |
| --- | --- | --- | --- |
| 等待/倒计时 | `cat_idle_prepare` | `samurai_idle_hold` | Cocos 独立节点待机 |
| 下劈过程 | `cat_ready_hold` | `samurai_slash_down` | Cocos 控制旋转下落 |
| 不错成功 | `cat_catch_success` | `samurai_recover` | 停在猫手位置 |
| 完美成功 | `cat_catch_perfect` 或 `cat_catch_success` | `samurai_recover` | 停在猫手位置 |
| 晚点失败 | `cat_fail_hit` | `samurai_recover` | 自然落到猫头位置 |
| 提前失败 | `cat_early_fail` | `samurai_recover` | 继续按失败轨迹处理 |

## 9. 参考槽位与命名

为了程序对齐特效和判定，请在 Spine 中提供这些参考骨骼或槽位。可以是空附件或小透明参考点。

猫：

```text
slot_hand_catch_l
slot_hand_catch_r
slot_head_hit
slot_feet_ground
```

武士：

```text
slot_grip_l
slot_grip_r
slot_feet_ground
ref_sword_hidden
```

命名规则：

- 英文小写。
- 单词用下划线连接。
- 不使用中文、空格、特殊符号。
- 同类资源命名保持一致。

## 10. Spine 性能硬性规则

以下规则来自微信小游戏商用性能约束，必须遵守。

- 单角色骨骼数量不超过 40 根。
- 单角色图集最大边长不超过 1024 px。
- 导出 `.skel` 二进制文件，不导出 JSON 作为正式运行文件。
- 禁止单角色使用大量零散独立小贴图。
- 贴图尽量合并公共图集，减少 DrawCall。
- 运行时单屏同时活跃 Spine 实例不超过 6 个。
- Cocos Spine 组件需要开启预乘 Alpha。
- 关闭自动混合，关闭 useTint。
- 节点隐藏、页面销毁、切后台时，程序会执行清空动画和暂停骨骼运算，Spine 动画不要依赖后台持续播放。
- 不做骨骼 Debug、调试线、帧率显示等上线内容。

## 11. 动画制作性能规则

- 不要每一帧都打关键帧，能用少量关键帧插值就不要逐帧硬打。
- 避免复杂网格变形；确实需要 mesh 时，顶点数量要少。
- 避免多层半透明大面积叠加。
- 避免复杂 IK 链和大量约束。
- 循环动画要短而稳定，不做超长常驻时间线。
- 特效不要塞进角色 Spine 里，星星、提示、按钮反馈由 UI 或轻量 Tween 实现。
- 普通按钮动画禁止使用 Spine。

## 12. 图集与纹理规则

- 动态角色图集和静态 UI 图集分开。
- 动画资源图集总数要受控，整个项目目标不超过 8 张 2048 图集。
- 禁止使用 4096 纹理。
- 透明 PNG 要适配纹理压缩。
- 无透明通道图片优先 JPG，质量 70 - 80。
- 特效帧图单帧不超过 512 px。
- 不使用全屏超大序列帧。

## 13. 导出设置

正式交付请使用：

- Export Type：Binary
- 文件：`.skel`、`.atlas`、`.png`
- Premultiplied Alpha：开启
- Atlas 最大尺寸：1024
- Scale：保持 1，除非程序侧确认需要统一缩放
- Runtime 版本：与 Cocos Creator 3.8.8 可用 Spine 运行时兼容

如果不确定 Spine 运行时版本，先提供 `.spine` 源文件和一次测试导出，由程序侧导入 Cocos 验证。

## 14. 交付清单

猫目录需要包含：

```text
cat.spine
cat.skel
cat.atlas
cat.png
README.md
preview/cat_preview.mp4 或 preview/cat_preview.gif（可选）
```

武士目录需要包含：

```text
samurai.spine
samurai.skel
samurai.atlas
samurai.png
README.md
preview/samurai_preview.mp4 或 preview/samurai_preview.gif（可选）
```

`README.md` 至少写：

- 动画名称列表。
- 哪些动画循环，哪些不循环。
- 是否有隐藏参考槽。
- 是否有特殊缩放或对齐注意事项。

## 15. 验收清单

提交前请逐项确认：

- Spine Pro 打开源文件没有丢图。
- `.skel`、`.atlas`、`.png` 文件齐全。
- 动画名和本文档完全一致。
- 猫高度约为武士三分之二。
- 猫准备姿势时手已经在头顶附近。
- 猫成功接刀时手比头更靠前/更靠上，画面上不像刀打到头。
- 猫失败时木剑自然落到头上，不做木剑回缩或变长表现。
- 武士不会出屏，站位稳定。
- 武士 Spine 内没有可见玩法木剑，或只有隐藏参考剑。
- 单角色骨骼数量不超过 40。
- 图集最大边长不超过 1024。
- 透明边缘没有黑边、白边、脏边。
- 循环动画首尾自然。
- 非循环动画最后一帧能作为结果画面停住。

## 16. 程序接入说明

程序侧会在 `GameManager` 中按状态调用：

```ts
setAnimation(trackIndex, animationName, loop)
```

并会在暂停、弹窗、切后台、页面销毁时统一暂停或清空 Spine 动画，符合微信小游戏性能规则。

木剑会继续由 Cocos 节点控制，不从 Spine 里取最终剑的位置。Spine 中的手、头、握剑槽位只用于视觉对齐和特效参考。