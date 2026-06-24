# 美术规范：百分百空手接白刃

## 美术方向

整体风格：国风恶搞、卡通夸张、轻松好笑，不血腥。

关键词：侠客猫、欠揍武士、白光刀气、夸张表情、失败喜剧、微信小游戏传播感。

禁止方向：写实血腥、恐怖断肢、过度阴暗、侵权临摹其他游戏角色或 UI。

## 交付目录

美术资源统一放在：

D:\workspace\百分百空手接白刃\art_delivery

目录结构：

- cat：侠客猫
- samurai：恶搞武士
- bg：背景
- ui：界面元素
- fx：特效
- audio：音效和音乐

## 命名规则

文件名统一使用英文小写、下划线、三位序号。

示例：

- cat_idle_001.png
- cat_catch_success_001.png
- cat_fail_early_001.png
- samurai_fake_slash_001.png
- samurai_real_slash_001.png
- fx_blade_flash_001.png
- bg_training_yard.png
- ui_button_retry.png

不要使用：最终版、修改版、新建文件夹、未命名、中文乱码文件名。

## 角色：侠客猫动作清单

必需动作：

- 待机 idle
- 准备接刀 ready
- 成功接刀 catch_success
- 点早抓空 fail_early
- 点晚被拍飞 fail_late
- 炸毛 shock
- 帽子飞掉 hat_fly
- 通关折刀 victory_break_blade

建议每个动作 4-8 帧，重点动作可 8-12 帧。

## 角色：恶搞武士动作清单

必需动作：

- 待机 idle
- 标准举刀 raise_blade
- 真刀下劈 real_slash
- 假刀空挥 fake_slash
- 半路停刀 hold_blade
- 整理头巾 adjust_headband
- 挠手 scratch_hand
- 挠脚 scratch_foot
- 偷笑 smirk
- 叉腰嘲讽 taunt
- 震惊石化 shocked

第 9 关重点动作：假刀、整理头巾、眼睛眯起、头巾竖起、刀刃白光。

第 10 关重点动作：假起刀、鬼脸、挠手、挠脚、整理头巾、跺脚、终极下劈。

## 特效清单

必需特效：

- 真刀白光 fx_blade_flash
- 假刀残影 fx_fake_slash
- 破风线 fx_wind_cut
- 接刀火花 fx_catch_spark
- 慢放残影 fx_slowmo_trail
- 成功闪光 fx_success_flash
- 失败冲击 fx_fail_impact
- 第 10 关长刀光 fx_final_blade_flash

真刀必须有明显白光，假刀不能有白光。这是玩法线索，不只是装饰。

## 背景清单

第一版只需要 3 张背景：

- bg_training_yard.png：1-3 关，新手练武场
- bg_bamboo_night.png：4-8 关，夜晚竹林
- bg_final_stage.png：9-10 关，终极擂台

背景不要太抢眼，要给角色和刀光留出清晰空间。

## UI 清单

必需 UI：

- 开始按钮
- 重试按钮
- 下一关按钮
- 关卡牌
- 慢放回放框
- 失败提示框
- 成功提示框
- 分享战报卡
- 音效开关
- 震动开关

UI 风格要轻量、清楚、适合手机竖屏。

## 导出建议

- 图片格式：PNG
- 背景可用 JPG 或 PNG
- 保留透明背景的角色、UI、特效必须用 PNG
- 单张图尽量控制体积，方便微信小游戏包体优化
- 原始 PSD、AI、Aseprite 文件可单独放 source_files，不直接进游戏包
## 当前优先效果图需求

当前 Cocos 原型只是技术占位，不代表最终画面。请优先阅读 `project-docs/EFFECT_REFERENCE_REQUEST.md`，先完成主游戏画面、出刀前准备、刀下落过程、成功接住、失败、结算、UI 元素拆分这些效果图。

后续代码实现会以这些效果图为准，不再让 Codex 凭空设计最终画面。

