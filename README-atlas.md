<p align="center">
  <img src="kryptokat-atlas.png" alt="KryptoKat — Hacker Cat at the Terminal" width="420">
</p>

<h1 align="center">🐾 MITRE ATLAS — A KryptoKat Field Guide 🐾</h1>
<h3 align="center"><i>Adversarial Threat Landscape for Artificial-Intelligence Systems</i></h3>
<h4 align="center"><i>"ATT&CK, but the cat is hunting your model."</i></h4>

<p align="center">
  <a href="https://atlas.mitre.org/"><img src="https://img.shields.io/badge/MITRE-ATLAS-red?style=for-the-badge" alt="MITRE ATLAS Badge"></a>
  <a href="https://github.com/mitre-atlas/atlas-data"><img src="https://img.shields.io/badge/Data-atlas--data-black?style=for-the-badge&logo=github" alt="ATLAS Data Repo"></a>
  <img src="https://img.shields.io/badge/Made%20by-KryptoKat-ff1493?style=for-the-badge" alt="Made by KryptoKat">
</p>

---

## 🐈‍⬛ What is this?

A practitioner reference for **MITRE ATLAS** — the **Adversarial Threat Landscape for Artificial-Intelligence Systems**. Where MITRE ATT&CK catalogs adversary tactics against traditional IT, ATLAS catalogs them against ML and AI systems — including the AI-specific tactics that don't exist anywhere else (like **ML Attack Staging**) and the AI-twisted versions of classic tactics (like reconnaissance via inference APIs).

ATLAS originated in 2020 as a Microsoft + MITRE collaboration called the *Adversarial ML Threat Matrix*. It is now a community-driven framework with regular updates from contributors including Zenity Labs.

> *"ATT&CK is for the network. ATLAS is for the model. KryptoKat reads both before breakfast."*

**Current scope (v5.4.0, February 2026):**

| Component | Count |
|---|---|
| Tactics | 16 |
| Techniques | 84 |
| Sub-techniques | 56 |
| Mitigations | 32 |
| Real-world case studies | 42 |

---

## 📚 Official Sources (Read These First)

| Resource | Link |
|---|---|
| 🌐 MITRE ATLAS Website | https://atlas.mitre.org |
| 🐙 ATLAS Data Repository (YAML / JSON / STIX 2.1) | https://github.com/mitre-atlas/atlas-data |
| 🛠️ ATLAS Navigator | https://mitre-atlas.github.io/atlas-navigator/ |
| 📊 Case Studies | https://atlas.mitre.org/studies |
| 🛡️ Mitigations | https://atlas.mitre.org/mitigations |
| 🤝 AI Incident Sharing Initiative | https://ai-incidents.mitre.org |
| 🗺️ MITRE ATT&CK (the parent framework) | https://attack.mitre.org |

---

## 🎯 The 16 ATLAS Tactics at a Glance

Tactics represent the **why** of an attack — the adversary's tactical goal. Techniques (covered below) are the **how**.

