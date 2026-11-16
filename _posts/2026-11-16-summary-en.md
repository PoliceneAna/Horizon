---
layout: default
title: "Horizon Summary: 2026-11-16 (EN)"
date: 2026-11-16
lang: en
---

> From 44 items, 15 important content pieces were selected

---

**Technology News**
1. [vLLM v0.34.0 ships extensible KV cache by default and removes Model Runner V1](#item-tech-news-1) ⭐️ 8.0/10
2. [Alibaba launches Qwen4-Max, a 2.4T-parameter sparse MoE flagship](#item-tech-news-2) ⭐️ 8.0/10
3. [Carnegie Mellon launches free full-semester CS lectures on YouTube](#item-tech-news-3) ⭐️ 7.0/10
4. [Jiff 1.0: A New Datetime Library for Rust](#item-tech-news-4) ⭐️ 7.0/10
5. [Microsoft traces major email outage to defect in July fix](#item-tech-news-5) ⭐️ 7.0/10
6. [Marimba reuses a frozen ASR encoder for calibrated speech queries](#item-tech-news-6) ⭐️ 7.0/10
7. [duetto steers Anticipatory Music Transformer at sampling time for live jazz](#item-tech-news-7) ⭐️ 7.0/10
8. [Tencent Hunyuan launches Hy4 flash MoE with low-cost 1M context](#item-tech-news-8) ⭐️ 7.0/10
9. [US and Nine Countries Sign San Francisco Declaration on AI Supply Chains](#item-tech-news-9) ⭐️ 7.0/10
10. [Amazon says Artex-driven AI agents stole API keys to fund model calls](#item-tech-news-10) ⭐️ 7.0/10
11. [US extends AI chip export controls to remote access](#item-tech-news-11) ⭐️ 7.0/10

**Financial News**
1. [China&\#x27;s October retail sales, industrial output and investment all miss forecasts](#item-finance-news-1) ⭐️ 8.0/10
2. [ETF experts: Nvidia turmoil may shift AI money to other Big Tech](#item-finance-news-2) ⭐️ 7.0/10
3. [Lutnick faces conflict-of-interest questions over sons’ firm’s Nvidia ties](#item-finance-news-3) ⭐️ 7.0/10
4. [Intel and CEO Lip-Bu Tan face shareholder class action over alleged concealment](#item-finance-news-4) ⭐️ 7.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [vLLM v0.34.0 ships extensible KV cache by default and removes Model Runner V1](https://github.com/vllm-project/vllm/releases/tag/v0.34.0) ⭐️ 8.0/10

vLLM v0.34.0 is now available, with 1,061 commits from 412 contributors and support for 10 new models including Mistral Large 4, MiniMax-M3.1-Flash, and Nemotron-3.5-Transcribe. Extensible KV cache is enabled by default on CUDA and ROCm: the engine sizes the cache from memory free after CUDA graph capture and warmup, so most models get a larger cache and higher throughput, though per-token decode latency can rise 6–18% on some H200 models at concurrency 128. Model Runner V1 has been removed, leaving Model Runner V2 as the only GPU runner; the release also reports up to 1.95× decode speedup for Step5 on 4×GB200 and 1.6× output throughput for GLM-5.3-Flash. Upgrading requires configuration changes: default block size is 64 \(was 16\), \`gpu\_memory\_utilization\` defaults to 1.0, ROCm 7.2 artifacts are no longer published, and \`huggingface\_hub &gt;= 2.0.0\` is required.

github · khluu · Nov 16, 23:22

**「Background」** vLLM sizes its KV cache against the fraction of GPU memory set by --gpu-memory-utilization, previously defaulting to 0.9; that budget was an estimate taken before the engine&\#x27;s warmup and CUDA-graph capture, which is why the old sizing could be recovered by passing 0.9 again. Model Runner is vLLM&\#x27;s GPU execution path that schedules batches and hosts logits processors, and until this release operators could still fall back to the original implementation by setting VLLM\_USE\_V2\_MODEL\_RUNNER=0.

**「Impact」** Operators upgrading from earlier vLLM releases must remove \`VLLM\_USE\_V2\_MODEL\_RUNNER=0\`, which now fails at startup, and should pass \`--block-size 16\` if they need the previous block-size behavior; to retain the old KV-cache sizing they can set \`--gpu-memory-utilization 0.9\` or \`--no-enable-extensible-kv-cache\`. ROCm users also must move to the ROCm 10.0 wheels and images because \`-rocm72\` is no longer published.

**Tags**: `#vLLM`, `#LLM inference`, `#open source`, `#KV cache`, `#performance`

---

<a id="item-tech-news-2"></a>
### [Alibaba launches Qwen4-Max, a 2.4T-parameter sparse MoE flagship](https://mp.weixin.qq.com/s/pJUt0xwD6H-WMyzd8TjZaQ) ⭐️ 8.0/10

Alibaba&\#x27;s Tongyi Qianwen team has released Qwen4-Max, a flagship model built on a new sparse mixture-of-experts architecture with 2.4 trillion total parameters, native vision understanding, and million-token context. According to the team&\#x27;s announcement, it performs strongly on coding, office-work, and long-horizon tasks, and its frontend coding ability ranked near the top of the global Code Arena blind test. The vendor also reports that average cost per task fell from ¥26.58 to ¥11.16 \(about 58%\) versus the previous generation, with token consumption down nearly 50% and API pricing lowered accordingly. Qwen4-Max is already live, while the team says smaller Qwen4 models with published weights will follow later — those open-weight models have not yet shipped.

telegram · zaihuapd · Nov 16, 02:52

**「Background」** Qwen4-Max succeeds Qwen3.8 Max at the same 2.4-trillion total parameter count, according to wccftech, so the change is about architecture, multimodal capability, and cost rather than raw scale alone. In a sparse mixture-of-experts model, not all parameters are used for every token; ForkLog reports that Qwen4-Max activates 71 billion parameters per token, which explains why its total parameter count is far larger than the compute used for each token.

**「What It Means for Developers」** Developers building on Qwen APIs get native image and video input plus a 1M-token context window with reasoning enabled by default, according to OpenRouter&\#x27;s model listing, while the roughly 58% drop in per-task cost \(26.58 yuan to 11.16 yuan\) and near-50% token reduction make long-context and agentic workloads cheaper to run. Artificial Analysis lists the model at $1.50 per 1M input tokens and $4.50 per 1M output tokens and notes that its weights remain proprietary, so teams that need self-hosted or fine-tuned open weights must wait for the promised smaller Qwen4 releases rather than Qwen4-Max itself.

<details><summary>References</summary>
<ul>
<li><a href="https://forklog.com/en/alibaba-launches-qwen4-max-ai-model-with-2-4-trillion-parameters/">Alibaba Launches Qwen 4 - Max AI Model with 2 . 4 Trillion Parameters</a></li>
<li><a href="https://wccftech.com/alibabas-new-qwen4-max-fails-to-overtake-moonshots-kimi-k3-1-pro-retaining-the-same-parameter-count-with-a-lower-price-and-revamped-native-vision-moe-architecture/">Alibaba&#x27;s New Qwen 4 - Max Fails To Overtake Moonshot&#x27;s Kimi...</a></li>
<li><a href="https://openrouter.ai/qwen/qwen4-max">Qwen 4 Max - API Pricing &amp; Providers | OpenRouter</a></li>
<li><a href="https://artificialanalysis.ai/models/qwen4-max">Qwen 4 Max - Intelligence, Performance &amp; Price ... | Artificial Analysis</a></li>

</ul>
</details>

**Tags**: `#Qwen`, `#large language models`, `#sparse MoE`, `#model release`, `#API pricing`

---

<a id="item-tech-news-3"></a>
### [Carnegie Mellon launches free full-semester CS lectures on YouTube](https://www.cs.cmu.edu/learn/) ⭐️ 7.0/10

Carnegie Mellon&\#x27;s CS Learn project launched free YouTube releases of full-semester lectures from current CMU computer science courses, with one course premiering each day this week and more scheduled for January, according to the program&\#x27;s lead. The releases cover a variety of topics and were produced by a small team using automation tools built by CMU students. The program lead described the releases as current CMU courses rather than a separate adaptation.

hackernews · pcompeau · Nov 16, 20:43 · [Discussion](https://news.ycombinator.com/item?id=50522980)

**「Background」** Carnegie Mellon already offers CS Academy, a free online interactive computer science curriculum for high schools that includes teacher training, an online textbook, and technical support. CS Learn applies free access to full-semester lecture recordings from current CMU courses rather than to an interactive high-school curriculum. Open courseware aggregators already list thousands of free courses from major universities, so the distinction here is CMU&\#x27;s current course catalog and its automated production approach.

**「Impact」** Learners can watch current CMU course lectures without enrolling, but the supplied material does not state a license, so organizations cannot yet assume permission to reuse, remix, or train on the videos; the licensing question raised in the comments was not answered.

**「Community discussion」** Commenters largely welcomed the open-courseware release. One argued that learning fundamentals is what lets AI serve as a power tool rather than a replacement, while another asked about licensing and raised the prospect of using the lectures with coding agents; a separate thread recalled Randy Pausch&\#x27;s last lecture and the Alice project.

<details><summary>References</summary>
<ul>
<li><a href="https://www.youtube.com/watch?v=hztO5vaBTRs">Demonstration of Carnegie Mellon CS Academy - YouTube</a></li>
<li><a href="https://www.openculture.com/freeonlinecourses">1,700 Free Online Courses from Top Universities | Open Culture</a></li>

</ul>
</details>

**Tags**: `#open courseware`, `#computer science education`, `#Carnegie Mellon`, `#YouTube`, `#free lectures`

---

<a id="item-tech-news-4"></a>
### [Jiff 1.0: A New Datetime Library for Rust](https://burntsushi.net/jiff/) ⭐️ 7.0/10

Jiff 1.0, a datetime library for Rust by burntsushi, has been announced. The release gives Rust developers a new option alongside the long-established chrono crate, with discussion centered on datetime API design and time-scale handling. The supplied announcement material does not provide a feature list or compatibility details, so specific API and migration claims remain unverified.

hackernews · burntsushi · Nov 16, 16:53 · [Discussion](https://news.ycombinator.com/item?id=50519744)

**「Background」** Jiff is Andrew Gallant&\#x27;s \(burntsushi\) Rust datetime library, and it had already been shipping as a 0.2 release with an established user base before this 1.0 announcement. The project&\#x27;s GitHub repository states that Jiff 0.2 will keep receiving critical bug fixes for roughly one year after 1.0, with no further active feature development, giving existing users a transition window rather than an abrupt break. Jiff is positioned as a higher-level alternative that puts time zone and daylight-saving handling into the core API; commenters in this thread describe chrono as the incumbent Rust datetime library that Jiff would be adopted in place of.

**「What it means for Rust projects」** Rust developers now have Jiff 1.0 as an alternative to chrono, pitched in its documentation as offering high-level datetime primitives that are difficult to misuse with reasonable performance. Because it is a separate crate, teams that adopt it alongside chrono-based dependencies will need conversion at API and serialization boundaries, and commenters note that broader uptake depends on the wider ecosystem adding support for Jiff.

**「Community Discussion」** Commenters welcomed Jiff as consistent with burntsushi&\#x27;s other libraries, and some hoped the wider Rust ecosystem would adopt it over chrono. A former chrono maintainer said the crate&\#x27;s stable API made incremental improvements meet resistance and contributed to burnout, while another commenter asked how Jiff handles time scales such as TAI and UT1 for simulations spanning microseconds to gigayears.

<details><summary>References</summary>
<ul>
<li><a href="https://github.com/BurntSushi/jiff">GitHub - BurntSushi/jiff: A datetime library for Rust that ...</a></li>
<li><a href="https://burntsushi.net/jiff/">A datetime library for Rust - Andrew Gallant&#x27;s Blog</a></li>
<li><a href="https://github.com/BurntSushi/jiff">GitHub - BurntSushi/jiff: A datetime library for Rust that ...</a></li>
<li><a href="https://docs.rs/jiff/latest/jiff/">jiff - Rust - Docs.rs</a></li>

</ul>
</details>

**Tags**: `#Rust`, `#datetime`, `#libraries`, `#API design`, `#chrono`

---

<a id="item-tech-news-5"></a>
### [Microsoft traces major email outage to defect in July fix](https://www.theregister.com/saas/2026/11/16/microsoft-blames-monster-email-outage-on-software-defect-introduced-in-july-fix/5310026) ⭐️ 7.0/10

Microsoft has blamed a major email outage on a software defect introduced by a fix shipped in July, according to The Register. The report attributes the incident to that earlier code change, but the supplied material does not identify the specific email service, affected regions, outage duration, or remediation timeline.

hackernews · Bender · Nov 16, 13:18 · [Discussion](https://news.ycombinator.com/item?id=50517321)

**「Earlier incident context」** Microsoft 365&\#x27;s worldwide outage occurred on November 12–13, 2026, and reports on the incident traced it to a hidden Windows bug in servers handling cloud connections. The defect originated in a fix prepared specifically for Microsoft 365 networking gateway servers; the resulting failure left more than 80% of those gateway servers unresponsive and triggered a cascading outage.

**「Community Discussion」** Commenters focused on why the defect escaped testing: one argued that a relatively low-end test environment passed the July code but differed from production, hiding what the commenter described as a concurrency bug. Another asked whether providers at Microsoft 365&\#x27;s scale should shed excessive traffic or block regions at critical thresholds instead of forwarding more requests downstream.

<details><summary>References</summary>
<ul>
<li><a href="https://www.bleepingcomputer.com/news/microsoft/microsoft-says-months-old-bug-caused-global-microsoft-365-outage/">Microsoft says months-old bug caused global Microsoft 365 outage</a></li>
<li><a href="https://cybersecuritynews.com/microsoft-outage-incident-report/">Microsoft Reveals How a Hidden Windows Bug Took Down Microsoft ...</a></li>

</ul>
</details>

**Tags**: `#Microsoft 365`, `#service outage`, `#software defect`, `#incident analysis`, `#production testing`

---

<a id="item-tech-news-6"></a>
### [Marimba reuses a frozen ASR encoder for calibrated speech queries](https://www.reddit.com/r/MachineLearning/comments/1xxsqro/marimba_a_system_one_model_for_speech_r/) ⭐️ 7.0/10

Marimba, a research model released with a paper, code, Apache-2.0 weights, a demo, and a pip package, answers typed yes/no, multiple-choice, or score questions about 8-second audio windows with calibrated probabilities. It uses one frozen Qwen3-ASR-0.6B encoder pass per window for all question types, combining zero-shot scoring of decoder hypotheses for term spotting, the ASR model&\#x27;s language scores, and small readouts on frozen layers 12 and 18 for speaker change/count and turn end. On 1,000 public questions it matched or beat Qwen3-Omni 30B-A3B on 6 of 9 tests, but lost on Speech Commands, trailed Smart Turn v3.2 on turn-end detection, and performed at chance on unseen scene classification; its turn-end readout was trained on Smart Turn data.

reddit · r/MachineLearning · /u/solanotodesch · Nov 16, 15:47

**「Background」** Marimba reuses Qwen3-ASR-0.6B, Alibaba&\#x27;s compact open-weight speech recognition model published on Hugging Face under Apache 2.0, which covers 30 languages and 22 Chinese dialects. The &quot;system one&quot; label refers to its fast, single-pass design: one frozen encoder pass per 8-second audio window serves every question type, instead of running a large generative omni model such as the 30B-A3B Qwen3-Omni it is benchmarked against. Because the encoder stays frozen, only small readouts attached to intermediate layers and the Platt calibration applied to decoder hypothesis scores are fitted to the specific question types.

**「Impact」** Developers can test whether one frozen ASR encoder pass can serve several typed audio queries, but should not treat the readouts as general-purpose: the reported chance-level result on an unseen scene-classification task and the in-distribution turn-end result limit how far the approach can be transferred without new training or evaluation.

<details><summary>References</summary>
<ul>
<li><a href="https://www.anchorterminal.com/tools/qwen3-asr-0-6b">Qwen 3 - ASR - 0 . 6 B review (2026): pricing, alternatives and grade C</a></li>

</ul>
</details>

**Tags**: `#speech recognition`, `#machine learning`, `#frozen encoders`, `#probabilistic calibration`, `#audio understanding`

---

<a id="item-tech-news-7"></a>
### [duetto steers Anticipatory Music Transformer at sampling time for live jazz](https://www.reddit.com/r/MachineLearning/comments/1xxkyh3/steering_a_pretrained_music_transformer_at/) ⭐️ 7.0/10

duetto is a real-time jazz partner for a MIDI keyboard that plays standards with the user as a small band—solo, comping, and walking bass—by steering the pretrained Anticipatory Music Transformer \(Thickstun et al., 2023\) at sampling time rather than fine-tuning it. Before each note sample, a rule layer masks disallowed events, such as an out-of-register pitch or an off-beat bass note, and biases likely ones such as current chord tones and downbeat guide tones; solo phrases come from the Weimar Jazz Database, transposed to the tune&\#x27;s chords and developed over a chorus, with about 61% of demo solo notes drawn from quoted phrases or the theme. The author reports roughly 12 ms/note for the medium model and 18 ms/note for the large model on a 3080 Ti, with the large model at about 90 ms/note on a Jetson Orin Nano, and notes that the system can drift from the player and that the balance between model output and rule bias is fragile.

reddit · r/MachineLearning · /u/GGAllin43 · Nov 16, 09:19

**「Background」** The Anticipatory Music Transformer \(Thickstun et al., 2023\) is a pretrained autoregressive model whose stated capability includes infilling control tasks such as accompaniment, which is why duetto can use it as-is rather than fine-tuning it. Its pretrained checkpoints are loadable through HuggingFace Transformers. duetto&\#x27;s alternative to fine-tuning is constrained/guided decoding: before each token is sampled, a rule layer masks disallowed events and biases likely ones in the logits, leaving the model weights untouched.

**「What practitioners can take from it」** AI-music practitioners evaluating symbolic accompaniment can use the released code, free for noncommercial use, as a concrete alternative to fine-tuning, but should expect to tune the rule layer per behavior: too much bias produces phrase-book output, while too little stops the result sounding like jazz.

<details><summary>References</summary>
<ul>
<li><a href="https://arxiv.org/abs/2306.08620">[2306.08620] Anticipatory Music Transformer</a></li>
<li><a href="https://github.com/jthickstun/anticipation">GitHub - jthickstun/ anticipation : Anticipatory Autoregressive Models</a></li>

</ul>
</details>

**Tags**: `#AI music generation`, `#sampling-time control`, `#pretrained transformers`, `#real-time interaction`, `#MIDI`

---

<a id="item-tech-news-8"></a>
### [Tencent Hunyuan launches Hy4 flash MoE with low-cost 1M context](https://mp.weixin.qq.com/s/5yBbf-ctYziM5r0i6Y17lA) ⭐️ 7.0/10

Tencent Hunyuan released Hy4 flash, a cost-optimized mixture-of-experts model with 224B total parameters and 12B active, plus multimodal support and a 1M-token context window. The company says it slightly outperforms Hy4 preview and cuts WorkIndex cost per task to 1/13 of Hy4 preview and 1/20 of Hy4. API pricing is ¥0.5 per million input tokens and ¥2 per million output tokens, with cache hits at ¥0.02; Hy4 flash is live on Tencent Cloud TokenHub, WorkBuddy, and Yuanbao, with open source planned. WorkBuddy is free and API usage is 50% off through November 30. Tencent’s performance and cost figures are vendor claims, and no independent benchmarks were provided.

telegram · zaihuapd · Nov 16, 07:17

**「Background」** Hy4 flash is the low-cost member of Tencent Hunyuan’s Hy4 family, following the Hy4 and Hy4 preview models referenced in the announcement. It uses a sparse mixture-of-experts design with 224B total parameters but only 12B active per token, a structure intended to reduce serving cost while retaining model capacity.

**「Impact」** Cost-sensitive developers can trial Hy4 flash on Tencent Cloud TokenHub at ¥0.5 per million input tokens and ¥2 per million output tokens \(¥0.02 for cached input\), with a 50% API discount through Nov. 30. It is already deployed across Tencent products including WorkBuddy, Yuanbao and WeCom, but teams needing open weights or OpenRouter access must wait, and because the quality claims are vendor-reported, they should benchmark the model on their own workloads first.

<details><summary>References</summary>
<ul>
<li><a href="https://www.tencent.com/zh-cn/tencent-launches-hy4-flash-to-power-high-speed-cost-efficient-ai-deployment-for-everyday-workflows/">腾讯混元 Hy4 flash 正式发布：赋能日常高效办公 - Tencent</a></li>
<li><a href="https://www.stdaily.com/web/gdxw/2026-11/16/content_614064.html">腾讯混元Hy4 flash发布 单任务成本仅为Hy4二十分之一</a></li>

</ul>
</details>

**Tags**: `#Tencent Hunyuan`, `#Hy4 flash`, `#Mixture-of-Experts`, `#long context`, `#LLM pricing`

---

<a id="item-tech-news-9"></a>
### [US and Nine Countries Sign San Francisco Declaration on AI Supply Chains](https://www.state.gov/releases/office-of-the-spokesman/2026/11/the-san-francisco-declaration-on-the-secure-foundations-of-enduring-prosperity/) ⭐️ 7.0/10

On November 15, the United States, Australia, India, Israel, Japan, South Korea, Qatar, Singapore, the UAE and the United Kingdom signed the San Francisco Declaration, which states that economic security is the foundation of national security and commits the signatories to jointly protect sensitive technologies and critical infrastructure supporting superintelligence \(SI\) supply chains. The declaration establishes five working groups: innovation policy frameworks, SI applications in critical sectors, full-stack SI supply chain collaboration, safe harbors and supply chain security hubs, and SI security and resilience. It is a political declaration rather than a binding agreement — the source discloses no enforcement mechanism, funding, deadlines or specific technologies covered, and the working groups have yet to produce published outputs.

telegram · zaihuapd · Nov 16, 10:40

**「What is Pax Silica?」** The declaration was signed on 15 November at the Pax Silica Founders Retreat, convened by US Under Secretary of State for Economic Affairs Jacob Helberg, according to the State Department. Pax Silica is the US-led partner framework that the declaration extends: the department said Pax Silica was &quot;entering a new phase&quot; and that partners had agreed to treat the security of AI-enabling technologies and their underlying infrastructure as a shared responsibility. The Financial Times reported that the accord is intended to protect AI supply chains from China.

**「What Changes for AI Supply-Chain Firms」** Companies building or procuring AI hardware, chips and data-center infrastructure across the ten signatory jurisdictions now have a named policy channel to watch: the declaration&\#x27;s proposed working groups on &quot;supply chain cooperation across the SI stack&quot; and on &quot;safe harbors and supply chain security hubs,&quot; which are where any future security or trust requirements for suppliers would be drafted. As signed, however, the text commits the parties only to establishing those groups &quot;so that common purpose may be carried into common practice&quot; — the groups remain proposed, with no published membership, mandate or timetable, so no new binding supplier obligations or export conditions take effect for developers yet.

<details><summary>References</summary>
<ul>
<li><a href="https://www.investing.com/news/world-news/us-nine-nations-sign-san-francisco-declaration-on-ai-security-5028448">U.S., nine nations sign San Francisco declaration on AI security By...</a></li>
<li><a href="https://buzb.uz/en/news/us-and-nine-countries-sign-declaration-on-ai-supply-chain-security">US and Nine Countries Sign Declaration on AI Supply Chain Security</a></li>
<li><a href="https://www.ft.com/content/3c2197fc-9618-4838-91e6-522ce1a96a22?syn-25a6b1a6=1">US and allies sign accord to protect AI supply chains from China</a></li>
<li><a href="https://www.electronicsweekly.com/news/business/san-francisco-agreement-on-secure-supply-chains-signed-2026-11/">San Francisco Agreement on secure supply chains signed</a></li>
<li><a href="https://thenationaltelegraph.com/news/pax-silica-san-francisco-declaration-ai-supply-chain/">Ten Governments Sign an AI Supply-Chain Pact in San Francisco ...</a></li>

</ul>
</details>

**Tags**: `#AI policy`, `#AI supply chain`, `#international agreement`, `#national security`, `#superintelligence`

---

<a id="item-tech-news-10"></a>
### [Amazon says Artex-driven AI agents stole API keys to fund model calls](https://cybernews.com/security/amazon-autonomous-cybercrime-artex-framework/) ⭐️ 7.0/10

Amazon says attackers used the open-source Artex pentesting framework to drive AI agents that stole API keys from internet-exposed AI applications including LiteLLM and Dify, validated the keys, and pooled them to pay for additional large-model calls. The company says the campaign began on October 3 and was disrupted by AWS&\#x27;s MadPot decoy network on November 5, and it attributes the activity to a China-related threat group with medium confidence. Amazon adds that not all listed targets were compromised and that it has notified AWS customers that may be affected; Cybernews reported the account.

telegram · zaihuapd · Nov 16, 13:00

**「Background」** ARTEX is an open-source agentic AI penetration-testing framework: instead of running a fixed script, it lets a model plan and carry out security-testing steps, a capability attackers redirected toward credential theft rather than authorized testing. MadPot is Amazon&\#x27;s globally distributed network of decoy threat sensors, which AWS uses to observe and disrupt malicious traffic; the sensors that logged this campaign were configured to present themselves as the publicly exposed AI applications the agents were probing.

**「Impact」** For operators of publicly reachable LiteLLM or Dify deployments, the reported pattern turns an exposed API key into both a direct compromise and a way to fund further automated activity, making key rotation and review of public access concrete concerns. Amazon says it has notified potentially affected AWS customers but did not specify how many or which customers were confirmed compromised.

<details><summary>References</summary>
<ul>
<li><a href="https://aws.amazon.com/blogs/security/amazon-threat-intelligence-observes-threat-actors-running-cybercrime-campaigns-with-artex-ai-agents/">Amazon Threat Intelligence observes threat actors running ...</a></li>
<li><a href="https://securityarsenal.com/blog/artex-framework-abuse-detecting-and-defending-against-ai-driven-automated-attacks">ARTEX Framework Abuse: Detecting and Defending Against AI ...</a></li>

</ul>
</details>

**Tags**: `#AI security`, `#API key theft`, `#autonomous agents`, `#AWS`, `#cybercrime`

---

<a id="item-tech-news-11"></a>
### [US extends AI chip export controls to remote access](https://www.reuters.com/legal/litigation/us-issues-rule-protect-advanced-ai-chips-being-accessed-remotely-2026-11-16/) ⭐️ 7.0/10

The US Commerce Department reportedly issued an interim final rule on Nov. 16 extending export controls on advanced AI chips and servers to remote access, aimed at preventing circumvention through third-country data centers. The Verge reported that the rule also requires licenses for reexporting AI chips to Indonesia, Malaysia, Singapore, Thailand and Brazil. The source did not include the rule text, effective date, performance thresholds, or enforcement details, so the full scope remains unconfirmed.

telegram · zaihuapd · Nov 16, 14:44

**「Background」** The Commerce Department’s Bureau of Industry and Security \(BIS\) released the measure as an interim final rule intended to address remote access to advanced “super intelligence” chips and servers, not only their cross-border shipment. BIS said the rule is meant to keep existing restrictions on access to sensitive technology from being circumvented through overseas data centers.

**「Impact」** Third-country data-center operators and reexporters would have to check for US export authorization before providing remote access to advanced AI chips or reexporting them to Indonesia, Malaysia, Singapore, Thailand, or Brazil; because the reported summary gives no thresholds or effective date, affected operators cannot yet determine which specific configurations are covered.

<details><summary>References</summary>
<ul>
<li><a href="https://www.bis.gov/press-release/bis-issues-rule-addressing-remote-access-american-super-intelligence-technology">www.bis.gov</a></li>

</ul>
</details>

**Tags**: `#AI chips`, `#export controls`, `#semiconductors`, `#data centers`, `#tech policy`

---

## Financial News

<a id="item-finance-news-1"></a>
### [China&\#x27;s October retail sales, industrial output and investment all miss forecasts](https://www.cnbc.com/2026/11/16/china-retail-sales-october-industrial-output-investment.html) ⭐️ 8.0/10

China&\#x27;s retail sales rose 0.4% from a year earlier in October and industrial output grew 4.8%, both below analysts&\#x27; forecasts of 0.8% and 5.3% growth, while fixed-asset investment shrank 8.1% in the first ten months of the year versus an expected 7% decline, according to CNBC&\#x27;s report on Monday&\#x27;s data.

rss · CNBC Finance · Nov 16, 03:53

**「Background」** The slump builds on a property downturn now in its fifth year, which has eroded household wealth and kept consumer spending weak, while fixed-asset investment had already fallen 4.1% year-on-year in the January–May period.

**「Who is exposed」** Because growth is leaning more heavily on exports — which rose 35.2% year on year in October — Chinese manufacturers and exporters would be the first to feel it if the European Union follows through on the further trade measures it is weighing to reduce its dependence on Chinese goods. The bloc&\#x27;s trade deficit with China reached €360 billion last year, the stated rationale for those measures.

<details><summary>References</summary>
<ul>
<li><a href="https://economy.ac/news/2026/06/202606289352">China ’s Domestic Market Remains Stagnant Despite... — The Economy</a></li>
<li><a href="https://www.bloomberg.com/news/articles/2026-11-03/eu-plans-changes-to-its-single-market-to-reduce-china-dependence">EU Plans Changes to Its Single Market to Reduce China ...</a></li>
<li><a href="https://www.reuters.com/world/china/pressured-home-eu-leaders-weigh-china-trade-steps-2026-10-14/">Pressured at home, EU leaders weigh China trade steps</a></li>

</ul>
</details>

**Tags**: `#China economy`, `#industrial output`, `#retail sales`, `#fixed-asset investment`, `#youth unemployment`

---

<a id="item-finance-news-2"></a>
### [ETF experts: Nvidia turmoil may shift AI money to other Big Tech](https://www.cnbc.com/2026/11/14/nvidia-ai-trade-data-centers-congress.html) ⭐️ 7.0/10

Investing experts interviewed on CNBC&\#x27;s &quot;ETF Edge&quot; argued that Nvidia&\#x27;s leadership turmoil — including CEO Jensen Huang&\#x27;s resignation — and potential Democratic pushback on data-center construction could redirect AI investment toward other Big Tech and chip names. Yorkville Ives cut its Nvidia price target to $225 from $300 on Thursday while keeping a buy rating, and Nvidia shares finished the week at $162.85.

rss · CNBC Finance · Nov 16, 12:13

**「Background」** Jensen Huang resigned as Nvidia CEO on Nov. 12 after disclosures about relationships with a subordinate and a woman U.S. officials identified as a Chinese spy, leaving CFO Colette Kress as interim CEO; separately, Democrats won control of Congress on Nov. 3 and are preparing legislation targeting AI and data-center development.

**「Who is affected」** Investors and businesses tied to AI computing are already reshuffling: as Nvidia&\#x27;s leadership crisis deepened, shares of rival chipmakers AMD and Broadcom drew buyers betting they win business from the chip giant, while smaller &quot;neocloud&quot; providers that depend on Nvidia&\#x27;s financing, such as CoreWeave and Nebius, remain the most exposed if that support weakens.

<details><summary>References</summary>
<ul>
<li><a href="https://finance.yahoo.com/technology/ai/articles/nvidia-ceo-jensen-huang-resigns-110116748.html">Nvidia CEO Jensen Huang Resigns — CFO Collette Kress in as...</a></li>
<li><a href="https://www.nytimes.com/2026/11/12/technology/nvidia-jensen-huang.html">Jensen Huang Resigns From Nvidia After Affairs - The New York...</a></li>
<li><a href="https://www.usnews.com/news/politics/articles/2026-11-06/democrats-planning-flood-of-ai-bills-when-they-take-control-of-congress">Democrats Planning Flood of AI Bills When They Take Control ...</a></li>
<li><a href="https://www.cnbc.com/2026/11/13/nvidia-jensen-huang-affairs-amd-broadcom-tsmc.html">Nvidia ’s turmoil is prompting a rotation across chip stocks.</a></li>
<li><a href="https://www.bloomberg.com/news/articles/2026-11-12/nvidia-turmoil-lifts-amd-broadcom-on-bets-for-business-gains">AMD , Broadcom Poised to Gain From Scandal Roiling Nvidia</a></li>

</ul>
</details>

**Tags**: `#Nvidia`, `#AI trade`, `#ETFs`, `#data-center policy`, `#semiconductors`

---

<a id="item-finance-news-3"></a>
### [Lutnick faces conflict-of-interest questions over sons’ firm’s Nvidia ties](https://www.cnbc.com/2026/11/13/howard-lutnick-nvidia-jensen-huang-china-cantor-fitzgerald.html) ⭐️ 7.0/10

Commerce Secretary Howard Lutnick is facing conflict-of-interest questions over his sons’ firm Cantor Fitzgerald’s reported Nvidia holdings and financing ties, amid scrutiny of Nvidia-related China export controls, CNBC reported. Cantor’s reported Nvidia share count fell 49% between September 2025 and March 2026, to 1.78 million shares, though CNBC said there is no evidence the change was tied to intelligence warnings or that the firm’s business interests influenced Lutnick’s decisions.

rss · CNBC Finance · Nov 16, 12:14

**「Background」** Howard Lutnick ran Cantor Fitzgerald—now led by his sons Brandon and Kyle—before becoming Commerce Secretary in February 2025; Commerce is the department responsible for imposing U.S. export controls, including the entity list that restricts companies suspected of diverting Nvidia chips to China. Nvidia CEO Jensen Huang resigned after disclosures about extramarital affairs, including one with a woman suspected of spying for China, according to BBC reporting.

<details><summary>References</summary>
<ul>
<li><a href="https://www.bbc.com/news/articles/cry49plv8v3go">Elon Musk joins &#x27;Bring Jensen Back&#x27; campaign to reinstate the...</a></li>

</ul>
</details>

**Tags**: `#Nvidia`, `#US export controls`, `#conflict of interest`, `#Cantor Fitzgerald`, `#semiconductors`

---

<a id="item-finance-news-4"></a>
### [Intel and CEO Lip-Bu Tan face shareholder class action over alleged concealment](https://www.investing.com/news/stock-market-news/intel-sued-by-shareholders-following-29-stock-plunge-5028171) ⭐️ 7.0/10

Intel, CEO Lip-Bu Tan and the company&\#x27;s CFO face a shareholder class action alleging they concealed weak PC demand and inventory buildup before Intel&\#x27;s Oct. 29 fourth-quarter revenue and profit forecast fell short of expectations, sending the stock down 28.6% the next day and wiping out about $140 billion in market value. The suit, led by a Michigan pension fund, was filed Friday in federal court in San Jose and seeks to represent investors who bought Intel stock between July 23 and Oct. 29, 2026.

telegram · zaihuapd · Nov 16, 11:10

**「Background」** Lip-Bu Tan has been Intel’s CEO since 2025, and the suit is a proposed class action in which one lead investor—a Michigan pension fund—seeks unspecified damages on behalf of shareholders who bought Intel stock between July 23 and Oct. 29, 2026.

<details><summary>References</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/Lip-Bu_Tan">Lip - Bu Tan - Wikipedia</a></li>
<li><a href="https://wccftech.com/intel-ceo-lip-bu-tan-named-defendant-class-action-lawsuit-pc-sales-slowdown/">Intel CEO Lip - Bu Tan Named As Defendant In New Class - Action ...</a></li>

</ul>
</details>

**Tags**: `#Intel`, `#shareholder lawsuit`, `#semiconductor`, `#stock plunge`, `#corporate disclosure`

---