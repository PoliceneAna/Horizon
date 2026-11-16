---
layout: default
title: "Horizon Summary: 2026-11-16 (ZH)"
date: 2026-11-16
lang: zh
---

> 从 44 条内容中筛选出 15 条重要资讯。

---

**科技新闻**
1. [vLLM v0.34.0：默认启用可扩展 KV 缓存并移除 Model Runner V1](#item-tech-news-1) ⭐️ 8.0/10
2. [Qwen4-Max 上线：2.4 万亿参数稀疏 MoE，后续将开源小模型](#item-tech-news-2) ⭐️ 8.0/10
3. [卡内基梅隆推出 CS Learn：YouTube 免费发布完整学期课程](#item-tech-news-3) ⭐️ 7.0/10
4. [Jiff 1.0 发布：Rust 日期时间库](#item-tech-news-4) ⭐️ 7.0/10
5. [微软将大规模邮件中断归因于 7 月修复引入的缺陷](#item-tech-news-5) ⭐️ 7.0/10
6. [Marimba：冻结 ASR 编码器的多问题语音查询模型](#item-tech-news-6) ⭐️ 7.0/10
7. [duetto：不微调，用采样时 logit 编辑让预训练音乐 Transformer 实时爵士伴奏](#item-tech-news-7) ⭐️ 7.0/10
8. [腾讯混元发布 Hy4 flash：224B MoE 与 1M 上下文](#item-tech-news-8) ⭐️ 7.0/10
9. [美与九国签署《旧金山宣言》协调保护 AI 供应链](#item-tech-news-9) ⭐️ 7.0/10
10. [亚马逊称 Artex 驱动 AI 代理窃取 API 密钥](#item-tech-news-10) ⭐️ 7.0/10
11. [美国将先进 AI 芯片出口管制延伸至远程访问](#item-tech-news-11) ⭐️ 7.0/10

**财经新闻**
1. [中国 10 月经济增长放缓：消费、工业与投资均不及预期](#item-finance-news-1) ⭐️ 8.0/10
2. [ETF 专家：英伟达动荡与国会变局或重塑 AI 交易](#item-finance-news-2) ⭐️ 7.0/10
3. [卢特尼克因家族公司与英伟达的关系面临利益冲突质疑](#item-finance-news-3) ⭐️ 7.0/10
4. [英特尔及 CEO 陈立武因 PC 需求与库存披露遭股东集体诉讼](#item-finance-news-4) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [vLLM v0.34.0：默认启用可扩展 KV 缓存并移除 Model Runner V1](https://github.com/vllm-project/vllm/releases/tag/v0.34.0) ⭐️ 8.0/10

vLLM 发布 v0.34.0，包含 1,061 次提交、412 名贡献者（其中 120 名新贡献者），新增 10 个模型集成，包括 Mistral Large 4、MiniMax-M3.1-Flash 和 Nemotron-3.5-Transcribe。该版本默认启用可扩展 KV 缓存，按预热后实际空闲显存确定缓存大小，官方称多数模型可获得更大缓存和更高吞吐，但在部分 H200 模型、并发 128 时每 token 解码延迟可能增加 6%–18%，可用 \`--gpu-memory-utilization 0.9\` 或 \`--no-enable-extensible-kv-cache\` 关闭。Model Runner V1 已被移除，V2 成为唯一 GPU runner；默认 \`--block-size\` 从 16 改为 64，ROCm 7.2 构建不再发布，并要求 \`huggingface\_hub &gt;= 2.0.0\`。发布说明还称在 GB200 上 Step5 解码最高提速 1.95 倍、GLM-5.3-Flash 吞吐提升 1.6 倍，GLM-5.3 长提示 TTFT 快 1.24–1.40 倍。

github · khluu · 11月16日 23:22

**「升级前的默认设置」** 在 v0.34.0 之前，vLLM 按 \`gpu\_memory\_utilization\`（默认 0.9）估算并分配 KV cache，默认 \`--block-size\` 为 16，GPU 侧由 Model Runner V1 负责执行，ROCm 构建则以 7.2 版本发布。本次发布包含 1,061 个提交，把这几项默认一并改写：KV cache 改为按预热后实际空闲显存扩展分配，block size 默认变为 64，Model Runner V1 被删除。因此已有部署需要按新默认重新核对启动参数与依赖版本。

**「影响」** 升级前需要迁移或调整配置：保留 \`VLLM\_USE\_V2\_MODEL\_RUNNER=0\` 会导致启动失败，依赖 V1 logits processor 的自定义代码需迁移到 \`vllm.v1.worker.gpu.sample.logits\_processor\`；要维持旧的 16 块大小和缓存估算行为，需显式传入 \`--block-size 16\` 与 \`--gpu-memory-utilization 0.9\`，同时把 \`huggingface\_hub\` 升到 2.0.0 以上。仍使用 ROCm 7.2 制品、\`fp\_quant\` 检查点、Marlin W4A8 或 Keye-VL 的部署无法直接升级。

**标签**: `#vLLM`, `#LLM inference`, `#open source`, `#KV cache`, `#performance`

---

<a id="item-tech-news-2"></a>
### [Qwen4-Max 上线：2.4 万亿参数稀疏 MoE，后续将开源小模型](https://mp.weixin.qq.com/s/pJUt0xwD6H-WMyzd8TjZaQ) ⭐️ 8.0/10

阿里通义千问发布新一代旗舰模型 Qwen4-Max，采用稀疏 MoE 架构，总参数 2.4 万亿，并原生支持视觉理解与百万 Token 长上下文。该文称其在前端编程的 Code Arena 盲测中位居全球前列，但未给出具体排名或第三方复现结果。按文章披露，单任务平均费用由 26.58 元降至 11.16 元（约降 58%），Token 消耗减少近 50%，API 定价同步下调。模型已上线，团队表示后续将推出更小的 Qwen4 系列并公开权重；上述性能、费用与开源计划均来自该摘要文章，尚待独立验证。

telegram · zaihuapd · 11月16日 02:52

**「背景」** 上一代旗舰 Qwen3.8 Max 的总参数量同为 2.4 万亿，因此 Qwen4-Max 的提升主要来自架构与成本优化，而非单纯扩大规模：据 Forklog 报道，新模型虽然总参数达 2.4 万亿，但每个 token 仅激活约 710 亿参数。据 wccftech 报道，Qwen4-Max 采用 3:1 的 GDN 与 QSA 层堆叠，在该媒体的 Intelligence Index 评测中落后于 Moonshot 的 Kimi K3.1 Pro 约 3 分，这意味着官方宣称的编程与长程任务领先地位仍待独立验证。

**「影响」** 对开发者而言，Qwen4-Max 的模型权重未公开，目前需通过 API 调用；Artificial Analysis 给出的阿里 API 报价为每百万输入 token 1.50 美元、每百万输出 token 4.50 美元，因此需要私有化或本地部署的团队无法直接部署 Max，只能等待官方后续开源的较小 Qwen4 模型。OpenRouter 还显示该模型默认开启推理，接入时需按此配置评估调用行为。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://forklog.com/en/alibaba-launches-qwen4-max-ai-model-with-2-4-trillion-parameters/">Alibaba Launches Qwen 4 - Max AI Model with 2 . 4 Trillion Parameters</a></li>
<li><a href="https://wccftech.com/alibabas-new-qwen4-max-fails-to-overtake-moonshots-kimi-k3-1-pro-retaining-the-same-parameter-count-with-a-lower-price-and-revamped-native-vision-moe-architecture/">Alibaba&#x27;s New Qwen 4 - Max Fails To Overtake Moonshot&#x27;s Kimi...</a></li>
<li><a href="https://openrouter.ai/qwen/qwen4-max">Qwen 4 Max - API Pricing &amp; Providers | OpenRouter</a></li>
<li><a href="https://artificialanalysis.ai/models/qwen4-max">Qwen 4 Max - Intelligence, Performance &amp; Price ... | Artificial Analysis</a></li>

</ul>
</details>

**标签**: `#Qwen`, `#large language models`, `#sparse MoE`, `#model release`, `#API pricing`

---

<a id="item-tech-news-3"></a>
### [卡内基梅隆推出 CS Learn：YouTube 免费发布完整学期课程](https://www.cs.cmu.edu/learn/) ⭐️ 7.0/10

卡内基梅隆大学计算机科学学院推出 CS Learn，开始在 YouTube 免费发布完整学期的现行计算机课程，覆盖多个主题。项目上线当天启动，本周每天首播一门课程，并计划在明年 1 月增加更多课程。负责人 Phillip Compeau 表示，部分学生开发的工具自动化了大量制作工作，使小团队也能承担制作工作。

hackernews · pcompeau · 11月16日 20:43 · [社区讨论](https://news.ycombinator.com/item?id=50522980)

**「背景」** 卡内基梅隆大学此前已推出面向高中的免费在线计算机科学课程 CS Academy，包含互动教材、教师培训与在线技术支持（tool-1-1）。免费开放课程本身也早有先例：Open Culture 汇总的免费在线课程约有 1700 门，来自耶鲁、MIT、哈佛、牛津等高校（tool-1-3）；讨论中也有评论者提到 MIT 早在约 25 年前就开始做同类开放课程。此次的不同点在于内容来自 CMU 当前在校课程的完整学期讲座，并以 YouTube 公开放送。

**「影响」** 对自学者而言，可以直接免费观看当前 CMU 课程的完整学期讲座；不过现有讨论只提出了许可协议问题，未显示具体授权条款，若计划二次使用、改编或让编程代理处理这些材料，仍需先确认许可。

**「社区讨论」** 有评论者认为，在 AI 时代把基础学扎实，AI 会成为更强的工具，否则人可能被取代；也有人强调开放课程之外还需要学习计划和问责机制。另有评论者询问课程采用何种许可协议，现有讨论中未见答复。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.youtube.com/watch?v=hztO5vaBTRs">Demonstration of Carnegie Mellon CS Academy - YouTube</a></li>
<li><a href="https://www.openculture.com/freeonlinecourses">1,700 Free Online Courses from Top Universities | Open Culture</a></li>

</ul>
</details>

**标签**: `#open courseware`, `#computer science education`, `#Carnegie Mellon`, `#YouTube`, `#free lectures`

---

<a id="item-tech-news-4"></a>
### [Jiff 1.0 发布：Rust 日期时间库](https://burntsushi.net/jiff/) ⭐️ 7.0/10

Jiff 1.0 发布，这是由 burntsushi 开发的 Rust 日期时间库。现有信息未披露具体 API、兼容范围或迁移路径；Hacker News 的讨论集中在日期时间 API 设计、与 chrono 等现有库的取舍，以及不同时间尺度的处理。

hackernews · burntsushi · 11月16日 16:53 · [社区讨论](https://news.ycombinator.com/item?id=50519744)

**「背景」** Jiff 的 0.2 版本此前已被不少 Rust 项目采用；维护者计划在 1.0 发布后的一年内继续为 0.2 提供关键缺陷修复，但不再进行新功能开发，以留出迁移过渡期。该库从一开始就把时区与夏令时处理放在 API 核心，目标是提供难以误用、性能合理的高层日期时间原语。

**「迁移与兼容性考量」** 对 Rust 开发者来说，Jiff 1.0 提供的是一套独立的高层日期时间原语，官方定位是让常见误用更难发生，同时保持合理性能；因此新项目可以直接按这套 API 设计代码，而不必沿用旧库的调用方式。已经在使用 chrono 的团队若要切换，应先核对现有代码和依赖链与新 API 的兼容性，并为迁移调用点预留成本。

**「社区讨论」** 前 chrono 维护者 quodlibetor 表示，chrono 的 API 稳定性反而使改进遭遇阻力并最终令其倦怠，他对 burntsushi 编写新库表示感谢；另有评论赞赏 Jiff 明确承认自己并非适用于所有场景，并询问 TAI、UT1 等时间尺度的支持。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://github.com/BurntSushi/jiff">GitHub - BurntSushi/jiff: A datetime library for Rust that ...</a></li>
<li><a href="https://burntsushi.net/jiff/">A datetime library for Rust - Andrew Gallant&#x27;s Blog</a></li>
<li><a href="https://docs.rs/jiff/latest/jiff/">jiff - Rust - Docs.rs</a></li>
<li><a href="https://github.com/BurntSushi/jiff">GitHub - BurntSushi/jiff: A datetime library for Rust that ...</a></li>
<li><a href="https://docs.rs/jiff/latest/jiff/">jiff - Rust - Docs.rs</a></li>

</ul>
</details>

**标签**: `#Rust`, `#datetime`, `#libraries`, `#API design`, `#chrono`

---

<a id="item-tech-news-5"></a>
### [微软将大规模邮件中断归因于 7 月修复引入的缺陷](https://www.theregister.com/saas/2026/11/16/microsoft-blames-monster-email-outage-on-software-defect-introduced-in-july-fix/5310026) ⭐️ 7.0/10

微软将一次大规模邮件服务中断归因于 7 月一项修复补丁引入的软件缺陷，称该缺陷在此前修复中埋下，随后在生产环境触发。现有材料没有提供故障持续时间、受影响用户规模或区域等细节，也未提供对这一定性的独立验证。

hackernews · Bender · 11月16日 13:18 · [社区讨论](https://news.ycombinator.com/item?id=50517321)

**「背景」** Microsoft 365 的网络网关服务器负责处理客户端与云服务之间的连接流量；相关报道称，本次事件中超过 80% 的此类服务器失去响应，进而形成级联故障。此次被归咎的缺陷来自 7 月专门为这些网关服务器准备的修复，意味着问题在数月后才随生产环境负载暴露出来。

**「社区讨论」** 评论中较有用的一点是测试环境与生产环境的差距：有评论者称，7 月代码在规格较低的 PASS 测试环境中通过，但该环境与高端生产机器不同，可能掩盖了并发缺陷，并质疑这种成本取舍是否常见、是否可接受。另有评论者用电网“黑启动”作类比，强调大型系统从零恢复的困难。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.bleepingcomputer.com/news/microsoft/microsoft-says-months-old-bug-caused-global-microsoft-365-outage/">Microsoft says months-old bug caused global Microsoft 365 outage</a></li>
<li><a href="https://cybersecuritynews.com/microsoft-outage-incident-report/">Microsoft Reveals How a Hidden Windows Bug Took Down Microsoft ...</a></li>

</ul>
</details>

**标签**: `#Microsoft 365`, `#service outage`, `#software defect`, `#incident analysis`, `#production testing`

---

<a id="item-tech-news-6"></a>
### [Marimba：冻结 ASR 编码器的多问题语音查询模型](https://www.reddit.com/r/MachineLearning/comments/1xxsqro/marimba_a_system_one_model_for_speech_r/) ⭐️ 7.0/10

Marimba 提出一种 system-one 语音模型：用户针对 8 秒音频窗口提出是/否、选项或评分问题，模型返回校准后的概率，而每个窗口只运行一次冻结的 Qwen3-ASR-0.6B 编码器。作者报告，在相同的 1,000 个公开问题上，它在 9 项测试中的 6 项追平或超过 Qwen3-Omni（30B-A3B），但在 Speech Commands 上仍落后；语言 ID 在 300 个 FLEURS 片段上达到 100%，说话人变化 AUROC 为 0.966–0.980。作者同时说明，turn-end 读出是在 Smart Turn 数据上训练的，因此该行只对自身是分布内；在 Smart Turn 自身测试集上，其 AUROC 为 0.930，低于 Smart Turn v3.2 的 0.982，在 ICSI 上则为 0.716 对 0.712。模型对未见任务不泛化，在 CochlScene 场景分类上各读出头的表现都只有随机水平；代码、Apache-2.0 权重和 Hugging Face 演示已提供，并可通过 pip install marimba-audio 安装。

reddit · r/MachineLearning · /u/solanotodesch · 11月16日 15:47

**「背景」** Marimba 复用的 Qwen3-ASR-0.6B 是阿里巴巴发布的开源权重语音识别模型，覆盖 30 种语言和 22 种中文方言，采用 Apache 2.0 许可。该模型原本用于语音转文本；Marimba 将它的编码器冻结，把同一段音频的单次编码表示供多个轻量读出任务共用，从而避免为每个任务重新训练编码器。

**「对开发者的影响」** 对语音和机器学习开发者而言，可复现包与 Apache-2.0 权重让“一次编码器前向、多问题读出”的方案可以直接测试；但其能力限于已支持的问题类型，遇到未见任务会失效，因此不适合直接当作通用音频理解模型。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.anchorterminal.com/tools/qwen3-asr-0-6b">Qwen 3 - ASR - 0 . 6 B review (2026): pricing, alternatives and grade C</a></li>

</ul>
</details>

**标签**: `#speech recognition`, `#machine learning`, `#frozen encoders`, `#probabilistic calibration`, `#audio understanding`

---

<a id="item-tech-news-7"></a>
### [duetto：不微调，用采样时 logit 编辑让预训练音乐 Transformer 实时爵士伴奏](https://www.reddit.com/r/MachineLearning/comments/1xxkyh3/steering_a_pretrained_music_transformer_at/) ⭐️ 7.0/10

开发者 /u/GGAllin43 发布 duetto：一个面向 MIDI 键盘的实时爵士搭档，能与你组成小编制演奏标准曲，在你演奏时伴奏、停下时独奏。它不做微调，直接使用预训练的 Anticipatory Music Transformer（Thickstun 等，2023），把全部控制放在采样阶段：演奏者的音符与模型的音符构成同一事件序列，模型逐个音符（起始、时值、音高）续写；每次采样前，规则层会修改 logits，屏蔽不允许的音符（必须等待的手、超出音域的音高、不在拍上的低音），并提高当前和弦音、强拍引导音等目标的概率。作者给出的速度数据是：在 3080 Ti 上 medium 模型约 12 ms/音、large 约 18 ms/音，large 在 Jetson Orin Nano 上约 90 ms/音仍足以现场演奏；服务器预先采样约 1 秒音乐，演奏者落键时重采样尚未播放的部分以压低延迟。演示（Autumn Leaves，160 bpm）中约 61% 的独奏音符来自引用的乐句或主题，乐句取自 Weimar Jazz Database 的转录独奏、按独奏者换气处切分并移调到曲目和弦上；代码免费供非商业使用。作者同时说明目前仍会偏离演奏者、响应难以预测，模型自身想法与规则的平衡很脆弱：偏向过多像乐句词典，过少则不再像爵士。

reddit · r/MachineLearning · /u/GGAllin43 · 11月16日 09:19

**「背景」** duetto 基于 Thickstun 等人于 2023 年提出的 Anticipatory Music Transformer；该模型以自回归方式生成音乐，并支持包括伴奏在内的 infilling 控制任务，因此演奏者与模型的音符可以被组织成同一条事件序列。duetto 不重新训练该模型，而是在每个音符采样前用规则层修改 logits，以施加音区、节拍与和声约束。

**「影响」** 对做符号音乐生成或实时人机合奏的开发者而言，这个项目提供了采样时约束解码作为免微调方案的具体数据点：大型模型在消费级 GPU（约 18 ms/音）和嵌入式设备（约 90 ms/音）上都能落在实时预算内，值得在无法承担微调成本或需要动态改变行为时尝试；但作者自述的漂移与“偏向强度”失衡表明，可控性仍是该路线待解的问题。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://arxiv.org/abs/2306.08620">[2306.08620] Anticipatory Music Transformer</a></li>

</ul>
</details>

**标签**: `#AI music generation`, `#sampling-time control`, `#pretrained transformers`, `#real-time interaction`, `#MIDI`

---

<a id="item-tech-news-8"></a>
### [腾讯混元发布 Hy4 flash：224B MoE 与 1M 上下文](https://mp.weixin.qq.com/s/5yBbf-ctYziM5r0i6Y17lA) ⭐️ 7.0/10

腾讯混元发布 Hy4 flash，这是一款总参数 224B、激活参数 12B 的 MoE 模型，支持多模态与 1M 上下文，并已在腾讯云 TokenHub、WorkBuddy 和元宝上线；官方还计划将其开源。其 API 定价为每百万 Token 输入 0.5 元、输出 2 元，命中缓存时仅 0.02 元；11 月 30 日前 WorkBuddy 限免、API 5 折。腾讯称其综合效果略优于 Hy4 preview，WorkIndex 单任务成本为 Hy4 preview 的 1/13、Hy4 的 1/20，但这些性能与成本优势均来自官方说法，尚无独立基准验证。

telegram · zaihuapd · 11月16日 07:17

**「背景」** Hy4 flash 属于 Hy4 系列的低成本成员，官方以 Hy4 preview 和 Hy4 作为效果与成本参照，这为理解其“日常任务性价比”定位提供了直接基线。它采用 MoE 架构，总参数 224B 但推理时仅激活 12B，因而能在保留较大模型容量的同时压低单次调用的算力开销。

**「对成本敏感部署的影响」** 对成本敏感的开发者来说，按官方公布的价格，Hy4 flash 每百万 Token 输入 0.5 元、输出 2 元，命中缓存时输入仅 0.02 元；腾讯在内部 WorkIndex 评测中称其单任务成本为 Hy4 preview 的 1/13、Hy4 的 1/20，约为 DeepSeek-V4.1-Flash-1017 忙时最高价档的 1/8。但这些成本与满意度数据均来自腾讯自测或 85 名内部用户的盲测，尚无独立基准验证，开源也仅处于计划阶段；打算替换现有模型的团队，应先用自己的任务集复测质量与真实计费，再决定是否迁移。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://finance.sina.com.cn/tech/roll/2026-11-16/doc-iniyxpwx1163480.shtml">实测腾讯 Hy4 flash：花两毛钱，就能让 AI 从零做个 3D 交互网页</a></li>
<li><a href="https://www.tencent.com/zh-cn/tencent-launches-hy4-flash-to-power-high-speed-cost-efficient-ai-deployment-for-everyday-workflows/">腾讯混元 Hy4 flash 正式发布：赋能日常高效办公 - Tencent</a></li>
<li><a href="https://www.stdaily.com/web/gdxw/2026-11/16/content_614064.html">腾讯混元Hy4 flash发布 单任务成本仅为Hy4二十分之一</a></li>

</ul>
</details>

**标签**: `#Tencent Hunyuan`, `#Hy4 flash`, `#Mixture-of-Experts`, `#long context`, `#LLM pricing`

---

<a id="item-tech-news-9"></a>
### [美与九国签署《旧金山宣言》协调保护 AI 供应链](https://www.state.gov/releases/office-of-the-spokesman/2026/11/the-san-francisco-declaration-on-the-secure-foundations-of-enduring-prosperity/) ⭐️ 7.0/10

11 月 15 日，美国与澳大利亚、印度、以色列、日本、韩国、卡塔尔、新加坡、阿联酋和英国签署《旧金山宣言》，确认经济安全是国家安全的基础，并将共同保护支撑超级智能（SI）供应链的敏感技术和关键基础设施。宣言提出设立五个工作组，分别聚焦创新政策框架、SI 在关键领域的应用、SI 全栈供应链协作、安全港与供应链安全枢纽，以及 SI 安全与韧性。现有信息只说明了签署方和拟设工作组，未披露具体技术清单、执行时间表或约束机制。

telegram · zaihuapd · 11月16日 10:40

**「背景」** 这份宣言在美国国务院经济事务副国务卿雅各布·赫尔伯格召集的“Pax Silica”创始人务虚会上签署；该会议是这一以保障关键技术和基础设施为目标的伙伴机制的阶段性活动。美国国务院在会后称，“Pax Silica”正进入新阶段，伙伴国已同意把相关技术和支撑基础设施的安全视为共同责任。

**「对企业的实际影响」** 由于该宣言目前只提出设立五个工作组——“创新政策框架、SI 在关键领域的应用、SI 全栈供应链协作、安全港与供应链安全枢纽、SI 安全与韧性”——并未附带约束性条款、合规期限或执行机制，相关十国的 AI 硬件、云服务与出口管制企业短期内现有合规义务不变。可跟踪的具体信号是这些工作组是否落地及其覆盖范围，尤其是“安全港与供应链安全枢纽”和“全栈供应链协作”两项，它们最可能牵动跨境设备与数据流动的实际安排。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.investing.com/news/world-news/us-nine-nations-sign-san-francisco-declaration-on-ai-security-5028448">U.S., nine nations sign San Francisco declaration on AI security By...</a></li>
<li><a href="https://www.ft.com/content/3c2197fc-9618-4838-91e6-522ce1a96a22?syn-25a6b1a6=1">US and allies sign accord to protect AI supply chains from China</a></li>
<li><a href="https://www.electronicsweekly.com/news/business/san-francisco-agreement-on-secure-supply-chains-signed-2026-11/">San Francisco Agreement on secure supply chains signed</a></li>
<li><a href="https://thenationaltelegraph.com/news/pax-silica-san-francisco-declaration-ai-supply-chain/">Ten Governments Sign an AI Supply-Chain Pact in San Francisco ...</a></li>

</ul>
</details>

**标签**: `#AI policy`, `#AI supply chain`, `#international agreement`, `#national security`, `#superintelligence`

---

<a id="item-tech-news-10"></a>
### [亚马逊称 Artex 驱动 AI 代理窃取 API 密钥](https://cybernews.com/security/amazon-autonomous-cybercrime-artex-framework/) ⭐️ 7.0/10

亚马逊称，攻击者使用开源渗透测试框架 Artex 驱动 AI 代理，从 LiteLLM、Dify 等公网暴露的 AI 应用窃取 API 密钥，验证其有效性后汇入共享池，再用这些密钥支付更多大模型调用。该活动据称始于 10 月 3 日，11 月 5 日被 AWS 的诱饵网络 MadPot 阻断。亚马逊以中等信心将活动归因于中国相关威胁组织，并表示并非所有被列入目标的应用都已失陷，已通知可能受影响的 AWS 客户。

telegram · zaihuapd · 11月16日 13:00

**「背景」** ARTEX 原本是一个合法的开源智能体式 AI 渗透测试框架，用于自动化攻击性安全测试；此次事件显示，其代理能力可被滥用为自动化的凭证窃取工具。AWS 安全博客称，MadPot 是由全球分布式诱饵传感器组成的网络，能伪装成暴露的服务并记录 AI 代理请求及其携带的操作记忆，亚马逊正是借此观察到相关活动。

**「影响与应对」** 对运行公网暴露的 LiteLLM、Dify 等 AI 应用的组织，直接后果是 API 密钥可能已被用于未授权模型调用，并被集中到共享池中以扩大后续调用；运维团队需要核查暴露实例并轮换可能泄露的密钥。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://aws.amazon.com/blogs/security/amazon-threat-intelligence-observes-threat-actors-running-cybercrime-campaigns-with-artex-ai-agents/">Amazon Threat Intelligence observes threat actors running ...</a></li>
<li><a href="https://securityarsenal.com/blog/artex-framework-abuse-detecting-and-defending-against-ai-driven-automated-attacks">ARTEX Framework Abuse: Detecting and Defending Against AI ...</a></li>

</ul>
</details>

**标签**: `#AI security`, `#API key theft`, `#autonomous agents`, `#AWS`, `#cybercrime`

---

<a id="item-tech-news-11"></a>
### [美国将先进 AI 芯片出口管制延伸至远程访问](https://www.reuters.com/legal/litigation/us-issues-rule-protect-advanced-ai-chips-being-accessed-remotely-2026-11-16/) ⭐️ 7.0/10

美国商务部 11 月 16 日发布一项临时最终规则，把针对先进 AI 芯片与服务器的出口管制从实物出口扩大到远程访问，意在阻止通过第三国数据中心绕开限制。据 The Verge 报道，规则还要求向印尼、马来西亚、新加坡、泰国和巴西再出口 AI 芯片时申请许可。来源称该规则由财政部和国家安全委员会主导起草，可能进一步收紧中国获取先进芯片的渠道。目前仅有简要转述，规则的具体适用范围、生效日期和许可细则尚未披露。

telegram · zaihuapd · 11月16日 14:44

**「背景」** 美国对先进 AI 芯片与服务器的出口管制此前主要覆盖受控物项的跨境出口和再出口，而境外通过数据中心远程调用受控算力并未被明确纳入同一管制框架。美国商务部工业与安全局（BIS）于 11 月 16 日发布的临时最终规则把这类远程访问也纳入管制，以封堵经由第三国数据中心规避限制的路径。

**「对运营与合规的影响」** 在新加坡、马来西亚等地运营数据中心或提供云端算力租赁的企业，向上述五国再出口受控 AI 芯片需先取得许可；此前被视为规避路径的境外机房远程提供算力方式也被纳入管制，合规审查范围需覆盖远程访问场景。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://media.bis.gov/sites/default/files/documents/BIS+Issues+Rule+Addressing+Remote+Access+to+American+Super+Intelligence+Technology.pdf">BUREAU OF INDUSTRY AND SECURITY - media.bis.gov</a></li>
<li><a href="https://www.bis.gov/press-release/bis-issues-rule-addressing-remote-access-american-super-intelligence-technology">www.bis.gov</a></li>

</ul>
</details>

**标签**: `#AI chips`, `#export controls`, `#semiconductors`, `#data centers`, `#tech policy`

---

## 财经新闻

<a id="item-finance-news-1"></a>
### [中国 10 月经济增长放缓：消费、工业与投资均不及预期](https://www.cnbc.com/2026/11/16/china-retail-sales-october-industrial-output-investment.html) ⭐️ 8.0/10

中国 10 月社会消费品零售总额同比仅增 0.4%，低于经济学家预期的 0.8%，并较 9 月 1.1%的六个月高点回落；规模以上工业增加值同比增长 4.8%，同样低于 5.3%的预期，较 9 月的 5.5%明显放缓。前 10 个月固定资产投资同比收缩 8.1%，弱于分析师预期的 7%降幅。

rss · CNBC Finance · 11月16日 03:53

**「背景」** 中国固定资产投资今年持续走弱：1 至 5 月同比下降 4.1%，到 10 月末累计降幅扩大到 8.1%；这一涵盖房地产、基建和设备采购的支出下滑，与已持续到第五年的房地产市场低迷相互强化，而后者被视为压低家庭财富、拖累消费的主要原因。

**「影响」** 中国家庭因楼市低迷持续侵蚀财富而抑制消费，出口企业则因增长愈发依赖外需而更易受全球人工智能资本开支回落和欧盟潜在贸易限制的冲击。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://economy.ac/news/2026/06/202606289352">China ’s Domestic Market Remains Stagnant Despite... — The Economy</a></li>

</ul>
</details>

**标签**: `#China economy`, `#industrial output`, `#retail sales`, `#fixed-asset investment`, `#youth unemployment`

---

<a id="item-finance-news-2"></a>
### [ETF 专家：英伟达动荡与国会变局或重塑 AI 交易](https://www.cnbc.com/2026/11/14/nvidia-ai-trade-data-centers-congress.html) ⭐️ 7.0/10

CNBC 的 ETF 专家称，英伟达 CEO 黄仁勋辞职后的动荡，加上民主党在 11 月 3 日选举后掌控国会、可能放缓数据中心建设，或使 AI 投资转向其他大型科技公司和芯片股。Yorkville Ives 随后将英伟达目标价从 300 美元下调至 225 美元，但维持买入评级；该股当周收于 162.85 美元。

rss · CNBC Finance · 11月16日 12:13

**「背景」** 据《纽约时报》报道，英伟达 CEO 黄仁勋于上周四辞职，此前其婚外情指控曝光；公司首席财务官科莱特·克雷斯暂代 CEO 职务。另在 11 月 3 日中期选举中，民主党赢得国会控制权，部分原因是选民反对 AI 数据中心，该党正计划推动针对 AI 和数据中心的立法及税收措施。

**「影响」** 据 CNBC 报道，Nvidia 的领导层危机正促使投资者转向 AMD、博通和台积电等其他芯片股，可能使这些竞争对手获得更多 AI 芯片业务与资金。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://finance.yahoo.com/technology/ai/articles/nvidia-ceo-jensen-huang-resigns-110116748.html">Nvidia CEO Jensen Huang Resigns — CFO Collette Kress in as...</a></li>
<li><a href="https://www.nytimes.com/2026/11/12/technology/nvidia-jensen-huang.html">Jensen Huang Resigns From Nvidia After Affairs - The New York...</a></li>
<li><a href="https://time.com/article/2026/11/04/midterm-elections-results-ai-industry-data-centers/">How AI Backlash Shaped the 2026 Midterms - TIME</a></li>
<li><a href="https://www.foley.com/insights/publications/2026/11/blue-wave-new-ai-rules-what-democratic-control-of-congress-means-for-ai-regulation/">Blue Wave, New AI Rules? What Democratic Control of Congress ...</a></li>
<li><a href="https://www.cnbc.com/2026/11/13/nvidia-jensen-huang-affairs-amd-broadcom-tsmc.html">Nvidia ’s turmoil is prompting a rotation across chip stocks.</a></li>
<li><a href="https://www.bloomberg.com/news/articles/2026-11-12/nvidia-turmoil-lifts-amd-broadcom-on-bets-for-business-gains">AMD , Broadcom Poised to Gain From Scandal Roiling Nvidia</a></li>

</ul>
</details>

**标签**: `#Nvidia`, `#AI trade`, `#ETFs`, `#data-center policy`, `#semiconductors`

---

<a id="item-finance-news-3"></a>
### [卢特尼克因家族公司与英伟达的关系面临利益冲突质疑](https://www.cnbc.com/2026/11/13/howard-lutnick-nvidia-jensen-huang-china-cantor-fitzgerald.html) ⭐️ 7.0/10

CNBC 报道，美国商务部长霍华德·卢特尼克因其儿子们领导的坎托·菲茨杰拉德与英伟达的持股和业务关系面临利益冲突质疑。证券申报文件显示，该机构报告的英伟达持股在 2025 年 9 月至 2026 年 3 月间下降 49%至 178 万股，市值从 6.52 亿美元降至 3.10 亿美元；坎托称这些持仓不重大，季度持仓文件中的头寸与客户互换交易有关。

rss · CNBC Finance · 11月16日 12:14

**「背景」** 英伟达 CEO 黄仁勋因婚外情曝光而辞职，其中一名女性被怀疑为中国间谍，此事令对华芯片出口管制成为焦点，也促使参议院要求黄仁勋与商务部长卢特尼克下月到场作证。是否将涉嫌转运英伟达芯片至中国的新加坡公司 Megaspeed 列入“实体清单”——即限制美国技术出口对象的名单，由商务部负责——已在特朗普政府内部引发公开分歧。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://edition.cnn.com/2026/11/16/tech/nvidia-sex-spies-serious-problems">Lies, spies and sex are just one part of the Nvidia story.</a></li>
<li><a href="https://www.nytimes.com/live/2026/11/12/business/nvidia-jensen-huang-resigns">Nvidia Updates: Huang ’s Resignation Reverberates Through...</a></li>
<li><a href="https://www.bbc.com/news/articles/cry49plv8v3go">Elon Musk joins &#x27;Bring Jensen Back&#x27; campaign to reinstate the...</a></li>

</ul>
</details>

**标签**: `#Nvidia`, `#US export controls`, `#conflict of interest`, `#Cantor Fitzgerald`, `#semiconductors`

---

<a id="item-finance-news-4"></a>
### [英特尔及 CEO 陈立武因 PC 需求与库存披露遭股东集体诉讼](https://www.investing.com/news/stock-market-news/intel-sued-by-shareholders-following-29-stock-plunge-5028171) ⭐️ 7.0/10

英特尔及其 CEO 陈立武、CFO 津斯纳被股东集体诉讼，原告指控公司在 2026 年 10 月 29 日发布不及预期的第四季度营收和利润预测前，隐瞒了 PC 需求疲软和库存积压的影响。诉讼由一家密歇根州养老基金牵头，上周五在圣何塞联邦法院提起，代表 2026 年 7 月 23 日至 10 月 29 日买入股票的投资者；预测发布次日英特尔股价下跌 28.6%，市值蒸发约 1400 亿美元。

telegram · zaihuapd · 11月16日 11:10

**「背景」** 陈立武自 2025 年起担任英特尔首席执行官，此前长期在风险投资领域任职，是此次证券集体诉讼的个人被告之一。该案由投资者发起，代表在 2026 年 7 月 23 日至 10 月 29 日期间买入英特尔股票的股东索赔，诉由是公司在这段时间内隐瞒了个人电脑（PC）需求疲软的情况。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/Lip-Bu_Tan">Lip - Bu Tan - Wikipedia</a></li>
<li><a href="https://wccftech.com/intel-ceo-lip-bu-tan-named-defendant-class-action-lawsuit-pc-sales-slowdown/">Intel CEO Lip - Bu Tan Named As Defendant In New Class - Action ...</a></li>

</ul>
</details>

**标签**: `#Intel`, `#shareholder lawsuit`, `#semiconductor`, `#stock plunge`, `#corporate disclosure`

---