| # | Tactic | ID | KryptoKat's Translation |
|---|---|---|---|
| 1 | [Reconnaissance](#-1-reconnaissance--amltao0043) | AML.TA0043 | Cat is studying the litterbox before pouncing |
| 2 | [Resource Development](#-2-resource-development--amltao0042) | AML.TA0042 | Cat is acquiring catnip and tools |
| 3 | [Initial Access](#-3-initial-access--amltao0001) | AML.TA0001 | Cat found the cat door |
| 4 | [AI Model Access](#-4-ai-model-access--amltao0000) | AML.TA0000 | Cat got into the room with the model |
| 5 | [Execution](#-5-execution--amltao0002) | AML.TA0002 | Cat is running unauthorized code on the keyboard |
| 6 | [Persistence](#-6-persistence--amltao0003) | AML.TA0003 | Cat is staying. Forever. |
| 7 | [Privilege Escalation](#-7-privilege-escalation--amltao0004) | AML.TA0004 | Cat is now an admin cat |
| 8 | [Defense Evasion](#-8-defense-evasion--amltao0005) | AML.TA0005 | Cat is invisible. Cat was never here. |
| 9 | [Credential Access](#-9-credential-access--amltao0006) | AML.TA0006 | Cat has your API keys |
| 10 | [Discovery](#-10-discovery--amltao0007) | AML.TA0007 | Cat is mapping the house from the inside |
| 11 | [Collection](#-11-collection--amltao0009) | AML.TA0009 | Cat is gathering all the things |
| 12 | [AI Attack Staging](#-12-ai-attack-staging--amltao0012) | AML.TA0012 | Cat is sharpening claws and crafting payloads |
| 13 | [Command and Control](#-13-command-and-control--amltao0011) | AML.TA0011 | Cat takes orders from a remote cat |
| 14 | [Exfiltration](#-14-exfiltration--amltao0010) | AML.TA0010 | Cat is leaving with the goods |
| 15 | [Impact](#-15-impact--amltao0040) | AML.TA0040 | Cat broke the model. The model stays broken. |
| 16 | [AI-Specific Impact](#-16-ai-specific-impact--newer-additions) | (newer) | Cat made the model do something cats shouldn't |

> ⚠️ ATLAS borrows most tactic names from ATT&CK but applies AI-specific techniques to them. Two tactics — **AI Model Access** and **AI Attack Staging** — are unique to ATLAS.

---

## 🐱 1. Reconnaissance — `AML.TA0043`

> *"Before the pounce, the cat watches."*

### Description
Reconnaissance is the adversary's information-gathering phase — collecting intelligence about a target AI system to plan subsequent operations. This includes mapping the model's architecture and family, enumerating its training data sources, identifying exposed inference APIs, profiling deployment infrastructure, and reading the public artifacts the AI team has voluntarily released (papers, model cards, blog posts, GitHub repos). In ATLAS, reconnaissance is unusually productive compared to traditional IT recon because the AI/ML community publishes far more about its own systems than enterprise IT teams ever would. Many recon activities are passive and produce no log entries on the target side.

### Adversary Goal
Gather information about the AI system to plan future operations — model architecture, training data sources, exposed APIs, deployment environment.

### Notable Techniques
- **Search for Victim's Publicly Available Research Materials** — papers, model cards, GitHub
- **Search for Publicly Available Adversarial Vulnerability Analysis** — known CVEs against the model family
- **Active Scanning** of AI/ML inference endpoints
- **Gather AI/ML Artifacts** — discovering deployed models, weights, configs

### 🐾 Why It Matters
Many models are over-documented. Model cards, papers, blog posts, and GitHub repos give attackers everything they need to plan poisoning, extraction, or evasion attacks before they ever send a query.

---

## 🐱 2. Resource Development — `AML.TA0042`

> *"The cat is shopping for tools."*

### Description
Resource Development covers the adversary's pre-attack work to acquire, build, or stage the assets needed for an operation against an AI system. This includes pulling pre-trained models from public registries, assembling poisoned datasets, generating adversarial examples, registering accounts on platforms like Hugging Face or GitHub, and increasingly — publishing weaponized models, datasets, or agent tools designed to be picked up by victims downstream. The 2026 v5.4.0 update added explicit techniques for poisoned agent-tool publication, reflecting how the MCP and agent-tool ecosystem has become a supply-chain attack surface in its own right. Resource Development is often invisible to the eventual target; the adversary's prep happens entirely on infrastructure they control.

### Adversary Goal
Acquire or build the resources (datasets, compute, models, accounts) needed to support an attack.

### Notable Techniques
- **Acquire Public AI Artifacts** — pulling pre-trained models or datasets
- **Obtain Capabilities** — adversarial example generators, prompt-injection toolkits
- **Develop Capabilities** — bespoke poisoning datasets, custom adversarial loss functions
- **Establish Accounts** on Hugging Face, GitHub, package registries
- **Publish Poisoned Datasets / Models** (added in 2025+ updates)
- **Publish Poisoned AI Agent Tool** (v5.4.0, Feb 2026)

### 🐾 Real-World Echo
**PoisonGPT** — Mithril Security demonstrated a lobotomized model uploaded to Hugging Face that bypassed safety benchmarks. Pure resource development weaponized.

---

## 🐱 3. Initial Access — `AML.TA0001`

> *"Cat found the door. Door was unlocked."*

### Description
Initial Access is the adversary's first foothold in the target environment hosting the AI system. In ATLAS this is materially broader than the ATT&CK version because the entry vectors include AI-specific paths: pulling a poisoned model from a public registry, ingesting a contaminated dataset, exploiting a misconfigured inference endpoint, or compromising an ML engineer's development environment via a malicious notebook or pickle file. Initial Access against AI systems frequently bypasses the network perimeter entirely — the attacker's payload arrives because someone on the team voluntarily downloaded it from a trusted-looking source. This is why supply-chain controls (signing, hashing, provenance) matter as much as network controls for ML infrastructure.

### Adversary Goal
Get into the AI system or the environment hosting it.

### Notable Techniques
- **AI Supply Chain Compromise** — poisoned models, datasets, or libraries
- **Valid Accounts** — stolen credentials to ML platforms
- **Phishing** targeting ML engineers
- **Exploit Public-Facing Application** — vulnerable inference endpoints
- **Drive-By Compromise** of ML developer environments

### 🐾 Real-World Echo
**ShadowRay** — exploitation of Ray AI framework default configurations let attackers gain initial access to ML infrastructure across many organizations.

---

## 🐱 4. AI Model Access — `AML.TA0000`

> *"Different from getting into the building. The cat is now in the same room as the model."*

### Description
AI Model Access is one of the two tactics unique to ATLAS (the other being AI Attack Staging). It captures a distinction that doesn't exist in traditional cybersecurity: the difference between *being on the network* and *being able to interact with the model itself*. Access levels form a spectrum — black-box access (query the inference API and observe outputs), grey-box access (some knowledge of architecture, hyperparameters, or sample weights), and white-box access (full weights and code in hand). Each level enables a fundamentally different class of attack: black-box enables extraction and evasion through query-based methods; white-box enables direct backdooring, surgical fine-tuning, and targeted adversarial example generation. Defenders must reason about model access as a separate trust boundary from network and host access.

### Adversary Goal
Specifically gain access to the **AI model itself** — through inference APIs, downloaded artifacts, or physical environment access.

### Notable Techniques
- **AI Model Inference API Access** — black-box queries
- **AI-Enabled Product or Service** — using the deployed product as the access vector
- **Physical Environment Access** — for embedded or on-device models
- **Full AI Model Access** — white-box, weights-in-hand

### 🧬 ATLAS-Unique
This tactic does **not** exist in ATT&CK. It's specifically about the boundary between *being on the network* and *being able to interact with the model*. Different access levels (black-box → grey-box → white-box) enable wildly different attack classes.

---

## 🐱 5. Execution — `AML.TA0002`

> *"The cat is running code. The cat should not be running code."*

### Description
Execution covers techniques that run adversary-controlled code or instructions inside the AI environment. AI systems introduce execution vectors that don't exist in traditional applications: serialized model files (pickle, joblib, safetensors variants) that execute arbitrary code at load time; prompts that reach a code interpreter through a tool-use surface; agent frameworks that compile or evaluate generated code; and notebook environments shared across ML teams. The 2026 v5.4.0 release added "Escape to Host" as a recognized technique, capturing the increasingly common pattern of an agent breaking out of its sandbox into the underlying compute environment. Execution is frequently the pivot point where an AI vulnerability becomes a traditional infrastructure compromise.

### Adversary Goal
Run malicious code or instructions in the AI environment.

### Notable Techniques
- **User Execution** — tricking ML engineers into running poisoned notebooks or models
- **Command and Scripting Interpreter** — through agent tool-use surfaces
- **AI Pickle File Execution** — maliciously crafted pickle/joblib files trigger code at load time
- **Prompt Injection as Execution Vector** — when prompts reach an interpreter
- **Escape to Host** (v5.4.0) — agent escapes its sandbox to the host system

### 🐾 Real-World Echo
**Sleepy Pickle / "Never a dill moment"** (Trail of Bits) — pickle-based code execution in ML pipelines. If you're loading models from anywhere you don't 100% trust, this is your nightmare.

---

## 🐱 6. Persistence — `AML.TA0003`

> *"The cat is in your house now. The cat is staying."*

### Description
Persistence is the adversary's effort to maintain access across reboots, retraining cycles, credential rotation, and other disruptions. AI systems support persistence vectors that survive even total infrastructure rebuilds: a backdoored model retrains with the trigger intact; a poisoned dataset re-poisons every fine-tune that draws from it; a corrupted RAG store quietly biases every future retrieval. The October 2025 update added "Modify AI Agent Configuration" as a persistence technique, recognizing that agent settings — system prompts, tool allowlists, memory policies — are durable state that adversaries can tamper with for long-term influence. Detecting AI persistence is harder than detecting traditional persistence because the malicious behavior may only activate on specific triggers, leaving the model looking benign during routine evaluation.

### Adversary Goal
Maintain access across reboots, retraining, or credential changes.

### Notable Techniques
- **Backdoor AI Model** — trained-in triggers that survive deployment
- **Modify AI Agent Configuration** (Oct 2025 addition) — alter agent settings to persist
- **Poison Training Data** with backdoor triggers that activate later
- **Account Manipulation** of ML platform identities
- **Memory / RAG Persistence** — see the [Agentic Top 10's ASI06](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/)

### 🐾 Memorable Reading
*"Sleeper Agents: Training Deceptive LLMs that Persist Through Safety Training"* (Anthropic, arXiv:2401.05566) — the literal definition of trained-in persistence.

---

## 🐱 7. Privilege Escalation — `AML.TA0004`

> *"The cat used to be a guest. Now the cat is the landlord."*

### Description
Privilege Escalation in AI systems takes traditional forms — exploiting platform vulnerabilities, abusing service accounts — and adds AI-specific paths. An agent's tool plugins often run with broader downstream permissions than the agent itself was scoped for; a confused-deputy pattern lets the agent act with the user's authority on behalf of an attacker; multi-agent chains can inherit privileges across boundaries that were never explicitly authorized. Privilege escalation is also where the architectural choice between "the LLM enforces authorization" and "downstream systems enforce authorization" gets stress-tested. The first design choice almost always loses — LLMs are not deterministic policy engines, and adversaries find the gaps quickly.

### Adversary Goal
Gain higher-level permissions in the AI environment — model weights, training pipelines, deployment systems.

### Notable Techniques
- **LLM Plugin / Tool Compromise** — escalating through agent tool privileges
- **Confused Deputy** — agent acts with elevated user authority
- **Exploitation for Privilege Escalation** in ML platforms
- **Inheritance via Agent Chain** — multi-agent privilege traversal

---

## 🐱 8. Defense Evasion — `AML.TA0005`

> *"You can't defend against the cat if you can't see the cat."*

### Description
Defense Evasion covers techniques used to avoid detection by security controls, with AI-specific variants targeting both AI-based defenses and the AI system being attacked. Adversarial perturbations craft inputs that humans perceive as benign but cause models to misclassify — a critical capability when the defender's detection layer is itself an ML classifier (malware detection, content moderation, anomaly detection). On the AI-system side, defense evasion includes obfuscating malicious payloads inside model files, hiding instructions in images for multimodal models to interpret, and using indirect prompt injection to bypass content filters that only inspect direct user input. The HiddenLayer black-box bypass case study (AML.CS0003) showed that adversarial evasion of ML-based security tools is achievable without any knowledge of the underlying model — making this tactic accessible to less sophisticated adversaries than defenders often assume.

### Adversary Goal
Avoid being detected by AI-specific or traditional security controls.

### Notable Techniques
- **Adversarial Perturbation** — inputs that look benign but cause misclassification
- **AI-Generated Deepfakes** to evade liveness detection
- **Evade ML Model** — crafted inputs that bypass ML-based security tools (malware classifiers, content filters)
- **Obfuscate AI Artifacts** — hidden payloads in model files
- **Indirect Prompt Injection** to bypass content filters

### 🐾 Real-World Echo
**HiddenLayer's bypass of an ML-based endpoint security product (AML.CS0003)** — adversarial perturbation defeated detection without knowing the model architecture. Black-box evasion in the wild.

---

## 🐱 9. Credential Access — `AML.TA0006`

> *"The cat now has all the keys."*

### Description
Credential Access in AI environments includes traditional credential theft (OS dumping, service account compromise) plus paths specific to AI artifacts and operations. Credentials show up in places teams don't expect: hardcoded into shared notebooks, embedded in system prompts, persisted in agent memory across sessions, written into model cards, or stored unencrypted in MLOps pipelines. RAG knowledge bases and vector stores frequently contain credentials that were ingested from internal documentation without sanitization. Once an adversary obtains a service token or API key for an LLM platform, the cost of every subsequent attack — extraction, exfiltration, denial-of-wallet — drops to near zero and may not trigger anomaly detection because the calls look legitimate.

### Adversary Goal
Steal credentials, API keys, or tokens used by the AI system or its operators.

### Notable Techniques
- **Unsecured Credentials** in prompts, system messages, or model memory
- **Credentials from AI Artifacts** — hardcoded keys in shared models or notebooks
- **OS Credential Dumping** from compromised ML infrastructure
- **Steal AI Model Credentials** — service account tokens

### 🐾 Why It Matters
System prompts often leak credentials (see [OWASP LLM07: System Prompt Leakage](https://genai.owasp.org/llm-top-10/)). Memory and RAG stores can persist them silently across sessions.

---

## 🐱 10. Discovery — `AML.TA0007`

> *"Now the cat maps the inside of the house."*

### Description
Discovery is post-foothold reconnaissance — the adversary, having gained some level of access, now enumerates the internal AI environment. This includes fingerprinting the model family, mapping its input/output schema and label space, finding deployed model artifacts and weights on shared filesystems, discovering connected RAG databases and vector stores, and (in agentic systems) enumerating the tools and capabilities available to the agent. Discovery is also where adversaries learn enough about the target's behavior to design effective AI Attack Staging in tactic 12. In multi-tenant or multi-agent environments, discovery often reveals far more than the defender intended to expose, because the internal trust assumptions ("only authorized callers can hit this endpoint") were never enforced beyond the perimeter.

### Adversary Goal
Learn the internal layout — what models exist, what data is available, what permissions the agent has.

### Notable Techniques
- **Discover AI Model Ontology** — input/output schema, classes, label space
- **Discover AI Model Family** — fingerprinting which architecture is in use
- **Discover AI Artifacts** — find deployed models, datasets, embeddings inside the env
- **Discover Agent Capabilities and Tools** (newer) — enumerate what the agent can do
- **RAG Database Discovery** — find the knowledge stores

---

## 🐱 11. Collection — `AML.TA0009`

> *"The cat gathers everything onto one pile."*

### Description
Collection is the staging of data for eventual exfiltration. In AI systems, the data of interest expands beyond traditional sensitive content (PII, financials, source code) to include AI-specific assets: query/response corpora that can be used to train surrogate models, embeddings that can be inverted to recover source text, RAG store contents, agent memory across sessions, and model artifacts themselves. Collection often happens slowly and in pieces — large bursts of inference queries are detectable, but a steady drip of carefully spaced queries can build a high-fidelity training corpus over weeks or months. The collection phase is where defenders have the best chance to detect an attack in progress, because the volume and pattern of access to AI-specific assets is observable in inference logs and storage telemetry.

### Adversary Goal
Aggregate data of interest before exfiltration.

### Notable Techniques
- **Data from AI Inference API** — building a query corpus
- **AI Artifact Collection** — scraping models, weights, embeddings
- **RAG Database Retrieval** — pulling from connected knowledge stores
- **Data from Agent Memory** — collecting context across sessions

---

## 🐱 12. AI Attack Staging — `AML.TA0012`

> *"The cat sharpens its claws before the pounce."*

### Description
AI Attack Staging is the second tactic unique to ATLAS. It captures a phase of the attack lifecycle that has no analog in traditional cybersecurity: the adversary's iterative work to develop, refine, and validate an AI-specific attack against the target before launching it. This typically means training a proxy or surrogate model that mirrors the target, generating adversarial examples and verifying their effectiveness offline, crafting backdoor triggers, or producing poisoned data tailored to the target's training pipeline. Attack staging exists because AI attacks frequently require empirical tuning — adversarial perturbations, jailbreak prompts, and extraction queries all need to be tested and iterated against something that behaves like the target. Strong observability of inference patterns is the defender's best lever here, since high-volume probing during the staging phase often shows distinct signatures.

### Adversary Goal
Prepare a tailored attack against the model — train surrogates, craft adversarial examples, build poisoning payloads.

### Notable Techniques
- **Create Proxy AI Model** — surrogate trained to mirror the target
- **Backdoor AI Model** with trained-in triggers
- **Verify Attack** offline against the proxy before launching at the real target
- **Craft Adversarial Data** — perturbations designed to evade or hijack
- **Poison Training Data** (`AML.T0020`)

### 🧬 ATLAS-Unique
Like AI Model Access, this tactic does **not** exist in ATT&CK. It captures the AI-specific reality that *the attack itself often has to be developed and tested against the target's behavior* before deployment.

---

## 🐱 13. Command and Control — `AML.TA0011`

> *"Cat A is on the inside. Cat B is calling the shots from outside."*

### Description
Command and Control (C2) is how adversaries communicate with compromised systems to direct ongoing operations. In AI environments, the novel C2 pattern is the use of legitimate AI service APIs as covert channels — repurposing tools the organization has already approved, whitelisted, and is paying for. The SesameOp case study (added late 2025) documents an attacker using a legitimate AI assistant API as a C2 channel, which blends seamlessly into normal AI traffic and is extremely difficult to distinguish from authorized usage. Agent tool invocations can also serve as bidirectional control channels: an agent calls out to fetch "data" that is actually next-stage instructions, then acts on them. C2 against AI systems is notable for hiding inside the noise floor of legitimate AI activity.

### Adversary Goal
Communicate with compromised AI systems to direct ongoing operations.

### Notable Techniques
- **Reverse Shell via Agent Tools** — using legitimate tools as C2 channels
- **AI Service API as C2** — repurposing legitimate AI APIs as control channels
- **Web Service** as covert C2

### 🐾 Real-World Echo
**SesameOp** (added late 2025) — adversaries used a legitimate AI assistant API as a covert command-and-control channel, blending malicious traffic into normal AI workflows. Genuinely novel C2 vector.

---

## 🐱 14. Exfiltration — `AML.TA0010`

> *"The cat leaves. The cat takes things."*

### Description
Exfiltration covers the techniques used to move data out of the AI environment, with several AI-specific channels that are difficult to detect with traditional egress monitoring. Inference APIs themselves serve as exfil channels: model inversion attacks reconstruct training data through carefully crafted queries; membership inference confirms whether specific records were in the training set; model extraction rebuilds the target's behavior in a surrogate. In agentic systems, tool invocations create entirely new exfil paths — the agent legitimately calls an external service, but the data being sent was attacker-influenced. EchoLeak (M365 Copilot) and Morris II demonstrate that exfiltration via prompt injection can require zero user interaction and zero malicious infrastructure, since the egress flows through services the organization has already authorized.

### Adversary Goal
Steal data, model weights, training data, prompts, or other sensitive information.

### Notable Techniques
- **Exfiltration via AI Inference API** (`AML.T0024`) — reconstructing training data via queries
- **Invert AI Model** (`AML.T0024.001`) — recover sensitive training data
- **Extract AI Model** (`AML.T0024.002`) — reconstruct weights/behavior
- **Infer Training Data Membership** (`AML.T0024.000`) — confirm specific records were in training
- **Exfiltration via AI Agent Tool Invocation** (`AML.T0086`) — using connected tools to move data out
- **Exfiltration via Cyber Means** — classic egress paths

### 🐾 Real-World Echo
**EchoLeak** (M365 Copilot) — indirect prompt injection in incoming email exfiltrated chat and mail content silently. **Morris II Worm** — RAG-based prompt injection self-propagates and exfiltrates PII without any user interaction.

---

## 🐱 15. Impact — `AML.TA0040`

> *"What it was all for."*

### Description
Impact is the adversary's final objective — the actual harm intended against the AI system, the organization deploying it, or the people relying on its outputs. ATLAS catalogs both technical impacts (denial of AI service, model integrity erosion through gradual poisoning, cost harvesting via denial-of-wallet attacks on cloud-hosted models) and external harms (societal harm, financial damage, reputational damage). Impact in AI systems is often gradual rather than catastrophic — a steadily drifting model degrades quality over weeks; a poisoned RAG store biases recommendations subtly; an extracted model erodes competitive advantage without ever triggering an alert. Defenders should pair traditional incident-response readiness with longitudinal model-quality monitoring, since AI impacts often look like "the model just isn't as good as it used to be" rather than a discrete security event.

### Adversary Goal
Disrupt, degrade, manipulate, or destroy the AI system or what it produces.

### Notable Techniques
- **Evade AI Model** — cause misclassification at inference time
- **Denial of AI Service** (`AML.T0029`) — DoS or DoW attacks on the model
- **Spamming AI System with Chaff Data** — degrade utility through volume
- **Erode AI Model Integrity** — gradual poisoning that drifts the model over time
- **Cost Harvesting** (`AML.T0034`) — torch the cloud bill
- **External Harms** — societal harm (`AML.T0048.002`), reputational damage, financial damage
- **AI Agent Tool Poisoning** (`AML.T0110`) — modify tools so future invocations execute attacker-controlled behavior

---

## 🐱 16. AI-Specific Impact — Newer Additions

> *"The 16th tactic. New as of v5.1.0 (Nov 2025)."*

### Description
The November 2025 v5.1.0 release expanded ATLAS to a 16th tactic specifically capturing impact categories that only exist because of AI and agentic systems — outcomes that don't map cleanly onto traditional CIA-triad impacts. These include AI agent goal hijack (the agent pursues attacker-chosen objectives while appearing to function normally), tool poisoning that affects all future invocations, and the broader category of agent-mediated harm where the agent itself becomes the attack vector against humans, peer agents, or downstream systems. The February 2026 v5.4.0 release continued this trajectory with techniques like Publish Poisoned AI Agent Tool and Escape to Host. This is the fastest-evolving area of ATLAS and reflects how thoroughly agentic deployment is reshaping the threat landscape — defenders working on agent systems should track this tactic's growth quarter by quarter.

### Context
The November 2025 v5.1.0 release expanded ATLAS to **16 tactics**, adding a tactic specifically capturing impacts that only exist because of AI/agentic systems. The February 2026 v5.4.0 release added more agent-focused techniques including **Publish Poisoned AI Agent Tool** and **Escape to Host**.

### Notable Techniques (selected)
- **AI Agent Goal Hijack** — overlaps directly with [OWASP ASI01](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/)
- **AI Agent Tool Poisoning** (`AML.T0110`)
- **Publish Poisoned AI Agent Tool** (v5.4.0)
- **Escape to Host** (v5.4.0)

### 🐾 KryptoKat's Note
This is the fastest-moving area of ATLAS. If you're working on agentic systems, **bookmark [the changelog](https://github.com/mitre-atlas/atlas-data/blob/main/CHANGELOG.md)** — new techniques are landing roughly quarterly.

---

## 🗂️ Notable Real-World Case Studies

ATLAS publishes **42 real-world case studies** as of v5.1.0. Highlights every defender should know:

| Case Study | What It Demonstrates |
|---|---|
| **PoisonGPT** | Lobotomized model on Hugging Face bypassing safety benchmarks |
| **ShadowRay** | Ray AI framework exploitation across many orgs |
| **Tay Poisoning** | Classic real-time data poisoning of a deployed chatbot |
| **HiddenLayer ML Endpoint Bypass (CS0003)** | Black-box adversarial evasion of ML-based security |
| **Morris II Worm** | RAG-based self-propagating prompt-injection worm |
| **EchoLeak (M365 Copilot)** | Zero-click indirect prompt injection → exfil |
| **SesameOp** | AI assistant APIs repurposed as C2 channel |
| **Proof Pudding (CVE-2019-20634)** | Model extraction & inversion bypassing email filters |
| **Deepfake Liveness Bypass** | Face-swap AI defeating identity verification |

Browse the full set: https://atlas.mitre.org/studies

---

## 🆚 ATLAS vs. ATT&CK vs. OWASP — Use All Three

The three frameworks are **complementary**, not redundant:

| Framework | Scope | Best For |
|---|---|---|
| **MITRE ATT&CK** | Traditional IT / OT / cloud | Network and endpoint threats, post-compromise behavior |
| **MITRE ATLAS** | AI/ML systems | Adversarial ML, model attacks, agent tactics |
| **OWASP LLM Top 10** | LLM applications | Prioritized application-level vulnerabilities |
| **OWASP Agentic Top 10** | Autonomous agent systems | Agent-specific vulns (goal hijack, rogue agents, etc.) |
| **MITRE D3FEND** | Defensive countermeasures | Mapping defenses back to ATT&CK/ATLAS techniques |
| **NIST AI RMF** | Risk management | Strategic governance and risk measurement |

**Practical mapping for the cybersecurity professional:**
- ATT&CK tells you *how* an adversary moves through a network
- ATLAS tells you *how* an adversary attacks the model itself
- OWASP tells you *which application-level vulnerabilities* enable those techniques
- D3FEND tells you *what to do about it*
- NIST tells leadership *how to govern the program*

---

## 🐾 Defender's Quick-Reference Cheat Sheet

| If you're defending... | Pay extra attention to ATLAS tactics |
|---|---|
| A public-facing inference API | Reconnaissance, AI Model Access, Exfiltration, Impact |
| A RAG application | Initial Access, AI Attack Staging, Collection, Exfiltration |
| An agentic system with tools | Execution, Privilege Escalation, C2, AI-Specific Impact |
| A model in a regulated domain | Defense Evasion, Impact (External Harms), Credential Access |
| A custom-trained / fine-tuned model | Resource Development, AI Attack Staging, Persistence |
| An on-device / edge model | AI Model Access, Discovery, Persistence |
| A multi-agent orchestration | Persistence, C2, AI-Specific Impact (Goal Hijack) |

---

## 🛠️ Working with ATLAS Programmatically

ATLAS data is available in **YAML, JSON, and STIX 2.1** for automated ingestion into SIEMs, threat intelligence platforms, and red-team tooling.

**Python example (from the official `atlas-data` repo):**
```python
import yaml

with open("ATLAS.yaml") as f:
    data = yaml.safe_load(f)

first_matrix = data["matrices"][0]
tactics = first_matrix["tactics"]
techniques = first_matrix["techniques"]
case_studies = data["case-studies"]

print(f"Tactics: {len(tactics)}")
print(f"Techniques: {len(techniques)}")
print(f"Case Studies: {len(case_studies)}")
```

**Tools that consume ATLAS:**
- 🛠️ [ATLAS Navigator](https://mitre-atlas.github.io/atlas-navigator/) — visual matrix explorer
- 🔴 [Promptfoo MITRE ATLAS preset](https://www.promptfoo.dev/docs/red-team/mitre-atlas/) — automated red-team scanning
- 🔴 [DeepTeam (Confident AI) ATLAS module](https://www.trydeepteam.com/docs/frameworks-mitre-atlas) — LLM red teaming
- 🔵 [MITRE D3FEND](https://d3fend.mitre.org) — defensive countermeasures

---

## 🤝 Contribute Back

ATLAS grows through community contributions. If you've observed a real-world AI attack:

- 📝 [AI Incident Sharing Program](https://ai-incidents.mitre.org) — anonymized incident reporting
- 🐙 [atlas-data GitHub](https://github.com/mitre-atlas/atlas-data) — propose new techniques or case studies
- 📧 ATLAS team contact via the [main site](https://atlas.mitre.org)

The October 2025 collaboration with **Zenity Labs** added 14 new agent-focused techniques. November 2025 (v5.1.0) added the 16th tactic. February 2026 (v5.4.0) added agent-focused techniques like **Publish Poisoned AI Agent Tool** and **Escape to Host**. Community contributions drive real coverage.

---

## 🔗 Related Field Guides

- 🐾 [KryptoKat's OWASP LLM Top 10 2025 Reference](https://github.com/<your-username>/kryptokat-owasp-llm-top10) *(replace with your repo URL)*
- 🐾 [KryptoKat's OWASP Agentic Top 10 2026 Reference](https://github.com/<your-username>/kryptokat-owasp-agentic-top10) *(replace with your repo URL)*

---

## 📝 License & Attribution

This reference summarizes content from **MITRE ATLAS™**, which is a trademark of The MITRE Corporation. ATLAS data and content are made available by MITRE for research and education. See [the official ATLAS site](https://atlas.mitre.org) for licensing and terms of use.

This reference is unofficial. KryptoKat is not affiliated with MITRE or The MITRE Corporation.

**ATLAS Project Lead:** Dr. Christina Liaghati (MITRE)

The hacker cat is just here for moral support. 🐈‍⬛

---

<p align="center">
  <i>Map the matrix. Watch the cat. Patch the model.</i><br>
  <b>— ハッカー猫 / KryptoKat</b>
</p>
