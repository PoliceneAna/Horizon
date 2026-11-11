---
layout: default
title: "Horizon Summary: 2026-11-11 (EN)"
date: 2026-11-11
lang: en
---

> From 47 items, 15 important content pieces were selected

---

**Technology News**
1. [Voltage glitching used to unlock A100 features in mining card](#item-tech-news-1) ⭐️ 8.0/10
2. [AWS releases official local service emulator, built in Rust by agent swarm](#item-tech-news-2) ⭐️ 8.0/10
3. [False Smoke Alarm Nearly Took Down Jane Street&\#x27;s Only NYC Datacenter](#item-tech-news-3) ⭐️ 7.0/10
4. [WSJ Headline Claims Nvidia Is Preparing to Oust CEO Jensen Huang](#item-tech-news-4) ⭐️ 7.0/10
5. [Tim Peters, author of the Zen of Python, has died](#item-tech-news-5) ⭐️ 7.0/10
6. [Linear Programming Proposed for Constrained Weight Editing](#item-tech-news-6) ⭐️ 7.0/10
7. [Google launches Gemini Decisions API with multimodal Decision 1](#item-tech-news-7) ⭐️ 7.0/10
8. [Anthropic IPO video details four-chip Claude strategy and a three-day AMD port](#item-tech-news-8) ⭐️ 7.0/10
9. [Paper argues &\#x27;AI slop&\#x27; is a community judgement, not a content property](#item-tech-news-9) ⭐️ 7.0/10
10. [Report alleges Alice Huang moved 240,000 banned Nvidia chips to China](#item-tech-news-10) ⭐️ 7.0/10

**Technology Blog**
1. [vLLM Encoder Disaggregation: Metadata-Only EPD for Multimodal Serving](#item-tech-blog-1) ⭐️ 8.0/10
2. [Glue Work Is Still a Trap in the AI Era](#item-tech-blog-2) ⭐️ 5.0/10

**Financial News**
1. [Goolsbee calls October inflation report &\#x27;borderline disturbing&\#x27; as Fed weighs rate hikes](#item-finance-news-1) ⭐️ 8.0/10
2. [China Ends Transition Period for Offshore Trust Income Tax With Over RMB 160 Billion Declared](#item-finance-news-2) ⭐️ 8.0/10
3. [FCC approves SpaceX&\#x27;s purchase of 800 MHz spectrum licenses](#item-finance-news-3) ⭐️ 7.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [Voltage glitching used to unlock A100 features in mining card](https://blog.kate.land/posts/using-voltage-glitching-to-unlock-the-a100/) ⭐️ 8.0/10

A blog post reports using voltage glitching to unlock A100-class capabilities in a mining card, a hardware-hacking procedure rather than an NVIDIA-supported modification. The write-up focuses on bypassing fused-off GPU features; commenters identify the card discussed as the 8 GB model and contrast it with the 10G CMP 170HX, which has shown 80 GB of memory but not full CUDA access. The approach carries hardware risk, and the source provides no indication that it is a general or repeatable unlock for other cards.

hackernews · lae · Nov 11, 10:48 · [Discussion](https://news.ycombinator.com/item?id=50451903)

**「Context: One die, two products」** Nvidia builds both the datacenter A100 and the mining-oriented CMP 170HX from the same GA100 die, relying on on-die fuses — programmed through the GA100&\#x27;s fuse controller — to disable memory capacity and features in the cheaper card rather than any physical difference in silicon. The blog&\#x27;s premise follows directly from that: if the limits are enforced by fuse settings, they can in principle be reversed through fault injection such as voltage glitching.

**「Impact」** Owners of CMP 170HX mining cards have a potential route to repurposing the GA100-based hardware, with prior write-ups documenting unlocks to 64 GB of memory and 74 SMs and one setup using two such cards for LLM inference. The catch is that results appear card- and method-specific—one account cross-flashes the 250 W card to NVIDIA’s 300 W VBIOS—so users should validate memory, stability, and power delivery per card rather than assume a full A100 equivalent.

**「Community discussion」** Commenters debate why NVIDIA would fuse off capacity: one speculates that an A100 may have had fabrication faults and was deliberately sold as a cheaper mining card, while another reports that the same cards rose from roughly $200 to $1k. A separate commenter trying a software-only unlock on a CMP 170HX says two weeks of effort have not succeeded and considers the fuse-based method riskier.

<details><summary>References</summary>
<ul>
<li><a href="https://blog.kate.land/posts/using-voltage-glitching-to-unlock-the-a100/">Using voltage glitching to unleash the A 100 in my mining card</a></li>
<li><a href="https://bytwork.com/en/articles/cmp-170hx-unlock">Unlocking the CMP 170 HX : How to get 64/80 GB of memory?</a></li>
<li><a href="https://gist.github.com/ropuls/d2978531ba3a1a183e70f62f3de2eb84">2x CMP 170 HX for LLM inference: unlock , cross-root P2P, serving...</a></li>

</ul>
</details>

**Tags**: `#voltage glitching`, `#GPU hardware hacking`, `#NVIDIA A100`, `#mining cards`, `#hardware reverse engineering`

---

<a id="item-tech-news-2"></a>
### [AWS releases official local service emulator, built in Rust by agent swarm](https://simonwillison.net/2026/Nov/11/aws-emulator/) ⭐️ 8.0/10

AWS has published aws-emulator, an official tool on GitHub for running tests against a local clone of its services without provisioning a paid API key. The project is written in Rust and, according to a guest post by Swaminathan Sivasubramanian on Werner Vogels&\#x27; blog, logged 29,684 commits in its first three weeks, attributed to a large swarm of coding agents rather than hand-written code. It currently requires Docker on macOS and Windows; Simon Willison notes that a single downloadable binary usable in a standard test suite across other languages and platforms would be preferable, and hopes AWS addresses that later.

rss · Simon Willison · Nov 11, 21:18

**「Background」** Developers testing AWS integrations ordinarily exercise live service endpoints, which means provisioning cloud resources and holding credentials; a paid API key is one such requirement. A local emulator replaces those endpoints with a machine-local clone so tests can run without that cloud-side setup.

**「Docker dependency limits test-suite use」** Developers can now run tests against local clones of AWS services without provisioning a paid API key, but on macOS and Windows the emulator requires Docker, so it cannot yet be dropped into an ordinary test suite as a single binary. It also should not stand in for authorization testing: the security documentation cited in the discussion states that the emulator never denies a request signed with its own key and does not evaluate IAM policies, resource-based policies, or KMS key policies the way AWS does, so those checks still need a real account.

**「Community discussion」** Commenters disagreed on whether this is a maintained product or an engineering exercise: one developer said they would stick with Floci and Testcontainers, noting those also cover GCP and Azure, while another argued that without agents AWS would never have attempted the project and that reliable clones of its services are no longer a moat. A commenter quoting the project&\#x27;s security documentation warned against using the emulator to test IAM policies, resource-based policies such as bucket policies, KMS key policies, or cross-account and cross-Region access, and said the emulator never denies a request signed with its own key.

**Tags**: `#AWS`, `#local emulator`, `#software testing`, `#Rust`, `#AI agents`

---

<a id="item-tech-news-3"></a>
### [False Smoke Alarm Nearly Took Down Jane Street&\#x27;s Only NYC Datacenter](https://michael.bacarella.com/2026/11/10/false-smoke-alarm-jane-street-datacenter/) ⭐️ 7.0/10

A first-person account describes how a false smoke alarm nearly forced a shutdown of Jane Street&\#x27;s only New York City datacenter. The author uses the incident to examine operational dependencies around alarm and fire-suppression behavior, emergency power-off expectations, on-site staffing, and remote-access limits. The account stops short of reporting a confirmed outage or a measured design failure, presenting the event as an incident narrative and a set of lessons for infrastructure teams.

hackernews · mbac32768 · Nov 11, 16:38 · [Discussion](https://news.ycombinator.com/item?id=50455394)

**「Background」** Datacenter fire-safety designs vary in whether smoke detection triggers clean-agent suppression, an emergency power-off \(EPO\) interlock, or neither, depending on the written sequence of operations for the hall. Because the site was Jane Street&\#x27;s only New York City datacenter, the account treats an alarm-driven shutdown as a single-site availability problem rather than a failover event.

**「Operational takeaway」** For infrastructure and SRE teams, the practical consequence is a checklist item: verify whether a site&\#x27;s smoke alarms, suppression systems, and emergency power-off procedures can be tested without creating an outage, and whether on-call staff can reach the facility when remote access is unavailable. The account presents those as operational concerns raised by the incident rather than as independently verified failures.

**「Commenter debate」** Commenters debated emergency power-off design: one asked why the site lacked at minimum a physical EPO button inside the datacenter and an interlink that would de-energize equipment after smoke detection, while another said the sequences of operations they write deliberately avoid shutting down CRACs on a smoke alarm. A separate commenter described being the nearby on-call employee expected to walk in and shut down servers when remote access was unavailable.

**Tags**: `#datacenter-operations`, `#incident-response`, `#site-reliability`, `#fire-suppression`, `#infrastructure`

---

<a id="item-tech-news-4"></a>
### [WSJ Headline Claims Nvidia Is Preparing to Oust CEO Jensen Huang](https://www.wsj.com/business/nvidia-is-preparing-to-oust-nvidia-ceo-jensen-huang-30f421ad) ⭐️ 7.0/10

A Wall Street Journal headline asserts that Nvidia is preparing to oust CEO Jensen Huang, but the supplied item contains no article text, named sources, board statement, or timeline, so the claim is unverified. No confirmed leadership change, interim CEO, or reason for an ouster is available in the supplied material. Nvidia&\#x27;s central role in AI hardware makes any such move high-stakes, but that does not establish that it is happening, and the community comments are speculative rather than evidence.

hackernews · jbredeche · Nov 11, 22:31 · [Discussion](https://news.ycombinator.com/item?id=50459703)

**「Earlier investigation」** Two days before the reported board move, Nvidia opened an investigation into reports that CEO Jensen Huang was the “target of a foreign intelligence effort,” and the AP reported that the company’s shares fell 5%. According to The Guardian, Huang had also told staff in a letter that he hoped to earn back their trust.

**「Community discussion」** Commenters focus partly on governance mechanics: one argues that dual-class share structures common at newer founder-led companies would give a founder disproportionate voting power and make a board-led ouster much harder, though the comment does not establish Nvidia&\#x27;s own share structure. Other comments speculate about unverified causes and predict short-term instability, but provide no sourcing.

<details><summary>References</summary>
<ul>
<li><a href="https://apnews.com/article/nvidia-jensen-huang-spy-china-63531dec0fe5c145afaac94dde31d478">Nvidia shares slide on internal investigation into CEO Jensen ...</a></li>
<li><a href="https://www.theguardian.com/technology/2026/nov/09/jensen-huang-image-nvidia">Jensen Huang ’s image has been shattered. Could he be pushed out...</a></li>

</ul>
</details>

**Tags**: `#Nvidia`, `#Jensen Huang`, `#corporate governance`, `#AI hardware`, `#semiconductor industry`

---

<a id="item-tech-news-5"></a>
### [Tim Peters, author of the Zen of Python, has died](https://discuss.python.org/t/in-memoriam-tim-peters-1952-2026/110028) ⭐️ 7.0/10

Tim Peters, a longtime Python contributor best known for writing the Zen of Python, has died, according to an in-memoriam post on the Python community discussion forum. The post gives his lifespan as 1952–2026. Python&\#x27;s \`import this\` command prints the Zen of Python, beginning “Beautiful is better than ugly.”

hackernews · ayhanfuat · Nov 11, 07:03 · [Discussion](https://news.ycombinator.com/item?id=50450488)

**「Context」** Tim Peters wrote “The Zen of Python,” the set of design aphorisms that Python users can display with \`import this\`; its lines include “Beautiful is better than ugly” and “Readability counts.” The text is a common reference point for discussions of Python’s design philosophy, and the supplied comments also point to his contributions to the Python Cookbook and to SpamBayes. Those earlier works help explain why the remembrance extends beyond the Zen text to his broader role as a longtime Python contributor.

**「Community discussion」** Commenters quoted the Zen of Python and recalled less-visible work: one credited Peters, along with Gary Robinson and Robert Woodhead, for turning Paul Graham&\#x27;s &quot;A Plan for Spam&quot; essay into SpamBayes, while others remembered his contributions to the Python Cookbook&\#x27;s second edition and his willingness to foster wide-ranging discussion.

**Tags**: `#Python`, `#Tim Peters`, `#open-source community`, `#obituary`

---

<a id="item-tech-news-6"></a>
### [Linear Programming Proposed for Constrained Weight Editing](https://nathan.rs/posts/weight-space-lp/) ⭐️ 7.0/10

A blog analysis on nathan.rs proposes using linear-programming solvers for constrained weight-space editing of neural networks. It presents a methodology, not a shipped tool or verified result: the supplied material contains no benchmarks or verified results and offers no independent validation. The post drew 35 Hacker News comments, where readers debated regularization, weight-space distillation, and whether math programming could replace RL loops.

hackernews · emschwartz · Nov 11, 12:30 · [Discussion](https://news.ycombinator.com/item?id=50452655)

**「Background」** Weight-space programming is an approach in which a general-purpose large language model reads and directly writes another neural network’s weights without gradient descent or a training loop \(tool-1-1\). The post follows MIT CSAIL’s “Sparks of Weight-Space Programming,” in which GPT-6 Astra was given a small network’s raw weights \(tool-1-3\); the earlier edit fixed thinking loops in Qwen3.5-0.8B through a hand-tuned search \(tool-1-2\).

**「Community Discussion」** Commenters debated where the approach belongs: dansitu argued that its simplicity suggests it should happen during training via regularization, while mirekrusin proposed using it for weight-space distillation by collecting paired examples and finding sparse edits. whatever1 went further, asserting that traditional math programming will replace or override the RL loop because rewards and penalties cannot enforce multiple strict objectives; these are opinions, not demonstrated results.

<details><summary>References</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/Weight-space_programming">Weight-space programming - Wikipedia</a></li>
<li><a href="https://proomt.com/item/can-a-linear-program-do-weight-space-programming-d1a13007-a589-44d0-b87e-067ea543171c">Can a Linear Program Do Weight-Space Programming ? · proomt</a></li>
<li><a href="https://x.com/nathanrs/status/2119845893755351417">Nathan Barry on X: &quot;In MIT CSAIL&#x27;s recent &quot;Sparks of Weight ...</a></li>

</ul>
</details>

**Tags**: `#machine-learning`, `#linear-programming`, `#weight-editing`, `#optimization`, `#model-interpretation`

---

<a id="item-tech-news-7"></a>
### [Google launches Gemini Decisions API with multimodal Decision 1](https://blog.google/innovation-and-ai/technology/developers-tools/gemini-decisions-api/) ⭐️ 7.0/10

Google&\#x27;s Gemini Decisions API adds Gemini Decision 1, a decision-focused model for developers. It supports the same three question types as Jev—yes/no, choice, and rubric scoring, including Jev&\#x27;s &quot;Noul&quot; term for yes/no—but accepts text, images, audio, video, and PDFs, whereas Jev is text/JSON-only and OpenAI&\#x27;s decision model handles text and images. Pricing is 10 cents per million input tokens with free output, matching the GPT-6 Luna decision model and above Jev&\#x27;s 4.2 cents per million. In a video test, Gemini returned graded probabilities for yes/no questions rather than the 1.0 or 0.0 outputs reported for Jev and OpenAI.

hackernews · iamdelirium · Nov 11, 18:32 · [Discussion](https://news.ycombinator.com/item?id=50456791)

**「Background」** Gemini Decision 1 joins an existing decision-model category already occupied by Jev and OpenAI&\#x27;s GPT-6 Luna, which return structured answers for constrained questions rather than free-form text. Jev uses the same three question formats Gemini supports—yes/no, choice, and rubric scoring—including the term “Noul” for a yes/no question; Jev accepts text and JSON only, while Gemini also accepts images, audio, video, and PDFs.

**「Cost and compatibility」** Developers who need yes/no, choice, or rubric decisions over audio, video, PDFs, images, and text can send those inputs directly to Gemini Decision 1. At 10 cents per million input tokens, however, it costs more than Jev&\#x27;s 4.2 cents per million, although Gemini&\#x27;s output is free; code that expects Jev- or OpenAI-style exact 1.0/0.0 yes/no answers must also handle Gemini&\#x27;s probability values such as 0.9234.

**「Community discussion」** Commenters asked how decision models calculate probabilities and whether developers are using them in coding harnesses; one described a cost calculation in which hundreds of short questions over a 100K-token context would cost roughly one search API call. Others said Gemini&\#x27;s higher price than Jev may be useful for audio and video inputs, while one commenter called the cost high but remained optimistic based on experience with another Gemma-based decision model.

**Tags**: `#Gemini API`, `#decision models`, `#AI developer tools`, `#Google AI`, `#model pricing`

---

<a id="item-tech-news-8"></a>
### [Anthropic IPO video details four-chip Claude strategy and a three-day AMD port](https://simonwillison.net/2026/Nov/11/anthropic-ipo-roadshow/) ⭐️ 7.0/10

Anthropic&\#x27;s IPO roadshow video, highlighted by Simon Willison, includes a &quot;Approach to compute&quot; segment in which co-founder Tom Brown says the company now trains and serves Claude across all four major chip families: AWS Trainium, Google TPUs, NVIDIA GPUs and AMD GPUs. Brown describes the multi-chip bet as unconventional because each chip needs its own tailored software and inference stack, and says Anthropic began working with AMD GPUs for the first time this year; where bringing on a new platform previously took dozens of engineers months, Anthropic says a system it calls Mythos got Claude running on AMD in three days with almost no human intervention, writing or porting nearly 100% of the kernels. Brown also describes a focus on &quot;total effective compute&quot; — physical capacity multiplied by discovered compute multipliers — and says Anthropic believes Claude will eventually discover such multipliers by itself as it approaches recursive self-improvement. These are the company&\#x27;s own claims from a roadshow presentation, not independently measured results, and Willison notes there is no official transcript; he published one he extracted with MacWhisper.

rss · Simon Willison · Nov 11, 15:11

**「Earlier hints and IPO context」** Anthropic had already hinted at a non-uniform compute fleet: a September postmortem of three recent incidents described bugs that affected only its TPU deployments. The roadshow video is part of the company&\#x27;s IPO marketing, and the same roadshow set a long-term adjusted operating margin target above 35% while disclosing that its seven co-founders would sell about $1.75 billion of stock in the offering.

**「Impact」** For organizations weighing AI hardware commitments, Anthropic&\#x27;s account puts a concrete number on porting cost: if a model can write nearly all of a new chip&\#x27;s kernels in three days rather than consuming dozens of engineers for months, the penalty for spanning multiple vendors falls and buyers gain more room to play AWS, Google, NVIDIA and AMD against each other. That rests entirely on Anthropic&\#x27;s own roadshow claim, with no independent verification of the three-day AMD port or of how much human oversight the process actually required.

<details><summary>References</summary>
<ul>
<li><a href="https://bingx.com/en/flash-news/post/anthropic-targets-adjusted-operating-margin-and-billion-founder-share-sale-in-ipo">Anthropic Targets 35% Long-Term Operating Margin; Founders to Sell...</a></li>

</ul>
</details>

**Tags**: `#Anthropic`, `#AI infrastructure`, `#multi-chip strategy`, `#IPO`, `#hardware`

---

<a id="item-tech-news-9"></a>
### [Paper argues &\#x27;AI slop&\#x27; is a community judgement, not a content property](https://www.reddit.com/r/MachineLearning/comments/1xtour7/ai_slop_is_a_social_judgement_r/) ⭐️ 7.0/10

A Reddit r/MachineLearning link post highlights a Nature Human Behaviour paper that reframes “AI slop” as a social judgement rather than a detectable property of content. According to the post, a community makes that judgement when it decides that some AI-generated content is unwanted, and studying slop this way is claimed to make it measurable and governable. The submission provides no methodology, data, or specific findings, so the paper’s proposed measures and governance implications cannot be verified from the supplied material alone.

reddit · r/MachineLearning · /u/learning\_by\_looking · Nov 11, 18:03

**「Background」** “AI slop” has been used as a loose label for AI-generated content that people find unwanted or low-quality, without an agreed way to identify it from the content itself. The Nature Human Behaviour paper is a conceptual social-science argument: it proposes that the label be studied as a community judgement, which is the precondition for its claim that slop can be measured and governed.

**「Governance needs community norms, not just detectors」** If &quot;slop&quot; is a community judgement rather than a property detectable in the content itself, a classifier&\#x27;s output cannot by itself establish that a post is slop: moderation and content-governance policies would have to name which community&\#x27;s norms are being applied and what those norms are. Wikipedia&\#x27;s existing entry already frames slop as content &quot;perceived as lacking in effort, quality, or meaning,&quot; which puts perception rather than an intrinsic artifact at the center of the label. The paper&\#x27;s authors present measurability and governability as the aim of the reframing, not as a demonstrated result, so the practical governance mechanism remains unverified from the linked material.

<details><summary>References</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/AI_slop">AI slop - Wikipedia</a></li>

</ul>
</details>

**Tags**: `#AI slop`, `#AI-generated content`, `#social science research`, `#content governance`, `#machine learning community`

---

<a id="item-tech-news-10"></a>
### [Report alleges Alice Huang moved 240,000 banned Nvidia chips to China](https://www.tomshardware.com/tech-industry/policy/alice-huang-reportedly-instrumental-in-securing-over-usd7-5-billion-of-nvidia-ai-gpu-imports-during-three-year-relationship-with-jensen-huang-helped-move-240-000-banned-chips-into-china-mostly-h100-and-h200) ⭐️ 7.0/10

The Information reported, according to Tom&\#x27;s Hardware, that Alice Huang used her relationship with Nvidia CEO Jensen Huang to help about 240,000 restricted Nvidia AI chips—mostly H100 and H200 GPUs—enter China, with imports valued at roughly $7.5 billion. The report names Shanghai Century Litong and Singapore-based Megaspeed as companies involved. The allegations have not been independently confirmed, and the supplied summary does not detail the evidence behind the figures.

telegram · zaihuapd · Nov 11, 14:41

**「Background」** Nvidia&\#x27;s H100 and H200 are data-center GPUs used for AI training and inference, and U.S. export controls restrict their sale to China absent a license, which is why the reported shipments are described as banned chips. The Information&\#x27;s investigation centers on whether intermediaries in Shanghai and Singapore were used to move such hardware into China, a routing pattern that falls within the scope of export-control enforcement.

**「Impact」** The allegation creates concrete compliance exposure for Nvidia&\#x27;s distribution chain: H100 and H200 exports to China are restricted, so the intermediaries named in the report could face scrutiny over end-user and end-use checks.

**Tags**: `#Nvidia`, `#AI芯片出口管制`, `#H100/H200`, `#供应链合规`, `#行业调查`

---

## Technology Blog

<a id="item-tech-blog-1"></a>
### [vLLM Encoder Disaggregation: Metadata-Only EPD for Multimodal Serving](https://vllm.ai/blog/2026-11-11-encoder-disaggregation-epd) ⭐️ 8.0/10

rss · vLLM Blog · Nov 11, 00:00

**「Background」** Multimodal requests pass through an encoder that turns images, video, and audio into embeddings before prefill and decode can run, and encoder demand varies with media size and modality independently of language-model load. Encoder/Prefill/Decode \(EPD\) disaggregation deploys these stages as separate vLLM instances so operators can scale each tier on its own hardware.

**「Solution」** In this progress report, the authors describe five changes. Metadata-only requests replace the downstream media item with a reference carrying the layout the encoder already computed—grids such as image\_grid\_thw, video timestamps, audio token counts—so the consumer rebuilds placeholders without re-fetching or re-preprocessing pixels; on an audio benchmark \(Qwen3-Omni-30B, MMAU test-mini, 1E+1PD, concurrency 64\) this raised throughput from 62.21 to 73.13 requests/s and cut mean latency from 980 to 853 ms, with accuracy moving from 75.90% to 75.65%, a gap the authors say needs investigation. Encoder-only instances get a dedicated Model Runner V2 path, CUDA Graph capture, and trimmed checkpoint loading, which on a pruned Kimi-K3 checkpoint dropped weight loading from 683 s to 0.31 s by reading 2 of 96 shards. Embeddings travel over NIXL or Mooncake, with per-modality output widths measured at init \(8192 visual, 2048 audio on Qwen3-Omni\) so buffers match, and failed transfers fail the affected request rather than crashing EngineCore. Mooncake Store adds cross-encoder cache reuse; in a controlled reassignment test on six H20 GPUs it cut repeated image encodings from 512 to zero and TTFT p50 from 1.209 to 0.819 s. Orchestration in vLLM Router, SMG, and llm-d scales all this independently. The results are honest: on DeepSeek V4.1 Flash, EPD beat the PD baseline by 6.6–9.5% per-GPU throughput only at concurrency 64–128 \(with 44–47% lower P90 TTFT\), lost at 16 and broke even at 32, and the 94–115% video gain folds in GPU preprocessing and NVDEC decoding. Cross-encoder reuse currently covers images only, with TP=1 and no dynamic LoRA.

**「Takeaway」** The authors argue that encoder disaggregation pays off only when media demand and load justify it, and that the remaining work is coordination—suppressing redundant encoding when prefill already has the embeddings, plus observability to tell compute, cache hits, and transfer apart.

**Tags**: `#multimodal serving`, `#encoder disaggregation`, `#vLLM`, `#remote embedding transfer`, `#GPU inference performance`

---

<a id="item-tech-blog-2"></a>
### [Glue Work Is Still a Trap in the AI Era](https://seangoedecke.com/glue-work-is-still-harmful-in-the-age-of-ai/) ⭐️ 5.0/10

rss · Sean Goedecke · Nov 11, 00:00

**「Background」** Sean Goedecke argues that glue work—the unglamorous coordination, reporting, documentation, and onboarding that keeps software teams running—is especially harmful when it depends on unrewarded volunteer labor; such processes, he says, ought to fail.

**「Solution」** He asks whether LLMs, now writing much of our code, free engineers to do more glue work, and answers no: he believes glue work matters less to companies than it did in the 2010s. His reasons are that AI agents let one engineer carry projects that once needed a small team, removing kickoff and status coordination; that the post-ZIRP labor market has reduced the influence of difficult gatekeepers who demanded consultation; that fewer junior hires mean less onboarding support; and that write-only “proof of work” reports can be generated with LLMs, since their purpose was never to be read. But he insists LLMs cannot automate all coordination: status checks, replies, and other interpersonal messages should be composed by the engineer, because making colleagues talk to an LLM will damage relationships. His prescription is to avoid becoming the permanent glue-work person, let bad processes fail, do small amounts of tactical glue work where it helps a project, and spend most time on code—driving AI agents and aligning them with company values.

**「Takeaway」** Goedecke’s conclusion is that AI reduces the write-only and coordination overhead that created glue-work roles without making human communication dispensable; engineers should use LLMs tactically but refuse to become the default coordinator.

**Tags**: `#glue work`, `#AI coding agents`, `#LLM communication`, `#software engineering culture`, `#coordination`

---

## Financial News

<a id="item-finance-news-1"></a>
### [Goolsbee calls October inflation report &\#x27;borderline disturbing&\#x27; as Fed weighs rate hikes](https://www.cnbc.com/2026/11/11/goolsbee-october-inflation-fed-rates-disturbing-distressing.html) ⭐️ 8.0/10

Chicago Fed President Austan Goolsbee called October&\#x27;s inflation report &quot;borderline disturbing&quot; after the consumer price index rose 0.4% on a seasonally adjusted basis, faster than economists had forecast and the third straight month of outsized increases. Other Fed officials said the central bank may need to act more decisively, and fed funds futures priced a December rate increase, with 15% odds of a half-point move, according to CME&\#x27;s FedWatch tool.

rss · CNBC Finance · Nov 11, 16:49

**「Background」** The Fed raised its benchmark rate by a quarter point — 0.25 percentage point — in September to a 3.75%-4% range and held it there in October; it normally moves in quarter-point steps, making a half-point increase unusually large.

**Tags**: `#Federal Reserve`, `#inflation`, `#interest rates`, `#monetary policy`, `#CPI`

---

<a id="item-finance-news-2"></a>
### [China Ends Transition Period for Offshore Trust Income Tax With Over RMB 160 Billion Declared](https://www.news.cn/20261111/9bcce99c779b4a6197ff45bbbc3e4c50/c.html) ⭐️ 8.0/10

China&\#x27;s State Taxation Administration said on November 11 that the 90-day transition period for taxing offshore trust income has ended, with more than RMB 160 billion in personal income tax cumulatively declared and over RMB 120 billion of that paid into government coffers in October alone. The authority attributed a nearly 90% year-on-year rise in national October personal income tax revenue partly to those payments, and said it will pursue back taxes and late fees from those who failed to declare or under-reported.

telegram · zaihuapd · Nov 11, 10:35

**「Background」** The 90-day window was set by a July 24, 2026 notice from the finance ministry and the tax authority, which waived late-payment surcharges for taxpayers who declared and paid offshore trust income tax within the period.

**「Who is affected」** High-net-worth individuals with offshore trust income who failed to declare or underreported now face demands to pay back taxes plus late-payment charges, and possible tax audits if they still do not correct their filings.

<details><summary>References</summary>
<ul>
<li><a href="https://t.me/zaihuapd/45068">在花 科技圈 – Telegram</a></li>

</ul>
</details>

**Tags**: `#offshore trusts`, `#personal income tax`, `#tax enforcement`, `#China fiscal policy`, `#high-net-worth taxation`

---

<a id="item-finance-news-3"></a>
### [FCC approves SpaceX&\#x27;s purchase of 800 MHz spectrum licenses](https://wap.cj.sina.cn/7x24/5206981) ⭐️ 7.0/10

The U.S. Federal Communications Commission approved SpaceX&\#x27;s acquisition of 546 paired 800 MHz licenses from Grain Management, covering nearly the entire U.S. population. After the deal, SpaceX would hold up to 89 MHz of low-band spectrum in each coverage area, and Verizon, AT&amp;T and T-Mobile have declined to give SpaceX access to their networks.

telegram · zaihuapd · Nov 11, 02:14

**「Background」** The FCC is the independent U.S. agency that regulates radio frequency use, so its approval is the regulatory step needed for a spectrum-license transfer to proceed.

**「Who is affected」** Because Verizon, AT&amp;T and T-Mobile declined to give SpaceX access to their networks, the 800 MHz licenses can only reach U.S. phone users if SpaceX builds its own radio network — leaving households and businesses in poorly covered areas waiting on a costly build-out before any new mobile option appears.

<details><summary>References</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/Federal_Communications_Commission">Federal Communications Commission - Wikipedia</a></li>

</ul>
</details>

**Tags**: `#SpaceX`, `#FCC`, `#spectrum licenses`, `#US telecom`, `#regulatory approval`

---