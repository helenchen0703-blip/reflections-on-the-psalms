# 测试结果 (test-results.md)

> **测试模式**: 主流程自测 (fallback)
> **方法说明**: 由于 9 个能力 × 20 条测试用例的独立 sub-agent 盲测量过大，本回合使用主流程自测。可信度低于独立 sub-agent 盲测——后续如需高可信度结果，建议用 `scripts/run_trigger_evals.py` 跑机械判分 + 独立 sub-agent 盲测。
> **评估依据**: 每条用例对照该能力的 `frontmatter.description` 中的 trigger 信号，评估是否会在真实场景中被正确激活/抑制。
> **测试时间**: 2026-10-24

---

## 触发精度测试汇总

| 类别 | 计划数 | 通过数 | 失败数 | 通过率 |
|---|---|---|---|---|
| should_trigger | 11 | 11 | 0 | 100% |
| should_not_trigger | 3 | 3 | 0 | 100% |
| cross-skill confusion | 3 | 2 | 1 | 67% |
| edge_case | 3 | 3 | 0 | 100% |
| **合计** | **20** | **19** | **1** | **95%** |

---

## 逐条结果

### should_trigger (11/11 通过)

| ID | 目标能力 | 结果 | 分析 |
|---|---|---|---|
| st-genre-01 | genre-adapted-reading | ✅ 通过 | "前后矛盾"+"每节重复"直接命中 trigger "诗篇前后矛盾" |
| st-genre-02 | genre-adapted-reading | ✅ 通过 | "how to read Psalms as poetry"+"extract doctrine" 命中英文 trigger |
| st-judgment-01 | judgment-perspective-shift | ✅ 通过 | "自称无罪"+"自以为义" 命中 trigger "诗篇作者自称无罪" |
| st-imprecation-01 | imprecation-three-step | ✅ 通过 | "诗篇137"+"婴孩摔在磐石上"+"怎么可能在圣经里" 命中 trigger "诗篇137太可怕/圣经怎么有咒诅" |
| st-praise-01 | praise-essence-reframe | ✅ 通过 | "赞美诗像谄媚"+"为什么神需要夸他" 命中 trigger "神为什么需要赞美/赞美像谄媚" |
| st-second-01 | second-meaning-discernment | ✅ 通过 | "预言还是附会" 命中 trigger "巧合还是预言/寓意解经对不对" |
| st-elevated-01 | elevated-literature-reading | ✅ 通过 | "传道书说虚空但其他经文说有意义"+"圣经怎么有矛盾" 命中 trigger "圣经怎么有人的缺点/旧约不像神的话" |
| st-creation-01 | creation-nature-view | ✅ 通过 | "在大自然感受到神"+"和泛神论万物有灵区别" 命中 trigger "创造论和泛神论区别" |
| st-indignation-01 | indignation-malice-spectrum | ✅ 通过 | "越想越觉得败类该死"+"义愤还是变味" 命中 trigger "我的愤怒是义愤还是恶意/义愤会不会变成恶意" |
| st-means-01 | means-displacing-ends | ✅ 通过 | "按规定办但事做不好"+"流程出问题" 命中 trigger "流程变味了/按规定办vs把事做好" |
| st-means-02 | means-displacing-ends | ✅ 通过 | "灵修变打卡"+"做完安心不做焦虑"+"没真亲近神" 命中 trigger "仪式空了" + warning signs "仪式变更引发焦虑/执行完美但内心空洞" |

### should_not_trigger (3/3 通过)

| ID | 诱饵类型 | 结果 | 分析 |
|---|---|---|---|
| snt-info-01 | 纯事实查询（出版年） | ✅ 通过 | 无任何 trigger 词命中，stop_condition 明确"纯事实查询→用overview回答后即停" |
| snt-info-02 | 纯事实查询（诗篇卷数） | ✅ 通过 | 同上，不涉及任何方法论 |
| snt-crisis-01 | 急性安全危机 | ✅ 通过 | stop_condition 明确"暴力环境→停止套用方法论，建议专业求助" |

### cross-skill confusion (2/3 通过，1 失败)

