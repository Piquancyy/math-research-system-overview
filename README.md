# Codex Math Research System

## Public Overview and Method Contract

这是一个面向长期数学研究的、以证据、可恢复状态和审计边界为中心的工作流系统。本仓库是系统的公开概览入口；它描述研究流程、状态契约、证明安全边界和操作原则，不把任何具体研究项目、未发表证明、私有运行时或会话数据公开出来。

The Chinese text is the primary reference for this README. The English reference at the end preserves the same scope and safety boundaries for readers who prefer English.

> [!IMPORTANT]
> 本系统管理研究过程和证据，不是自动证明器。绿色 dashboard、Git 提交、TeX 编译、有限计算、agent 共识、本地模型输出或任何单一自动检查，都不能单独证明定理，也不能单独关闭 <code>public-claim-ready</code>。

> [!WARNING]
> 一个没有精确 active Claim 的目录，不应为了让工具变绿而初始化 <code>proof-system/</code>。状态文件、事务记录、agent 报告和构建日志都是工作流证据，不是数学证明权威。

## 全局目标

让长期数学研究在以下方面保持可恢复、可复核和诚实：

1. 命题在迭代中不悄然变强，假设、结论、常数和端点始终可追溯。
2. 引用的定理先与原始来源核对，再决定是否能够复用、翻译或加强。
3. 每一个证明关键桥段都有公式级映射、估计、误差和极限说明。
4. 失败路线、反例和隐藏假设被保留为可检索的研究障碍，而不是被聊天摘要抹去。
5. 来源、证明、对抗、双语、机械和公开宣称状态彼此分离，不用一个绿色信号掩盖其他开放义务。
6. 长任务在上下文切换后可以从耐久项目文件恢复，而不是依赖不可靠的 handoff prose。
7. 自动化和 agent 帮助探索与审查，但不替代主流程的证据检查，也不通过投票产生证明。

## 本次修订范围

本次修订只更新仓库 <code>Piquancyy/math-research-system-overview</code> 的主 README，统一其公开定位和系统契约。

- 不更新独立合作者的仓库、分支、镜像、fork 或私有版本。
- 不把本地 Codex 运行时、具体数学项目或未发表研究材料复制到本仓库。
- 不把本 README 的更新、Git 提交或 GitHub 远端状态解释为任何数学命题已经证明。
- 当前仓库的公开内容以方法说明为主；本 README 不假设仓库内存在可直接执行的实现目录。

## 仓库定位

本仓库应被理解为：

- 一个公开的研究方法和系统边界说明；
- 一个面向维护者、研究者和审查者的概念入口；
- 私有运行时与具体数学项目之间的接口说明；
- 对“哪些证据可以支持哪种结论”的明确约束。

本仓库不应被理解为：

- 自动定理证明器；
- 具体开放问题的解答；
- 任何单一模型、agent 或有限搜索的证明替代品；
- 私有项目的备份、会话数据库、凭据仓库或运行日志仓库；
- 允许公开再分发全部本地实现和内部研究材料的许可证声明。

公开可见性不等于授予代码、文字、研究成果或第三方材料的再利用权。许可证和第三方来源应以仓库实际元数据及其各自许可条款为准。

## 一页式系统模型

~~~~mermaid
flowchart TB
    A["研究问题或定理"] --> B["精确 active Claim"]
    B --> C["Claim Card 与来源范围"]
    C --> D["来源保真审查"]
    D --> E["公式级证明证书"]
    E --> F["对抗审查与障碍记录"]
    F --> G["适用时的双语同步"]
    G --> H["隔离构建与机械检查"]
    H --> I["冻结 closure bundle"]
    I --> J["公开宣称审查"]
    J --> K["public-claim-ready 仅表示门控闭合"]
    L["主 agent"] --> B
    L --> D
    L --> E
    L --> F
    M["有界 agents / 工具"] -. "候选、搜索、压力测试" .-> D
    M -. "proof_authority=false" .-> J
    N["具体数学项目"] --> C
    N --> E
    N --> F
~~~~

系统有四个边界层：

| 层 | 负责内容 | 明确不负责 |
| --- | --- | --- |
| 公开概览仓库 | 方法、状态语义、证据边界、维护原则 | 私有项目、凭据、会话和未发表证明 |
| 用户级运行时 | skills、hooks、agents、脚本、路由和工具契约 | 替具体项目作出数学判断 |
| 具体数学项目 | Claim、来源、TeX、证书、障碍、门控和研究输出 | 其他项目的运行数据与无关缓存 |
| 公开结果审查 | 冻结证据、当前版本和披露范围的最后检查 | 把工作流一致性当作定理真值 |

