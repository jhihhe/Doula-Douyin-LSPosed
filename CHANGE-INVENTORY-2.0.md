# Doula 2.0：与 1.1.6 的完整变化清单

维护：@Jhih he。核对日期：2026-11-26（北京时间）。

以1.1.6正式发行时保存的源码SHA256清单为基线，不以最近一次提交代替发行版本。按用户可见行为去重整理为**21组新增/扩展、19组旧功能变化/修复**；组间存在关联，不等于40个独立Bug，也不代表全部已经实机验收。

源码126→161个文件：新增35、修改58、删除0；工具新增6/修改3，测试新增70/修改38。124/126个旧src内容可由Git历史对象匹配，VoiceForwardRepairs.java与HostContracts.java发行旧内容不在本地Git对象，只确认摘要改变，不编造行级差异。源码本身不公开。

“实机通过”仅指所列手机、宿主、作品与操作样本；“回放/契约”指生产方法或真实DEX检查，“待验”继续保留。

## 21组新增与扩展

| # | 用户可见行为 | 实现文件 | 证据和范围 |
| --- | --- | --- | --- |
| 1 | 模块总开关与桌面重新启用 | ModuleControl.java / SettingsProvider.java | 总开关关闭保留配置，桌面重新启用恢复；58实机通过。记录：2026-11-25-413-round6 |
| 2 | 悬浮倍速按钮 | FloatSpeedButton.java / FloatButtonHost.java | 出现、1.5→2.0实机通过；拖动/锁定完整矩阵待验。记录：2026-11-24-413-device-acceptance |
| 3 | 顶部标签改名 | TopTabRename.java / TabRenameHooks.java | 同城→附近已验证；选中标签完整覆盖待验。记录：2026-11-24-413-device-acceptance |
| 4 | 首页标签净化 | PureHome.java / CompatibilityFixes.java | 顶栏9→2实机通过。记录：2026-11-24-413-device-acceptance-round2 |
| 5 | 进度时间颜色、亮度预览和纵向位置 | ProgressStyleOptions.java / ProgressColorPicker.java / ProgressTimeStyle.java | Android色板触摸、保存取消和位置QA通过；不当作全部宿主场景通过。记录：2026-11-26-immersive-settings |
| 6 | 实时视频模糊填边的全屏沉浸 | HomeFullScreen.java / VideoFrameSource.java / VideoBackdrop.java | 真实帧更新、主体像素一致、换片与合集往返通过。记录：2026-11-26-immersive-repair |
| 7 | 完整显示短视频 | VideoContain.java | 契约与回放通过；真实多比例对照未齐，普通视频分类守卫仍待复验。记录：2026-11-25-413-status-summary |
| 8 | 不喜欢快捷按钮及确认 | DislikeShortcut.java / AutoPlayShortcut.java | 已接线与回放，未做真实提交反馈的闭环。记录：2026-11-25-feedback-inventory |
| 9 | 直播在线人数 | LiveViewerCount.java / LiveRoomViewerCount.java | 69实图2.4万、PCU更新与关闭恢复通过。记录：2026-11-25-413-round6 |
| 10 | 双击下载独立区域 | MediaGesture.java / UiAdditions.java | 代码/入口/契约通过，全部媒体下载矩阵待验。记录：2026-11-25-image-media-audit |
| 11 | 图集多选与全选保存 | ShareToolsRepair.java | 界面和分类已接，逐类保存成品实机未齐。记录：2026-11-25-image-media-audit |
| 12 | 实况照片原图与视频合成保存 | LivePhotoSave.java / ShareToolsRepair.java | 原生编码契约与回放通过，真实宿主实况成品待验。记录：2026-11-25-live-photo-encoder-audit |
| 13 | 已读好友白名单 | MessageTools.java / ReadTypingRepairs.java | 58自用两端真实已读对照通过。记录：2026-11-25-413-round6 |
| 14 | 选择会话后一键已读 | MessageTools.java | 59自用单聊实际确认与对端已读通过。记录：2026-11-25-413-round6 |
| 15 | 自选好友自动续火花 | AutoStreak.java / MessageTools.java | 默认关闭；每天首次前台发送；59自用端一次发送及重复resume不重发通过，不保证对方回复/火花状态。记录：2026-11-25-413-round6 |
| 16 | 已查看阅后消息可用原件归档 | OnceViewArchive.java | FD截断/删除/解码回归通过；真实一次性样本待验。记录：2026-11-25-message-feature-contracts |
| 17 | 来电铃声与振动静音 | CallSilence.java | 精确入口与回放通过，真实来电待验。记录：2026-11-25-message-feature-contracts |
| 18 | 文章独立过滤 | ArticleFilter.java / FeedFilterRepairs.java | 代码与回放通过，真实文章样本待验。记录：2026-11-25-feedback-inventory |
| 19 | 长按复制简介 | BioCopy.java | 46真实复制且留在主页通过。记录：2026-11-24-413-device-acceptance-round2 |
| 20 | 提高画质 | PlaybackQuality.java / QualitySelectionTrace.java | DASH请求/普通流选择有观察，未证明最高档；不承诺4K。记录：2026-11-25-quality-fallback413-audit |
| 21 | 普通视频后台播放 | BackgroundPlay.java / BackgroundCheckTrace.java | 64同一作品音轨HOME后on/off/on通过；覆盖旧summary的FAIL。记录：2026-11-25-413-round6 |

