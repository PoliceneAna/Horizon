---
layout: default
title: "Horizon Summary: 2026-11-11 (EN)"
date: 2026-11-11
lang: en
---

> From 49 items, 15 important content pieces were selected

---

**Technology News**
1. [Microsoft announces .NET 11, a new major version of the platform](#item-tech-news-1) ⭐️ 9.0/10
2. [AMD Zen 6 Deep-Dive Details Core, I/O Die, and 32-Core Chiplets](#item-tech-news-2) ⭐️ 8.0/10
3. [DeepMind introduces AlphaProof Code for formal code verification](#item-tech-news-3) ⭐️ 8.0/10
4. [Protecting SSH Keys with macOS Secure Enclave](#item-tech-news-4) ⭐️ 7.0/10
5. [Synaptics patent claims halt open-source DisplayLink driver work](#item-tech-news-5) ⭐️ 7.0/10
6. [Essay argues AI-assisted coding yields fragile, opaque codebases](#item-tech-news-6) ⭐️ 7.0/10
7. [VulnCheck&\#x27;s November update tracks Anthropic-discovered vulnerabilities](#item-tech-news-7) ⭐️ 7.0/10
8. [Chrome and partners ship modern-web-guidance 1.0 for coding agents](#item-tech-news-8) ⭐️ 7.0/10
9. [MiniMax opens MiniMax H3 Image weights with 10-second 4K generation](#item-tech-news-9) ⭐️ 7.0/10
10. [Telegram Post Claims Public Launch of Gemini 4 Carbon](#item-tech-news-10) ⭐️ 7.0/10

**Technology Blog**
1. [vLLM&\#x27;s Encoder Disaggregation: Metadata-Only EPD for Multimodal Serving](#item-tech-blog-1) ⭐️ 8.0/10
2. [Why AI Makes Glue Work Less Important, Not More](#item-tech-blog-2) ⭐️ 5.0/10

**Financial News**
1. [Polymarket says annualized revenue has topped $1.8 billion](#item-finance-news-1) ⭐️ 7.0/10
2. [Fed Governor Waller Leans Toward December Rate Increase, Cites Possible Half-Point Move](#item-finance-news-2) ⭐️ 7.0/10
3. [FCC Approves SpaceX&\#x27;s 800 MHz Spectrum Acquisition](#item-finance-news-3) ⭐️ 7.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [Microsoft announces .NET 11, a new major version of the platform](https://devblogs.microsoft.com/dotnet/announcing-dotnet-11/) ⭐️ 9.0/10

Microsoft announced .NET 11, a new major release of its cross-platform development platform, in a devblogs post that points readers to the &quot;What&\#x27;s new in .NET 11&quot; documentation for the detailed feature list. The supplied announcement material provides limited version-level specifics, so individual API, runtime, and tooling changes could not be confirmed from it directly. Community commenters instead flagged concrete items they had read in the documentation, including runtime-level async support and a reported change in decimal literal parsing such as \(decimal\)0.1 producing 0.1000000000000000055511151231 in .NET 11 versus 0.1 in .NET 10.

hackernews · runesoerensen · Nov 10, 16:01 · [Discussion](https://news.ycombinator.com/item?id=50442225)

**「Background」** .NET 11 follows .NET 10 as the next major version of the platform, and its runtime documentation headlines Runtime Async, a new compilation model that Microsoft says the .NET runtime libraries themselves are already built with. Microsoft&\#x27;s runtime notes for .NET 11 also list updated minimum hardware requirements alongside JIT, ReadyToRun, and WebAssembly improvements. Opting an application&\#x27;s own code into Runtime Async is a separate choice, and Microsoft advises testing dependencies and diagnostics before adopting it.

**「Decimal compatibility check」** A community commenter reported that casting 0.1 to decimal yields 0.1 under .NET 10 but 0.1000000000000000055511151231 under .NET 11, and pointed readers to Microsoft&\#x27;s compatibility notes. Applications that rely on decimal for currency or exact arithmetic should verify this reported behavior against the compatibility documentation and test it before upgrading.

**「Community discussion」** Commenters argued that C\# and .NET remain underappreciated largely because of legacy perception — that .NET is Windows-only or that little has changed since .NET Framework — while an ex-Microsoft commenter said large Office, Security, and Azure services run on .NET Core across both Windows and Linux. One commenter highlighted the reported decimal parsing behavior change as a compatibility concern, and another expressed surprise that runtime async support could deliver equivalent performance without compiler-generated state machines.

<details><summary>References</summary>
<ul>
<li><a href="https://learn.microsoft.com/en-us/dotnet/core/whats-new/dotnet-11/runtime">What&#x27;s new in .NET 11 runtime | Microsoft Learn</a></li>
<li><a href="https://devblogs.microsoft.com/dotnet/announcing-dotnet-11/">Announcing .NET 11 - .NET Blog - devblogs.microsoft.com</a></li>

</ul>
</details>

**Tags**: `#dotnet`, `#C\#`, `#Microsoft`, `#software release`, `#compatibility`

---

<a id="item-tech-news-2"></a>
### [AMD Zen 6 Deep-Dive Details Core, I/O Die, and 32-Core Chiplets](https://chipsandcheese.com/p/amds-zen-6-family-feeding-the-beast) ⭐️ 8.0/10

A Chips and Cheese technical deep-dive examines AMD&\#x27;s Zen 6 architecture, covering changes to both the core and I/O die. The core-level material includes a reduction in integer multiply units from three to two, PDEP/PEXT throughput falling from three to two instructions per cycle, four vector loads per cycle at 256 bits or less, and a 32-core &quot;C&quot; core chiplet with increased L3 cache. The article also addresses the new I/O die, which commenters expect to move to a smaller node; that expectation is community discussion rather than a confirmed specification.

hackernews · pixelpoet · Nov 10, 17:02 · [Discussion](https://news.ycombinator.com/item?id=50443090)

**「Background」** AMD&\#x27;s consumer CPUs use a chiplet layout: CPU cores sit on core complex dies, while memory and I/O functions sit on a separate I/O die. Zen 4 and Zen 5 on AM5 are the immediate predecessors, and commenters identify their I/O-die memory controller as a limitation when both memory channels are populated. Zen 5 also introduced 2-ahead branch prediction, making Zen 6&\#x27;s branch-predictor changes an evolution of that prior design.

**「Impact」** For AM5 users, the memory controller remains the practical bottleneck: a commenter reports that Zen 4/5 systems are extremely hard or impossible to push above 3600 MT/s when using both memory channels, making the I/O die the part to watch for anyone tuning AM5 memory speeds.

**「Community discussion」** Commenters focused on the memory controller, with one calling an improved I/O die the top Zen 6 priority and reporting that Zen 4/5 AM5 systems struggle above 3600 MT/s with both memory channels. Others debated whether cutting integer multiply and PDEP/PEXT throughput are linked, speculated that freed area serves VNNI pipes, and asked how a 32-core CCD would be organized below the NUMA level.

**Tags**: `#amd`, `#cpu-architecture`, `#zen6`, `#hardware`, `#chips`

---

<a id="item-tech-news-3"></a>
### [DeepMind introduces AlphaProof Code for formal code verification](https://deepmind.google/blog/introducing-alphaproof-code/) ⭐️ 8.0/10

DeepMind has introduced AlphaProof Code, an AI agent for formal verification of software that generates machine-checkable proofs, with community discussion identifying Lean as the proof language. The available material presents this as a vendor announcement: it provides no supported language list, version, release date, or independent benchmark results. DeepMind&\#x27;s stated capabilities should therefore be read as announced rather than independently measured.

hackernews · ilreb · Nov 10, 12:11 · [Discussion](https://news.ycombinator.com/item?id=50439193)

**「Background」** Formal verification proves that code satisfies a mathematical specification, with a proof assistant such as Lean checking each proof step rather than relying on tests alone. DeepMind&\#x27;s work builds on earlier formal-verification efforts that covered only smaller portions of code; according to Signal&\#x27;s CTO, AlphaProof Code is intended to expand that scope, and reporting on the work says the agent produced 6.5 million lines of checked proof for Signal&\#x27;s encryption code over four weeks.

**「Impact」** Teams adopting AlphaProof Code would still need to validate the specifications and theorems supplied to the agent, because a successful proof establishes only that code meets those stated properties. Community reports that AI-generated Lean proofs can be gamed point to adversarial review of generated proofs as a practical safeguard.

**「Community Discussion」** Commenters questioned what a clean verification result establishes: hedora doubted that a nontrivial library could have zero bugs and suspected either incorrect theorems or narrowly scoped properties, while thibsrn noted that the agent appears to check implementation against a specification rather than challenge the specification itself. r0ze-at-hn reported experimenting with AI-generated Lean and warned that the model can &quot;cheat&quot; when writing proofs, recommending a separate adversarial prompt to review the output.

<details><summary>References</summary>
<ul>
<li><a href="https://deepmind.google/blog/introducing-alphaproof-code/">Formal Verification of Signal’s Protocol with... — Google DeepMind</a></li>
<li><a href="https://shiftdelete.net/en/alphaproof-code">AlphaProof Code Verifies Signal Encryption at Machine Level</a></li>

</ul>
</details>

**Tags**: `#AI formal verification`, `#Lean theorem proving`, `#code verification`, `#DeepMind`, `#program proofs`

---

<a id="item-tech-news-4"></a>
### [Protecting SSH Keys with macOS Secure Enclave](https://gatezh.com/posts/macos-secure-enclave-ssh-keys/) ⭐️ 7.0/10

A practical guide explains how macOS users can protect SSH private keys by storing them in the Secure Enclave, with access gated by Touch ID or user presence. It is aimed at developers and security-conscious engineers implementing the approach on their own machines, not at a new Apple release or a shipped third-party feature. The supplied discussion treats the method as useful but flags reliability after system upgrades, fingerprint fatigue from frequent prompts, and incompatibility with fully headless automation. Because no article text is supplied, the guide&\#x27;s exact commands, supported key types, and limitations cannot be verified here.

hackernews · js2 · Nov 11, 04:28 · [Discussion](https://news.ycombinator.com/item?id=50449748)

**「Background」** Apple&\#x27;s Secure Enclave is a hardware-backed key store whose private keys are designed to be non-exportable; on macOS, access can be gated by Touch ID or Apple Watch authentication, and tools such as Secretive use this capability for SSH signing. Secretive still relies on Keychain APIs to locate and read those keys—making bundle-ID consistency important—while an alternative native route uses \`sc\_auth\` with \`ssh-keychain.dylib\` instead of a separate app.

**「Impact」** Developers who use Secure Enclave-backed SSH keys for unattended work should plan a separate credential path: a commenter reports that Secretive cannot access the enclave when the machine is headless and no user is logged in, even when the key is set to notify rather than require Touch ID. The same discussion suggests keeping low-risk development keys outside the human-presence flow to avoid training users to approve prompts reflexively.

**「Community Discussion」** Commenters found the approach useful but reported concrete failure modes: one said WireGuard lost keychain-backed profiles after a macOS upgrade because the app could no longer open the keychain, and another described fingerprint fatigue after 20 daily approval requests. A third argued the Secure Enclave model scales poorly for headless agentic development because access requires a logged-in human, while others recommended Secretive or a hardware token such as TKey for SSH key handling.

<details><summary>References</summary>
<ul>
<li><a href="https://termique.app/blog/ssh-keys-macos-touch-id/">SSH Keys on macOS with Touch ID: Secure Enclave Setup (2026)</a></li>
<li><a href="https://github.com/maxgoedjen/secretive">GitHub - maxgoedjen/secretive: Protect your SSH keys with ... Secure SSH Keys with Secure Enclave on macOS | Pavel Popov Use TouchID for ssh with Secretive | BK&#x27;s Blog SSH key and Touch ID on Mac, the Secretive setup Protect your SSH keys with Touch ID on macOS - Korben Protecting SSH Keys with macOS Secure Enclave (Native ...</a></li>

</ul>
</details>

**Tags**: `#macOS Secure Enclave`, `#SSH keys`, `#security`, `#keychain`, `#automation`

---

<a id="item-tech-news-5"></a>
### [Synaptics patent claims halt open-source DisplayLink driver work](https://lwn.net/SubscriberLink/1102549/acbc92e00cee3a3f/) ⭐️ 7.0/10

Synaptics has asserted patent-infringement claims against open-source DisplayLink driver work, and development on those drivers has stopped, according to an LWN report. The dispute affects Linux users and developers who depend on DisplayLink for display output through docking stations. A demand letter quoted in the discussion seeks US$25,000 in compensation if its demands are not met by a stated deadline; the available material does not show that the claims have been adjudicated in court.

hackernews · speckx · Nov 10, 18:02 · [Discussion](https://news.ycombinator.com/item?id=50443824)

**「Background」** DisplayLink is Synaptics&\#x27; proprietary display-over-USB technology; its Ubuntu support is distributed through Synaptics&\#x27; own APT repository or a standalone installer rather than as an upstream kernel driver. An earlier open-source attempt, the Rust-based &quot;Vino&quot; driver built partly with AI and via clean-room reverse engineering, disappeared after Synaptics sent legal threats, establishing a pattern that precedes the current halt to DisplayLink driver work.

**「Impact」** Linux users who rely on DisplayLink docks for additional monitors have fewer options for community-maintained support now that open-source driver work has stopped; Synaptics distributes its own Ubuntu driver through its APT repository or a standalone installer. That leaves driver compatibility and updates tied to vendor-provided packages rather than community fixes.

**「Community Discussion」** Commenters disputed the legal basis for treating reverse engineering as patent infringement, arguing that patents publicly disclose an invention in exchange for marketing exclusivity and that a trade-secret claim would be the more appropriate theory. Several also called the US$25,000 demand unreasonable or a scare tactic, while others described replacing DisplayLink docks with USB-C/DisplayPort Alt Mode hardware.

<details><summary>References</summary>
<ul>
<li><a href="https://www.phoronix.com/news/Synaptics-Blocks-Vino-Driver">Synaptics Appears To Use Legal Threats To Block Open - Source ...</a></li>
<li><a href="https://www.synaptics.com/products/displaylink-graphics/downloads/ubuntu">Ubuntu Driver for Downloads Section | Synaptics</a></li>
<li><a href="https://www.synaptics.com/products/displaylink-graphics/downloads/ubuntu">Ubuntu Driver for Downloads Section | Synaptics</a></li>

</ul>
</details>

**Tags**: `#open source`, `#patents`, `#Linux drivers`, `#DisplayLink`, `#hardware support`

---

<a id="item-tech-news-6"></a>
### [Essay argues AI-assisted coding yields fragile, opaque codebases](https://evanxmerz.com/post/ai-usage-generates-a-fragile-codebase/) ⭐️ 7.0/10

An essay argues that AI-assisted development can produce fragile, opaque codebases, raising code-quality and maintainability concerns for developers and teams using AI coding tools. The supplied item does not include the essay&\#x27;s underlying data or methodology, so its claims are presented as an argument rather than a measured result. The post drew a substantial Hacker News discussion, with commenters disputing whether its criticisms still apply to current AI coding models and practices.

hackernews · plun9 · Nov 10, 10:25 · [Discussion](https://news.ycombinator.com/item?id=50438318)

**「Context: generation speed vs. maintainability」** AI-assisted coding tools generate code from natural-language prompts and can produce working results quickly, but they do not by themselves enforce a codebase&\#x27;s design conventions, test depth, or readability. The article&\#x27;s argument therefore turns on the gap between generation speed and the review and testing practices that keep code maintainable.

**「Community discussion」** Commenters disagree over whether the critique is current: iagooar argues that newer models and explicit anti-overengineering instructions mitigate shallow tests and unnecessary complexity, while momojo acknowledges the fragility and opacity described and compares AI-generated code to mass-produced injection-molded parts. peterbell\_nyc asks what adversarial reviews and deterministic maintainability gates the author used, framing review discipline and tooling as central to the argument.

**Tags**: `#AI-assisted coding`, `#code quality`, `#software maintainability`, `#engineering practices`, `#Hacker News discussion`

---

<a id="item-tech-news-7"></a>
### [VulnCheck&\#x27;s November update tracks Anthropic-discovered vulnerabilities](https://www.vulncheck.com/blog/anthropic-glasswing-november-update) ⭐️ 7.0/10

VulnCheck published a November update to its tracking of vulnerabilities discovered by Anthropic, covering findings tied to Project Glasswing, Anthropic&\#x27;s AI-driven vulnerability-discovery effort. The post is a vendor-maintained tracking list rather than an announcement of new model capability, and the supplied material does not give the number of entries, CVE identifiers, affected projects, or disclosure dates. Hacker News discussion focused on whether public tracking can represent the real impact of AI-assisted bug finding.

hackernews · panic · Nov 10, 22:17 · [Discussion](https://news.ycombinator.com/item?id=50447074)

**「Background」** Project Glasswing is Anthropic’s AI-assisted vulnerability-discovery effort, and VulnCheck’s November update assesses it seven months into the project. By that point VulnCheck had tracked 442 CVEs attributable to Anthropic—roughly 0.5% of all CVEs published that year—with only two identified as exploited in the wild.

**「Impact」** VulnCheck reports that seven months into Project Glasswing it has tracked 442 Anthropic-attributable CVEs—about 0.5% of all CVEs published this year—while only two have been observed exploited in the wild. For open-source maintainers and security teams, that makes exploit evidence and reachability more useful triage criteria than raw AI-generated report volume; Anthropic&\#x27;s opt-in OSS Scanner also sends AI reports to projects without human review, so recipients need a process for unsolicited findings.

**「Community discussion」** Commenters disputed whether the tracked data can measure AI-assisted discovery&\#x27;s impact: one said the ledger covers only Anthropic&\#x27;s coordinated disclosure program for open-source software while Project Glasswing findings often land in partners&\#x27; proprietary code, and another said serious issues in private codebases never receive CVE numbers. A separate reported experience was positive: nine Fil-C issues flagged by Anthropic were all real bugs with no false positives, though the commenter used the proposed fixes mainly as inspiration rather than applying them wholesale.

<details><summary>References</summary>
<ul>
<li><a href="https://www.vulncheck.com/blog/anthropic-glasswing-november-update">After 7-months, Glasswing Overwelms Maintainers with... | VulnCheck</a></li>
<li><a href="https://thehackernews.com/2026/10/anthropic-launches-free-ai.html">Anthropic Launches Free AI Vulnerability Scanner for Open-Source...</a></li>
<li><a href="https://www.vulncheck.com/blog/anthropic-glasswing-november-update">After 7-months, Glasswing Overwelms Maintainers with... | VulnCheck</a></li>

</ul>
</details>

**Tags**: `#AI-assisted security`, `#vulnerability discovery`, `#software security`, `#Anthropic`, `#CVE tracking`

---

<a id="item-tech-news-8"></a>
### [Chrome and partners ship modern-web-guidance 1.0 for coding agents](https://github.com/GoogleChrome/modern-web-guidance) ⭐️ 7.0/10

Chrome, with Firefox, MDN, and Edge, has released version 1.0 of modern-web-guidance, an open-source agent skill and CLI containing more than 200 curated guides intended to make coding agents prefer native browser APIs over older JavaScript patterns. The package is about 1.7MB, includes a pure-JS search index reported at roughly 7MB with ~10ms query times, and adds a deterministic legacy-scan trained on 30,000 GitHub repos to identify patterns agents can modernize. The project reports that agents using the guidance passed 92% of about 1,700 Playwright/AST assertions across 200 tasks, up from 55% unguided; those evaluation and performance figures are vendor claims, not independent measurements. It is available through npx modern-web-guidance@latest install, search, and legacy-scan commands.

hackernews · paulirish · Nov 10, 18:01 · [Discussion](https://news.ycombinator.com/item?id=50443812)

**「Why this guidance exists」** Modern browsers now natively handle tasks that previously required custom JavaScript or dependencies — the source cites \`&lt;dialog&gt;\` and \`showModal\(\)\` for modal focus and backdrop behavior, \`CSS.highlights\` for text-range highlighting, and \`field-sizing\` for auto-growing textareas. The project&\#x27;s premise is that coding agents often recognize these APIs by name but still default to incumbent \`&lt;div&gt;\`-plus-JavaScript patterns, so the guidance supplies platform-specific domain knowledge at generation time.

**「Impact」** Developers adopting the skill should check recommended APIs against their target browsers: a commenter lists features such as CSS @function, calc-size\(\), and flex-wrap: balance as stable in Chrome but unsupported in Firefox and Safari, so agent-generated code could widen cross-browser gaps despite the collaboration with Firefox and Edge.

**「Community discussion」** Commenters surfaced a cross-browser tension: surround listed guidance-recommended features that are stable in Chrome but not supported by Firefox or Safari, while advisedwang argued that LLMs following Chrome&\#x27;s guidance could further entrench one browser and revive “view in \[dominant browser\]” warnings. simonw suggested publishing a grep-friendly Markdown index on GitHub Pages so agents can fetch guidance over HTTP without installing the npm package, and bakkoting reported filing an issue about using fromBase64/toBase64 instead of atob/btoa.

**Tags**: `#coding-agents`, `#web-platform`, `#open-source`, `#browser-standards`, `#developer-tools`

---

<a id="item-tech-news-9"></a>
### [MiniMax opens MiniMax H3 Image weights with 10-second 4K generation](https://huggingface.co/MiniMaxAI/MiniMax-H3-Image) ⭐️ 7.0/10

MiniMax released open weights for MiniMax H3 Image, an image model for developers and image-generation users that supports text-to-image, image-reference, and image-editing workflows and is available on Hugging Face and through MiniMax&\#x27;s API. The company says the model can produce 4096×4096 images—about 16 megapixels—in roughly 10 seconds and accept up to 16 reference images. It also claims standard-mode generation at 1.5–2× the speed of “mainstream tools” and 3–4× in a Highspeed mode; these figures are vendor claims without independent benchmarks. Standard 4K generation is listed at about $0.069 per image, with a launch-week price of about $0.034, and the model is integrated into MiniMax Code and Hailuo.

telegram · zaihuapd · Nov 10, 15:39

**「Background」** “Open weights” means MiniMax published the model’s trained parameters for download on Hugging Face, so the model can be run locally or adapted, not only accessed through a hosted API. The stated 4096×4096 output is roughly 16 megapixels, the resolution the release describes as 4K.

**「Impact」** Developers can download the weights from Hugging Face to test 4K, multi-reference image editing with self-hosting, or use the API at the listed per-image price; the source does not specify hardware requirements for local deployment.

**Tags**: `#image-generation`, `#open-weights`, `#text-to-image`, `#image-editing`, `#minimax`

---

<a id="item-tech-news-10"></a>
### [Telegram Post Claims Public Launch of Gemini 4 Carbon](https://deepmind.google/models/model-cards/gemini-4-carbon/) ⭐️ 7.0/10

A Telegram post claims Google has made Gemini 4 Carbon publicly available as its flagship model, emphasizing cybersecurity and long-horizon agent workflows and ranking it first on benchmarks including CursorBench 4.0. The post says the model is offered through the Gemini API, Google AI Studio and Gemini for business at $2 per million input tokens and $10 per million output tokens—the same price as Argon—and is in preview for /swarm multi-agent collaboration in Antigravity. It also claims Gemini 4 Carbon costs more than 2x less than the next-best external model, but the item is a single promotional post with no independent verification or technical detail.

telegram · zaihuapd · Nov 10, 15:48

**「Built on the prior Gemini 4 release」** Gemini 4 Carbon is built on Gemini 4 Argon, the flagship Google DeepMind shipped immediately before it: the Carbon model card lists Argon as the base and describes text, image, audio and video inputs within a combined input-output context window of up to 1M tokens. The source post also notes Carbon carries Argon&\#x27;s pricing — $2 per million input tokens and $10 per million output tokens.

**「Impact」** If the stated availability holds, developers building security or long-horizon agent applications could use Gemini 4 Carbon through the Gemini API at the quoted $2/$10 per-million-token rates; they should verify the model card, quotas and benchmark methodology before relying on the launch or pricing claims.

<details><summary>References</summary>
<ul>
<li><a href="https://deepmind.google/models/model-cards/gemini-4-carbon/">Gemini 4 Carbon - Model Card — Google DeepMind</a></li>
<li><a href="https://www.youtube.com/watch?v=sUcvhFGc4mw">Inside the lab: How Google built Gemini 4 for coding agents - YouTube</a></li>

</ul>
</details>

**Tags**: `#Gemini 4 Carbon`, `#Google DeepMind`, `#AI models`, `#AI agents`, `#cybersecurity`

---

## Technology Blog

<a id="item-tech-blog-1"></a>
### [vLLM&\#x27;s Encoder Disaggregation: Metadata-Only EPD for Multimodal Serving](https://vllm.ai/blog/2026-11-11-encoder-disaggregation-epd) ⭐️ 8.0/10

rss · vLLM Blog · Nov 11, 00:00

**「Background」** Multimodal inference adds an encoding stage — images, video frames, and audio become embeddings — before prefill and decode, and its demand shifts with media size and modality independently of language-model load. vLLM&\#x27;s EPD disaggregation deploys encoder, prefill, and decode as separate instances, but earlier handoffs still made the downstream consumer re-fetch, decode, and preprocess media the encoder had already handled.

**「Solution」** The post describes five changes. Metadata-only requests replace downstream media with encoder-published structural metadata — image\_grid\_thw, video\_grid\_thw plus timestamps for Qwen3-VL, audio token counts — so consumers rebuild placeholders while embeddings arrive through NIXL \(CPU EC\) or Mooncake TransferEngine. A dedicated Model Runner V2 MMEncoderModelRunner skips token sampling and irrelevant checkpoint shards: on a pruned Kimi-K3 checkpoint it read 2 of 96 shards, cutting load from 683s to 0.31s. Transfer buffers now carry per-modality widths, since Qwen3-Omni emits 8192-wide visual and 2048-wide audio outputs. Mooncake Store adds cross-encoder reuse; in a six-H20 reassignment run, repeated encodings dropped from 512 to zero and TTFT p50 fell from 1.209 to 0.819s. Audio metadata-only lifted throughput from 62.21 to 73.13 requests/s, though accuracy slipped from 75.90% to 75.65%, which the authors say remains to be investigated. For DeepSeek V4.1 Flash on GB200, EPD beat PD by 6.6–9.5% per-GPU throughput and 44–47% lower P90 TTFT at concurrency 64–128 counting all 12 GPUs, but lost at 16 and broke even at 32. Because metadata-only consumers lack the original media, failed transfers now fail the affected request rather than risking EngineCore.

**「Takeaway」** The authors&\#x27; point is that EPD works by removing duplicated preprocessing and shared-state friction, not by separation itself — the gains appear only under the right load and reuse conditions, and remain vendor- and community-run measurements.

**Tags**: `#encoder disaggregation`, `#multimodal serving`, `#vLLM`, `#remote embedding transfer`, `#cross-encoder caching`

---

<a id="item-tech-blog-2"></a>
### [Why AI Makes Glue Work Less Important, Not More](https://seangoedecke.com/glue-work-is-still-harmful-in-the-age-of-ai/) ⭐️ 5.0/10

rss · Sean Goedecke · Nov 11, 00:00

**「Background」** Glue work is the informal, often unrewarded coordination labor—meetings, updates, onboarding, reports—that keeps software teams running. Sean Goedecke, who has argued that processes dependent on such sacrifice should fail, asks whether LLM-written code frees engineers to do more of it.

**「Solution」** He argues the opposite: glue work is less important to companies than it was in the 2010s, for four asserted reasons. AI agents let one engineer take on work that once required a small team, reducing coordination tasks like kickoffs and status meetings; the end of ZIRP \(zero-interest-rate policy\), he says, forced out or moderated many ego-driven gatekeepers, lowering the need to manage difficult people; fewer junior hires mean less informal onboarding; and LLMs can quickly produce write-only “proof of work” reports and compliance templates, even if nobody reads them. He insists this does not mean all glue work can be automated: communicating with colleagues—status checks, replies, pings—should be written by the engineer, because delegating it to an LLM will damage relationships.

**「Takeaway」** His conclusion is that engineers should still avoid becoming “the glue work person” and let bad processes fail, while doing only small tactical glue work that helps their projects. Most effort, he says, should remain on code and on directing AI agents toward company values.

**Tags**: `#glue work`, `#AI coding agents`, `#engineering culture`, `#career advice`, `#team coordination`

---

## Financial News

<a id="item-finance-news-1"></a>
### [Polymarket says annualized revenue has topped $1.8 billion](https://www.cnbc.com/2026/11/10/polymarket-annualized-revenue-us-growth.html) ⭐️ 7.0/10

Polymarket told CNBC its annualized revenue has surpassed $1.8 billion, up from more than $1 billion reported in June, as its U.S. exchange saw over $14.5 billion in notional volume in October versus $4 billion in June. The company has also begun a $1 billion funding round valuing it at $21 billion, while it faces a Commodity Futures Trading Commission investigation into its advertising practices and past access restrictions for U.S. residents.

rss · CNBC Finance · Nov 10, 13:00

**「Background」** Polymarket launched its U.S. exchange in May 2026 as a separate venue from its offshore platform, which it had promised to keep closed to U.S. users under a 2022 settlement with the Commodity Futures Trading Commission. The CFTC is now investigating whether Polymarket violated that settlement, which underpins the regulatory risk hanging over its domestic growth.

<details><summary>References</summary>
<ul>
<li><a href="https://www.reuters.com/business/finance/us-agency-is-again-probing-if-polymarket-broke-2022-settlement-sources-says-2026-10-27/">US agency is again probing if Polymarket broke 2022 ...</a></li>

</ul>
</details>

**Tags**: `#Polymarket`, `#prediction markets`, `#revenue growth`, `#private financing`, `#CFTC regulation`

---

<a id="item-finance-news-2"></a>
### [Fed Governor Waller Leans Toward December Rate Increase, Cites Possible Half-Point Move](https://www.cnbc.com/2026/11/10/fed-governor-waller-sees-december-hike-likely.html) ⭐️ 7.0/10

Federal Reserve Governor Christopher Waller said he leans toward a December rate increase and would consider a half-point \(0.5 percentage point\) move if inflation readings are hotter than forecast. October CPI rose 0.4% for headline and 0.3% for core prices excluding food and energy, each 0.1 percentage point above consensus, and traders fully priced a quarter-point December increase while assigning 12.5% odds to a half-point move.

rss · CNBC Finance · Nov 10, 17:13

**「Background」** The Fed held rates steady at its October meeting after a quarter-point increase in September; Waller argued that failing to carry out expected increases would loosen policy in an undesirable way and risk the central bank&\#x27;s credibility.

**Tags**: `#Federal Reserve`, `#monetary policy`, `#interest rates`, `#inflation`, `#CPI`

---

<a id="item-finance-news-3"></a>
### [FCC Approves SpaceX&\#x27;s 800 MHz Spectrum Acquisition](https://wap.cj.sina.cn/7x24/5206981) ⭐️ 7.0/10

The U.S. Federal Communications Commission approved SpaceX&\#x27;s acquisition of 546 paired 800 MHz spectrum licenses through a deal with Grain Management, covering nearly the entire U.S. population.

telegram · zaihuapd · Nov 11, 02:14

**「Background」** The 800 MHz band is low-band, paired spectrum that travels far and penetrates buildings, making it useful for nationwide mobile coverage; the FCC said the licenses had been underutilized in recent years.

**「Impact」** US wireless carriers face a new competitor, and households could gain an alternative mobile coverage option, because SpaceX&\#x27;s low-band licenses cover nearly the entire population and penetrate buildings, while Verizon, AT&amp;T and T-Mobile declined to grant it network access.

<details><summary>References</summary>
<ul>
<li><a href="https://arstechnica.com/tech-policy/2026/10/starlink-spectrum-deal-boosts-musk-plan-to-beat-att-t-mobile-and-verizon/">Starlink spectrum deal boosts Musk plan to beat AT... - Ars Technica</a></li>
<li><a href="https://www.phonearena.com/news/spacex-closer-to-becoming-threat-to-t-mobile-verizon-and-at-t_id184460">SpaceX could soon turn up the heat on T - Mobile , Verizon , and AT &amp; T</a></li>
<li><a href="https://finance.yahoo.com/technology/articles/real-consequences-t-verizon-t-134500537.html">‘Real consequences’: AT&amp;T, Verizon and T-Mobile warn FCC as Elon...</a></li>
<li><a href="https://www.thenews.com.pk/latest/1419259-spacex-vs-telecom-elon-musks-starlink-enters-mobile-marketwhat-to-know">SpaceX vs. Telecom : Elon Musk&#x27;s Starlink enters mobile...</a></li>

</ul>
</details>

**Tags**: `#FCC`, `#SpaceX`, `#spectrum acquisition`, `#US telecom`, `#regulation`

---