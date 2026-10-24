# Counter-Examples — 候选清单 (阶段 1 产出)

> extractor: counter-example-extractor | 全量扫描 91 页 OCR 文本

```yaml
- id: ce01
  title: 以自我为中心的来世信念
  type: counter-example
  source_chapter: 第 4 章 诗篇中的死亡
  source_quote: |
    "以自我为中心的来世信念（天堂当作补偿、地狱逃避）
    是有害的迷信。只有以神为中心的信仰才稳固。"
  failure_mode: |
    把天堂当作「我受了苦所以得到补偿」的地方，
    把地狱当作「我逃避惩罚」的反面——
    信仰的核心变成「我得到什么」，而非「与神连结」。
    一旦补偿不足以激励，或恐惧不足以威吓，信仰就崩塌。
  mechanism: |
    自我中心的信仰把神当作实现自我利益的工具，
    而非信仰的对象本身。工具一旦不能兑现承诺就被抛弃。
  warning_signs:
    - "信仰动力完全来自对天堂奖赏的期待或对地狱惩罚的恐惧"
    - "若问'为什么信神'，答案的核心是'为了我自己'"
    - "对神的渴望不超过对天堂的渴望"
  bound_to:
    - "以神为中心的信仰才稳固 (p04)"
  tags: [counter-example, self-centered, afterlife, superstition]

- id: ce02
  title: 仪式沦为神的代替品
  type: counter-example
  source_chapter: 第 5 章 主的荣美
  source_quote: |
    "人发展抽象分析思维后和谐瓦解，仪式沦为神的代替品。"
  failure_mode: |
    仪式原是见神的面的途径，与神的同在未分化时是整全的。
    当人发展抽象分析思维后，开始把仪式本身当作神——
    不再透过仪式与神相遇，而是在仪式中找到安全感。
    途径取代了目的，仪式成为代替品。
  mechanism: |
    人倾向于抓住可操控的东西。仪式可操控（可重复、可标准化），
    神不可操控。因此人本能地用仪式替代与神的真实相遇。
  warning_signs:
    - "对仪式的执着超过对神同在的渴望"
    - "仪式执行完美但内心空洞"
    - "仪式变更引发强烈焦虑（因为安全感来源是仪式不是神）"
  bound_to:
    - "途径喧宾夺主警戒原则 (p01)"
    - "被提昇文学的阅读法 (f06)"
  tags: [counter-example, ritual, means-displacing-ends, worship]

- id: ce03
  title: 律法主义流弊
  type: counter-example
  source_chapter: 第 6 章 比蜜甘甜
  source_quote: |
    "律法主义流弊——圣学带来属灵骄傲。当途径喧宾夺主，
    取目的而代之时，便成为一种祸害。——Charles Williams"
  failure_mode: |
    律法本是「真实的」（揣得住水的、不决堤的），
    诗人对律法的喜爱是真诚的。
    但当律法从「通向神意的途径」变成「证明自己圣洁的标准」时，
    律法学得越好的人越骄傲，律法成为属灵骄傲的工具。
  mechanism: |
    人把律法从「外部的真实描述」内化为「内部的自我评价标准」，
    用对律法的遵守程度来衡量自己和他人的属灵地位。
    越精通律法越容易自义，越容易轻视他人。
  warning_signs:
    - "对律法的精通伴随着对他人的轻视"
    - "律法知识成为身份优越感的来源"
    - "更关心'是否遵守'而非'律法指向什么'"
  bound_to:
    - "途径喧宾夺主警戒原则 (p01)"
    - "低等本性被提昇后旧性仍存留 (p06)"
  tags: [counter-example, legalism, pride, means-displacing-ends]

- id: ce04
  title: 随意附会第二义
  type: counter-example
  source_chapter: 第 10 章 第二层含义
  source_quote: |
    "一旦接纳这种诠释方法，自然极易自我蒙蔽。
    我们所见的往往不过是自己愚昧的倒影。
    许多从前盛行的寓意式解释，无不过度牵强、武断和滑稽。"
  failure_mode: |
    一旦允许第二义存在，人就会把自己的想法任意附会到文本上，
    声称「这是更深层的含义」，实则是自我投射。
    不同时代的附会互相矛盾，无一公正裁判可决断。
  mechanism: |
    人有确认偏误——倾向于在文本中找到自己想找的东西。
    「寓意解经」给了确认偏误一个体面的外衣。
    巧思架构的故事无法制止他人以巧思从中挖出自圆其说的隐义。
  warning_signs:
    - "第二义与说话人的原义毫不相干"
    - "不同人看出的'第二义'互相矛盾"
    - "附会者声称独占奥秘的解释权"
    - "在甲时代看是牵强的，在乙时代看却显而易见——说明是文化投射"
  bound_to:
    - "第二层含义三类辨识法 (f05)"
    - "第二义须与原义一体同源 (p07)"
  tags: [counter-example, allegory-abuse, confirmation-bias, hermeneutics]

- id: ce05
  title: 把诗篇当教义清单读
  type: counter-example
  source_chapter: 第 1 章 导论
  source_quote: |
    "诗篇必须当作诗歌读……不可当作教义论文或预言清单来读。"
  failure_mode: |
    把诗歌的意象逐字逐句提取为命题，像读教义手册一样——
    结果是读到矛盾（同一首诗中同时自义又认罪）、
    读到困惑（咒诅诗篇中的仇恨与爱的诫命冲突）、
    读到抵触（赞美像谄媚独裁者）。
  mechanism: |
    人的思维偏好命题化——把诗歌意象还原为可提取的教义陈述。
    但诗歌的意义不在逐行命题而在意象的累积与回响。
    命题化读法必然遗漏诗歌的整体意境。
  warning_signs:
    - "读到一首诗篇时感到矛盾或困惑"
    - "试图逐节提取'教义要点'"
    - "把对仗的两行当作对立或递进的命题"
    - "用系统神学的框架去套诗歌"
  bound_to:
    - "体裁适配阅读法 (f01)"
    - "诗篇必须当作诗歌读 (p02)"
  tags: [counter-example, genre-mismatch, propositionization, reading-error]
```