## 19组旧功能变化与修复

| # | 用户可见行为 | 实现文件 | 证据和范围 |
| --- | --- | --- | --- |
| 1 | 41.3播放、分享、刷新、消息、弹幕、表情和导航适配 | Host413.java / HostProfile.java / VersionMap.java | 多轮实机与真实DEX回归；旧版本分支保留，未全量旧版实机。记录：2026-11-25-413-round6 |
| 2 | 主题实际重建与原标签恢复 | ThemeAlignment.java / ImmersiveUi.java / ThemeTabRestore.java | 深浅互切及消息标签恢复通过；原HyperOS环境未回验。记录：2026-11-24-413-device-acceptance-round3 |
| 3 | 长按设置入口随标签重绑、Splash兼容、避免双弹窗 | SettingsEntry.java / FollowBottomCompatibility.java | 66单层及98入口实图通过。记录：2026-11-26-controls-handle-collection |
| 4 | 长按面板专属四卡片与去重 | ShareToolsRepair.java / LongPressContextCompat.java | 98一组四卡片、原生推荐项仍在。记录：2026-11-26-controls-handle-collection |
| 5 | 双击按动作语义分发，点赞交原生 | UiAdditions.java / LongPressRepairs.java / RuntimeRepairs.java | 73真实点赞、分享、评论、设置通过。记录：2026-11-25-413-round8-device |
| 6 | 普通视频/图文分类与视频信息字段 | ShareToolsRepair.java / UiAdditions.java | 普通视频工具正确、图文33张、ID/作者/时间/时长/IP有正例；POI和分享信息入口仍部分。记录：2026-11-25-413-round8-device |
| 7 | 长按昵称保存头像41.3接入 | ProfileRepairs.java | 真实头像文件写入通过。记录：2026-11-24-413-device-acceptance-round2 |
| 8 | 自然播完、评论打开守卫、播完暂停接入 | RuntimeRepairs.java / LiveAdvanceRepair.java / PhotoPause413.java | 自然完成与评论75秒不翻页通过；直播15秒、评论关闭恢复、暂停后手动重播仍部分。记录：2026-11-25-413-round5 |
| 9 | 底栏背景和按钮alpha分开及透明恢复 | CompatibilityFixes.java / FollowBottomCompatibility.java | 实际70%按钮、同视频背景对照与合集返回样本通过；红米原环境待验。记录：2026-11-26-bottom-background-layout |
| 10 | 导航高度按手势条上沿计算，新装/重置默认0dp | NavigationInsets.java / FirstRunDefaults.java | 0/8/40实测误差小于0.6px，保留已有自定义值。记录：2026-11-26-controls-handle-collection |
| 11 | 进度轨道跟底栏移动，30秒内播放态显示 | NativeProgress413.java / NavigationInsets.java / UiAdditions.java | 29秒同作品播放态on/off/on、进度更新通过；图文不误强显。记录：2026-11-26-short-progress |
| 12 | 发布时间地点字宽字距及最小字号 | PublicationStyle.java / PublishInfoRepairs.java | 6→11sp、单行省略，Android排版回归；省市宿主样本另有记录。记录：2026-11-26-ui-regressions |
| 13 | 设置字号、深浅色、基础毛玻璃独立 | SettingsMenu.java / ImmersiveUi.java / LiquidGlass.java / DoulaPort.java | 独立Android QA及真实设置旧ID缺失0；不把448断言当全部宿主通过。记录：2026-11-26-immersive-settings |
| 14 | 侧栏5→10项，修头像/关注晚绑定 | Host413.java / RuntimeRepairs.java / FollowButtonRepair.java | 实际十项及头像开关重启往返通过。记录：2026-11-26-controls-handle-collection |
| 15 | 合集feu/container真正清灰底 | CompatibilityFixes.java | 102原生属性color0/alpha0、container null；撤回99只看灰变黑的结论。记录：2026-11-26-controls-handle-collection |
| 16 | 大文件按可用空间、截断清理、HEIC/AVIF等MIME | LegacyMediaSave.java / MediaRepairs.java | Android下载器1GiB+64KiB/GIF及清理通过；源站限速未结案。记录：2026-11-25-413-round6 |
| 17 | 已读/输入状态、语音转发、防撤回及缓存原件 | ReadTypingRepairs.java / VoiceForwardRepairs.java / MessageMenuRepairs.java / RuntimeRepairs.java | 自用已读/语音、文字和已缓存PNG/MP4冷启保留通过；未缓存及一次性格式不扩大。记录：2026-11-25-413-round6 |
| 18 | 最新七类41.3映射恢复 | LongPressContextCompat.java / CommentRepairs.java / CommentVisibility410.java / CommentTime410.java / SceneRegisterHooks.java | 真实DEX与生产回放、冻结完整构建通过；Compose真实分配/显示和各实际点击待验。记录：2026-11-26-mapping-recovery413 |
| 19 | 关注二次确认可关闭、再开启恢复 | FollowConfirm411.java / SettingsMenu.java | 生产hook回放和真实设置false→true回读；未做实际关注操作。记录：2026-11-26-ui-regressions |