## 核心研究流程

### 1. 分类与入口

先判断当前请求属于哪类工作：

- source-first：需要获取和核对原始来源；
- proof-gate-first：需要关闭或重开某个证明门；
- adversarial：需要寻找反例、隐藏假设、端点失败或过强结论；
- mechanical-only：只做确定性机械检查，且不改变数学结论。

数学线程的短后续请求仍应从当前项目状态恢复，而不是当作没有上下文的新问题。系统入口应先运行分类和 dashboard；若项目没有精确 Claim，不得凭模板初始化证明状态。

### 2. 固定精确 Claim

每个受管项目必须有可审计的 active Claim。Claim Card 至少固定：

- 定理、问题或命题的完整表述；
- 全部假设、变量、空间、范围和依赖；
- 结论及其精确强度；
- 常数、端点、参数依赖和退化情形；
- 原始来源、版本、页码或题面范围；
- 脆弱证明桥段和必须逐项检查的地方；
- 已知反例、障碍、失败路线和条件性输入；
- 允许的结论分类和公开宣称边界。

Claim 的任何实质变化都必须显式记录为 replacement、refinement、strengthening、weakening、correction 或 scope-change。旧证据不会因为文字相似而自动继承；改变 Claim 或来源记录通常应重新打开依赖的 gates。

### 3. 来源优先

在保留或加强引用的定理前，先检查来源，不用“文献中似乎有类似结果”作为证据。来源审查应核对：

- DOI 或官方出版商页面；
- Version of Record 的标题、版本、定理编号和正文；
- 假设、结论强度、常数、端点和量词；
- 本地表述是否添加了来源没有的统一性、端点或参数范围；
- 本地证明是否悄然使用了来源未提供的性质。

机构访问必须经过正常的官方重定向和已验证的官方认证域名。任何密码、cookie、authorization header、token、OTP、MFA 值或签名下载地址都不得写入记录、日志、报告或证明证据。

若出现 CAPTCHA、OTP、MFA、设备确认或其他只能由人完成的阻断，记录阻断类别即可，改用最新且精确记录的 arXiv <code>vN</code> 版本。正式出版物不能仅凭 arXiv fallback 关闭正式来源门；只有当引用本身明确指向该精确 arXiv 版本，并且记录了版本和工件哈希时，arXiv 来源才可以按其自身范围闭合。

### 4. 公式级证明证书

证明关键桥段必须在首次使用处写出可复核的证书，不能把必要推理隐藏在短语中。重点包括：

- 明确的映射、定义域、陪域和可逆性或有界性；
- 每一步范数、不等式、常数和参数依赖；
- 误差项、截断项、逼近序列和收敛模式；
- 期望、条件期望、鞅转移、积分交换和极限交换的条件；
- endpoint degeneration、norm comparison 和 time-frequency transfer；
- 从有限计算、求解器或枚举结果回到数学陈述的翻译映射。

“显然”“routine”“by density”“by functoriality”“passing to the limit”等短语可以作为叙述，但不能替代证明所需的公式、假设、界和极限。编译通过也不能证明这些桥段成立。

### 5. 对抗审查与障碍

对抗审查的目标不是制造 agent 共识，而是尽早暴露：

- 反例和最小失败模型；
- 被遗漏的假设、量词或可测性条件；
- 端点、退化参数和非交换次序；
- 结论强于来源或强于证书的地方；
- 只在有限维、稠密子集或局部模型上成立的步骤；
- 失败路线中可复用的负面信息。

失败路线必须进入 obstruction ledger，并标明它失败的精确位置、使用过的假设、是否产生反例以及下一次可以复用的障碍。失败不是“没有结果”；它也不是自动的反证，除非反证证书完整。

### 6. 双语 TeX

若项目同时维护英文和中文稿件：

1. 先稳定英文 master；
2. 再同步中文版本一次；
3. 保持假设、结论、常数、端点、标签和依赖完全对应；
4. 检查重复手工 <code>\\tag{...}</code>、未定义引用和引用漂移；
5. 在隔离目录分别构建并检查 fatal error、undefined reference、undefined citation 和严重 overfull box；
6. 不让翻译版悄然增加、削弱或改变定理强度。

