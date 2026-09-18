# 🎙️ Fawkes — Podcast Research Notes
## Digital Rights & Surveillance Technology Episode

> **Source Project:** [Shawn-Shan/fawkes](https://github.com/Shawn-Shan/fawkes) — 5,609 ⭐ | 511 forks | BSD-3-Clause License | Python  
> **Lab:** SANDLab, University of Chicago  
> **Published:** USENIX Security 2020  
> **Forked to:** `bro26man-hash/fawkes`

---

## 1. PROJECT OVERVIEW

**Fawkes** is a privacy-preserving tool that protects individuals against unauthorized facial recognition systems. It works by applying carefully computed, imperceptible perturbations to images — essentially "poisoning" a person's facial data so that facial recognition models trained on the modified images will misidentify the person as someone else.

- **Input:** A directory of facial images
- **Output:** Cloaked images with perturbations tuned to a `low` / `mid` / `high` privacy-vs-perturbation-tradeoff scale
- **Core mechanism:** Optimization-based adversarial perturbations targeting the feature extractor stage of deep learning face recognition pipelines
- **Default computation time:** ~60 seconds per image on CPU; dramatically faster on GPU
- **License:** BSD-3-Clause (permissive open-source)
- **Topics:** `adversarial-machine-learning`, `face-recognition`, `privacy-enhancing-technologies`, `privacy-protection`

**Key reference:** Shan et al., *"Fawkes: Protecting Personal Privacy against Unauthorized Deep Learning Models,"* Proceedings of USENIX Security 2020.

---

## 2. SOCIETAL CONCERNS

### A. The Normalization of Biometric Surveillance
Facial recognition is no longer confined to law enforcement. It's deployed in:
- **Retail analytics** — tracking customer movements and demographics
- **Social media** — automatic tagging, suggestion, and content moderation
- **Workplaces** — employee time-tracking, access control, and productivity monitoring
- **Public spaces** — smart city infrastructure, transit, and event security
- **Border control & immigration** — biometric identification at ports of entry

Fawkes exists because the *default* is surveillance. The burden of privacy has shifted from institutions (who should justify collection) to individuals (who must proactively cloak their data). This is a fundamental power asymmetry.

### B. Non-Consensual Data Harvesting
The core problem Fawkes addresses: facial recognition models can be trained on your images **without your knowledge or consent**. A single photo shared publicly, a social media profile, a security camera catch — any of these can become training data. Unlike traditional PII (names, SSNs), your face is:
- **Always on** — you can't change it like a password
- **Universally collectible** — no opt-out from being seen in public
- **Immutable** — unlike a breached email, your biometrics can't be reissued

### C. The Chilling Effect
When people know (or even suspect) that their face is being captured and analyzed:
- **Self-censorship** — avoiding protests, meetings, or online expression
- **Behavioral modification** — altering natural behavior under observation
- **Chilling of association** — avoiding people, places, or events deemed "sensitive"
- This is a direct threat to First Amendment rights, freedom of assembly, and偷 privacy as a precondition for democratic participation.

### D. Disproportionate Impact on Marginalized Communities
Facial recognition has well-documented biases:
- **Racial bias** — higher error rates for darker-skinned individuals (MIT Media Lab research)
- **Gender bias** — worse performance for women, especially women of color
- **Over-policing** — communities already subject to predictive policing face compounding surveillance
- Fawkes is a tool of empowerment for these communities, but its effectiveness depends on **access** (see: computational barrier) and **adoption density** (if only some people cloak, the uncloaked become even more identifiable).

### E. Function Creep & Mission Drift
Even if facial recognition starts with "security," it inevitably expands:
- From identifying suspects → tracking ordinary citizens
- From law enforcement → insurance companies, landlords, employers
- From identification → emotion inference, behavior prediction, social scoring
- The tool's original scope is never the final scope. Infrastructure built for one purpose is always repurposed.

---

## 3. ETHICAL TENSIONS

### Tension 1: Individual Privacy vs. Collective Security
- **Pro-surveillance argument:** Facial recognition helps find missing children, prevent terrorism, solve crimes
- **Pro-privacy counter:** The aggregate effect of universal biometric identification is a society where the state can track every movement of every person — a tool of authoritarianism regardless of who wields it
- **Fawkes' implicit position:** The individual should have the right to defend themselves, even if it reduces aggregate surveillance effectiveness

### Tension 2: Arms Race Dynamics
- Fawkes is an **adversarial** tool — it doesn't delete data or regulate collectors, it *poisons* the training data
- This creates an **escalation dynamic**: better cloaking → better detection → better cloaking
- Ethical question: Is it responsible for researchers to publish methods that could be repurposed by malicious actors? (Fawkes' perturbation is benign, but the *principle* applies to the broader adversarial ML field)

### Tension 3: The Accessibility Gate
- **GitHub issue #177** (open): A community member proposed a phone app version, suggesting server-side computation with a subscription model (analogous to Nextcloud's freemium approach)
- The SANDLab team explicitly stated they have **no plans for a mobile app** because it "requires significant computational power that would be challenging for the most powerful mobile devices"
- **Ethical concern:** If Fawkes requires a GPU and 60 seconds per image, it's a tool for the technically privileged. The communities most affected by surveillance (low-income, elderly, disabled, non-technical) are least able to use the defense. This is a **digital divide in privacy**.

### Tension 4: Effectiveness Uncertainty
- **GitHub issue #192** (open, with heart reaction): "Does this still work today?" — A user tested Fawkes on Linux and Windows and confirmed it runs, but **cannot verify whether it actually works against modern models**. After ~5 years with no updates, the core question is: Is Fawkes still effective against contemporary facial recognition systems?
- A commenter noted: "as claimed" — highlighting the tragedy of the situation: even the *willing* cannot easily verify the tool's efficacy without setting up their own facial recognition training pipeline
- **Ethical concern:** A privacy tool whose effectiveness cannot be independently verified by its users is a tool whose value is unproven. This raises questions about:
  - Should researchers provide verification tooling alongside defensive tools?
  - Is it ethical to maintain a project without ongoing validation against modern models?
  - Does the burden of proof belong with the toolmaker or the user?

### Tension 5: Incomplete Ecosystem / Abandonment Risk
- The last commit to the original repository was **August 2023** — nearly 3 years ago as of 2026
- **GitHub issue #193** (open): A user is missing the pre-trained weight file `webface_dense_robust_extract.h5` and cannot obtain it — "literally the only thing keeping me from fully switching over"
- **GitHub issue #185** (open): Request for video support — modern surveillance is overwhelmingly video-based, not still-image-based. Fawkes only protects individual photos
- **GitHub issue #186**: Windows installation failures
- **GitHub issue #187**: Cannot run on Linux (Ubuntu)
- **Ethical concern:** A tool that is difficult to install, doesn't support the dominant surveillance medium (video), and shows signs of abandonment may create a **false sense of security** — worse than no tool at all, because it might make users believe they're protected when they're not

### Tension 6: The "Poisoning" Paradox
- Fawkes doesn't just protect *your* data — it degrades the training data for *everyone* whose images appear alongside yours
- **Secondary effects:** If you cloak your face and post it publicly, you may degrade the accuracy of facial recognition for *uninvolved third parties* who appear in the same photos, scenes, or training batches
- **Ethical question:** Does my right to privacy extend to the right to degrade systems that might affect others? Where is the boundary of individual action's systemic impact?

---

## 4. PODCAST ANGLES & STORY HOOKS

### 🎯 Angle A: "The Privacy Arms Race" — Is Defense Possible in a Surveillance Society?
- **Hook:** Start with a vivid demonstration — show how Fawkes transforms a face image imperceptibly, then show how a modern facial recognition system fails to identify it
- **Core tension:** Every surveillance technology creates a corresponding counter-surveillance technology. Does this arms race benefit anyone, or does it just escalate the cost of privacy?
- **Guest ideas:** SANDLab researchers, digital rights advocates (EFF), facial recognition critics
- **Questions to explore:**
  - Is individual defense (cloaking) sufficient, or do we need structural/regulatory solutions?
  - Should privacy tools be as easy to use as the surveillance tools they counter?
  - What does it say about our society that defending your own face requires adversarial machine learning?

### 🎯 Angle B: "Who Gets to Be Invisible?" — The Digital Divide in Privacy
- **Hook:** Frame it this way — if privacy is a right, why does exercising it require a GPU and technical expertise?
- **Core tension:** Fawkes is powerful but gated. The communities most surveilled (low-income neighborhoods, immigrant communities, communities of color) are least able to access and use the tool
- **Discussion points:**
  - The phone app proposal (issue #177) and the lab's refusal
  - Subscription models vs. free tools: who funds privacy?
  - Is a "privacy tool for the privileged" a form of surveillance gentrification?

### 🎯 Angle C: "Does It Still Work?" — The Trust Problem in Abandoned Security Tools
- **Hook:** The simple, haunting question from issue #192: After 5 years without updates, can anyone actually verify Fawkes works?
- **Core tension:** A privacy tool that can't be verified is a privacy placebo. The burden of proof shouldn't fall entirely on the user.
- **Discussion points:**
  - How many other "security" tools are in the same state?
  - Is open-source maintenance a forgotten responsibility?
  - What would "good enough" verification look like? (A local testing script? A reference model? A public benchmark?)
  - The difference between "open source" and "openly maintained"

### 🎯 Angle D: "The Face Cannot Change" — Biometrics as a Unique Privacy Problem
- **Hook:** You can change your password, your email, your phone number. You cannot change your face.
- **Core argument:** Facial recognition creates a category of privacy harm that's fundamentally different from traditional data breaches
- **Discussion points:**
  - Facial data is *inherently public* — you broadcast it constantly
  - It's *connections-based* — your face links to your associations, locations, and activities
  - It's *irreversible* — once biometric data is compromised, it's compromised forever
  - Fawkes is a creative workaround, but is it the right kind of solution for the right kind of problem?

### 🎯 Angle E: "The Third-Party Harm of Self-Defense" — When Cloaking Hurts Others
- **Hook:** My face cloak might be protecting me — but could it be making surveillance *worse* for the stranger standing next to me?
- **Core tension:** Individual privacy action has systemic externalities. This is therivacy version of "my_free_speech_ends_where_your_mouth_begins."
- **Discussion points:**
  - Does degrading a surveillance system's accuracy constitute harm to non-consenting parties?
  - Is there an ethical framework for "collective privacy defense"?
  - Should there be coordination or standards for how cloaking is applied in public spaces?

### 🎯 Angle F: "From Still Photos to Video Surveillance" — The Gap Between Research and Reality
- **Hook:** Fawkes protects your Facebook profile photo. But modern surveillance is live, video-based, and continuous.
- **Core tension:** Academic privacy tools often protect against the threat model that was current when the research was published, not the threat model that exists today
- **Discussion points:**
  - Issue #185: Video support requested, never delivered
  - Real-world surveillance: CCTV networks, body cameras, ALPR systems, drone surveillance
  - The "research-to-deployment" gap in privacy technology

---

## 5. KEY QUOTES & REFERENCES

### From the Fawkes README / Project Website
> *"Note that we do not have any plans to release any Fawkes mobile apps, because it requires significant computational power that would be challenging for the most powerful mobile devices."*
- Source: [sandlab.cs.uchicago.edu/fawkes](https://sandlab.cs.uchicago.edu/fawkes/)

### From the Academic Paper
> *"Fawkes protects personal privacy against unauthorized deep learning models by computing imperceptible perturbations to facial images."*
- Citation: Shan et al., *USENIX Security 2020*

### From Community Discussion (Issue #192)
> *"After ~5 years with no update, I'm also curious to know if it works with modern day models? and would like to know of a reliable way to test this independently?"* — **unidiver**, April 2026

### From Community Discussion (Issue #193)
> *"pls yes. this is literally the only thing keeping me from fully switching over."* — **Huaian666**, June 2026

---

## 6. OPEN ISSUES — QUICK REFERENCE

| # | Title | Relevance to Episode | Status |
|---|-------|----------------------|--------|
| #192 | Does this still work today? | **HIGH** — Effectiveness unverified against modern models | Open |
| #193 | Missing pre-trained weight file | **MEDIUM** — Accessibility/blocking issue | Open |
| #185 | Video support upgrade | **HIGH** —投影 gap between tool and real-world surveillance | Open |
| #177 | Phone app idea (computational barrier) | **HIGH** — Privacy accessibility & equity | Open |
| #186 | Windows installation failure | **LOW** — Usability barrier | Open |
| #187 | Cannot run on Linux/Ubuntu | **LOW** — Usability barrier | Open |

---

## 7. BROADER CONTEXT — RELATED PROJECTS & MOVEMENTS

For episode research, consider cross-referencing with:

| Project/Organization | Focus | Relevance |
|----------------------|-------|-----------|
| **[CV Dazzle](https://cvdazzle.com/)** | Cosmetic counter-surveillance makeup/hair | Similar adversarial approach, different medium |
| **[Security In A Box](https://securityinabox.org/)** | Digital security tools for activists | Contextualizes Fawkes within broader privacy ecosystem |
| **[EFF Surveillance Self-Defense](https://ssd.eff.org/)** | Practical surveillance defense guides | Regulatory & educational complement to Fawkes |
| **[Clearview AI litigation](https://www.eff.org/deeplinks/2020/02/clearview-ai)** | Corporate facial recognition controversies | The "offensive" side of the debate |
| **[Ban Facial Recognition movement](https://www.eff.org/issues/facial-recognition)** | Municipal bans and legislative efforts | Structural/regulatory alternative to individual defense |
| **[Adversarial Patch](https://github.com/mtrazzi/adversarial-patch)** | Physical-world adversarial ML | Extends Fawkes' approach from digital to physical |

---

## 8. POTENTIAL GUESTS & EXPERTS

- **SANDLab team** (University of Chicago) — original Fawkes researchers
- **Shawn Shan** — lead author of the Fawkes paper
- ** Emily Wenger** — co-author, now at Brown University?
- **Ben Y. Zhao** — co-author, UChicago architecture/security expert
- **Alvaro Bedoya** — Georgetown Law, facial recognition & civil liberties
- **Giant Grizzard** — EFF, surveillance technology policy
- **Joy Buolamwini** — MIT Media Lab / Algorithmic Justice League, facial recognition bias research
- **Cory Doctorow** — digital rights, surveillance capitalization critic

---

## 9. PRODUCTION NOTES

### Tone Considerations
- This topic sits at the intersection of **technical depth** and **human stakes** — avoid making it either too academic or too sensational
- Acknowledge the genuine security value of facial recognition (finding missing children, etc.) while rigorously examining the costs
- The "arms race" framing can either energize or depress — choose the angle that serves the episode's emotional arc

### Structural Options
1. **Investigative:** Follow the Fawkes story from paper → tool → community → abandonment questions
2. **Debate format:**邀请 pro-surveillance and pro-privacy voices to argue the core tensions
3. **Personal narrative:** Start with a host experiment — try Fawkes, attempt to verify it, document the experience
4. **Systems view:** Use Fawkes as a lens to examine the entire surveillance-privacy ecosystem

### Key Questions to Tie Together
- If privacy is a right, why is its exercise so technologically gated?
- Is individual defense sufficient when structural change is needed?
- What obligations do researchers have to maintain the tools they create?
- Can a "poisoning" approach ever be a stable, long-term solution — or is it inherently an arms race?
- Who bears the cost when privacy tools fail or are abandoned?

---

*Notes compiled from GitHub analysis of `Shawn-Shan/fawkes` — repository forked to `bro26man-hash/fawkes` for reference and further study.*
