---
layout: default
title: "Horizon Summary: 2026-11-11 (ZH)"
date: 2026-11-11
lang: zh
---

> 从 47 条内容中筛选出 15 条重要资讯。

---

**科技新闻**
1. [用电压毛刺解锁矿卡上的 A100 能力](#item-tech-news-1) ⭐️ 8.0/10
2. [AWS 推出官方本地模拟器 aws-emulator](#item-tech-news-2) ⭐️ 8.0/10
3. [误报烟雾警报险些关停 Jane Street 纽约唯一数据中心](#item-tech-news-3) ⭐️ 7.0/10
4. [《华尔街日报》称英伟达准备罢免 CEO 黄仁勋，细节未证实](#item-tech-news-4) ⭐️ 7.0/10
5. [Python 社区悼念《Zen of Python》作者 Tim Peters](#item-tech-news-5) ⭐️ 7.0/10
6. [博客探讨用线性规划做权重编辑](#item-tech-news-6) ⭐️ 7.0/10
7. [Google 发布 Gemini Decision 1 决策模型 API](#item-tech-news-7) ⭐️ 7.0/10
8. [Anthropic 路演视频披露 Claude 多芯片训练策略](#item-tech-news-8) ⭐️ 7.0/10
9. [论文主张 AI slop 是社区的社会判断](#item-tech-news-9) ⭐️ 7.0/10
10. [The Information 调查称约 24 万颗英伟达 H100/H200 经第三方渠道入华](#item-tech-news-10) ⭐️ 7.0/10

**科技博客**
1. [vLLM 编码器解耦：EPD 多模态服务进展](#item-tech-blog-1) ⭐️ 8.0/10
2. [AI 时代，胶水工作依然有害](#item-tech-blog-2) ⭐️ 5.0/10

**财经新闻**
1. [美联储古尔斯比称 10 月通胀报告“近乎令人不安”](#item-finance-news-1) ⭐️ 8.0/10
2. [离岸信托收益征税过渡期结束，累计申报个税超 1600 亿元](#item-finance-news-2) ⭐️ 8.0/10
3. [美 FCC 批准 SpaceX 收购全美 800 兆赫兹频谱牌照](#item-finance-news-3) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [用电压毛刺解锁矿卡上的 A100 能力](https://blog.kate.land/posts/using-voltage-glitching-to-unlock-the-a100/) ⭐️ 8.0/10

一篇博客文章记录了作者用电压毛刺（voltage glitching）对 NVIDIA 矿卡上的片上熔丝动手，从而“解锁”出 A100 级别的能力。据评论区读者核对，这次的对象是 8GB 显存的 CMP 型号，而非此前被证实存在 80GB 隐藏显存的 10GB 版本，这让结果更显意外。这是爱好者自行逆向的个案，不是 NVIDIA 官方支持的功能，也无独立第三方复现或性能数据佐证；文章的完整技术细节与成功条件需以原文为准。

hackernews · lae · 11月11日 10:48 · [社区讨论](https://news.ycombinator.com/item?id=50451903)

**「背景：同一 GA100 芯片与熔丝分区」** NVIDIA 的 CMP 170HX 挖矿卡与数据中心 A100 基于同一颗 GA100 芯片；据文章说明，NVIDIA 通过芯片上的熔丝（fuse）控制器关闭部分硬件功能，从而用同一晶圆产出不同产品。所谓电压毛刺（voltage glitching）属于故障注入：在启动或读取熔丝时短暂扰动供电，使芯片误判这些熔丝配置，这正是本次解锁尝试的切入点。

**「对矿卡持有者的实际影响」** 对仍持有 CMP 170HX 的读者，这项电压毛刺尝试提供了一条绕过熔断、恢复 A100 级硬件资源的路径，但评论者将其视为比软件解锁风险更高的硬件改动。已有软件方案可把 GA100 矿卡开到 64 GB 显存和 74 个 SM，甚至改刷 300 W VBIOS；不过有评论者报告 80 GB 版本在 CUDA 中仍未完全可用，复现前应核对具体型号、显存版本和驱动兼容性。

**「社区讨论」** 评论者对熔丝为何被烧断存在分歧：一位读者（amelius）认为更可能是 A100 晶圆存在过多制造缺陷、只能降级为矿卡出售，因为数据中心产品的利润更高；另一位（notenchange）则已花两周尝试纯软件方式解锁 CMP 170HX 的 80GB 显存但未成功，并表示不敢冒险走烧熔丝这条路。另有读者提出用外接 PCIe 转接板加独立电源、让主机保持运行来加快反复尝试，也有人提到这类卡价格已从约 200 美元涨到 1000 美元。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://blog.kate.land/posts/using-voltage-glitching-to-unlock-the-a100/">Using voltage glitching to unleash the A 100 in my mining card</a></li>
<li><a href="https://bytwork.com/en/articles/cmp-170hx-unlock">Unlocking the CMP 170 HX : How to get 64/80 GB of memory?</a></li>
<li><a href="https://gist.github.com/ropuls/d2978531ba3a1a183e70f62f3de2eb84">2x CMP 170 HX for LLM inference: unlock , cross-root P2P, serving...</a></li>

</ul>
</details>

**标签**: `#voltage glitching`, `#GPU hardware hacking`, `#NVIDIA A100`, `#mining cards`, `#hardware reverse engineering`

---

<a id="item-tech-news-2"></a>
### [AWS 推出官方本地模拟器 aws-emulator](https://simonwillison.net/2026/Nov/11/aws-emulator/) ⭐️ 8.0/10

AWS 已在 GitHub 发布官方本地模拟器 aws-emulator，让开发者在无需配置付费 API 密钥的情况下，对多项 AWS 服务的本地克隆运行测试。该项目用 Rust 编写，前三周录得 29,684 次提交，开发过程涉及大量 AI agent。当前在 macOS 和 Windows 上运行仍需要 Docker，作者希望未来能改为可直接下载的单二进制文件。

rss · Simon Willison · 11月11日 21:18

**「背景」** 在云服务集成测试中，开发者通常需要为 AWS 各服务配置真实的 API 访问，这会产生费用并依赖远端环境。aws-emulator 的定位是在本地运行这些服务的克隆，使测试无需为调用申请付费 API 密钥；西蒙·威利森将其描述为 AWS 终于推出的官方本地模拟器。

**「对开发者的实际影响」** 对需要在 CI 或本地跑集成测试的开发者来说，这省去了为测试专门申请付费 API key 和真实云资源的步骤；但在 macOS 和 Windows 上它目前依赖 Docker，无法作为单一下载即用的二进制嵌入多语言测试流程。更需注意的是，安全文档明确说明不能用它验证 IAM 策略与权限边界、资源型策略（如存储桶策略）、KMS 密钥策略以及跨账户或跨区域访问，因为模拟器不会像 AWS 那样判定这些控制，也不会拒绝用其自身密钥签名的请求，相关权限结论仍须在真实环境中验证。

**「社区讨论」** HN 评论中，有人质疑该项目究竟是开发练习，还是会被正式发布并长期维护的产品，并提到 Floci 和 Testcontainers 作为替代方案；另有评论引用安全页面指出，不应使用该模拟器测试 IAM 策略、资源策略、KMS 密钥策略以及跨账户或跨区域访问等安全控制。

**标签**: `#AWS`, `#local emulator`, `#software testing`, `#Rust`, `#AI agents`

---

<a id="item-tech-news-3"></a>
### [误报烟雾警报险些关停 Jane Street 纽约唯一数据中心](https://michael.bacarella.com/2026/11/10/false-smoke-alarm-jane-street-datacenter/) ⭐️ 7.0/10

一篇第一人称事故叙述称，一次误报的烟雾警报几乎迫使 Jane Street 关闭其纽约市唯一的数据中心。该叙述聚焦误报如何升级为接近停机的运维事件，并列出警报与灭火系统行为、紧急断电（EPO）预期、现场值守和远程访问限制等具体教训。现有材料未提供停机时长、设备损失或正式事后报告的细节。

hackernews · mbac32768 · 11月11日 16:38 · [社区讨论](https://news.ycombinator.com/item?id=50455394)

**「背景」** 这类误报险情的核心在于报警、灭火与断电逻辑之间的联动；问题并不在烟雾本身。如果烟雾探测直接触发紧急断电（EPO），一次传感器误判就可能让整座机房失去电力。评论中的工程师还指出，机房内是否设置实体 EPO 按钮，以及是否将 EPO 与烟雾报警联锁，是此类事件中需要预先明确的设计条件。

**「影响」** 对 Jane Street 和依赖其纽约唯一站点的业务而言，直接后果是必须把“误报导致停机”纳入 EPO、灭火与制冷联动以及现场响应演练；叙述特别指出远程访问存在限制，因此现场人员能否及时处置会直接影响可用性。

**「社区讨论」** 评论者对 EPO 设计存在分歧：rdl 质疑机房内为何没有至少一个实体紧急断电按钮，以及为何未把 EPO 与烟雾警报联动；rainbowzootsuit 则根据自身运维经验表示，其数据大厅的序列操作特意不在烟雾报警时关闭 CRAC，以避免误报放大停机风险。另有评论者分享了因住得离机房近而被同事当作紧急现场联络人的经历。

**标签**: `#datacenter-operations`, `#incident-response`, `#site-reliability`, `#fire-suppression`, `#infrastructure`

---

<a id="item-tech-news-4"></a>
### [《华尔街日报》称英伟达准备罢免 CEO 黄仁勋，细节未证实](https://www.wsj.com/business/nvidia-is-preparing-to-oust-nvidia-ceo-jensen-huang-30f421ad) ⭐️ 7.0/10

《华尔街日报》一则标题称，英伟达正准备罢免 CEO 黄仁勋；若属实，这将是这家 AI 芯片核心公司最高管理层的重大变动。但该条目没有提供文章正文，也没有董事会决议、时间表、接任安排或公司回应等细节，因此无法确认“准备罢免”是已启动的程序还是尚未证实的报道。现有材料只能确认标题本身，黄仁勋是否留任、由谁接任以及对公司运营的影响均无可核实信息。

hackernews · jbredeche · 11月11日 22:31 · [社区讨论](https://news.ycombinator.com/item?id=50459703)

**「背景」** 这则报道出现前，事态已发酵数日：据 AP 报道，英伟达因有消息称黄仁勋成为“外国情报行动的目标”而启动内部调查，股价随之下跌约 5%（tool-1-2）；黄仁勋则在一封信中重申自己对公司的承诺，称希望能重新赢回同事和员工的信任（tool-1-3）。WSJ 的最新报道进一步称，董事会正准备让这位创始人兼首席执行官去职，起因是他有过两段婚外情，其中一段涉及一名疑似中国间谍（tool-1-1）。

**「评论讨论」** 评论者中有人指出，创始人领导的公司在双重股权结构下通常让创始人握有不成比例投票权，罢免会非常困难。另一些人则围绕未经证实的私人关系和对华芯片销售指控猜测原因；这些均为个人意见，未提供可核实证据。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.wsj.com/business/nvidia-is-preparing-to-oust-nvidia-ceo-jensen-huang-30f421ad">Exclusive | Nvidia is Preparing to Oust Nvidia CEO Jensen Huang -...</a></li>
<li><a href="https://apnews.com/article/nvidia-jensen-huang-spy-china-63531dec0fe5c145afaac94dde31d478">Nvidia shares slide on internal investigation into CEO Jensen ...</a></li>
<li><a href="https://www.theguardian.com/technology/2026/nov/09/jensen-huang-image-nvidia">Jensen Huang ’s image has been shattered. Could he be pushed out...</a></li>

</ul>
</details>

**标签**: `#Nvidia`, `#Jensen Huang`, `#corporate governance`, `#AI hardware`, `#semiconductor industry`

---

<a id="item-tech-news-5"></a>
### [Python 社区悼念《Zen of Python》作者 Tim Peters](https://discuss.python.org/t/in-memoriam-tim-peters-1952-2026/110028) ⭐️ 7.0/10

Python 社区正在悼念 Tim Peters（1952–2026）。据讨论中引述的内容，他是《Zen of Python》的作者——这段以“Beautiful is better than ugly.”开头的准则至今仍可通过 \`python -c &quot;import this&quot;\` 从 CPython 中打印出来——同时也是长期参与 Python 发展的贡献者。评论者提到，他与 Gary Robinson（以及 Robert Woodhead 等人）把 pg 的《A Plan for Spam》一文中的思路实现为 SpamBayes 程序，并参与了《Python Cookbook》第二版的写作。目前可见的信息来自社区讣告帖与讨论，除此之外没有更多细节。

hackernews · ayhanfuat · 11月11日 07:03 · [社区讨论](https://news.ycombinator.com/item?id=50450488)

**「背景」** 对许多 Python 使用者来说，Tim Peters 的名字首先与《Python 之禅》联系在一起：在 Python 解释器中运行 \`import this\` 会打印这段由他署名的格言，它长期被开发者当作理解 Python 设计取舍的入门材料。社区评论还提到，他与 Gary Robinson 等人将垃圾邮件过滤方案发展成 SpamBayes 项目，并参与《Python Cookbook》第二版的写作。

**「对开发者的意义」** 对普通 Python 使用者而言，最直接的接触点仍是内置的 \`import this\`：运行它就会输出 Tim Peters 写下的这段准则，因此新老开发者都会继续通过这一复活节彩蛋读到他的文字。

**「社区回忆」** 评论者多以自己的经历回忆他：有人称他是自己持续阅读 python-dev 与 bugs.python.org 时最喜爱的一位，并提到他在《Python Cookbook》第二版中“We read Knuth so you don&\#x27;t have to”式的讲解；也有人（ofek）表示他总乐于推动讨论，几乎每次交流都能带来新的理解，比如让人第一次意识到投票系统有如此多的类型与研究。另有评论（leoc）补充了他在 SpamBayes 项目中与 Gary Robinson、Robert Woodhead 的合作关系，属于参与者的事后追述。

**标签**: `#Python`, `#Tim Peters`, `#open-source community`, `#obituary`

---

<a id="item-tech-news-6"></a>
### [博客探讨用线性规划做权重编辑](https://nathan.rs/posts/weight-space-lp/) ⭐️ 7.0/10

一篇博客分析提出，线性规划求解器或可成为神经网络权重空间编辑的工具，把“修改某些权重、保留其他行为”的诉求表达为线性约束下的优化问题。该文讨论的是方法可行性，而非已发布的软件版本或基准结果；目前没有提供基准或独立验证，因此仍属探索性主张。对 AI/ML 研究者来说，值得关注的是它尝试用显式约束优化补充启发式权重编辑。

hackernews · emschwartz · 11月11日 12:30 · [社区讨论](https://news.ycombinator.com/item?id=50452655)

**「背景」** 这里说的 weight-space programming，指由通用大模型直接读取并改写另一个神经网络的权重，而不经过梯度下降或训练循环。Nathan Barry 的文章是对 MIT CSAIL 近期《Sparks of Weight-Space Programming》的延伸分析：后者用 GPT-6 Astra 直接编辑小型网络权重，前者则讨论能否把其中的手工搜索改写成线性规划。

**「影响」** 对想复现或采用该方法的开发者，直接限制是缺少基准和独立验证结果，当前只能把它视为方法提案，无法据此判断实际编辑效果或可靠性。

**「社区讨论」** 评论者提出了几种落地路径：用配对样本收集行为方向，再通过线性规划寻找稀疏权重编辑以做权重空间蒸馏；或把这类约束放进训练正则化，乃至用传统数学规划替代依赖奖励/惩罚的 RL 循环。也有评论认为，若 LP 求解器能辅助类似 Astra 的权重编辑流程，可能提升其效果；这些均为评论者观点，帖子未给出验证。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/Weight-space_programming">Weight-space programming - Wikipedia</a></li>
<li><a href="https://x.com/nathanrs/status/2119845893755351417">Nathan Barry on X: &quot;In MIT CSAIL&#x27;s recent &quot;Sparks of Weight ...</a></li>

</ul>
</details>

**标签**: `#machine-learning`, `#linear-programming`, `#weight-editing`, `#optimization`, `#model-interpretation`

---

<a id="item-tech-news-7"></a>
### [Google 发布 Gemini Decision 1 决策模型 API](https://blog.google/innovation-and-ai/technology/developers-tools/gemini-decisions-api/) ⭐️ 7.0/10

Google 发布了名为 Gemini Decision 1 的决策模型 API，由此加入 Jev 和 OpenAI 所在的决策模型类别。它支持与 Jev 相同的三类问题：是/否问题（沿用 Jev 的“Noul”一词）、多选问题和 rubric 评分；定价为每百万输入 token 10 美分、输出免费，与 GPT-6 Luna 决策模型持平，而 Jev 以每百万 4.2 美分更便宜。与仅支持文本和 JSON 的 Jev、支持文本和图像的 OpenAI 不同，Gemini Decision 1 支持文本、图像、音频、视频和 PDF 输入。Simon Willison 用一段视频做了实测，该模型对是/否问题返回的是连续概率（robot 0.923、dragon 0.0498、usa 0.923、france 0.083），而非 Jev 和 OpenAI 那样的 1.0 或 0.0；这属于单次测试结果，并非独立评测。

hackernews · iamdelirium · 11月11日 18:32 · [社区讨论](https://news.ycombinator.com/item?id=50456791)

**「背景」** 所谓决策模型 API，并不是让模型生成一段自由文本，而是直接回答“是/否”、在多个选项中择一，或按评分标准打分，并对是/否问题返回概率。Google 此次是在 Jev 和 OpenAI 已推出同类 API 之后进入该类别；Jev 仅支持文本和 JSON，OpenAI 的对应模型可处理文本与图像，而 Gemini Decision 1 把输入扩展到音频、视频和 PDF。

**「对开发者的影响」** 对需要处理音视频或 PDF 的开发者，Decision 1 可直接把媒体作为输入做是/否、选择或评分判断，省去先转录再交给纯文本决策模型的一步；但其是/否结果是连续概率而非 Jev 和 OpenAI 那样的 0/1，现有按精确 0/1 分支的代码需改为阈值判断。其标价为每百万输入 token 10 美分、输出免费，仍高于 Jev 的 4.2 美分。

**「社区讨论」** 评论者最关心概率从何而来：eminence32 指出，语法约束的输出无法得到概率，并追问这些模型究竟如何计算概率；kodoman 则询问是否已有人在 Pi 这类编码框架中使用决策模型。成本与实际用途也是讨论焦点，2001zhaozhao 估算，传入 100K token 上下文再问上百个问题，总费用约等于一次 Google 搜索 API 调用；waximabbax 认为 Gemini 虽比同类的其他决策模型贵，但音频和视频输入在特定场景下可能非常有用。另有 theanonymousone 称，除 Jev 之外，respan/span-02 是其用过最好的决策模型（据称基于 Gemma4 26A4 微调）。

**标签**: `#Gemini API`, `#decision models`, `#AI developer tools`, `#Google AI`, `#model pricing`

---

<a id="item-tech-news-8"></a>
### [Anthropic 路演视频披露 Claude 多芯片训练策略](https://simonwillison.net/2026/Nov/11/anthropic-ipo-roadshow/) ⭐️ 7.0/10

Anthropic 的 IPO 路演视频披露了此前未公开的算力细节：Claude 目前跨 AWS Trainium、Google TPU、NVIDIA GPU 和 AMD GPU 四类芯片训练和推理；据 Simon Willison 从无官方文字稿的视频中提取的转录，公司称这源于早年押注的多芯片策略。视频中，联合创始人 Tom Brown 表示，今年首次接入 AMD GPU 时，公司让 Mythos 尝试，结果它在三天内让 Claude 跑在 AMD 上，基本无需人工干预，Claude 移植或编写了近 100% 的 kernel。公司还把“计算乘数”的发现速度列为算力优势的第二来源，称总有效算力是物理容量与计算乘数的乘积，例如 4 倍乘数可将同一模型的训练需求从 100 单位降到 25 单位，并称这些乘数会叠加、未来可能由 Claude 自行发现，以接近递归自我改进。

rss · Simon Willison · 11月11日 15:11

**「多芯片策略与先前线索」** 所谓多芯片策略，是让同一套 Claude 模型在 AWS Trainium、Google TPU、NVIDIA GPU、AMD GPU 等不同加速器上分别维护训练与推理软件栈；每类芯片都需要定制适配，工程成本很高。Anthropic 在 9 月发布的三起问题复盘中曾提到，部分 bug 仅影响其 TPU 部署，这已间接显示其推理环境并非单一芯片；此次路演视频则集中披露了跨这四类芯片训练与服务 Claude 的方案。

**「影响」** 对使用 Claude 的开发者而言，这一披露表明同一服务可能跨 AWS、Google、NVIDIA 和 AMD 后端运行；但公司未披露各芯片上的性能、成本或可用性差异，开发者目前无法据此判断延迟和价格是否受后端硬件影响。

**标签**: `#Anthropic`, `#AI infrastructure`, `#multi-chip strategy`, `#IPO`, `#hardware`

---

<a id="item-tech-news-9"></a>
### [论文主张 AI slop 是社区的社会判断](https://www.reddit.com/r/MachineLearning/comments/1xtour7/ai_slop_is_a_social_judgement_r/) ⭐️ 7.0/10

r/MachineLearning 上的一则链接帖指向《Nature Human Behaviour》论文，该论文主张“AI slop”不是能从内容本身检测出的属性，而是社区判定某些 AI 生成内容不受欢迎时形成的社会判断。作者认为，只有把 slop 作为社会判断来研究，才能对其进行测量和治理。该帖子只给出这一概念框架，未交代论文的方法、数据或实证结果，因此相关结论仍属论文主张，而非可独立验证的技术发现。

reddit · r/MachineLearning · /u/learning\_by\_looking · 11月11日 18:03

**「背景：从内容属性到社区判断」** “AI slop”此前通常被理解为能从内容本身辨认出来的低质 AI 生成物，而这篇文章的论点正是反过来：所谓 slop 并非藏在文本里的某种特征。论文提出，只有当某个社区认定某些 AI 生成内容不受欢迎时，slop 才作为社会判断成立。按这一框架，研究重点便从检测内容特征转向观察社区如何划界，作者称这是让该现象可测量、可治理的前提。

**「对治理与检测的含义」** 按该论文的框架，「AI slop」的治理对象不再是内容本身可检测的特征，而是社区作出的判定；这意味着内容审核与「slop 检测」基准需要以社区标注的负面判断作为标签，而不只是训练分类器识别某种文体特征。维基百科等既有定义把 slop 描述为「被认为」缺乏投入、质量或意义、且通常高产量生成的 AI 内容，这与论文的社区相对视角并不完全冲突，但也说明仅凭内容侧特征难以稳定界定。该帖未提供论文的方法、数据或结论细节，因此这一治理路径如何测量、能否落地，尚无法从现有材料核实。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/AI_slop">AI slop - Wikipedia</a></li>

</ul>
</details>

**标签**: `#AI slop`, `#AI-generated content`, `#social science research`, `#content governance`, `#machine learning community`

---

<a id="item-tech-news-10"></a>
### [The Information 调查称约 24 万颗英伟达 H100/H200 经第三方渠道入华](https://www.tomshardware.com/tech-industry/policy/alice-huang-reportedly-instrumental-in-securing-over-usd7-5-billion-of-nvidia-ai-gpu-imports-during-three-year-relationship-with-jensen-huang-helped-move-240-000-banned-chips-into-china-mostly-h100-and-h200) ⭐️ 7.0/10

《The Information》的一项调查称，黄乐（Alice Huang）借助与英伟达 CEO 黄仁勋的关系，在三年内协助约 24 万颗受美国出口管制的英伟达 AI 芯片进入中国，其中以 H100、H200 为主，涉及进口金额约 75 亿美元。报道点名上海世纪利通与新加坡 Megaspeed 等公司参与相关流转。上述内容来自 The Information 调查及 Tom&\#x27;s Hardware 的转述，本条目仅为简要概述，未提供完整证据链，具体规模与参与方仍属调查指控而非已确认事实。材料中也没有英伟达或涉事公司的回应。

telegram · zaihuapd · 11月11日 14:41

**「背景」** 美国对华先进计算芯片出口管制对英伟达 H100、H200 等数据中心 GPU 设有许可要求，使这些芯片无法通过常规渠道直接进入中国市场。此类高价值加速卡由此容易转入经第三地转运、由中间商牵线的灰色供应链，具体交易是否合规取决于运输路径、申报与最终用途。

**「合规影响」** 若调查结论被监管机构采纳，被点名的第三方渠道商及其下游买家可能成为美国出口管制执法的审查对象，通过非官方渠道采购 H100/H200 的企业需要额外核查最终用途与转售链条，并承担供货突然中断的合规风险。

**标签**: `#Nvidia`, `#AI芯片出口管制`, `#H100/H200`, `#供应链合规`, `#行业调查`

---

## 科技博客

<a id="item-tech-blog-1"></a>
### [vLLM 编码器解耦：EPD 多模态服务进展](https://vllm.ai/blog/2026-11-11-encoder-disaggregation-epd) ⭐️ 8.0/10

rss · vLLM Blog · 11月11日 00:00

**「背景」** 多模态推理先编码图像、视频帧和音频，编码负载独立于预填充/解码需求变化；作者介绍 vLLM 的 EPD 解耦，把三阶段拆成可独立扩缩的实例，并称 main 已支持 DeepSeek V4.1 Flash 的 metadata-only EPD。

**「方案」** 关键机制是让编码器只做编码，下游用 metadata-only 请求按编码器发布的布局元数据重建占位符，再经 EC connector 取得嵌入，避免重复预处理媒体。编码实例走专用 MMEncoderModelRunner 并支持 ViT CUDA Graph，裁剪的 Kimi-K3 checkpoint 权重加载从 683 秒降至 0.31 秒；跨节点嵌入由 NIXL+CPU EC 或 Mooncake EC 传输，输出宽度按模态实测。Mooncake Store 支持跨编码器复用：6 张 H20、InternVL3\_5-38B-HF、2E+4PD 的重分配实验中，512 张图的重复编码从 512 降到 0，TTFT p50/p90 从 1.209/1.656 秒降至 0.819/0.891 秒，TPOT 基本不变，但作者称这是最佳案例。编排端，Python proxy 降低 JSON 和流式响应开销，vLLM Router、SMG 与 llm-d 负责路由和独立扩缩；DeepSeek V4.1 Flash 在 GB200 上计入全部 12 张 EPD GPU 后，并发 64–128 时每 GPU 吞吐仍比 8 张 GPU 的 PD 基线高 6.6–9.5%、P90 TTFT 低 44–47%，但并发 16 时更差、32 时约打平。作者也承认共享复用暂限于图像、MRv2、编码器 TP=1 且不支持动态 LoRA，并发冷请求仍可能重复计算；音频 metadata-only 评测的准确率从 75.90% 变为 75.65%，差异尚待调查。

**「启示」** 因此，EPD 的关键不是“拆开”本身，而是按阶段需求独立分配资源并避免重复工作；它已有可测收益，但收益随并发和缓存命中率变化，仍需按工作负载验证。

**标签**: `#multimodal serving`, `#encoder disaggregation`, `#vLLM`, `#remote embedding transfer`, `#GPU inference performance`

---

<a id="item-tech-blog-2"></a>
### [AI 时代，胶水工作依然有害](https://seangoedecke.com/glue-work-is-still-harmful-in-the-age-of-ai/) ⭐️ 5.0/10

rss · Sean Goedecke · 11月11日 00:00

**「背景」** 胶水工作指正式流程之外那些软性的“非技术”活：撮合团队沟通、写报告、更新文档、带新人，通常得靠某个人自愿承担才能完成。作者 Sean Goedecke 认为，只能靠无偿牺牲维持的流程就该淘汰；LLM 接管大部分编码之后，这一点并未改变。

**「方案」** 他给出四个理由，认为胶水工作在 2020 年代其实更不重要：AI agent 的放大效应让单个工程师就能接手过去需要小团队的项目，启动会、状态会、转发内部进展等协调需求随之减少；ZIRP 结束后，那些影响力被高估、动辄否决项目的“守门人”被挤出行业或被迫收敛；公司少招初级员工，不需要有人悄悄自愿去带新人；他称为“证明我在干活”的只写报告，现在用 LLM 就能快速产出，反正本来也没人读。

但他反对把胶水工作整体外包给模型：报告可以自动生成，人际沟通不行。查项目进度、回别人的消息都该自己写，让别人去跟你的 Claude Opus 实例对话，是最快毁掉同事关系的方式。他的建议与 2024 年类似：不要变成“那个做胶水工作的人”，让坏流程失败以便被改变，但愿意做少量真正能推进项目的战术性协调，大部分时间留给代码和驱动 AI agent 对齐公司价值。

**「启示」** 作者的结论是，LLM 消除的是胶水工作中的文书与协调负担，而非人际沟通本身；因此胶水工作对公司比 2010 年代更不重要，工程师的价值更应体现在代码和指挥 AI agent 上，而不是无偿的协调劳动。

**标签**: `#glue work`, `#AI coding agents`, `#LLM communication`, `#software engineering culture`, `#coordination`

---

## 财经新闻

<a id="item-finance-news-1"></a>
### [美联储古尔斯比称 10 月通胀报告“近乎令人不安”](https://www.cnbc.com/2026/11/11/goolsbee-october-inflation-fed-rates-disturbing-distressing.html) ⭐️ 8.0/10

芝加哥联储行长古尔斯比称 10 月通胀报告“近乎令人不安”，该月 CPI 经季节调整环比上涨 0.4%，高于经济学家预期，且为连续第三个月大幅上涨；美联储正在权衡 12 月是否加息及加息幅度。

rss · CNBC Finance · 11月11日 16:49

**「背景」** 美联储 9 月已加息 25 个基点至 3.75%-4%区间，10 月按兵不动，12 月会议将决定下一步利率行动。

**「市场影响」** CME FedWatch 显示，利率期货一致预期 12 月加息，押注 50 个基点的概率为 15%，到 1 月利率升至 4.25%-4.5%的概率为 60%，反映投资者对短期借贷成本上升的预期。

**标签**: `#Federal Reserve`, `#inflation`, `#interest rates`, `#monetary policy`, `#CPI`

---

<a id="item-finance-news-2"></a>
### [离岸信托收益征税过渡期结束，累计申报个税超 1600 亿元](https://www.news.cn/20261111/9bcce99c779b4a6197ff45bbbc3e4c50/c.html) ⭐️ 8.0/10

中国国家税务总局 11 月 11 日表示，对离岸信托收益征税的 90 天过渡期已结束，期内累计申报个人所得税超过 1600 亿元人民币，其中 10 月当月入库超过 1200 亿元；税务总局称，这推动 10 月全国个人所得税收入同比增长近 90%。

telegram · zaihuapd · 11月11日 10:35

**「背景」** 离岸信托指在境外设立的信托安排。2026 年 7 月 24 日，财政部、税务总局公告规定，在 90 天过渡期内完成申报缴税可免收滞纳金；过渡期结束后，未主动申报或申报不实的纳税人将被督促补缴并加收滞纳金，仍不改正的将依法立案稽查。

**「影响」** 未主动申报或申报不实的离岸信托受益人将面临补缴税款、加收滞纳金乃至立案稽查，直接影响其境外信托资产的合规安排。

**标签**: `#offshore trusts`, `#personal income tax`, `#tax enforcement`, `#China fiscal policy`, `#high-net-worth taxation`

---

<a id="item-finance-news-3"></a>
### [美 FCC 批准 SpaceX 收购全美 800 兆赫兹频谱牌照](https://wap.cj.sina.cn/7x24/5206981) ⭐️ 7.0/10

美国联邦通信委员会（FCC）批准 SpaceX 从 Grain Management 收购 546 组成对 800 兆赫兹频谱牌照，覆盖近乎全部美国人口；交易完成后，SpaceX 在各覆盖区域的频谱资源最高可达 89 兆赫兹。该频段属低频段，信号穿墙能力强，几乎适配所有智能手机；Verizon、AT&amp;T 和 T-Mobile 目前均拒绝 SpaceX 接入其网络。

telegram · zaihuapd · 11月11日 02:14

**「背景」** 美国联邦通信委员会（FCC）是监管美国无线电频率使用的独立联邦机构，频谱牌照的转让通常需要其批准。

**「影响」** 这批低频牌照几乎适配所有智能手机，但 Verizon、AT&amp;T 和 T-Mobile 均拒绝让 SpaceX 接入其网络，因此 SpaceX 若要使用这些频谱，就需自建网络；这也意味着美国手机用户未来可能多出一个潜在的网络服务选择。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/Federal_Communications_Commission">Federal Communications Commission - Wikipedia</a></li>

</ul>
</details>

**标签**: `#SpaceX`, `#FCC`, `#spectrum licenses`, `#US telecom`, `#regulatory approval`

---