## GitHub 与 Telegram 反馈处置

| 反馈 | 本次正向变化 | 是否可以结案 |
| --- | --- | --- |
| [#13](https://github.com/jhihhe/Doula-Douyin-LSPosed/issues/13)、[#29](https://github.com/jhihhe/Doula-Douyin-LSPosed/issues/29) 自动播快捷入口 | 41.3按钮及独立显示开关有实际对照 | 该子项通过；#29提醒/定时数值保存另列待验 |
| [#25](https://github.com/jhihhe/Doula-Douyin-LSPosed/issues/25)、[#28](https://github.com/jhihhe/Doula-Douyin-LSPosed/issues/28) 进度不跟底栏移动 | 41.3轨道与时间同移，0/8/40dp实际对照 | #25旧环境已有用户“没问题了”；#28原41.1环境未回验 |
| [#27](https://github.com/jhihhe/Doula-Douyin-LSPosed/issues/27) 合集返回透明失效/遮挡 | 当前41.3真实合集返回多个样本恢复 | 当前路径通过；原40.8/努比亚环境待验 |
| [#16](https://github.com/jhihhe/Doula-Douyin-LSPosed/issues/16) 评论打开仍连播 | 41.3评论打开75秒不翻页 | 有改善实证；直播不跳过等子项仍待验 |
| [#26](https://github.com/jhihhe/Doula-Douyin-LSPosed/issues/26)、群反馈进入我底栏消失 | 原有“个人主页隐藏底部导航”开关可关 | 既有可选行为，不算2.0新增；个别环境仍需回验 |
| [#14](https://github.com/jhihhe/Doula-Douyin-LSPosed/issues/14)、[#24](https://github.com/jhihhe/Doula-Douyin-LSPosed/issues/24) 主题不跟随 | 当前手机深浅重建、恢复标签通过 | HyperOS和实时系统切换完整矩阵未齐 |
| [#10](https://github.com/jhihhe/Doula-Douyin-LSPosed/issues/10) 过滤失效 | 推荐响应有真实命中，恢复41.3入口 | 搜索/合集广告、文章和开屏正例不足，未整体结案 |
| [#30](https://github.com/jhihhe/Doula-Douyin-LSPosed/issues/30) 41.0无法加载 | 当前41.3能初始化 | 不等于原一加41.0问题解决，仍待验 |
| [群双击点赞反馈话题](https://t.me/Doula_LSPosed/32/1022)及近期同类反馈 | 修动作语义表，73真实红心计数变化 | 当前41.3样本已修复，不只依赖“待发版”的回复 |
| 群播完暂停后不能手动恢复 | 413完成回调已迁移，但410–412仍有pausedAids持有 | 未证明解决，保留待排查 |
| 群41.2红米Android17透明闪烁 | 当前413背景/按钮alpha分离、回前台/晚覆盖恢复 | 原机型未复验，不写彻底修好 |
| 群41.3支持请求 | 增加精确413适配及当前实机验证 | 已进入支持范围；逐功能以各行范围为准 |
| 群防自动更新请求 | 没有新增阻止宿主更新能力 | 仍是需求 |
| 群无操作后计时退出/锁屏请求 | 现有定时退出不等于按无操作时长触发 | 本次未新增，仍是需求 |
| 群短视频播放时不见进度 | 当前29秒同作品播放态开关往返通过 | 当前路径已解决，原反馈其他机型待验 |
| 群动图/大文件/慢下载 | 下载器原字节、格式识别、空间/截断改善 | 下载器层通过；全部宿主入口和源站慢速未结案 |

反馈核对来自本次实时读取的GitHub全部30条issue及其103条评论、Telegram Bug反馈话题当前可读消息。未宣称已翻遍群内全部历史附件；没有批量关闭issue，也未把远端已关闭自动算作新修复。原始评论、私人聊天记录、账号与签名资料不公开。

## 验证记录索引

本地逐项记录位于docs/validation/下，文件名见表格；[公开验证摘要](VALIDATION.md)与[口语更新日志](RELEASE-2.0.md)保留范围。发行包同代码检查另核对冻结输入、适配DEX、签名、权限和完整解码载荷，不以只改版本号代替验证。