双语一致只证明两份文字对齐，不证明其中的数学陈述为真。

### 7. 机械验证

机械门负责确认确定性的工程事实，例如：

- Python 和脚本语法；
- JSON、状态投影和证据 manifest 的结构；
- TeX 的隔离构建；
- 重复 tag、label、citation 和 undefined reference；
- fatal log、危险 proof-moving phrases 和严重 overfull box；
- 路径、哈希、文件身份、事务父节点和恢复日志；
- 有界 probe 的进度、checkpoint、超时和大小边界。

机械门不能替代来源、证明或对抗门。绿色 mechanical signal 只能说明指定检查在指定输入上通过。

## Proof Gates 与结果分类

### Gate 矩阵

| Gate | 它回答的问题 | 需要的证据 | 不能由什么替代 |
| --- | --- | --- | --- |
| source-fidelity | 本地 Claim 是否与精确原始来源一致 | 来源工件、版本记录、逐项假设/结论/常数/端点对照 | 文献印象、摘要、旧报告或相似定理 |
| proof-certificate | 关键证明桥是否有公式级证书 | 显式映射、估计、误差、极限和参数依赖 | “显然”、模型解释、编译成功 |
| proof-adversary | 是否搜索过反例、隐藏假设和端点失败 | 主流程复核后的对抗报告与障碍记录 | agent 投票或多数意见 |
| bilingual-sync | 中英文稿是否保持同一数学强度 | 英文 master、同步记录、重复 tag 和双语构建报告 | 人工浏览几段文字 |
| mechanical-verification | 当前字节是否通过确定性检查 | 与当前输入绑定的机械报告和 manifest | 历史日志、未绑定输出或绿色界面 |
| closure | 必需 gate 是否对同一 Claim、同一来源和同一版本闭合 | 冻结 Claim、closure dependencies、哈希和新鲜报告 | 旧 gate 字段、模板和 runtime 自身 |
| public-claim-ready | 是否达到公开宣称的 review-grade 前置条件 | 全部必需 gate、当前 TeX、原始来源、证书、对抗、双语（适用时）、机械和冻结 closure bundle | 任一单独 gate、Git 提交或模型结论 |

### 结果分类

| 分类 | 含义 |
| --- | --- |
| <code>open</code> | 仍有必要义务未解决。 |
| <code>conditional</code> | 结论依赖未证明假设或缺失输入。 |
| <code>counterexample</code> | 当前表述被具体反例或可复核障碍否定。 |
| <code>proved-local</code> | 有局部公式级证书，但全局或其他 gates 尚未闭合。 |
| <code>source-faithful</code> | 当前声明范围已与指定原始来源逐项核对。 |
| <code>mechanically-verified</code> | 指定的确定性机械检查在绑定输入上通过。 |
| <code>public-claim-ready</code> | 精确 Claim 的全部必需门和冻结证据已达到公开宣称审查前提。 |

这些分类可以沿不同维度同时出现。例如，一个结果可能是 <code>proved-local</code> 且 <code>mechanically-verified</code>，但仍然是 <code>open</code> 的 public gate。<code>public-claim-ready</code> 是流程状态，不是关于定理真值的元数学证明。

### Dashboard 如何解释

- <code>red</code>：状态、来源、事务、隐私或机械结构有阻断问题；先修复结构再继续。
- <code>yellow</code>：存在开放 gate、陈旧证据或未完成义务；不得公开升级结论。
- <code>green</code>：当前系统壳层和指定检查一致；仍需检查数学来源、公式证书和对抗证据。
- <code>stale-state-file</code>：关键状态文件超过新鲜度阈值，不能直接当作当前研究状态。
- <code>no-project-state</code>：没有 active Claim 和 <code>proof-system/</code>；对本公开概览仓库这是正常状态，不应人工制造。

必须区分“工具和路由可用”与“当前项目的 gate 已执行”。可发现的 skill、agent 模板、旧输出目录或已存在的 gate 字段，都不等于当前 Claim 的证据已经审查。

## 具体项目的固定状态接口

以下文件属于具体数学项目，不属于本公开概览仓库的运行时内容：