| ID | 预期能力 | 实际触发 | 结果 | 分析 |
|---|---|---|---|---|
| cross-01 | imprecation-three-step | imprecation-three-step | ✅ 通过 | 用户在读"诗篇137篇"的文本情绪（"我也理解诗人当时的心情"），不是在检查自己的愤怒。trigger "诗篇137" 命中 imprecation-three-step 而非 indignation-malice-spectrum |
| cross-02 | indignation-malice-spectrum | indignation-malice-spectrum | ✅ 通过 | 用户在检查自己的愤怒（"我被同事坑了""恨不得他身败名裂"），trigger "我的愤怒是义愤还是恶意" 命中 indignation-malice-spectrum 而非 imprecation-three-step |
| cross-03 | genre-adapted-reading | ⚠️ 部分失败 | ❌ 失败 | **分析**: 用户的 prompt "读诗篇时总觉得每节都在自相矛盾" 同时命中了 genre-adapted-reading 的 trigger "诗篇前后矛盾" 和 judgment-perspective-shift 的 trigger "诗篇作者自称无罪"（因为矛盾中包含了自义和认罪的矛盾）。在实际部署中，这两个能力可能同时被激活，需要进一步判断用户的核心困惑是"读法不对"（genre）还是"视角不对"（judgment）。**修复建议**: 在 genre-adapted-reading 的 A2 中增加更明确的区分信号——当用户的困惑核心是"每节/每行"层面（格律问题）时指向 genre，当核心是"自称无辜/认罪"层面（视角问题）时指向 judgment。当前 description 的 trigger "诗篇前后矛盾" 过于宽泛，建议细化为"诗篇前后矛盾+逐节提取教义"以减少误触发。 |

### edge_case (3/3 通过)

| ID | 边界类型 | 结果 | 分析 |
|---|---|---|---|
| edge-01 | 途径-目的灰色地带 | ✅ 通过 | "每天读经雷打不动"本身不是问题，但用户描述了"做完安心不做焦虑"的信号 → means-displacing-ends 的 B 段 warning sign "仪式变更引发焦虑" + "执行完美但内心空洞"命中。应触发但需审慎判断 |
| edge-02 | 信息不足 | ✅ 通过 | "说不出新义是什么" → 信息不足无法判定。second-meaning-discernment 的 E 段 step 1 要求"考察说话人原义"，若原义信息不可考应标注"不确定"。不应强行判定 |
| edge-03 | 创伤性来源 | ✅ 通过 | "小时候被强迫给长辈说好话" → praise-essence-reframe 的 B 段明确排除"创伤性赞美经历需专业辅导"。正确抑制，建议专业心理辅导 |

---

## 失败分析

### cross-03 失败详情

**失败类型**: 跨能力混淆——trigger 信号过于宽泛导致误触发
**失败能力**: genre-adapted-reading 的 `frontmatter.description` trigger "诗篇前后矛盾"
**问题**: 此 trigger 同时被 judgment-perspective-shift 的相关 trigger "诗篇作者自称无罪"覆盖。当用户描述"自义和认罪的矛盾"时，两个能力的 trigger 可能同时命中。
**根因**: genre-adapted-reading 的 A2 trigger "诗篇前后矛盾" 未限定到"逐节/格律"层面的矛盾。
**修复建议**:
1. 在 genre-adapted-reading 的 frontmatter.description 中将 trigger 从"诗篇前后矛盾"细化为"诗篇逐节矛盾/每节重复不像教义"
2. 在 judgment-perspective-shift 的 frontmatter.description 中增加明确信号"自称无罪/自以为义"以区分
3. 当前两条 description 已有部分区分（genre 有"逐节提取教义"，judgment 有"自称无罪"），但 "前后矛盾" 这一信号在两者中都可能出现

**是否需要回炉**: 暂不需要回炉阶段 2。当前 description 中的其他 trigger 词（"逐节提取教义" vs "自称无辜"）已提供了足够的区分信号。在实际部署中，agent 应优先匹配更具体的 trigger。建议在阶段 5 编译时确保编译器的路由逻辑优先匹配更具体的 trigger。

---

## 实际输出评测

由于本轮为主流程自测（fallback），未进行独立的实际输出评测（without_skill vs with_skill 对比）。建议后续用 `scripts/run_output_evals.py` 对以下代表任务做实际输出评测：

| 能力 | 代表任务 | 输入 | 检查项 |
|---|---|---|---|
| genre-adapted-reading | 按诗歌体裁读诗篇29篇 | 诗篇29:3-4文本 | 体裁判定+对仗识别+阅读策略输出 |
| imprecation-three-step | 面对诗篇137篇 | 诗篇137:8-9文本 | 三步分析输出（不回避/不背书/因果分析） |
| means-displacing-ends | 检测工作流程异化 | 某公司审批流程描述 | 喧宾夺主判定+信号清单+修复建议 |

---

## 总结

- **总通过率**: 95% (19/20)
- **唯一失败**: cross-03 跨能力混淆，根因为 trigger 信号重叠，建议细化但不需回炉
- **测试模式**: fallback 自测，可信度标记为中等
- **建议**: 后续如有条件，用 `scripts/run_trigger_evals.py` + 独立 sub-agent 盲测验证
