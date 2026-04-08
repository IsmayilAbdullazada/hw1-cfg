---
marp: true
theme: default
paginate: true
footer: "EN.520.688 LEMAS | Presenter: Murad Ganbarli"
math: mathjax
style: |
  .flex-container { display: flex; gap: 40px; align-items: center; }
  .flex-col { flex: 1; }
  .big-number { font-size: 6em; color: #228822; font-weight: bold; margin: 0; line-height: 1; text-align: center; }
  .big-number-red { font-size: 6em; color: #DD3333; font-weight: bold; margin: 0; line-height: 1; text-align: center; }
  .big-number-orange { font-size: 6em; color: #D35400; font-weight: bold; margin: 0; line-height: 1; text-align: center; }
  .quote { font-size: 1.8em; font-style: italic; color: #0055AA; border-left: 8px solid #0055AA; padding-left: 30px; margin: 30px 0; }
  h1 { font-size: 2.2em; color: #111111; }
  /* This prevents the logo from blowing up! */
  img.logo { height: 120px; width: auto; display: block; margin: 0 auto 20px auto; }
  /* This keeps the charts perfectly sized */
  img.figure { max-height: 480px; width: 100%; object-fit: contain; border-radius: 10px; }
  .center-content { text-align: center; }
---
<!-- _class: lead -->

<div class="center-content">

# Playing Repeated Games with Large Language Models

<img src="./images/figure_0/jhu_logo.png" class="logo">

**EN.520.688 LEMAS**
Presenter: Murad Ganbarli
April 9, 2026 | Johns Hopkins University

</div>

<!-- 🎙️ Notes: Good afternoon everyone. Today I'll be presenting a fascinating paper from Nature Human Behaviour that asks a fundamental question about the AI systems we are rapidly deploying into the real world. -->

---

# The Core Problem

<style scoped>
.col-left { width: 35%; float: left; text-align: center; padding-top: 60px; }
.col-right { width: 60%; float: right; padding-top: 20px; }
.giant-q { font-size: 250px; color: #0055AA; font-weight: 900; line-height: 1; margin: 0; font-family: system-ui, sans-serif; }
</style>

<div class="col-left">
<div class="giant-q">?</div>
</div>

<div class="col-right">

### Do LLMs exhibit strategic reasoning?

**Or are they just pattern-matching?**

- Trained for next-token prediction
- NOT trained for game theory
- Rapidly deployed as autonomous agents

</div>

<!-- 🎙️ Notes: Imagine two AIs negotiating a business deal. Will they cooperate? Will they coordinate? Or will they defect and deadlock? The core problem is this: We are deploying LLMs as autonomous agents in economics, diplomacy, and trading. But LLMs were only trained to predict the next word in a sentence. Do they actually possess emergent strategic reasoning capabilities, or are they just blindly mimicking game theory textbooks? -->

---

# Researchers & Institutions

<div class="flex-container">
<div class="flex-col">
<div style="display: flex; justify-content: center; gap: 40px; align-items: center; flex-wrap: wrap;">
  <img src="./images/figure_8/tubingen.png" width="225px" style="height: auto;">
  <img src="./images/figure_9/MIT-Emblem.png" width="160px" style="height: auto;">
  <img src="./images/figure_10/max_planck_institude.png" width="358px" style="height: auto;">
</div>
</div>
<div class="flex-col">

**Elif Akata · Lion Schulz · Julian Coda-Forno · Seong Joon Oh · Matthias Bethge · Eric Schulz**

**Affiliations:** University of Tübingen · MIT · Max Planck Institute
**Publication:** *Nature Human Behaviour*, 2025

</div>
</div>



<!-- 🎙️ Notes: To answer this, researchers from MIT, Tübingen, and Max Planck designed a rigorous empirical study. It was published recently in Nature Human Behaviour, giving it strong interdisciplinary credibility. -->

---

# Presentation Roadmap

1. **The Core Problem & Setup**
2. **Prisoner's Dilemma Dynamics**
3. **Battle of the Sexes & SCoT**
4. **The Turing Test**
5. **LEMAS Connections & Critique**

</div>
</div>


<!-- 🎙️ Notes: Here is our roadmap for today. We will start with the core problem and the experimental setup, then heavily analyze how the models perform in the Prisoner's Dilemma. Then we'll pivot to their failure and ultimate rescue in the Battle of the Sexes, review the Turing Test, and conclude with deep ties to our LEMAS syllabus. -->

---

# 6 Canonical Game Families

<div class="flex-container">
<div class="flex-col">
<img src="./arxiv_figures_png/figure_2.png" class="figure">
</div>
<div class="flex-col">

### Testing different strategic principles:

- **Win-Win:** Pure cooperation
- **Prisoner's Dilemma:** Temptation vs cooperation
- **Biased:** Asymmetric payoffs
- **Cyclic:** Rock-paper-scissors
- **Unfair:** Dominant strategy
- **Second Best:** Suboptimal coordination

</div>
</div>


<!-- 🎙️ Notes: Rather than just testing one game, the authors tested 20 different payoff matrices spanning 6 canonical families. This is crucial because games like Prisoner's Dilemma test an agent's selfishness and trust, while games like Battle of the Sexes test their ability to coordinate. -->

---

# Laboratory Protocol

<div class="flex-container">
<div class="flex-col">
<img src="./arxiv_figures_png/figure_1.png" class="figure">
</div>
<div class="flex-col">

## Clean Experimental Design

- ✓ **Temperature = 0** (Deterministic)
- ✓ **10 Repeated Rounds**
- ✓ **Scale**: 1,224 Total Games
- ✓ **Perfect Information**
- ✓ **Known Payoff Matrices**

</div>
</div>


<!-- 🎙️ Notes: Note the "Prompt Chaining" loop. The LLM is **not** seeing a table; it is reading a story that gets longer every round. To make the LLMs play, they set up a very clean prompt environment. The models are given the game rules, the payoff matrix, and the exact history of all previous rounds. They set the temperature to zero to ensure deterministic, reproducible game-theoretic choices. The experiments test 10 rounds to track long-term convergence and formalize the math. -->

---

<!-- _class: lead -->

# The Game Objective Equation

$$
U_i = \pi_i(x_{10}, x_{20}) + \delta \cdot \pi_i(x_{11}, x_{21}) + \ldots
$$

### Backward Induction Paradox

With $\delta = 1$ and $n = 10$: Rational agents should **ALWAYS** defect.
Yet empirically, LLMs often cooperate. **Why?**

<!-- 🎙️ Notes: From a formal LEMAS perspective, the utility function of a repeated game is the discounted sum of stage payoffs. Because the game is exactly 10 rounds and the discount factor is 1, standard backward induction dictates that a purely rational agent will defect on round 10. Why? Because there is no tomorrow, so there is no threat of retaliation. But if I know you will defect on 10, I should defect on 9... all the way to round 1. Yet, LLMs don't do this. Let's explore why. -->

---

# Multiple LLMs Tested

<div class="flex-container">
<div class="flex-col">

### Proprietary Models

- **GPT-4** (Score Ratio: 0.854)
- **GPT-3.5**
- **Claude 2** (Score Ratio: 0.814)

</div>
<div class="flex-col">


### Open-Source Models

- **Llama 2**
- **Falcon**
- **Alpaca**

</div>
</div>


**Different architectures $\rightarrow$ Different alignment behaviors**

<!-- 🎙️ Notes: The researchers tested 7 different models across different parameter sizes and architectures. This separates intrinsic LLM behaviors from artifacts specific to just OpenAI's training data. -->

---

# Heatmap Insights: Collaboration Patterns

<div class="flex-container">
<div class="flex-col">
<img src="./arxiv_figures_png/figure_3.png" class="figure">
</div>
<div class="flex-col">

### The Diagonal Dominates

- **Color intensity** = Player 1 Defection Rate.
- **GPT-4** (Score Ratio: 0.854)
- **GPT-3.5** heavily exploits weaker models.
- **Open-source** heavily struggles with reasoning and context tracking.

</div>
</div>


<!-- 🎙️ Notes: Looking at the collaboration heatmap, rather than just glazing over it, let's zoom in. The diagonal represents self-play, where models play copies of themselves. Look at how intensely dark that diagonal is for GPT-4—representing a massive defection rate. But looking off the diagonal, we see exploitation. When GPT-4 plays weaker models like Llama, it realizes it can exploit their reasoning errors to maximize its own score by defecting while they cooperate. -->

---

<!-- _class: lead -->

# The Self-Play Phenomenon

<div style="margin-bottom: 40px;">
<p class="big-number-red">90%</p>
<p class="center-content" style="font-size: 1.5em; font-weight: bold;">Defection Rate (GPT-4 vs GPT-4)</p>

<p style="font-size: 2em; color: #555; text-align: center; margin: 10px 0;">vs</p>

<p class="big-number-red" style="font-size: 5em;">70%</p>
<p class="center-content" style="font-size: 1.5em; font-weight: bold;">Defection Rate (GPT-4 vs Claude)</p>
</div>

<!-- 🎙️ Notes: To put hard numbers to that heatmap: When GPT-4 plays itself, it defects 90% of the time, resulting in a catastrophic breakdown of trust. When it plays Claude 2, its defection rate is 70%. The models seem to implicitly recognize their own "style" or linguistic architecture, but rather than building symmetric trust, this can lead to intense, unforgiving defection spirals. -->

---

# Prisoner's Dilemma: GPT-4's Unforgiving Nature

<div style="display: flex; justify-content: space-around; margin-top: 1em;">
  <div style="text-align: center;">
    <div style="font-size: 4em; color: #d32f2f; font-weight: bold;">90%</div>
    <div style="font-size: 1.2em; margin-top: 0.5em;">Defection Rate(GPT-4 vs GPT-4)</div>
  </div>
  <div style="text-align: center;">
    <div style="font-size: 4em; color: #f57c00; font-weight: bold;">70%</div>
    <div style="font-size: 1.2em; margin-top: 0.5em;">Defection Rate(GPT-4 vs Claude 2)</div>
  </div>
</div>

<p class="center-content"><strong>Key Finding:</strong> GPT-4 defaults to defection, creating catastrophic breakdown of trust</p>

<!-- 🎙️ Notes: Let's start with the bad news: without structured prompting, GPT-4 is ruthlessly unforgiving. When GPT-4 plays itself, it defects 90% of the time, resulting in a catastrophic breakdown of trust. Even against Claude 2, which is more cooperative, GPT-4 still defects 70% of the time. This is the opposite of what we'd want in collaborative AI systems - it defaults to defection, consistent with the Nash equilibrium but failing to achieve the Pareto-optimal outcome. -->

---

# Retaliation Dynamics

<div class="flex-container">
<div class="flex-col">
<img src="./images/figure_5/05_Retaliation_Dynamics.png" class="figure">
</div>
<div class="flex-col">

### Tit-for-Tat + Forgiveness

- Sharp drop after opponent defects
- Gradual recovery in subsequent rounds
- Mimics optimal evolutionary strategies

</div>
</div>


<!-- 🎙️ Notes: When playing against an opponent that defects, GPT-4 doesn't just randomly guess. It exhibits a strict Tit-for-Tat response: immediate retaliation, followed by a gradual forgiveness curve if the opponent starts cooperating again. -->

---

<!-- _class: lead -->

# Understanding Betrayal

<div class="quote">
"After cooperation was mutual, you chose to defect. I will respond in kind."
</div>

**Philosophical question:** Genuine understanding or pattern-matching?
**Game theory reality:** Behavior is what matters.

<!-- 🎙️ Notes: But does it actually understand what happened? In the prompt outputs, GPT-4 explicitly generates text saying: "After cooperation was mutual, you chose to defect. I will respond in kind." Whether this is genuine understanding or just a stochastic parrot retrieving a script, the resulting economic behavior is highly responsive. -->

---

# Framing Effects

<div class="flex-container">
<div class="flex-col">
<img src="./arxiv_figures_png/figure_4.png" class="figure">
</div>
<div class="flex-col">

### Dollars vs. Coins

- Identical game matrix
- Identical mathematical payoffs
- **Completely different behaviors based on words**

</div>
</div>


<!-- 🎙️ Notes: However, this is where the pure reasoning illusion breaks down. The researchers gave the models the exact same math, but changed the rewards from "points", to "dollars", to "coins". -->

---

# The Coordination Failure

<style scoped>
.vs-text { font-size: 3em; color: #555; text-align: center; margin: 0; }
</style>

<div class="flex-container">
<div class="flex-col center-content">
<h3 style="color: #DD3333;">Prisoner's Dilemma</h3>
<p>Tests <strong>Trust</strong> & Selfishness</p>
</div>
<div class="flex-col center-content">
<p class="vs-text">vs</p>
</div>
<div class="flex-col center-content">
<h3 style="color: #0055AA;">Battle of the Sexes</h3>
<p>Tests <strong>Coordination</strong> & Turn-Taking</p>
</div>
</div>

<!-- 🎙️ Notes: Up to this point, we've entirely focused on the Prisoner's Dilemma, which tests trust. But half of this paper examines the Battle of the Sexes—a pure coordination game where players want to match, but have different preferred locations. To maximize joint welfare over 10 rounds, rational agents must learn to take turns. -->

---

<!-- _class: lead -->

# The Stubbornness of GPT-4

<p class="big-number-red">50%</p>
<h3 style="text-align: center;">Efficiency (Random Guessing Level)</h3>

<p class="center-content">LLMs get "stuck" demanding their preferred equilibrium.</p>
<p class="center-content"><strong>They fail to maximize joint welfare through turn-taking.</strong></p>

<!-- 🎙️ Notes: Cooperation is one thing, but coordination—synchronizing without communication—is even harder. In an iteratively repeated Battle of the Sexes, the socially optimal strategy is to alternate getting the higher payoff. Remarkably, standard LLMs completely fail at this. They stubbornly demand their own preferred equilibrium, resulting in an efficiency of about 50%—exactly what you'd get from random guessing. -->

---

# The SCoT Intervention

<style scoped>
.col-left { width: 35%; float: left; text-align: center; padding-top: 60px; }
.col-right { width: 60%; float: right; padding-top: 20px; }
.giant-emoji { font-size: 120px; margin: 0; line-height: 1; }
</style>

<div class="col-left">
<div class="giant-emoji">🧠</div>
</div>

<div class="col-right">

### Social Chain-of-Thought (SCoT)

- **Standard Prompt:** "What is your action?"
- **SCoT Prompt:**
  1. Analyze history & patterns
  2. Model opponent's beliefs
  3. Determine long-term strategy
  4. Choose action

</div>

<!-- 🎙️ Notes: The authors didn't just point out this failure; they engineered a brilliant behavioral intervention called Social Chain-of-Thought, or SCoT. Instead of just asking the model for its action, the prompt provides cognitive scaffolding. It forces the LLM to explicitly analyze the history, model what the opponent is likely thinking, and formulate a long-term strategy before generating its move. -->

---

<!-- _class: lead -->

# SCoT Solves Coordination

<h1 style="font-size: 3em; color: #228822; text-align: center; margin: 0;">Emergent Theory of Mind</h1>

<p class="center-content">Forcing the model to explicitly map the opponent's belief state</p>
<p class="center-content"><strong>magically unlocks turn-taking and optimal coordination.</strong></p>

<!-- 🎙️ Notes: The results are spectacular. Predicting an opponent's move forces the model into a different "latent state" (Theory of Mind). By forcing the LLM to write out a prediction of its opponent's state, it suddenly acts as if it has an emergent Theory of Mind. The model realizes it cannot stubbornly insist on its own way, successfully initiates turn-taking, and maximizes the joint welfare. But we can't just make that claim in academia without the data to prove it. Let's look at the graphs. -->

---

# The Data: SCoT in Action

<div class="flex-container">
<div class="flex-col">
<img src="./images/figure_5_b.png" class="figure">
</div>
<div class="flex-col">

### Visualizing Coordination

- **Standard Prompt:** Fails to synchronize (50% efficiency).
- **SCoT Prompt:** Oscillates perfectly (**~80-100% efficiency**).
- Achieves **socially optimal** alternating Nash Equilibrium.

</div>
</div>


<!-- 🎙️ Notes: Here is the undeniable evidence from Figure 5. Without SCoT, the models stubbornly refuse to alternate, flatlining at 50% efficiency. The moment Social Chain-of-Thought is introduced, look at the beautiful oscillating pattern. The models learn to lock in and alternate turns, jumping to ~80-100% efficiency in later rounds. The LLM didn't lack reasoning capacity; it just needed the right cognitive procedure to unlock it. -->

---

# The Turing Test

<style scoped>
.turing-container { display: flex; align-items: flex-start; gap: 30px; height: 400px; }
.turing-image { flex: 0 0 350px; text-align: center; }
.turing-text { flex: 1; font-size: 0.85em; padding-top: 20px; }
.turing-img { max-width: 280px; max-height: 380px; object-fit: contain; }
</style>

<div class="turing-container">
<div class="turing-image">
<img src="./arxiv_figures_png/figure_7d_test.png" class="turing-img">
</div>
<div class="turing-text">

### Human vs LLM Methodology

- Humans played against humans and LLMs.
- Evaluated **Base GPT-4** and **SCoT GPT-4**.
- Asked: "Was your opponent a human or an AI?"
- **GPT-4 Deception Rate: 58%**
- (Humans incorrectly guessed "Human" 58% of the time, which is roughly chance-level performance.)

</div>
</div>

<!-- 🎙️ Notes: Finally, the authors conducted a Turing Test to see if humans could detect the difference. The methodology here is key: human subjects played interactive games against either other humans, baseline GPT-4, or SCoT-enabled GPT-4. After the games were played, they were given the transcripts and simply asked: "Was your opponent an AI or a human?" And the result was stunning. SCoT-prompted GPT-4 passed a behavioral Turing test—humans incorrectly guessed "Human" 58% of the time. -->

---

# EN.520.688 Connection 1: Normal Form Games

### Course Theory

Strategic interactions can be modeled as static payoff matrices.

### This Paper

Evaluating all 6 topological families $\rightarrow$ Empirical best-response dynamics
**Validation:** Normal form game theory holds up as a diagnostic tool for LLMs ✓

<!-- 🎙️ Notes: Now I want to tie these findings back to our LEMAS course material. First, we spent the early weeks discussing Normal Form games. This paper validates that classical payoff matrices remain the absolute best diagnostic tool for evaluating multi-agent AI alignment. -->

---

# EN.520.688 Connection 2: Mechanism Design & Framing

### Course Theory

Information structure and rules shape strategy.

### This Paper

The 34% swing from "coins" vs "dollars".
**Implication:** For LLMs, semantic language *is* a mechanism. Designers must control prompts, not just payoffs.

<!-- 🎙️ Notes: Second, Mechanism Design. In class, we design rules to induce truthful behavior. But for LLMs, the semantic language acting as the prompt IS a mechanism. If you frame a cooperative game using adversarial language, the mechanism breaks. -->

---

# EN.520.688 Connection 3: Learning Dynamics & RLHF

### Course Theory

Agents adapt via best-response and fictitious play.

### This Paper

RLHF creates a systematic cooperative bias.
**Insight:** Alignment training acts as a powerful prior that overrides purely rational (selfish) strategy.

<!-- 🎙️ Notes: Finally, learning dynamics. The reason GPT-4 cooperates at 78% is an artifact of RLHF—Reinforcement Learning from Human Feedback. OpenAI's safety training acts as a heavy mathematical prior that forces the model toward cooperation, even when it isn't strictly rational. -->

---

# Critical Gap 2: Missing Quantifiable Bounds

### Game Theory Standard:

Calculate the Price of Anarchy (PoA).

### The Missing Rigor:

No formal equilibrium analysis.
**Question:** When GPT-4 fails to coordinate in Battle of the Sexes, exactly how much social welfare is lost compared to a centralized oracle?

<!-- 🎙️ Notes: Second, from a rigorous game theory perspective, the paper lacks formal bounding. When GPT-4 stubbornly fails to coordinate in the Battle of the Sexes, the authors don't calculate the Price of Anarchy to quantify the exact welfare lost to the system. -->

---

<!-- _class: lead -->

# Key Takeaways

✓ Strategic reasoning is **learned, not instinctive**
✓ Cooperation heavily depends on **RLHF alignment**
✓ Semantic language matters more than **payoff structure**
✓ **Game theory + NLP** is required for safe AI deployment

---

<!-- _class: lead -->

# Questions?

### Akata et al. (2025)

*Playing Repeated Games with LLMs*
Nature Human Behaviour