| 路径 | 作用 |
| --- | --- |
| <code>proof-system/PROJECT_STATE.json</code> | 生命周期、active Claim、iteration head、投影哈希和恢复要求。 |
| <code>proof-system/CLAIM_REGISTRY.json</code> | Claim 身份、谱系和显式父子变更。 |
| <code>proof-system/iterations/</code> | 不可变事务记录链。 |
| <code>proof-system/ACTIVE_STATE.md</code> | 当前任务类别、可信状态和下一行动。 |
| <code>proof-system/CLAIM_CARD.md</code> | 精确命题、假设、结论、常数、端点、来源和脆弱步骤。 |
| <code>proof-system/OBSTRUCTION_LEDGER.md</code> | 失败路线、反例和可复用障碍。 |
| <code>proof-system/SOURCE_FIDELITY.md</code> | 来源定理或题面与本地 Claim 的逐项比较。 |
| <code>proof-system/PROOF_GATE.json</code> | 机器可读 gate 状态和证据绑定。 |
| <code>proof-system/PUBLIC_CLAIM_READY.md</code> | 默认 non-ready 的公开宣称镜像；不能脱离其他证据单独使用。 |
| <code>proof-system/EVIDENCE_LEDGER.jsonl</code> | 命令、工件和状态连续性记录；不是数学证明。 |

运行时缓存、快照、租约、恢复目录和 telemetry 应留在本地的 <code>.math-research-system/</code> 命名空间，不应被当作项目证明证据或公共源码。具体项目的 <code>proof-system/</code> 也不应未经审查复制到公共仓库。

## 事务、快照与恢复

受管项目的状态更新必须遵守以下原则：

- <code>init</code> 需要先有准确、明确、可审计的 active Claim；不能以占位符初始化。
- 旧项目用显式 <code>state-migrate</code>，不能由 audit 或 dashboard 自动推断迁移。
- Claim 改变用 <code>claim-transition</code>，普通投影用 <code>iteration-commit</code>。
- 受保护的 Claim Card 和来源记录用 <code>canonical-record-update</code>。
- 冻结 closure 依赖和哈希用 <code>closure-bind</code>。
- Gate 状态用 validator-backed <code>gate-update</code>，不能直接编辑活跃的 gate JSON 来伪造闭合。
- 中断事务先用 <code>transaction-recover</code> 预览，再在核对 journal、PID、父节点、候选文件和备份哈希后显式恢复。
- 快照用于广泛编辑前的回滚；restore 默认是 dry-run，只有审阅恢复计划后才能强制执行。
- 状态、候选投影、证据 ledger 和目录身份必须经过私有文件、硬链接、符号链接、路径别名和共享文件身份检查。
- Windows 上的严格目录锚点和事务命令应从项目外的中性进程工作目录启动；失败时保留现场并诊断已知占用者，不通过放宽安全边界绕过锁。
- 不使用强制 push、历史重写或删除用户文件来解决状态冲突。

事务完整性是工程证据。它不能关闭 proof gate，也不能证明定理。

## Outcome Harvest

Outcome Harvest Pipeline 与探索同步运行，不是项目结束后的整理工作。

只有以下内容可以成为 durable node：

- 项目内的持久正规工件；
- 已提交的研究状态 iteration；
- 精确局部结果、反例、障碍、新工具、不变量、归约或应用映射；
- 明确的分支拆分、合并或阶段闭合。

普通聊天、agent 消息、搜索命中、TeX 构建、格式改动、未持久化 probe 和 proof-graph 条目本身不是 durable node。没有独立结果机会时，也应记录 <code>none</code>，因为“没有可收获结果”是审计事实的一部分。

checkpoint 只哈希并关联工件，不解析它来创造定理，不写 proof gate，也不改变 Claim。自动 checkpoint 的 <code>proof_authority</code> 必须为 <code>false</code>；它不能产生 candidate、关闭 <code>M</code> 或把局部结果升级为论文结论。Card 接纳、来源、优先权、新颖性、独立价值和发表判断仍需要明确的人类审查。

## Agents、本地模型与主流程边界

### 有界 agent 计划

主流程应保留关键路径。只有在存在真正独立的来源、证据、反例或验证任务时才分派 sidecar，并且每一波都应：

1. 明确角色、输入范围、输出工件和停止条件；
2. 设定有界预算，不让并行工作逃离当前 Claim；
3. 立即等待结果，完成主流程整合和冲突处理；
4. 关闭已完成的 agent，避免生命周期资源泄漏；
5. 由主 agent 重新检查报告、引用、公式和文件哈希。

常见角色包括 radical、conservative、counterexample、moderator、literature scout、proof adversary 和 TeX verifier。它们的输出是候选材料和压力测试，不是证明权威。

当系统判定必须进行 adversarial wave 时，应实际完成 radical、conservative、counterexample 三个独立角色，再由 moderator 综合；不能以“大家同意”代替此流程。若本轮确实无法分派，只能记录固定的机械性、强耦合、容量不足、来源未冻结或写冲突原因，并在下一轮重新检查。

所有 route receipt、agent agreement 和 sidecar 报告都应标记：

- <code>proof_authority=false</code>；
- <code>gate_impact=none</code>；
- 不能关闭任何 Proof Gate；
- 不能把模型共识升级为 public claim。

### 本地模型边界

本地 Qwen 路由仅适合不含数学内容的、隔离 inbox 内的触发性任务。数学命题、公式、TeX、来源段落、证明状态、研究 transcript 和状态恢复不得发送到该路由。其输出是 <code>candidate-unverified</code>，必须由强模型或确定性检查独立验证，并且不能递归触发自身，也不能成为数学证明上下文中的已接受推理。

## 上下文周期与长期恢复

长任务应在安全阶段边界创建耐久状态，而不是等到历史过长才临时总结。至少应记录：

- 精确 Claim、路线和目标；
- 假设、常数、端点和脆弱步骤；
- 证书路径、文件哈希和来源版本；
- 开放义务、失败路线和反例；
- 来源漂移、接受/拒绝的候选路线；
- gate 状态、closure 绑定和下一项确定性检查；
- 当前结论分类以及是否允许公开表述。

新的任务必须重新读取并验证这些项目文件；handoff prose 只能帮助导航，不能作为证明证据。

当前自动周期策略默认为 <code>shadow</code>。达到压力阈值时先记录 telemetry，不自动削弱推理强度、跳过证明义务、改变 gate 或归档任务。只有在原生 compaction 后仍满足压力条件、校准和提升门明确通过时，才可以启用候选 hard policy。上下文续接本身不是数学证据。

## 本地运行入口

本仓库是公开概览，不承诺在根目录提供可执行实现。以下命令描述安装在用户级运行时中的典型入口；实际路径以本机安装结果为准。

~~~~powershell
# 分类一个数学请求
python <MATH_SYSTEM_SCRIPT> classify --request-file <UTF8_REQUEST_FILE>

# 从项目外的中性目录审计具体项目
powershell -NoProfile -ExecutionPolicy Bypass -File <MATH_SYSTEM_HEALTH> -Command dashboard -Project <ABSOLUTE_PROJECT_PATH> -StaleDays 30 -NoAutoGit

# 只读检查 worktree 前提
powershell -NoProfile -ExecutionPolicy Bypass -File <MATH_SYSTEM_HEALTH> -Command worktree-ready -Project <ABSOLUTE_PROJECT_PATH> -ReadOnly -Json

# 广泛编辑前创建快照
python <MATH_SYSTEM_SCRIPT> snapshot --project <ABSOLUTE_PROJECT_PATH> --label before-proof-edit

# 检查工具链，不把检查结果当作数学证明
powershell -NoProfile -ExecutionPolicy Bypass -File <MATH_SYSTEM_HEALTH> -Command doctor -Project <ABSOLUTE_PROJECT_PATH>
~~~~

在 Windows 上，涉及严格目录锚点或受管事务的命令应从项目外启动，并显式传入绝对项目路径。若请求只是读取工作记录，可使用 records-only；若需要完整扫描 TeX、日志和 manifest，则使用 full read-only audit。明确的外部报告必须写到项目外的新文件，不能覆盖已有报告或把报告放进被审计项目。

## 机械与出版前检查清单

在声称一个项目达到 review-grade closure 前，主流程应逐项确认：

- Claim Card 是当前、精确且无占位符；
- 原始来源已经获取、版本化并逐项比较；
- source-acquisition record 与工件哈希相符；
- 每个关键证明桥都有公式级证书；
- obstruction ledger 已更新，失败路线没有被隐藏；
- adversarial 报告针对同一个 Claim 和当前文件；
- 英文 master 与中文稿（若适用）已同步；
- TeX 在隔离目录构建，标签、引用、日志和危险短语检查通过；
- mechanical manifest 和报告绑定当前输入字节；
- closure dependencies 没有漂移；
- public gate 没有从模板、旧报告、runtime 或自引用的 live metadata 关闭；
- 公开文字没有把 local、conditional、source-faithful 或 mechanically-verified 写成无条件定理；
- 私密信息、凭据、会话数据库、浏览器状态和大体量运行输出未进入公共仓库。

这份清单是发布前检查，不是定理证明本身。

## 安全、隐私与版本控制

禁止提交以下内容：

- 密码、API token、cookie、session、authorization header、OTP、MFA 值和签名 URL；
- <code>auth.json</code>、<code>cap_sid</code>、浏览器存储、会话数据库和安装标识；
- 私有数学项目的 Claim、证明、来源下载物、未公开数据和运行上下文；
- runtime cache、telemetry、快照、租约、临时日志和大型搜索输出；
- 未审查的第三方材料、个人信息或受限出版物全文。

版本控制规则：

- 混合工作树中只 stage 明确属于当前任务的路径；
- 不用 <code>git add -A</code> 静默吸收无关改动；
- 不强制推送，不改写历史，不通过删除文件解决冲突；
- Git commit、CI 通过和远端分支状态都只是工程记录；
- 公共仓库中的文档不得暗示私有运行时路径、私有项目内容或第三方材料已经公开。

若本地研究驾驶舱存在网络服务，只绑定回环地址，并在没有鉴权时禁止暴露到局域网或公网。

## 维护与变更原则

README 的每次重大更新都应回答：

1. 系统现在解决哪一种具体的研究流程风险？
2. 哪些证据属于流程治理，哪些证据才与数学结论直接相关？
3. 是否改变了 Claim、gate、状态、来源或公开宣称语义？
4. 是否引入了新的隐私、凭据、路径、依赖或可恢复性风险？
5. 文档是否仍然只描述实际存在的公开内容？
6. 是否需要同步本地 skill、agent、hook、脚本或项目状态契约？
7. 是否明确标出独立版本、私有运行时和具体项目的边界？

若系统契约改变，应先更新规范性本地规则和确定性检查，再更新本 README。不能只改 README 让公开文字领先于实际工具行为，也不能只改工具而让 README 继续保留过时的证明边界。

## 当前边界

本项目不声称解决任何具体开放问题，不声称完成任何未公开证明，也不把工作流一致性解释为数学正确性。它提供的是一种更严格的研究基础设施：固定 Claim，检查来源，写出证书，保存障碍，执行对抗和机械审查，在证据充分且当前字节冻结后，才允许讨论公开宣称。

---

# Mathematical Research System

## English Reference

This repository is a public overview and method contract for a long-running mathematical research workflow. It describes how to preserve exact claims, source fidelity, formula-level proof certificates, adversarial review, bilingual manuscript alignment, mechanical verification, durable state, and publication boundaries.

At this revision, the repository is documentation-oriented. It does not contain private runtime state, active project evidence, unpublished proofs, session databases, credentials, or a complete executable implementation. Independent collaborator repositories and variants are intentionally outside the scope of this update.

> The system manages research process and evidence. It is not an automated theorem prover. A green dashboard, successful build, finite computation, Git commit, agent agreement, or model output is not proof authority by itself.

## Research contract

The global objective is to make long-running mathematical work recoverable, source-faithful, formula-explicit, adversarially tested, mechanically reproducible, and honest about its status.

The workflow is:

1. Classify the request and recover current project state.
2. Freeze an exact active Claim before initializing managed proof state.
3. Inspect the Version of Record or the exact cited problem source before reusing or strengthening a theorem.
4. Decompose the argument into explicit proof obligations.
5. Write formula-level certificates for every proof-critical bridge.
6. Run adversarial checks for counterexamples, hidden hypotheses, endpoint failures, and over-strengthening.
7. Synchronize bilingual manuscripts from a stabilized English master when applicable.
8. Run deterministic, isolated mechanical checks.
9. Freeze the current Claim, sources, evidence files, and hashes into a closure bundle.
10. Treat public-claim-ready as a review gate, never as a substitute for mathematical judgment.

## Evidence and gate boundaries

The main gates are:

- source fidelity: the local statement matches its exact source in hypotheses, conclusion, constants, endpoints, and scope;
- proof certificate: proof-critical maps, estimates, errors, limits, and parameter dependence are explicit;
- adversarial review: independent pressure testing has been integrated by the main workflow;
- bilingual synchronization: English and Chinese statements, labels, constants, and dependencies agree;
- mechanical verification: the current input bytes pass deterministic syntax, build, reference, manifest, and log checks;
- closure: all required evidence is bound to one exact Claim and one current set of bytes;
- public claim readiness: the review-grade prerequisites are closed for the exact Claim.

No gate may be closed from a template, an old report, a model vote, the live self-referential gate file, or a runtime capability report. Gate receipts and agent reports must remain explicitly non-authoritative for theorem truth.

## Status vocabulary

Use explicit classifications instead of a generic proved label:

| Status | Meaning |
| --- | --- |
| <code>open</code> | Essential obligations remain unresolved. |
| <code>conditional</code> | The conclusion depends on an unproved assumption or missing input. |
| <code>counterexample</code> | The current statement is refuted or blocked by a concrete, checkable obstruction. |
| <code>proved-local</code> | A local certificate exists, while other global or review gates remain open. |
| <code>source-faithful</code> | The stated scope has been checked against the specified original source. |
| <code>mechanically-verified</code> | Deterministic checks passed on the bound inputs. |
| <code>public-claim-ready</code> | Required source, proof, adversarial, bilingual when applicable, mechanical, and closure evidence is current and aligned. |

A result may carry multiple axis classifications. Public claim readiness is an operational promotion status, not a proof of theorem truth.

## Durable project state

A managed project uses <code>proof-system/</code> as its fixed interface. Its durable records include project lifecycle and Claim identity, immutable iteration history, active state, an exact Claim Card, an obstruction ledger, a source-fidelity record, machine-readable proof gates, a non-ready public marker, and an evidence ledger.

The public overview repository does not need a <code>proof-system/</code>. A project must never initialize one merely to obtain a green dashboard. Managed mutation must be transactional, parent-aware, hash-checked, and recoverable. Interrupted transactions block new mutation until explicitly inspected and recovered.

Snapshots and Git history are useful rollback and continuity evidence. They cannot close proof gates.

## Source fidelity and bilingual work

Source acquisition begins with the DOI or official publisher page and the Version of Record. Compare the exact theorem or problem statement, hypotheses, conclusion, constants, endpoints, and quantifiers. When a human-only access barrier prevents formal retrieval, record the barrier category and use the latest exact arXiv version only within its recorded scope. Never store credentials, cookies, tokens, OTP/MFA values, or signed URLs in research evidence.

For bilingual TeX, stabilize the English master first and synchronize the Chinese version once. Check duplicate manual tags, labels, citations, undefined references, fatal logs, and serious overfull boxes in isolated builds. Translation alignment is not a mathematical correctness certificate.

## Agents and model outputs

Use bounded sidecars only for genuinely independent research, evidence, adversarial, or verification lanes. Define the role, scope, budget, output artifact, and integration step. The main workflow must inspect and verify every report. When an adversarial wave is required, use distinct radical, conservative, and counterexample roles followed by moderator synthesis.

Agent outputs, route receipts, agreement, and local model outputs have <code>proof_authority=false</code> and <code>gate_impact=none</code>. They cannot close a proof gate or turn a local result into a public theorem claim. Local model routing must not receive mathematical proof content or private state, and unverified output remains candidate-unverified.

## Outcome harvest and context recovery

Durable outcomes are attached to persistent project artifacts or committed research iterations. Checkpoints hash and observe outcomes; they do not create theorem cards, close gates, or promote claims. If no independent outcome is present, recording <code>none</code> is valid audit information.

Before a context cycle, persist the exact Claim, route, hypotheses, constants, endpoints, fragile steps, source versions and hashes, open obligations, failed routes, source drift, accepted and rejected candidates, gate status, and the next deterministic check. A successor task must reread and verify those files. Handoff prose is navigation, not proof evidence. Context rollover must not reduce reasoning strength or skip any proof obligation.

## Security and maintenance

Do not publish credentials, session data, private project materials, unpublished proofs, raw source downloads, runtime caches, telemetry, or large unreviewed outputs. Keep public documentation separate from private research state. Use explicit paths in mixed worktrees, avoid silent staging, avoid force-push and history rewriting, and treat version-control records as engineering evidence only.

When the system contract changes, update the deterministic local rules and checks before changing this overview. The README must describe the actual public repository and must not imply that private runtime components or collaborator variants were synchronized.

## Revision boundary

This revision updates only the primary README of the main overview repository. It does not modify independent collaborator versions, private mirrors, forks, or project-specific proof state.

The system does not claim to solve a particular open problem. It provides disciplined infrastructure for deciding what is open, conditional, locally certified, source-faithful, mechanically verified, or ready for further human review.
