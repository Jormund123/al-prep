# THE QUESTION BANK — Artificial Life MA-INF 4201

**How to use this.** Every question that has been asked on a written paper, with the answer written the way you should write it. Then variants I built by changing the numbers, the wording, or the direction — because that is exactly what the examiner changes. Cover the answer, write it out, compare.

**Two kinds of question in here. Treat them differently.**

- 🔒 **MEMORIZE** — the answer is fixed text plus a fixed drawing. Learn the block. 13 of the 20.
- ⚙️ **RECIPE** — the examiner re-parameterizes it every sitting, so learn the procedure and run it on whatever numbers appear. 7 of the 20: Wolfram number, reverse Wolfram, rule count, glider direction, L-System target, EA mutation probability, Wheel of Fortune.

**Marking rules that apply to every answer below.**

- 1 point ≈ one crisp sentence, one formula line, or one labelled sketch. A 5-pointer wants ~5 scoring items, not one paragraph.
- Goerke wants **exact values and the lecture's own words**. The 2017 paper says outright: *"Wants explanations for all answers including formulas (which variable means what?)"*
- **Define every symbol you write.** An undefined variable in a formula is a lost mark.
- Never leave a sub-part blank. Naming the mechanism earns points even when the calculation fails.

**Drawing convention — write this once at the top of your script:** `. = dead/white/0`, `# = alive/black/I`.

---
---

# ASKED ON ALL FOUR PAPERS

**These ten appeared on every written paper we have.** Together roughly 55 of the 90 points. Nothing else in this file matters until these are automatic.

---

## Q1 · Game of Life 🔒+⚙️
**Recurrence: 4/4. Worth 10 points on three of four papers.**

### Asked as

- *"Explain the Game of Life, every detail of it. [pattern given] Draw the next 2 steps of this pattern and explain the rules of the GoL."* — 2023 `qn-02` 1, **10 pt**
- *"Explain all parts of Conway's Game of Life with the example of a blinker."* — 2023 `qn-03`, **10 pt**
- *"Explain all parts of Conway's Game of Life…"* — 2017 Q1, **10 pt**
- *"Draw a Game of Life pattern (Glider) that moves to the lower left corner. Draw 4 steps of this pattern."* — 2023 `qn-02` 5, 5 pt
- *"Within the Game of Life there is a pattern called glider. Give an example that moves to the lower-right and draw the 4 time-steps."* — 2025 T12, 5 pt (four 7×7 grids were printed, labelled t=0…t=3)

### THE BLOCK TO WRITE — 10-point version

Write these five parts in this order. Each is worth ~2 points.

**① The CA specification** (do not skip this — "every detail" means this)

> Conway's Game of Life, proposed by John H. Conway in **1970**, is a cellular automaton with
> - $d = 2$ — a two-dimensional rectangular grid
> - $r = 1$ — a **Moore** neighbourhood (and Moore periphery)
> - $k = 2$ — binary states per cell: $O$ = dead, $I$ = alive
> - **the rule is legal** (it is symmetric and has a silent state)
> - the rule implements concepts from **population dynamics**: birth, survival, death from overcrowding, death from loneliness.

**② The rule, in the lecture's notation `23/3` (= S23/B3)**

> - **Birth:** a cell is born if **exactly 3** neighbouring cells are alive.
> - **Survival:** a living cell survives if **2 or 3** neighbours are alive.
> - **Death from overcrowding:** a living cell dies if **more than 3** neighbours are alive.
> - **Death from loneliness:** a living cell dies if **fewer than 2** neighbours are alive.

**③ The rule table** — indexed by $S_a(t)$, the number of living cells in the periphery

```
   S_a(t)              8   7   6   5   4   3   2   1   0
   ---------------------------------------------------------
   if a(t) is DEAD:    O   O   O   O   O   I   O   O   O
   if a(t) is ALIVE:   O   O   O   O   O   I   I   O   O
                       \_______________/   \___/   \____/
                          overcrowding    survive  loneliness
```

**④ The worked example** — evolve whatever pattern you were given (see the drawings below).

**⑤ The closing point** — this is the part that separates 8/10 from 10/10:

> Gosper's Glider Gun proves **unbounded growth** is possible. Glider streams are information (one glider = one bit); colliding gliders can be erased, delayed, reflected or doubled, which allows **Boolean gates (AND, OR, NOT, NAND, NOR, XOR)** to be built — hence Game of Life is **computationally universal (Turing-complete)**.

### THE DRAWINGS

**Blinker — period 2, "the archetype of a periodic class II behaviour"**

```
      t=0            t=1            t=2  (= t=0)

   . . . . .      . . . . .      . . . . .
   . . . . .      . . # . .      . . . . .
   . # # # .      . . # . .      . # # # .
   . . . . .      . . # . .      . . . . .
   . . . . .      . . . . .      . . . . .
```

Say the reasoning out loud, cell by cell — this is what "explain with the example of a blinker" means:
- The **centre** cell has 2 living neighbours → **survives**.
- The **two end** cells have 1 living neighbour each → **die of loneliness**.
- The cells **above and below the centre** are dead with **exactly 3** living neighbours → **born**.
- Everything else has ≤ 2 neighbours and stays dead.

**Glider — LOWER RIGHT** (2017 Q17, 2025 T12). Verified step by step.

```
     t=0              t=1              t=2              t=3              t=4

  . . . . . .      . . . . . .      . . . . . .      . . . . . .      . . . . . .
  . . # . . .      . . . . . .      . . . . . .      . . . . . .      . . . . . .
  . . . # . .      . # . # . .      . . . # . .      . . # . . .      . . . # . .
  . # # # . .      . . # # . .      . # . # . .      . . . # # .      . . . . # .
  . . . . . .      . . # . . .      . . # # . .      . . # # . .      . . # # # .
  . . . . . .      . . . . . .      . . . . . .      . . . . . .      . . . . . .

                                                          t=4 = t=0 shifted one right + one down
```

**Glider — LOWER LEFT** (2023 `qn-02` 5). Horizontal mirror.

```
     t=0              t=1              t=2              t=3              t=4

  . . . . . .      . . . . . .      . . . . . .      . . . . . .      . . . . . .
  . . . # . .      . . . . . .      . . . . . .      . . . . . .      . . . . . .
  . . # . . .      . . # . # .      . . # . . .      . . . # . .      . . # . . .
  . . # # # .      . . # # . .      . . # . # .      . # # . . .      . # . . . .
  . . . . . .      . . . # . .      . . # # . .      . . # # . .      . # # # . .
  . . . . . .      . . . . . .      . . . . . .      . . . . . .      . . . . . .

                                                          t=4 = t=0 shifted one LEFT + one down
```

**Also state the glider's three properties:** it consists of **5 living cells**; in **4 steps it moves one cell diagonally**; the original shape is reconstructed in an adjacent position although **all five cells have changed state**, so the shape recurs but the pattern is **NOT periodic**. It is **the prototypic class IV pattern**.

### ⚙️ THE DIRECTION RECIPE — how to never get the diagonal wrong

Do not memorize four pictures. Memorize one, and this 60-second check:

1. Draw your $t=0$.
2. Hand-evolve **one** step.
3. Compare centres of mass. Moved the wrong way? **Mirror your $t=0$ horizontally** (for left↔right) or **vertically** (for up↔down) and you are done.

Memorize the lower-right one above as your anchor. Then:
- **lower-left** = mirror left–right
- **upper-right** = mirror top–bottom
- **upper-left** = rotate 180° (mirror both)

### VARIANTS — solve these

**V1.** *"Draw a glider that moves to the upper right. Give t=0 and t=1."*

<details><summary>Answer</summary>

Mirror the lower-right anchor top-to-bottom:
```
     t=0                    t=1

  . . . . . .            . . # . . .
  . # # # . .            . . # # . .
  . . . # . .            . # . # . .
  . . # . . .            . . . . . .
  . . . . . .            . . . . . .
  . . . . . .            . . . . . .
```
Centre of mass has moved up and right. ✔
</details>

**V2.** *"Draw the next two steps of this pattern:"*
```
  . . . . .
  . # # . .
  . # # . .
  . . . . .
```
<details><summary>Answer</summary>

This is the **Block**, a **still life**. Every one of the four cells has exactly **3** living neighbours, so all four survive; every surrounding dead cell has at most 2 living neighbours, so nothing is born. **$t=1$ and $t=2$ are identical to $t=0$.** State that it is a stable class II pattern.
</details>

**V3.** *"Explain the Game of Life using the Toad as your example."*

<details><summary>Answer</summary>

Same blocks ①②③⑤, with this drawing (period-2 oscillator):
```
      t=0                t=1                t=2 (= t=0)

   . . . . . .        . . . # . .        . . . . . .
   . . # # # .        . # . . # .        . . # # # .
   . # # # . .        . # . . # .        . # # # . .
   . . . . . .        . . # . . .        . . . . . .
   . . . . . .        . . . . . .        . . . . . .
```
</details>

**V4.** *"Is the Game of Life rule totalistic? Justify."*

<details><summary>Answer</summary>

**No — it is *outer*-totalistic (semi-totalistic).** A strictly totalistic rule relies only on the grand total of all 9 cells (center plus 8 neighbors). Game of Life fails this: a grand total of 4 could mean (alive cell + 3 neighbors = survives) OR (dead cell + 4 neighbors = stays dead). Because identical totals create different results, it instead depends separately on the center's state and the sum of outer neighbors. This defines outer-totalistic.

Full classification: **silent state ✔, symmetric ✔, legal ✔, peripheral ✘, totalistic ✘ (outer-totalistic).**
</details>

### ⚠️ TRAPS

- **Writing "totalistic ✔"** for Game of Life. It is outer-totalistic. Costs a mark on `sheet-03`-style follow-ups.
- **Forgetting the CA specification** ($d$, $r$, $k$, legal) on a 10-pointer. "Every detail of it" is a literal instruction.
- **Drawing the glider without labelling $t=0..t=3$.** Unlabelled grids score nothing.
- **Getting the diagonal backwards.** Use the one-step check. Always.

---

## Q2 · Evolutionary Algorithm — full explanation + application 🔒
**Recurrence: 4/4. Always 10 points. The single biggest question on the paper.**

### Asked as

- *"Explain EAs, the idea behind them, the pros and cons. Develop steps for an Evolutionary algorithm for the following problem: You want to mix the perfect soda, there are **7** fixed ingredients and **70** possible additives. You can always use **15** additives at a time, the additives cannot be more than **3%** of the total mix and each additive cannot be more than **1%**. To evaluate the quality you have a pool of students willing to test the sodas, the best result is achieved if the students always compare **2 drinks** to each other."* — 2023 `qn-02` 3, **10 pt**
- *"Define all parts and steps of an Evolutionary Algorithm. What are the benefits and what are downsides? Use this to define an EA that solves the following scenario: [**6** ingredients] … up to **Y=15** additives out of possible **Z=60**. Every additive mustn't be more than **1%**, all additives together mustn't be more than **3%**. You may also use a council of students that rate the sodas; the best comparison is achieved when **two** sodas are compared."* — 2025 T2, **10 pt**
- *"Explain all parts of an EA with an example that had some genome restrictions."* — 2023 `qn-03`, **10 pt**
- *"Explain every aspect of EAs and how they contribute [+ exploration vs exploitation]"* — 2017 Q3, **10 pt**

**Note the pattern: the recipe numbers change every year (7/70, 6/60), the structure never does.** Do not memorize 70; memorize the layout.

### THE BLOCK TO WRITE

**① The idea (2 sentences)**

> An Evolutionary Algorithm is a **stochastic, population-based optimization method** inspired by biological evolution. It maintains a population of candidate solutions, evaluates each with a fitness function, and repeatedly selects the better ones to produce offspring by recombination and mutation, so the population improves over generations.

**② The parts** — name all six

| Part | What it is |
|---|---|
| **Individual** | One candidate solution. |
| **Genome** | The encoding of that solution (bit string, vector of reals, tree, …). |
| **Fitness function** | Maps a genome to a quality value; the thing being optimized. |
| **Population** | The set of $\mu$ individuals held at one time. |
| **Generation** | One full pass of the cycle. |
| **Operators** | Selection, recombination/inheritance, mutation. |

**③ The EA cycle** — draw it as a loop, name every step

```
        +-------------------- Initialization --------------------+
        |                                                        |
        v                                                        |
   Fitness evaluation                                            |
        |                                                        |
        v                                                        |
   External selection   (which individuals survive: (mu+lambda)   |
        |                or (mu,lambda), elitism, rank-based)     |
        v                                                        |
   Parent selection     (who reproduces: wheel of fortune,        |
        |                softmax, tournament)                     |
        v                                                        |
   Inheritance / Recombination  (crossover of parent genomes)     |
        |                                                        |
        v                                                        |
     Mutation           (random change of single genes)           |
        |                                                        |
        v                                                        |
     Finished?  --- no -------------------------------------------+
        |
       yes -> return best individual
```

**④ Pros and cons**

| Benefits | Downsides |
|---|---|
| Needs **no gradient** and no model of the objective function. | **No guarantee** of finding the global optimum. |
| Works on **discrete, continuous and mixed** genomes. | **Many fitness evaluations** — expensive if evaluation is costly. |
| **Anytime behaviour** — a usable answer at any interruption. | **Many parameters** to tune (population size, mutation rate, selection pressure). |
| **Trivially parallel** — individuals evaluate independently. | Can **stagnate** in a local optimum or collapse to a super-individual. |
| Robust against noisy or changing fitness. | Results are **not reproducible** without fixing the random seed. |

**⑤ The application** — see the recipe below.

### ⚙️ THE SODA RECIPE — how to instantiate it for whatever numbers they give

Let the paper's numbers be: **$n$ fixed ingredients**, **$Y$ additives chosen from $Z$ possible**, each additive **≤ 1 %**, all additives together **≤ 3 %**, fitness by **pairwise tasting**.

**Genome.** Two parts:
- a vector of $n$ **real numbers** giving the proportions of the fixed ingredients (normalised to sum to 97 %);
- a list of **$Y$ (index, amount) pairs**, where index $\in \{1..Z\}$ selects the additive and amount $\in [0, 1\,\%]$ gives its share.

> Say why you chose this: it is compact, and it makes the "exactly $Y$ additives" constraint **structural** — it cannot be violated because the genome has exactly $Y$ slots.

**Constraint handling.** Name a strategy, do not leave it implicit — **and check first which constraint is actually binding.**

> ⚠️ **Do this arithmetic before designing the repair operator.** $Y$ additives at the per-item cap would total $Y \times 1\% = 15\%$, but the **total cap is 3 %**. So the **per-item cap is slack and the total cap is binding**:
> - at most $3\%/1\% = \mathbf{3}$ of the 15 additives can sit at their ceiling;
> - the **average** additive must be $\le 3\%/15 = \mathbf{0.2\,\%}$, not 1 %;
> - therefore **clipping to $[0,1\%]$ alone does NOT enforce the constraints** — a clipped genome can still total 15 %. The **normalisation to the 3 % budget is the operator that does the real work**; the per-item clip is a secondary, rarely-active correction.

- *All additives $\le 3\%$ (the binding one)* — if $\sum$ amounts $> 3\%$, **rescale all amounts by $3\% / \sum$**. This is a **repair** operator; the alternative is a **penalty** subtracted from fitness. Repair is better here because a human tasting is far too expensive to waste on an infeasible recipe.
- *Each additive $\le 1\%$ (the slack one)* — **clip** the amount gene to $[0, 1\%]$ **after** rescaling.
- *Indices must be distinct* — repair duplicates by resampling.
- *"Up to" $Y$ additives* — keep $Y$ fixed slots and let **amount $= 0$ mean "slot unused"**, so "at most $Y$" is satisfied structurally and can never be violated.
- *The base ingredients* then share the remaining $\ge 97\%$, normalised to sum with the additives to 100 %.

**Why an EA at all? — quantify it, this is the other half of the marks.** The discrete part of the search space alone is
$$\binom{Z}{Y} = \binom{60}{15} \approx 5.32\times10^{13} \qquad\text{(2025)}, \qquad \binom{70}{15} \approx 7.21\times10^{14} \qquad\text{(2023)}$$
and that is **before** the continuous ingredient proportions. With a human tasting panel you can afford perhaps a few hundred fitness evaluations. Exhaustive search is therefore off by more than ten orders of magnitude, and no gradient exists because the fitness comes from human judgement — **which is exactly the situation EAs are for.**

**Fitness.** This is the part the question is really testing:
- The students give **pairwise comparisons**, not absolute scores. So the raw output is a **relative** ordering, not a number.
- Therefore use **tournament selection** (directly consumes pairwise comparisons) or convert the comparisons into a **rank** and use **rank-based** selection. Explicitly say: *fitness-proportional selection is not applicable, because no absolute fitness value exists.*
- Note the practical limit: each comparison costs a human tasting, so **fitness evaluation is by far the most expensive step**, and the population must be kept small.

### ⭐ HOW TO DECIDE WHICH SELECTION METHOD TO NAME

**Step 1 — remember there are TWO selection steps, and name one of each. They are separate marks.**

| | **External selection** | **Parent selection** |
|---|---|---|
| Answers | *How many survive, and which?* | *Which survivors reproduce?* |
| Choose from | $(\mu+\lambda)$ / $(\mu,\lambda)$, elitism, deterministic rank truncation | **wheel of fortune, softmax, tournament** |
| Asked alone as | 2025 T6, `qn-02` 13 (the fitness diagrams) | 2025 T11, `qn-02` 9, `qn-03` (Wheel of Fortune) |

> ⚠️ **Wheel of fortune, softmax and tournament are ONLY parent selection. $(\mu+\lambda)$ and elitism are ONLY external selection.** Never offer one where the other belongs.
>
> ⚠️ **"Wheel of fortune" and "rank-based" are not alternatives.** The lecture's wheel of fortune **is** rank-proportionate: *"a widely used way to implement a probabilistic, **rank proportionate** parent selection is the wheel of fortune."* So "rank-based wheel of fortune" is one coherent choice. The genuine axis is **fitness-proportional vs rank-proportional shares**.

**Step 2 — for parent selection, read what the FITNESS FUNCTION produces. That sentence in the question is the one that decides; the constraint numbers are decoration.**

| What the fitness gives you | Name this | Because |
|---|---|---|
| Absolute numbers, comparable scale | **wheel of fortune**, fitness-proportional | sector size $\propto$ fitness; simplest |
| Absolute numbers, one individual dwarfing the rest | **wheel of fortune on ranks** | rank ignores the *size* of the gap ⇒ no super-individual takeover |
| You must control selection pressure explicitly | **softmax**, $\omega_p = \dfrac{e^{f(p)/\tau}}{\sum_q e^{f(q)/\tau}}$ | large $\tau$ ⇒ near-equiprobable; small $\tau$ ⇒ greedy |
| A **full ranking**, no numbers | **rank-based** ⇒ wheel of fortune on ranks | ranks are exactly what you have |
| Only **pairwise comparisons** | **tournament** | tournament *is* pairwise comparison — nothing to convert |
| Fitness noisy or very expensive | **tournament** | needs only comparisons; robust to noise |

**Step 3 — for external selection, the safe default is $(\mu+\lambda)$ with elitism**, because it guarantees the best solution found is never lost and the performance graph is monotone. Switch to $(\mu,\lambda)$ only if the question says the **fitness drifts over time** or that escaping local optima matters.

**Step 4 — write the choice PLUS one because-clause.** The examiner cannot mark "tournament" right or wrong — both methods are legitimate. **He marks the justification.** So:

> *"Parent selection: **tournament**, because the panel only ever compares two sodas at a time, so no absolute fitness value exists and a fitness-proportional wheel is not applicable."*

An unjustified correct choice scores less than a justified defensible one. **If you are unsure, pick either, justify it in one clause, and move on.**

> **This is why the soda question plants the sentence** *"the best result is achieved if the students always compare 2 drinks to each other"* — it exists to make **tournament** correct. Change it to *"the panel ranks the batches"* and **rank-based** becomes correct instead.

**Operators.**
- **Parent selection:** tournament (pairs of sodas compared — matches the panel exactly).
- **Recombination:** one-point crossover on the ingredient vector; for the additive list, take a random subset from each parent and repair duplicates.
- **Mutation:** perturb an ingredient proportion by a small Gaussian step; with low probability replace one additive index by a random unused one.
- **External selection:** $(\mu + \lambda)$ with **elitism**, so the best recipe found is never lost.

**Termination.** Fixed number of generations, or a fixed tasting budget, or stagnation of the best individual.

### VARIANTS

**V1.** *"Design an EA to find the best chocolate recipe: 5 base ingredients, up to 10 flavourings from 40 possible, each flavouring ≤ 2 %, all flavourings ≤ 8 %. A panel ranks batches from best to worst."*

<details><summary>Answer — write this</summary>

**Genome.** Two parts:
- 5 real numbers = the proportions of the base ingredients;
- 10 fixed slots, each a pair (index $\in\{1..40\}$, amount $\in[0,2\%]$). **Amount $=0$ means the slot is unused**, so "up to 10" holds structurally.

**Constraints — the total cap is the binding one.** $10\times2\% = 20\%$ but the total is capped at $8\%$, so at most $8/2 = 4$ flavourings can be at their ceiling and the average must be $\le 8/10 = 0.8\%$. Therefore:
1. If $\sum$ amounts $> 8\%$, **rescale all amounts by $8\%/\sum$** (repair).
2. **Then** clip each amount to $[0,2\%]$.
3. Resample duplicate indices.
4. Normalise the 5 base proportions to fill the remaining $\ge 92\%$.

**Fitness.** The panel returns a **full ranking** of the batches, so there is no absolute fitness value — only an ordering. Use **rank-based selection**, and the **wheel of fortune with rank-proportional shares is directly applicable**: $\omega_i = \frac{2(P-r(i)+1)}{P(P+1)}$. *(Contrast with the soda task, where the panel compares only two at a time and tournament selection is the natural fit.)*

**Operators.** Parent selection: wheel of fortune on the ranks. Recombination: one-point crossover on the base vector; random subset of flavouring slots from each parent, then repair. Mutation: small Gaussian step on a proportion; with low probability swap a flavouring index for an unused one. External selection: $(\mu+\lambda)$ with **elitism**, so the best recipe is never lost.

**Termination.** Fixed number of tasting rounds (the panel is the cost bottleneck), or stagnation of the best batch.

**Why an EA.** The discrete part alone is $\binom{40}{10} = 847{,}660{,}528 \approx 8.5\times10^8$ combinations, before the continuous proportions; fitness is human judgement, so there is **no gradient and no model**, and only a few hundred evaluations are affordable.
</details>

**V2.** *"Where do exploration and exploitation enter an EA?"* (2017 Q3b)

<details><summary>Answer</summary>

- **Exploration** — random **initialization** of the population, and **mutation**, which introduce genuinely new points in the search space.
- **Exploitation** — **selection** (external and parent), **elitism**, and **recombination of good parents**, which concentrate the search around already-good solutions.
- The **balance** is what controls the algorithm: too much exploration is random search, too much exploitation collapses the population onto one point (a super-individual) and stagnates.
</details>

**V3.** *"Name three termination criteria for an EA."*

<details><summary>Answer</summary>

Any three of: a **fixed number of generations**; a **fixed time or evaluation budget**; a **target fitness reached**; **stagnation** of the best fitness over $k$ generations; the **population has converged** (diversity below a threshold).
</details>

**V4.** *"Which step of an EA is the most expensive, and why?"*

<details><summary>Answer</summary>

**Fitness evaluation** — it must be done for every individual in every generation, and in real applications it involves a simulation, an experiment, or (as in the soda task) a human tasting.

If fitness evaluation is explicitly excluded, the answer is **external selection**, which requires sorting the population, $O(n \log n)$; parent selection can reach $O(n^2)$; mutation is only $O(n)$ random numbers.
</details>

### ⚠️ TRAPS

- **Answering only the theory half and skipping the application** (or vice versa). It is one question worth 10 points with two halves — budget 5 minutes each.
- **Ignoring the pairwise-comparison hint.** It is in the question for a reason: it forces tournament or rank-based selection. Saying "fitness-proportional" here is wrong.
- **Not naming a constraint-handling strategy.** "Genome restrictions" is literally the phrase `qn-03` uses.

---

## Q3 · The 5 criteria of life 🔒
**Recurrence: 4/4. Always 5 points. The cheapest points on the paper.**

### Asked as

- *"Name 5 attributes, commonly used to define natural life."* — 2025 T8
- *"Name 5 common criteria for life mentioned at the beginning of the lecture."* — 2023 `qn-02` 14
- *"Name 5 properties commonly associated with life."* — 2023 `qn-03`
- *"Name 5 criteria of life."* — 2017 Q4

### THE BLOCK TO WRITE

Open with one framing sentence, then **a numbered list — never a paragraph.** The marker is counting items.

> There is no commonly accepted definition of life; instead there are several sets of criteria that must be fulfilled. One common set is:

1. **Metabolism** — the organism takes in, converts and releases matter and energy.
2. **Reproduction** — it produces new individuals of its own kind.
3. **Growth** — it increases in size and complexity over its lifetime.
4. **Reaction to the environment** — it responds to external stimuli.
5. **Movement out of itself** — it moves under its own power, not only when pushed.

Optional sixth and seventh if you want padding: **existence in space and time**, **storage of information about oneself** (the genome), **phylogenetic development** (the species evolves), **ontogenetic development** (the individual develops), **decay and death**.

### VARIANTS

**V1.** *"Name 7 criteria of life."*

<details><summary>Answer</summary>
Take the five above plus **existence in space and time** and **storage of information about oneself**. Alternatively quote **Koshland's 7 pillars** by name: a program to make copies of itself; adaptation and evolution through mutation and selection; a complex, compartmentalized structure; the ability to take energy from the environment; regeneration systems; responsiveness through feedback; numerous separated metabolic reactions.
</details>

**V2.** *"Name a border case of life and explain why it is problematic."*

<details><summary>Answer</summary>

Pick one and give the reason:
- **Virus** — it reproduces and stores information about itself, but has **no metabolism of its own** and replicates only inside a host cell.
- **Mule** — satisfies every criterion **except reproduction** (it is sterile), which shows no single criterion can be treated as strictly necessary.
- **Crystal** — grows and is highly organised, but has **no metabolism, no reproduction, no reaction to stimuli**.
- **Fire** — consumes, grows, moves and reacts, but does **not reproduce a description of itself**.
</details>

**V3.** *"Which criteria of life are not met by Conway's Game of Life?"* (`sheet-03` A8 — plausible exam crossover)

<details><summary>Answer</summary>

- **Metabolism — not met.** No energy or matter is taken in or converted; there is no energy budget at all.
- **Growth (ontogenetic development) — not met.** A pattern does not develop through a life cycle; it persists, oscillates, moves or dies.
- **Phylogenetic development — not met.** There is no mutation and no selection, hence no evolution.
- **Reaction to the environment — only trivially met.** Cells react to neighbours, but there is no external environment and no adaptation.
- **Reproduction — partly met.** A glider gun does produce new gliders, and self-replicating patterns exist.

Closing sentence: Game of Life satisfies the structural and dynamic criteria but fails the energetic and evolutionary ones — which is exactly why it is **weak** Artificial Life.
</details>

**V4.** *"What is the difference between strong and weak Artificial Life?"*

<details><summary>Answer</summary>

- **Strong AL** aims to **really create** artificial lifeforms — life out of non-living material — and works mainly on a **molecular** basis. The claim is that the artefact **is** alive.
- **Weak AL** aims to **identify the properties, principles and circumstances** of life; rather than creating a living entity it **simulates** the conditions and behaviour of life. Most AL researchers, and this entire lecture, are weak AL.
</details>

### ⚠️ TRAPS

- **Writing a paragraph instead of a list.** Five bullets, five marks. Prose containing the same five ideas scores worse.
- **Giving fewer than asked.** If it says 5, give 5 (or 6 for safety). Do not give 3.

---

## Q4 · Wolfram number ↔ rule table ⚙️
**Recurrence: 4/4. 5 points forward, 10 points reverse.**

### Asked as

- *"Give a rule table for the Wolfram number 42_D with d=1, r=1, k=2."* — 2023 `qn-02` 6
- *"Write down the ruleset for the Wolfram number 42_D."* — 2023 `qn-03`
- *"[Wolfram number] rule table"* — 2017 Q5
- *"Name **all possible** Wolfram Numbers that produce the following d=1, k=2, r=1 patterns [t=0, t=1, t=2 shown]. Explain how you calculated the numbers."* — 2025 T1, **10 pt**
- Oral C: $d{=}1, k{=}2, \mathbf{r{=}2}$, number **65538**

### ⚙️ THE RECIPE — forward

**Step 1.** Write the 8 neighbourhoods in **descending binary order** with their weights. This ordering IS the method:

```
 neighbourhood:  111   110   101   100   011   010   001   000
 weight:         2^7   2^6   2^5   2^4   2^3   2^2   2^1   2^0
                 128    64    32    16     8     4     2     1
```

**Step 2.** Convert the decimal number to 8 bits, MSB = the `111` column.
**Step 3.** Fill the output row.
**Step 4.** Classify the rule (this is the standard free follow-up).

### WORKED — rule 42

$$42 = 32 + 8 + 2 = 2^5 + 2^3 + 2^1$$

So the bits at weights $2^5, 2^3, 2^1$ are set — the neighbourhoods **101, 011, 001**:

```
 42_D = 0 0 1 0 1 0 1 0_B

 neighbourhood:  111  110  101  100  011  010  001  000
 new state:       0    0    I    0    I    0    I    0

 as cells:       ###  ##.  #.#  #..  .##  .#.  ..#  ...
                  .    .    #    .    #    .    #    .
```

**Classification of rule 42:**
- **Silent state?** $000 \to 0$. **Yes.**
- **Symmetric?** Mirror pair $110 \to 0$ but $011 \to I$. **No.**
- **Legal?** Needs symmetric AND silent. **No.**
- **Totalistic?** SUM $=2$ gives $110{\to}0$, $101{\to}I$, $011{\to}I$ — not constant. **No.**
- **Peripheral?** $111 \to 0$ but $101 \to I$, so the centre matters. **No.**

### ⚙️ THE RECIPE — reverse (the 10-pointer)

Given an evolution picture over $t=0,1,2$, find **all** Wolfram numbers consistent with it:

1. Write the rows aligned, one under the other.
2. For **every** cell of row $t{+}1$, read its neighbourhood from row $t$ (itself + one either side). Each reading is one constraint "$abc \to o$".
3. Collect constraints into the 8-row table. **If two cells give the same neighbourhood but different outputs, no rule produces the picture** — say so, that is the answer.
4. Count the **unconstrained** lines. If $m$ of the 8 are pinned down, there are $$2^{\,8-m}$$ consistent Wolfram numbers.
5. Report as: fixed part $+$ any subset of the free weights.

### ✅ WORKED EXAMPLE — a full instance in the 2025 T1 format

> ⚠️ The 2025 protocol records the task but **not the grids that were printed**, so the exact numbers from the real paper cannot be recovered. The instance below is constructed in the same format; the **method is what transfers**.

**Question.** *"Name all possible Wolfram Numbers that produce the following $d{=}1$, $k{=}2$, $r{=}1$ patterns. Explain how you calculated the numbers."* Cells outside the window are white.

```
 position:  1  2  3  4  5  6  7  8  9
     t=0:   .  .  .  .  #  .  .  .  .
     t=1:   .  .  .  #  .  #  .  .  .
     t=2:   .  .  #  .  .  .  #  .  .
```

**What is being reversed:** the forward question gives you a number and asks for the pattern. Here you get the pattern and must find every number that could have produced it. Because a 3-row picture does not exercise all 8 neighbourhoods, **several rules fit — the answer is a set, not one number.**

**Step 1 — one constraint per cell of each new row.**

| Step | Pos | Neighbourhood at $t$ | Output at $t{+}1$ | Constraint |
|---|---|---|---|---|
| 0→1 | 3 | `000` | `.` | $000 \to 0$ |
| 0→1 | 4 | `001` | `#` | $001 \to 1$ |
| 0→1 | 5 | `010` | `.` | $010 \to 0$ |
| 0→1 | 6 | `100` | `#` | $100 \to 1$ |
| 1→2 | 3 | `001` | `#` | agrees ✓ |
| 1→2 | 4 | `010` | `.` | agrees ✓ |
| 1→2 | 5 | `101` | `.` | **$101 \to 0$ (new)** |
| 1→2 | 6 | `010` | `.` | agrees ✓ |
| 1→2 | 7 | `100` | `#` | agrees ✓ |

All remaining cells sit in the white margins and repeat $000 \to 0$.

**Step 2 — fill the table.** Five of the eight lines are pinned; three are never presented by this picture.

```
 neighbourhood:  111  110  101  100  011  010  001  000
 output:          x    x    0    I    x    0    I    0
 weight:         128   64   32   16    8    4    2    1
```

**Step 3 — count.** $m = 5$ pinned $\Rightarrow 2^{8-5} = 2^{3} = \mathbf{8}$ consistent Wolfram numbers.

**Step 4 — report them.** Fixed part $= 16 + 2 = 18$; free weights $= \{128, 64, 8\}$.

$$\boxed{\;\{18,\; 26,\; 82,\; 90,\; 146,\; 154,\; 210,\; 218\} \;=\; 18 + \text{any subset of } \{128,\,64,\,8\}\;}$$

**Step 5 — verify one.** Rule **90** is in the set ($18 + 64 + 8$), and rule 90 (XOR of the two neighbours) does generate exactly this Sierpiński opening. Rule **18** ($= 18 + \varnothing$) also does. Both are correct — that is the point of the question.

**The two sentences that earn marks:** the **white margins** are what give you $000 \to 0$ for free; and $111$, $110$, $011$ are unconstrained **because a single seed cannot produce two or three adjacent live cells within three steps**, so the picture carries no information about those neighbourhoods.

### VARIANTS

**V1.** *"Write the rule table for Wolfram number 90 and classify it."*

<details><summary>Answer</summary>

$90 = 64+16+8+2 = 2^6+2^4+2^3+2^1$ → neighbourhoods 110, 100, 011, 001:
```
 111  110  101  100  011  010  001  000
  0    I    0    I    I    0    I    0
```
Rule 90 is **XOR of the two neighbours** (the centre is ignored). Classification: **silent ✔** ($000\to0$), **symmetric ✔**, **legal ✔**, **peripheral ✔**, **totalistic ✘** (SUM=2 gives $110{\to}I$, $101{\to}0$, $011{\to}I$).

From a single seed it draws the **Sierpiński triangle**:
```
 t=0    . . . . . . . # . . . . . . .
 t=1    . . . . . . # . # . . . . . .
 t=2    . . . . . # . . . # . . . . .
 t=3    . . . . # . # . # . # . . . .
 t=4    . . . # . . . . . . . # . . .
```
</details>

**V2.** *"Write the rule table for Wolfram number 110. Is it legal?"*

<details><summary>Answer</summary>

$110 = 64+32+8+4+2$ → neighbourhoods 110, 101, 011, 010, 001:
```
 111  110  101  100  011  010  001  000
  0    I    I    0    I    I    I    0
```
**Silent ✔** but **not symmetric** ($100 \to 0$ while its mirror $001 \to I$), therefore **not legal**. Rule 110 is the famous **class IV** rule, later proved **Turing-complete**.
</details>

**V3.** *"Give the rule table for Wolfram number 184."*

<details><summary>Answer</summary>

$184 = 128 + 32 + 16 + 8 = 2^7 + 2^5 + 2^4 + 2^3$ → neighbourhoods 111, 101, 100, 011:
```
 111  110  101  100  011  010  001  000
  I    0    I    I    I    0    0    0
```
**Silent ✔**, **symmetric ✘** ($110\to0$ vs $011\to I$), **not legal**, not peripheral, not totalistic. (Rule 184 is the classic **traffic-flow** rule.)
</details>

**V4.** *"$d=1, k=2, r=2$, Wolfram number 65538. How many lines does the table have and how many outputs are I?"*

<details><summary>Answer</summary>

$n = 2r+1 = 5$, so the table has $L = 2^5 = \mathbf{32}$ lines and there are $Z = 2^{32}$ rules.
$65538 = 65536 + 2 = 2^{16} + 2^{1}$, so **exactly two** of the 32 lines output $I$ — those at weights $2^{16}$ and $2^{1}$. Indexing the 32 neighbourhoods from $11111$ (weight $2^{31}$) down to $00000$ (weight $2^0$), those are the neighbourhoods with binary index $16 = 10000_B$ and $1 = 00001_B$.

**The moral to state:** the Wolfram numbering is not special to $r=1$; it is just "read the output column as a base-$k$ number", and the table gets longer.
</details>

### ⚠️ TRAPS

- **Getting the column order backwards.** `111` is the MSB. Always write the header row first.
- **Confusing $L$ (table lines) with $Z$ (number of rules).**
- On the reverse question, **forgetting to report ALL numbers.** The question says "all possible" — the $2^{8-m}$ count is the point.

---

## Q5 · Langton's Ant 🔒
**Recurrence: 4/4. Always 5 points.**

### Asked as

- *"Name the 4 micro behaviors of Langton's Ant and give a short scribble visualization **for each of them**."* — 2025 T3
- *"Explain the 4 steps of microbehaviour of Langton's Ant, support your explanation by a drawing of each step."* — 2023 `qn-02` 10
- *"[4 micro-behaviours]"* — 2023 `qn-03`
- *"Compare the patterns and behaviour on a uniform **white** plane vs a uniform **black** plane."* — 2017 Q7

### THE BLOCK TO WRITE

**The rule, first, in words:**
> At a **white** cell: turn **90° right**, flip the cell, move forward one step.
> At a **black** cell: turn **90° left**, flip the cell, move forward one step.

**The four micro-behaviours — scan → turn → flip → move.** Four separate drawings are demanded.

```
   (1) SCAN                 (2) TURN                (3) FLIP                (4) MOVE

   . . . . .              . . . . .              . . . . .              . . . . .
   . . ^ . .              . . > . .              . . > . .              . . # > .
   . . . . .              . . . . .              . . . . .              . . . . .

   read the state         turn 90° R because     invert the cell        step one cell
   of the cell under      the cell was WHITE     under the ant          forward along
   the ant                (90° L if BLACK)       (white -> black)       the new heading
```

1. **Scan** — the ant reads the state of the cell it stands on. This is its only input; it has no memory.
2. **Turn** — 90° **right if white**, 90° **left if black**. Only the heading changes.
3. **Flip** — the ant inverts the cell it stands on. This is its only way of writing.
4. **Move** — one cell forward along the new heading.

### The three macroscopic phases (uniform white plane)

| Phase | When | What |
|---|---|---|
| **1 — Symmetric growth** | to ≈ step **420** | small, almost symmetric pattern |
| **2 — Chaotic growth** | ≈ step **400 – 10 000** | growth with no distinguishable structure; **deterministic chaos** |
| **3 — Highway** | from ≈ step **10 000** | a highly structured, **persistent, repetitive** pattern with **cycle time 104 steps**, carrying the ant off to infinity |

```
 black
 cells ^                                        /
       |                                      /   <- Phase 3: HIGHWAY, period 104
       |              ~~~~~~~~~~~~~~~~~~~~~~/
       |        ~~~~~                            <- Phase 2: CHAOTIC
       |  /\/\/                                  <- Phase 1: SYMMETRIC
       +--+----------------+--------------------> t
         ~420           ~10 000
```

Add the lecture's own remark, worth a mark on any "explain" version:
> Although the rule is simple and every step is comprehensible, the short-term behaviour is hard to impossible to predict and the mid-term behaviour resists prediction entirely. The only way to know the grid at time $t$ is to **run the simulation**.

### The first four steps, drawn

```
  t=0                t=1                t=2                t=3                t=4

. . . . .          . . . . .          . . . . .          . . . . .          . . . . .
. . ^ . .          . . # > .          . . # # .          . . # # .          . . ^ # .
. . . . .          . . . . .          . . . v .          . . < # .          . . # # .
. . . . .          . . . . .          . . . . .          . . . . .          . . . . .
```

At $t=4$ the ant is back on its starting cell, which is now **black**, so it turns **left** and the square breaks open.

### VARIANTS

**V1.** *"Compare Langton's Ant on a uniform white plane with a uniform black plane."* (2017 Q7)

<details><summary>Answer</summary>

**They are mirror images with identical statistics.** The rule is **colour-symmetric**: exchanging the two colours swaps "turn right" with "turn left" and changes nothing else. So the black-plane run produces the **left–right mirrored** trajectory. **All three phases occur in the same order at the same step counts**, and the highway still has **period 104** — it simply runs off in the mirrored diagonal direction. The trail colours are inverted.
</details>

**V2.** *"Langton's Ant starts on a white square of an infinite checkerboard. Describe the behaviour and draw the first steps."*

<details><summary>Answer</summary>

On a checkerboard the colours alternate, so the ant alternates **right, left, right, left** and produces a **perfectly regular diagonal staircase** to infinity — no chaotic phase and no highway.

```
   step 1: white -> turn R, flip, move E          . . . . o
   step 2: black -> turn L, flip, move N          . . . o .
   step 3: white -> turn R, flip, move E          . . o . .
   step 4: black -> turn L, flip, move N          . o . . .
   ... repeating for ever                         o . . . .
```
This shows that **the initial configuration, not the rule, decides whether the behaviour is chaotic.**
</details>

**V3.** *"Why is Langton's Ant called a two-dimensional Turing machine?"*

<details><summary>Answer</summary>

| Turing machine | Langton's Ant |
|---|---|
| Tape | the 2-dim grid |
| Tape alphabet | $\{$white, black$\}$ |
| Read/write head | the ant |
| Internal state | the ant's **heading** (N, E, S, W) — four states |
| Transition function | read symbol → write flipped symbol → change state (turn) → move |
| Halting state | **none** — the ant never halts |

Gajardo, Moreira and Goles (2000) proved a **single** Langton's Ant can implement **any Boolean function**.
</details>

**V4.** *"What does the notation RL mean for Langton's Ant?"*

<details><summary>Answer</summary>

It is the generalisation to $k > 2$ cell states. The state is **increased by one cyclically** at every move, and the rule is written as a **string of turn directions, one letter per state**. **Langton's original ant is `RL`** — turn **R**ight on state 0 (white), **L**eft on state 1 (black). Other rules named in the lecture: `RLR`, `LLRR`, `RRLLLRLLLRRR`; different strings give wildly different long-term behaviour.
</details>

### ⚠️ TRAPS

- **Drawing one picture instead of four.** Both papers say "of each step" / "for each of them".
- **Omitting which colour causes which turn.** Write "white ⇒ right, black ⇒ left" in words next to the drawing.
- **Forgetting the number 104.** It is the most markable single figure in this answer.

---

## Q6 · Braitenberg vehicles 🔒
**Recurrence: 4/4 — and it fills TWO slots on most papers** (2023 asked it twice, 2025 asked it twice). Treat it as worth **10 points**.

### ⭐ FIRST: WHICH OF THE THREE QUESTIONS DID YOU GET?

Three distinct Braitenberg questions have been asked. **Find your wording in the left column and write the answer named on the right — do not write all three.**

| If the paper says… | Paper | Write |
|---|---|---|
| *"What is the **probabilistic / stochastic component** of a **type 1** vehicle?"* · *"…and how is that beneficial?"* · *"Which part of a Type I vehicle **can profit from a stochastic element**?"* | `qn-02` 7 · 2025 T14 · `qn-03` | **§ Q6a** |
| *"What would happen if you **change proximity to distance sensors** in Braitenberg 3b?"* · *"Someone accidentally **replaced all the proximity-sensors with distance-sensors**. Explain the expected behaviour and draw an imagery example."* | `qn-02` 8 · 2025 T4 | **§ Q6b** |
| *"Imagine a Braitenberg vehicle **for obstacle avoidance** …"* (design it / draw the scene) | 2017 Q9 | **§ Q6c** |

---

### § Q6a — The stochastic component of a type 1 vehicle

**The answer, in three parts. Write all three; the third is what most people miss.**

**① What a type 1 vehicle is.**
> A type 1 vehicle has **one sensor and one motor**, connected positively: *"The more there is of the quality to which the sensor is tuned, the faster the motor goes."* With a temperature sensor it speeds up in warm areas and slows down in cold ones. Because the connection is positive and the sensor gives only positive values, **the vehicle always moves forward**.

**② WHAT the stochastic component IS** — this is the literal answer to *"what is it"* and *"which part"*:
> The stochastic component is **not** designed in — it comes from **small perturbations from the mechanical construction, from the surface, and from friction**, which cause the vehicle to **change its direction slightly**. So the part that carries the randomness is the vehicle's **heading / direction of travel**, not the sensor reading and not the motor speed.

**③ WHY it is beneficial** (the half that 2025 T14 adds explicitly):
> Moving only straight ahead — even with changing speed — is boring, and the vehicle would explore nothing. **It is the stochastic component that makes the behaviour interesting.** Because the vehicle **moves quickly in warm regions and slowly in cold ones**, and now wanders rather than going straight, it **spends longer in the cold regions**. From an outside perspective it therefore looks as if the vehicle **"loves" cold regions and "dislikes" warm ones** — apparently goal-directed behaviour produced with **no goal, no map and no plan**. That is the entire point of Braitenberg's argument.

```
        Type 1                          resulting trajectory

          [S]                    WARM region        COLD region
           |  +                  ~~~~~~~~~~~~       ------------
           v                      /   fast           \  slow, wanders,
          (M)                    /   straight-ish     \/\/\  stays longer
         ==O==                  /                      \/\/\
                               /                        \/\/
     one sensor, one motor,   passes through quickly    lingers here
     positive connection
                          => looks like it "loves" cold
```

---

### § Q6b — Proximity sensors replaced by distance sensors

**The whole answer turns on ONE fact. State it first, then the consequence.**

**① The sensor characteristic is inverted.**

```
   PROXIMITY sensor                  DISTANCE sensor
   value                             value
     ^                                 ^
     |\                                |      /
     | \                               |    /
     |  \                              |  /
     |   \___                          |/
     +--------> distance               +--------> distance
   near      far                     near      far

   near  ->  LARGE value             near  ->  SMALL value
```

> A **proximity** sensor gives a **large** value when the object is **close**. A **distance** sensor gives a **small** value when the object is close. Swapping them therefore **inverts the sensor-motor mapping**.

**② The consequence — spell out both directions.**
> A type 3b has **crossed inhibitory** connections, so a large sensor value strongly inhibits the motor on the **opposite** side and the vehicle turns away.
>
> With **distance** sensors, an obstacle that is **close** now produces a **small** value and therefore **almost no inhibition** — both motors run at full speed and the vehicle **drives straight into the obstacle**. Conversely, **open space** produces a **large** value and **strong inhibition** of the opposite motor, so the vehicle **turns away from free space and towards obstacles**.

**③ The verdict, in one sentence.**
> **The obstacle-avoiding vehicle becomes an obstacle-seeking vehicle and collides.** In Braitenberg's vocabulary the 3b "explorer" now behaves like a **3a**: it approaches the nearest object and stops at — or crashes into — it.

```
   WITH PROXIMITY (correct)          WITH DISTANCE (swapped)

     #########  obstacle               #########  obstacle
         ^                                 ^
        /                                  |
       /   curves away                     |   drives straight in
      /                                    |
    (=O=)                                (=O=)
```

---

### § Q6c — Design a Braitenberg vehicle for obstacle avoidance

**① Name the type and the wiring.**
> Use a **type 3b**: **two proximity sensors, two motors, connections CROSSED and INHIBITORY (negative)**. Type 3b is **the most popular of the Braitenberg vehicles and is found in many robotic applications**, because the structure is easy to implement.

**② State the rule in the lecture's own words.**
> *"The closer the object is, the higher the proximity value is, the more the motor on the opposite side will be inhibited."* The inhibited motor slows down, so the robot **turns away from the obstacle**.

**③ Name the principle.**
> The basic principle behind 3b obstacle avoidance is **antagonistic inhibition**, which appears to be a **fundamental principle in living nature** (compare lateral inhibition in activator-inhibitor reaction-diffusion systems).

**④ Draw the scene — the question demands vehicle AND obstacle AND trajectory.**

```
         ###########  obstacle
              |
              | proximity HIGH on the LEFT sensor
              v
        [SL]     [SR]           SL --\ /-- SR      CROSSED,
          \   \ /   /                  X           INHIBITORY (-)
           \   X   /              ML --/ \-- MR
        ( ML ) ( MR )
           \_____/            left sensor  -> inhibits RIGHT motor
              |                            -> right motor slows
              v                            -> vehicle turns RIGHT,
        trajectory curves away                away from the obstacle
```

**⑤ Add the weakness — a bonus sentence that costs nothing.**
> 3b obstacle avoidance is fascinating and powerful compared to its complexity, but it is **not "fool-proof": corners are already a challenge** for this kind of purely reactive control. In a corner the vehicle alternately turns left and right and ends up **static or oscillating**. Fixes: add a **stochastic component**, use a **steeper sensor-motor characteristic**, or add **memory**.

```
   THE CORNER PROBLEM

     ######
     #                turn left  ->  turn right  ->  turn left ...
     #   (=O=)  <-->
     #                result: STATIC or OSCILLATING
     ######
```

---

### REFERENCE — the vehicle types (backing material for all three answers)

```
     2a          2b            3a          3b
   S---M       S   M         S---M       S   M
   |   |        \ /          |   |        \ /
   S---M       S/ \M         S---M       S/ \M
    (+)         (+)           (-)         (-)
  uncrossed    crossed      uncrossed    crossed
  excitatory   excitatory   inhibitory   inhibitory
```

| Type | Connection | Behaviour with a light source | Braitenberg's word |
|---|---|---|---|
| **1** | one sensor, one motor, positive | always drives forward, faster with more stimulus | — |
| **2a** | positive, **uncrossed** | drives **away** from the light, slowing as it gets further; stops when the light is no longer visible | **fear** |
| **2b** | positive, **crossed** | drives **towards** the light with **increasing** speed, and would hit it | **aggression** |
| **2c** | both sensors to both motors | dismissed by Braitenberg — *"a somewhat more luxurious version of Vehicle 1"* | — |
| **3a** | negative, **uncrossed** | turns **towards** the light and **stops in front of it, facing it frontally** — ends up *"sitting motionless in front of the light source"* | **love** |
| **3b** | negative, **crossed** | turns **away**, passing *"almost in slow motion"*, then **speeds up** once heading away and may leave the playground | **explorer** |
| **3c** | 4 sensor pairs, 2a+2b+3a+3b combined | dislikes heat, destroys light bulbs, prefers oxygen and organic matter | — |
| **5–7** | — | **5**: internal states with chains of logic elements. **6**: type-5 structure designed by an **evolutionary process**. **7**: **learning** the internal structure (Mnemotrix). | — |

> Types **1, 2 and 3 have a linear** increasing or decreasing characteristic between the physical modality (distance, proximity, light, …) and the motor value — e.g. *the closer the object is, the slower the motor will run*.

### VARIANTS

**V1.** *"What would happen if you swapped proximity for distance sensors in a Braitenberg **3a**?"*

<details><summary>Answer</summary>
3a with proximity sensors approaches an object and stops facing it. Inverting the sensor characteristic inverts this: **the vehicle now turns away from objects and accelerates into open space** — it behaves like a **3b explorer**. State the general rule: **swapping proximity for distance sensors converts 3a ↔ 3b behaviour**, because it flips the sign of the sensor-motor mapping.
</details>

**V2.** *"How would you build a vehicle that keeps a fixed working distance $d_w$ from a wall?"*

<details><summary>Answer</summary>
Use a **3a-style inhibitory mapping whose zero-crossing sits at $d_w$**, so the motor command is proportional to $(d - d_w)$:
- **closer than $d_w$** → negative → the vehicle **reverses**;
- **further than $d_w$** → positive → the vehicle **advances**;
- **exactly $d_w$** → zero → it **holds station**.

$d_w$ is a **stable fixpoint** of the sensor-motor loop.
</details>

**V3.** *"Why is type 3b preferred over type 2a for obstacle avoidance?"*

<details><summary>Answer</summary>
Both turn away from the stimulus, but **2a is excitatory and accelerates as it escapes**, whereas **3b is inhibitory and slows down near the obstacle**, passing it *"almost in slow motion"* before speeding up again. Braking near danger is both **safer** (less impact energy if it does collide) and **technically easier** with real motors. That is why 3b is the one found in real robotic applications.
</details>

**V4.** *"What is a type 2c vehicle and why did Braitenberg dismiss it?"*

<details><summary>Answer</summary>
A **2c** connects **both sensors to both motors**. Braitenberg dismissed it immediately because with symmetric input to both motors there is no differential steering — it is *"nothing but a somewhat more luxurious version of Vehicle 1"*. The interesting contrast is between **2a and 2b**.
</details>

### ⚠️ TRAPS

- **Answering all three questions when only one was asked.** Use the routing table at the top.
- **Not drawing the scene.** 2017 Q9 and 2025 T4 both say "draw". Vehicle **and** obstacle **and** trajectory.
- **Saying "it would behave oddly" on the sensor-swap question.** Be specific: *near → small value → no inhibition → drives into the obstacle.*
- **Confusing 2a/2b with 3a/3b.** **2 = excitatory (+), 3 = inhibitory (−); a = uncrossed, b = crossed.**
- **On Q6a, giving only "there is noise".** Name its *source* (mechanical construction, surface, friction), what it acts on (the **direction**), and the *benefit* (lingers in cold regions ⇒ looks like it "loves" cold).


---

## Q7 · Lindenmayer System producing `OAOAOA…O` ⚙️
**Recurrence: 4/4. Always 5 points. Same target string every year.**

### Asked as

- *"Develop a Lindenmayer with max. 4 rules that produces **OAOAOAOAOAOAOAO** at t=3 starting with t=0 and the axiom O."* — 2023 `qn-02` 16
- *"Create an L-System that creates the sequence **0A0A0A0A0A0A0** at step t=3 with a maximum of 4 rules."* — 2023 `qn-03`
- *"Define a L0-System that when starting with O generates the following sequence at exactly time-step t=3: **OAOAOAOAOAOAO**"* — 2025 T16
- 2017 Q11 — same question

### THE ANSWER

**Two rules suffice.**

$$V = \{O, A\}, \qquad w = O, \qquad P: \; O \to OAO, \;\; A \to A$$

**Verify by expanding — always show this table, it is most of the marks:**

| $t$ | string | length |
|---|---|---|
| 0 | `O` | 1 |
| 1 | `OAO` | 3 |
| 2 | `OAOAOAO` | 7 |
| 3 | `OAOAOAOAOAOAOAO` | **15** |

Show one expansion explicitly so the marker sees the parallel rewriting:
> $t=2 \to t=3$: `O A O A O A O` → `(OAO) A (OAO) A (OAO) A (OAO)` = `OAOAOAOAOAOAOAO`

**Length recurrence:** $L(t+1) = 2L(t) + 1$ with $L(0)=1$, so $L(t) = 2^{t+1} - 1$: 1, 3, 7, 15, 31, …

**Also define the formalism** (one line, free marks):
> An L-System is the 4-tuple $(V, C, w, P)$ — $V$ variables, $C$ constants, $A = V \cup C$ the alphabet, $w$ the axiom, $P$ the production rules. This is a **D0L-System**: **d**eterministic, **0**-context (context-free), with all symbols rewritten **in parallel** at each step.

### ⚠️ THE LENGTH DISCREPANCY — read this before the exam

The papers do not agree on the target length:

- 2017 and 2023 print **`OAOAOAOAOAOAOAO` = 15 symbols** (8 O, 7 A) → solved exactly by $O \to OAO,\; A \to A$ at $t=3$. ✔
- `qn-01` (2025) records **`OAOAOAOAOAOAO` = 13 symbols** (7 O, 6 A).

**13 is not reachable at $t=3$ from axiom `O` with rules of this family.** Proof sketch: if $O \to$ (alternating string with $p$ O's) and $A \to$ (alternating string with $q$ A's), then with $q=1$ the O-count is $p^t$, which for $t=3$ gives 1, 8, 27, … — never 7. So the 2025 protocol almost certainly **miscounted from memory**.

**What to do in the exam:** **count the O's and A's in the string actually printed on your paper**, then match the length sequence. If it is $2^{t+1}-1$, the two-rule answer above works. If it is not, say which length you counted and give the rules for that length — and state your reasoning. Never assume 15.

### ⚙️ THE GENERAL RECIPE

To hit an alternating target of length $L$ at step $t$ from axiom `O`:

1. **Count the symbols** in the printed target. Get $L$, and the counts of each letter.
2. **Compute the length sequence** for a candidate rule. For $O \to O A O$, $A \to A$: $L(t) = 2^{t+1}-1$.
3. **Match.** If $L$ is 3, 7, 15, 31 at $t = 1, 2, 3, 4$ — use the two-rule answer.
4. If the target grows differently, adjust the right-hand side: $O \to OAOAO$ gives $L(t+1) = 3L(t)+2$, i.e. 1, 5, 17, 53.
5. **Always verify by full expansion** to the required $t$. The expansion table is worth more marks than the rules themselves.

### VARIANTS

**V1.** *"Give an L-System producing `OAOAOAO` at t=2 from axiom O."*

<details><summary>Answer</summary>
Same rules: $O \to OAO$, $A \to A$. $t=0$: `O` (1) → $t=1$: `OAO` (3) → $t=2$: `OAOAOAO` (7). ✔
</details>

**V2.** *"Give an L-System producing `OAOAOAOAOAOAOAOAOAOAOAOAOAOAOAO` (31 symbols) at t=4 from axiom O."*

<details><summary>Answer</summary>
Same rules again — $L(4) = 2^5 - 1 = 31$. ✔ **This is why you learn the recurrence and not the string.**
</details>

**V3.** *"Create an L-System with exactly three rules that produces the 32-symbol string `ABBCBCCABCCACAABBCCACAABCAABABBC` at step 5, starting from axiom A."* (`sheet-04`)

<details><summary>Answer</summary>

Length 32 $= 2^5$ at $t=5$ from a 1-symbol axiom means **every rule must exactly double its symbol**: each rule has a right-hand side of length 2. With three variables $A, B, C$ the rules have the form $A \to xy$, $B \to xy$, $C \to xy$.

Read the answer off the target by expanding backwards: the step-1 string is the first 2 symbols' worth, i.e. $A \to AB$. Then step 2 = 4 symbols `ABBC`, so $B \to BC$. Step 3 = 8 symbols `ABBCBCCA`, so $C \to CA$.

$$P: \quad A \to AB, \qquad B \to BC, \qquad C \to CA$$

Verify: $t{=}0$ `A` → $t{=}1$ `AB` → $t{=}2$ `ABBC` → $t{=}3$ `ABBCBCCA` → $t{=}4$ `ABBCBCCABCCACAAB` (16) → $t{=}5$ 32 symbols. ✔

**The general method to state:** length $2^t$ ⇒ every right-hand side has length 2; then read successive prefixes of the target to recover each rule.
</details>

**V4.** *"What are the turtle-graphics constants in an L-System?"*

<details><summary>Answer</summary>

Aligned with the Logo turtle-graphics syntax: **`+`** turn left by angle $\alpha$, **`−`** turn right by $\alpha$, **`[`** remember the current position (push to stack), **`]`** restore the last position (pop from stack). Variables are read as "draw forward". Example: $F \to F[-F]F[+F][F]$ draws a plant.
</details>

### ⚠️ TRAPS

- **Not verifying by expansion.** The rules alone are half the answer.
- **Assuming the length is 15.** Count what is printed.
- **Forgetting the parallel rewriting.** All symbols are replaced simultaneously — say it.

---

## Q8 · von Neumann — name and explain 2 aspects 🔒
**Recurrence: 4/4. Always 5 points. Pure recall — but the choice of the second aspect matters.**

### Asked as

- *"Name 2 things that John von Neumann is associated with."* — 2025 T10
- *"Name and explain two aspects of Artificial Life that are connected with John von Neumann."* — 2023 `qn-02` 11
- *"Name two concepts associated with John von Neumann and explain them briefly."* — 2023 `qn-03`
- 2017 Q14 — same

### ⚠️ PICK TWO THAT DO NOT OVERLAP

> The tempting pair is **"the Universal Constructor" + "cellular automata"**. Do not use it. **The Universal Constructor *is* a cellular automaton**, so a strict marker can treat them as **one** aspect and award half the marks. Every wording says *"two"*, and they must be **independent**.

**Use this pair — both concrete, both drawable, no overlap:**

---

### ① The Universal Constructor (self-replicating automaton, 1940s)

> Von Neumann was fascinated by the idea of building a machine capable of **reproducing itself**. He designed a system that is **universal with respect to computation AND universal with respect to construction** — so that among everything it can build is **a copy of itself**. That is **replication**, the artificial counterpart of biological reproduction.

**Give the concrete figures — this is where the marks are:**

| | |
|---|---|
| Lives on | a virtually **infinite rectangular grid CA**, with an unlimited supply of elements |
| States | **29** per cell |
| Size | approximately **150 000 elements** |
| Parts | a **construction unit**, a **construction arm** (which can cut, fuse and sense), a **tape unit**, and an **(infinite) tape** encoding the sequence of actions |
| Later implementation | Nobili-Pesavento, **1995**, using **32 states** |

> A **tape of cells encodes the sequence of actions** to be performed. Using a writing head (the construction arm) the machine prints out a new pattern of cells, **allowing it to make a complete copy of itself *and of the tape*.** Copying the tape as well is what makes it genuine replication rather than mere construction.

---

### ② The von Neumann neighbourhood

> In a cellular automaton, the **von Neumann neighbourhood** of a cell consists of **the cell itself plus the cells sharing an edge with it** — the four orthogonal neighbours in two dimensions. It is the standard alternative to the **Moore** neighbourhood, which also includes the diagonal (corner) neighbours.

$$n_{\text{von Neumann}} = 2d + 1 \qquad\text{vs}\qquad n_{\text{Moore}} = 3^{\,d} \qquad (r = 1)$$

```
   von Neumann, r=1              Moore, r=1

       . # .                       # # #
       # C #                       # C #
       . # .                       # # #

   n = 2d+1 = 5 cells           n = 3^d = 9 cells
   (C + the 4 edge neighbours)  (C + all 8 surrounding)
```

**Say where it is actually used in this course — that turns a name into an explanation:**

- **Langton's Loop** — $d=2$, von Neumann, written by the lecture as $n = 4r+1 = 5$, with $k=8$ states.
- **Byl's, Chou-Reggia's and Perrier's loops** — all von Neumann.
- **The forest-fire CA** — $d=2$, $r=1$, **von Neumann**, $k=3$.
- **The BTW sandpile** — a toppling cell redistributes one grain to each of its **$r=1$ von Neumann** neighbours.
- **The contrast worth naming:** Conway's Game of Life deliberately uses **Moore**, not von Neumann.

---

### OTHER DEFENSIBLE SECOND ASPECTS

If you would rather not use the neighbourhood, any of these works — **provided it does not overlap with ①**:

| Aspect | What to write |
|---|---|
| **Co-founding CA theory** | With **Stanislav Ulam (1940)** and **Arthur Burks**, von Neumann originated cellular automata as a model of computation — *"Theory and Organisation of Complicated Automata"* (**1949**). The **original idea of a 2-dimensional CA was Ulam's and von Neumann's**, not Wolfram's; Wolfram began the systematic study of the 1-dim case only in **1982**. |
| **The von Neumann architecture** | The classical stored-program computer architecture — with the irony the lecture points out explicitly: **cellular automata are called NON-von-Neumann computers**, even though von Neumann invented both. Naming that irony shows you understand the distinction rather than tripping on it. |
| **Self-replication as a concept** | The distinction between biological **reproduction** and artificial **replication**, and the question of what a machine needs in order to build a copy of itself — which he answered with the six required elements (below). |

**The six elements von Neumann specified as necessary** (`sheet-04` A1 asks for this):
several **computational elements**; a **manipulating element** (like a hand); a **cutting element** to disconnect parts; a **fusing element** to connect parts; a **sensing element** to recognise parts; and **"girders"** — rigid structural building blocks forming the chassis and the information carrier.

---

### VARIANTS

**V1.** *"Describe von Neumann's Universal Constructor."* (`sheet-04` A1)

<details><summary>Answer</summary>
Everything in ① above, **plus the six required elements** listed just above, **plus** the conceptual point that the tape is copied along with the machine. Add the homework the lecture sets alongside it: *write a program that prints out its own source code* — **a Quine** — as the software analogue of self-replication.
</details>

**V2.** *"What is the difference between reproduction and replication?"*

<details><summary>Answer</summary>
**Reproduction** is the biological capability of a living system to produce new individuals of its kind — one of the fundamental properties of biological life. **Replication** is the equivalent capability for **artificial** systems: a machine producing a copy of itself. The lecture uses "replication" precisely to avoid claiming the artificial system is alive.
</details>

**V3.** *"Name the parameters of Langton's Loop."*

<details><summary>Answer</summary>

$d=2$ rectangular grid; **von Neumann** neighbourhood with $n = 4r+1 = 5$; $k = 8$ states $(0..7)$ with **0 the silent state**; only **219** of the $k^n = 8^5 = 32\,768$ rule-table entries yield something other than the silent state; **86 cells** in the starting configuration; the loop **replicates after 151 time steps**.

Structure: a square **loop body** plus a **construction arm**, each a **channel covered by a sheath**, carrying the message string `70-70-70-70-70-70-40-40` separated by `1`s counter-clockwise, **duplicated at the T-junction**.

Milestones: step 7 the arm first extends; steps 29–34 the first corner forms; step 122 the daughter loop closes; steps 125–129 it detaches; **step 151 both loops are operating**; step 152 the next cycle starts — and thereafter **mother and daughter both breed further loops**.
</details>

**V4.** *"Name the self-replicating loops and their sizes."*

<details><summary>Answer</summary>

| Loop | Year | $k$ | Neighbourhood | Start cells $S$ | Period $p$ |
|---|---|---|---|---|---|
| **Langton's Loop** | 1984 | 8 | von Neumann | 86 | 151 |
| **Byl's Loop** | 1989 | 6 | von Neumann | 12 | 25 |
| **Chou-Reggia Loop** | 1993 | 8 | von Neumann | **5** | **15** |
| **Tempesti Loop** | 1995 | 10 | Moore | 148 | 304 |
| **Perrier Loop** | 1996 | 64 | von Neumann | 158 | 235 |

**Chou-Reggia is the smallest self-reproducing loop known**, obtained by removing all sheaths. Byl reduced Langton's by removing the inner sheath; Tempesti added construction capabilities; Perrier added a program stack and an extensible data tape.
</details>

**V5.** *"What is Chris Langton associated with?"* (the mirror-image question — plausible)

<details><summary>Answer</summary>
Four things, all named on one slide: he **organised the First Conference on Artificial Life in 1987**; he built the CA-based self-replicating structure called **Langton's Loop**; he defined the **$\lambda$ measure of complexity**; and he invented the simple Turing machine called **Langton's Ant**. He also coined the framing *"life as it could be"*.
</details>

### ⚠️ TRAPS

- **Picking two overlapping aspects.** "Universal Constructor" + "cellular automata" can be marked as one. Pair the Universal Constructor with the **neighbourhood**, the **1949 co-founding**, or the **architecture** instead.
- **Naming two things but explaining neither.** Every wording says *"and explain"*. Two sentences minimum each.
- **Giving the von Neumann architecture without the irony.** The lecture calls CAs **NON-von-Neumann computers** — mention it, or it looks like you have missed the distinction.
- **Forgetting the numbers.** 29 states, ~150 000 elements, 32-state Nobili-Pesavento implementation, $n = 2d+1$.


---

## Q9 · Wheel of Fortune ⚙️
**Recurrence: 4/4. 5 points. Asked as concept AND as derivation.**

### Asked as

- *"What is the task of the Wheel of Fortune?"* — 2023 `qn-03`
- *"What is the purpose of Wheel of Fortune in EAs?"* — 2023 `qn-02` 9
- *"Given P individuals. You want to use the wheel of fortune for selection. This takes into account every individual. **Derive a formula for $\omega_1(P)$**, the probability that the highest-rank individual is selected. State the formula in dependence of the population-size P."* — 2025 T11
- 2017 Q15 — same family

### THE ANSWER — concept version

> The Wheel of Fortune (Roulette-Wheel Selection) is a **probabilistic, rank-proportionate parent-selection** method. Its task is to choose which individuals become parents, in such a way that **better individuals are more likely to be chosen but weaker individuals still have a non-zero chance**.
>
> Each individual gets a **sector of a wheel** whose size grows as its fitness improves — equivalently, as its fitness-dependent rank $r(f(g))$ becomes smaller. The wheel is then spun once per parent needed.
>
> **Why not just take the best?** Keeping a chance for weaker individuals **maintains diversity** and prevents premature convergence onto a **super-individual**; it is the **exploration** component of the selection step. Using **rank** rather than raw fitness makes the pressure independent of the fitness scale.

```
     P = 4, rank-proportional shares

            ____
          /  4   \        best individual: 4/10
         /--------\       second:          3/10
        | 3  |  1  |      third:           2/10
         \--------/       worst:           1/10
          \  2   /        --------------------
            ----          total:          10/10
```

### ⚙️ THE DERIVATION — 2025 T11

The lecture's own numbers confirm the scheme: $P=2 \Rightarrow \tfrac23 + \tfrac13$; $P=3 \Rightarrow \tfrac36 + \tfrac26 + \tfrac16$; $P=4 \Rightarrow \tfrac4{10} + \tfrac3{10} + \tfrac2{10} + \tfrac1{10}$.

**Derive it in four lines:**

1. Rank the $P$ individuals so the best has rank $r = 1$ and the worst $r = P$. Give the individual of rank $r$ a share proportional to $P - r + 1$, so the best gets weight $P$ and the worst weight $1$.
2. The normalising total is
   $$\sum_{j=1}^{P} j \;=\; \frac{P(P+1)}{2}$$
3. Hence the selection probability of the individual with rank $r(i)$ is
   $$\omega_i \;=\; \frac{P - r(i) + 1}{\tfrac{P(P+1)}{2}} \;=\; \frac{2\,\bigl(P - r(i) + 1\bigr)}{P(P+1)}$$
4. For the **highest-ranked** individual, $r = 1$, so the numerator is $P$:
   $$\boxed{\;\omega_1(P) \;=\; \frac{P}{\tfrac{P(P+1)}{2}} \;=\; \frac{2}{P+1}\;}$$

**Define the symbols:** $P$ = population size; $r(i)$ = fitness rank of individual $i$ (1 = best); $\omega_i$ = probability that $i$ is selected in one spin.

**Sanity-check against the lecture:** $P=2 \Rightarrow \omega_1 = 2/3$ ✔; $P=3 \Rightarrow 2/4 = 1/2 = 3/6$ ✔; $P=4 \Rightarrow 2/5 = 4/10$ ✔.

### VARIANTS

**V1.** *"What is the probability that the WORST individual is selected?"*

<details><summary>Answer</summary>
$r = P$, so the numerator is $P - P + 1 = 1$:
$$\omega_P = \frac{2}{P(P+1)}$$
Check $P=4$: $2/20 = 1/10$ ✔.
</details>

**V2.** *"What is the probability that the best individual is selected at least once in $\rho$ spins (with replacement)?"*

<details><summary>Answer</summary>
Each spin independently misses it with probability $1 - \omega_1$, so
$$P(\text{at least once}) = 1 - (1-\omega_1)^{\rho} = 1 - \left(1 - \frac{2}{P+1}\right)^{\rho} = 1 - \left(\frac{P-1}{P+1}\right)^{\rho}$$
</details>

**V3.** *"For $P = 9$, give $\omega_1$, $\omega_5$ and $\omega_9$ numerically."*

<details><summary>Answer</summary>
Total $= 9\cdot10/2 = 45$.
- $\omega_1 = (9-1+1)/45 = 9/45 = 1/5 = 0.200$ — matches $2/(P+1) = 2/10$ ✔
- $\omega_5 = (9-5+1)/45 = 5/45 = 1/9 \approx 0.111$
- $\omega_9 = (9-9+1)/45 = 1/45 \approx 0.022$
Sum over all ranks $= 45/45 = 1$ ✔
</details>

**V4.** *"Name the three probabilistic parent-selection methods and give the softmax formula."*

<details><summary>Answer</summary>

The lecture lists: **Wheel of Fortune (Roulette-Wheel Selection)**, **Boltzmann / Softmax Selection**, and **Tournament Selection**.

**Softmax:**
$$\omega_p = \frac{e^{\,f(p)/\tau}}{\sum_{q} e^{\,f(q)/\tau}}$$
where $f(p)$ is the fitness of individual $p$ and $\tau > 0$ is the **temperature**. A **large $\tau$** gives a nearly **equiprobable** distribution (weak selection pressure); a small $\tau$ concentrates probability on the best. It is easy to implement and easy to control the selection pressure with.

**Tournament:** some individuals are drawn randomly from the population and compared **pairwise**; the winner of each tournament enters the pool of parents, and further stages of tournaments among winners increase the pool's fitness further.
</details>

### ⚠️ TRAPS

- **Answering only "it selects parents".** Say *why* the weak keep a chance: diversity, avoiding a super-individual, exploration.
- **Using raw fitness instead of rank.** The lecture's wheel is **rank**-proportionate — that is what makes $\omega_1 = 2/(P+1)$ independent of the actual fitness values.

---

## Q10 · Fibonacci and the golden ratio ⚙️
**Recurrence: 4/4. 5 points.**

### Asked as

- *"How does the Fibonacci-Sequence and the golden ratio relate? Derive a formula and give exemplary calculations."* — 2025 T18
- *"Proof that golden ratio is the limit of Fibonacci (bzw calculate)"* — 2023 `qn-02` 15
- *"What is the relation between the golden ratio and the Fibonacci sequence?"* — 2023 `qn-03`
- *"Fibonacci **vs logistic growth**"* — 2017 Q16 (**different variant — see V1**)

### THE ANSWER — the limit derivation

**State the sequence first:**
$$x_{i+1} = x_i + x_{i-1}, \qquad x_0 = 0,\; x_1 = 1$$
$$\{\,0,\,1,\,1,\,2,\,3,\,5,\,8,\,13,\,21,\,34,\,55,\,89,\,\ldots\,\}$$
Mentioned by **Leonardo of Pisa (Fibonacci) in 1202**, inspired by a growing rabbit population with unbounded reproduction.

**Derivation (the sheet's route — cleanest for "derive a formula"):**

Let $\beta$ be the limit of the ratio of consecutive terms:
$$\beta = \lim_{n\to\infty} \frac{F_{n+1}}{F_n}$$
Divide the recurrence $F_{n+2} = F_{n+1} + F_n$ by $F_{n+1}$:
$$\frac{F_{n+2}}{F_{n+1}} = 1 + \frac{F_n}{F_{n+1}}$$
Take the limit on both sides. The left side tends to $\beta$, and $F_n/F_{n+1} \to 1/\beta$:
$$\beta = 1 + \frac{1}{\beta} \quad\Longrightarrow\quad \beta^2 - \beta - 1 = 0$$
$$\beta = \frac{1 + \sqrt{5}}{2} \approx 1.618033988\ldots$$
(the negative root is discarded because the ratio is positive).

**The "exemplary calculations" the question demands — always include this table:**

| $n$ | $F_n$ | $F_{n+1}/F_n$ |
|---|---|---|
| 1 | 1 | $1/1 = 1.0000$ |
| 2 | 1 | $2/1 = 2.0000$ |
| 3 | 2 | $3/2 = 1.5000$ |
| 4 | 3 | $5/3 = 1.6667$ |
| 5 | 5 | $8/5 = 1.6000$ |
| 6 | 8 | $13/8 = 1.6250$ |
| 7 | 13 | $21/13 = 1.6154$ |
| 8 | 21 | $34/21 = 1.6190$ |

The ratios **oscillate around and converge to** $\varphi \approx 1.618$.

**The lecture's alternative (geometric) derivation** — worth knowing in case the question says "golden ratio" first:

> The golden ratio divides an interval so that *the whole is to the longer part as the longer is to the shorter*:
> $$\frac{1}{x} = \frac{x}{1-x} \;\Longrightarrow\; 1-x = x^2 \;\Longrightarrow\; x^2 + x - 1 = 0$$
> with solutions $\varphi \approx 1.618033988$ and $\rho = 1/\varphi \approx 0.618033988$.

**The identities — each is a free extra line:**
$$\varphi - \rho = 1, \qquad \varphi\cdot\rho = 1, \qquad \frac{1}{\varphi} = \varphi - 1, \qquad \frac{1}{\rho} = \rho + 1, \qquad \varphi^2 = 1 + \varphi, \qquad \rho^2 = 1 - \rho$$

### VARIANTS

**V1.** *"Compare the Fibonacci sequence with logistic growth."* (2017 Q16 — **this is a different question, prepare it**)

<details><summary>Answer</summary>

Give **both formulas**, then compare on **boundedness**:

| | **Fibonacci** | **Logistic growth (Verhulst, 1838)** |
|---|---|---|
| Formula | $x_{i+1} = x_i + x_{i-1}$ | $x_{i+1} = x_i + a(M - x_i)\,x_i$ |
| Growth rate | proportional to the population itself | throttled by the **remaining resources** $(M - x_i)$ |
| Behaviour | grows **geometrically** with ratio $\varphi \approx 1.618$, **unbounded** | rises almost exponentially, **inflects at $x = \tfrac12 M$**, converges to the ceiling $M$ |
| Shape | exponential curve | **sigmoid** curve |
| Realism | the lecture's point: *"unbounded reproduction is not realistic"* | models restricted resources |

Continuous version: $dP/dt = P(1-P)$, solving to $P(t) = \dfrac{1}{1+e^{-t}}$ — the **sigmoid** or **Fermi function**.

```
   x                          x
   ^        Fibonacci         ^   M ---------------  logistic
   |            /             |          _______
   |          /               |        /
   |        /                 |      /   inflection at M/2
   |     _/                   |   _/
   +----------> i             +----------> i
   unbounded                  self-limiting
```
</details>

**V2.** *"Derive the fixpoints of the logistic map $x_{i+1} = a\,x_i(1-x_i)$ and draw $x^*(a)$."*

<details><summary>Answer</summary>

At a fixpoint the value stops changing, so $x^* = a x^*(1 - x^*)$. Either $x^* = 0$, or dividing by $x^*$:
$$1 = a(1-x^*) \;\Longrightarrow\; x^* = 1 - \frac{1}{a}$$
So $x^* \in \{0,\; 1 - 1/a\}$.

**The exact thresholds to quote:** $0<a<1$ decay to 0; $1<a<3$ convergence to the fixpoint; $3 < a < 3.44949$ period 2; then 4, 8, 16 …; $3.56995 < a < 4$ onset of deterministic chaos; $a = 4$ chaos; $a > 4$ divergence.

```
  x*  ^                                   ,;'  bifurcation
  1.0 |                            ___--=='    diagram
      |                     ___----   \\\
      |          ______----             ''
      |     ----                     (period doubling)
  0.5 |   /
      |  /
  0.0 |_/______________________________________> a
      0     1        2        3   3.45  3.57  4
```
</details>

**V3.** *"Prove or disprove: the Fibonacci sequence rises faster than the exponential function."* (`sheet-05`)

<details><summary>Answer</summary>

**Disprove.** The Fibonacci sequence **is** (asymptotically) an exponential function: since $F_{n+1}/F_n \to \varphi$, we have $F_n \sim C\varphi^n$ — it grows exponentially with **base $\varphi \approx 1.618$**. So it does not rise faster than "the exponential function" in general; it rises faster than any exponential with base $< \varphi$ and slower than any with base $> \varphi$ (e.g. $2^n$ overtakes it). Exact form (Binet): $F_n = \dfrac{\varphi^n - (-1/\varphi)^n}{\sqrt5}$.
</details>

**V4.** *"What is the golden angle and where does it appear?"*

<details><summary>Answer</summary>

**137.51°** — the angle obtained by dividing a full turn in the golden ratio. It appears in **phyllotaxis**: each new leaf grows where the inhibitor left by existing leaves is weakest, which drives the angle between successive leaves toward 137.51°. The visible spiral counts in pinecones and sunflowers are **consecutive Fibonacci numbers**.
</details>

### ⚠️ TRAPS

- **Skipping the numeric table.** Two of the four wordings explicitly say "give exemplary calculations" / "bzw calculate".
- **Answering the limit question when 2017 Q16 asked for the logistic comparison.** Read which one you got.

---
---

# ASKED ON THREE OF THE FOUR PAPERS

**Q11 alone has been a 10-pointer every time it appeared.** Together ≈20 points.

---

## Q11 · The Didabot experiment 🔒
**Recurrence: 3/4 — and it was worth 10 points on every one of them.** Missing from 2025 only.

### Asked as

- *"Explain the Didabot experiment. What was the purpose of the Didabots? What were the results? What happens when you use more than one Didabot?"* — 2023 `qn-02` 2, **10 pt** (the protocol adds: *"we were supposed to write down everything we know about the experiment"*)
- *"Explain the Didabot experiments and the observed differences between a single and multiple bots."* — 2023 `qn-03`, **10 pt**
- 2017 Q2, **10 pt**

**Treat this as seriously as Game of Life.** It has never appeared for fewer than 10 points.

### THE BLOCK TO WRITE — six parts

**① What a Didabot is**

> Didabots are a development of the **AI Lab of the University of Zürich** (Switzerland) for **teaching students** — the name is short for **Didactic Robots** (Maris & Schaad, 1995). The goal was *"to create a group of general purpose robots that are small and flexible and can easily be programmed from a host computer"*.
>
> **Structure:** a chassis with **two motors (differential steering)** and **6 wheels**, a µProcessor board, **six infrared (IR) proximity sensors**, six ambient light sensors, nine touch sensors, a beeper, a light bulb, and two wheel encoders.
>
> **In the Didabot experiment only two of the IR proximity sensors are used — the two pointing diagonally to the front.**

**② The purpose of the experiment**

> To investigate **reactive obstacle avoidance** capabilities in an arena containing many rectangular obstacles (boxes). The robot is controlled in a **Braitenberg type 3b** manner:
> *"if there is a sensory stimulation on the left, turn (a bit) to the right; if there is a sensory stimulation on the right, turn (a bit) to the left."*
>
> **There is no clustering rule, no tidying rule, and no map. The only programmed behaviour is obstacle avoidance.** This is the single most important sentence in the whole answer.

**③ The unexpected result**

> After a while the box distribution has changed in a very specific way: **the boxes build clusters — heaps of several boxes close together — plus some boxes pushed against the boundary of the arena.**
> (Maris, M. & te Boekhorst, R., 1996, *"Exploiting Physical Constraints: Heap formation through behavioral error in a group of robots"*, IROS '96, Osaka.)

```
   ARENA BEFORE                        ARENA AFTER

   +---------------------+            +---------------------+
   |   []      []    []  |            |[][]           []    |
   |        []       []  |            |[]            [][][] |
   |  []        []       |    ==>     |                     |
   |     []  []      []  |            |      [][][]         |
   |  []       []        |            |[]     [][]      [][]|
   +---------------------+            +---------------------+
   boxes scattered at random          heaps in the interior AND
                                      boxes lined up at the walls
```

**④ Why it happens — the four essential properties**

The lecture lists exactly four; name all four:

1. **The boxes can be pushed around** by the robot.
2. **The boxes are smaller than the distance between the two sensors used.**
3. **The front of the robot is not flat, but curved.**
4. **Braitenberg type 3b obstacle-avoidance behaviour.**

**The mechanism:**

> When a box is *somewhere in reach* of the sensors, the type 3b control produces normal obstacle avoidance. But when the box is **directly in front**, it sits **between the two sensors** and is therefore **"invisible" to the robot**. It then "sits on the nose" of the Didabot and is **pushed around** by the moving robot until it is eventually released.

```
   BOX SEEN (off to one side)          BOX NOT SEEN (dead ahead)

        [box]                                  [box]
          \                                      |
        \  \  /                                \ | /
         (SL SR)                                (SL SR)
          \___/                                  \___/
      sensor triggered ->              box falls in the BLIND SPOT
      3b turns away                    between the sensors ->
                                       robot pushes it along
```

**⑤ The two release mechanisms (single Didabot)**

| Mechanism | How it works | Where the box lands |
|---|---|---|
| **Spontaneous release** | Because the nose is **curved**, the **natural jiggling** of the robot has a probability of moving the box aside until it comes into the reach of one sensor. The 3b behaviour then makes the robot turn. | At an **arbitrary** position. |
| **Induced release** | The robot encounters **an obstacle or another box** with its sensors; the 3b behaviour makes it turn, and the box on the nose is released. | **Close to an obstacle or another box — and this is what forms the heaps.** |

> So heaps grow **autocatalytically**: the more boxes are already in one place, the more likely a passing Didabot is to trigger an induced release there and add another. Clusters form **everywhere in the inner part of the arena, and explicitly at the boundaries** (the wall itself triggers induced release).

**What the heap size and count depend on** (a free extra sentence): the **density of objects**, the **probability of spontaneous release** (and hence **the shape of the robot**), the **characteristics of the sensors**, and the **details of the type 3b implementation**.

**⑥ Emergence — the conclusion**

> The behaviour has been described as *"cleaning up"*, *"making free space"*, or *"trying to build clusters"* — **but in fact the programmed micro-behaviour is just reactive obstacle avoidance following Braitenberg's principle of antagonistic inhibition.** The tidying is **emergent**: a complex global pattern arising from a multiplicity of relatively simple local interactions, with **no representation of the goal anywhere in the robot**.

### ⑦ ONE vs MANY DIDABOTS — the part the question always asks

> With multiple identical Didabots in the arena, **each one does exactly the same thing**: type 3b obstacle avoidance, box pushing, heap building. The two existing release principles — spontaneous and induced — remain active. **But a third mechanism becomes active:**
>
> **Induced release type 2:** **two Didabots approaching each other** perform an avoiding movement (type 3b behaviour) **and thus release any boxes they are carrying.**

```
    SINGLE DIDABOT                     MULTIPLE DIDABOTS

    releases: spontaneous              releases: spontaneous
              induced (obstacle/box)             induced (obstacle/box)
                                                 induced TYPE 2 (robot-robot)
         [box]
           \                             (=O=)  ->     <-  (=O=)
          (=O=)  ->                        \             /
                                          [box]       [box]
                                        both turn away, both drop
```

> ⚠️ **Say only what the slides say.** The lecture's stated difference for multiple robots is **the third release mechanism**, and that several Didabots are building clusters of boxes. It is reasonable to add that clustering therefore proceeds **faster** with more robots, and that robots also **interfere with each other's heaps** — but flag that as your own inference, since the deck does not state it. Do not invent numbers.

### VARIANTS

**V1.** *"Why do the boxes end up at the walls of the arena?"*

<details><summary>Answer</summary>

The **wall is an obstacle**. When a Didabot carrying a box on its nose approaches the wall, its sensors detect it and the 3b behaviour makes it turn — an **induced release** — depositing the box at the boundary. Since every robot travelling outward eventually meets the wall, boxes accumulate there as well as in interior heaps.
</details>

**V2.** *"What would happen if the boxes were LARGER than the distance between the two sensors?"*

<details><summary>Answer</summary>

**No heaps would form.** A box larger than the sensor separation can never fall into the blind spot between the two sensors, so it is **always detected**, the 3b behaviour always turns the robot away, and **no box is ever pushed**. The robot would perform pure obstacle avoidance and the box distribution would stay essentially unchanged. This shows the effect depends on a **physical/morphological accident**, not on the control program — which is exactly the paper's title, *"Exploiting Physical Constraints"*.
</details>

**V3.** *"What would happen if the front of the robot were flat instead of curved?"*

<details><summary>Answer</summary>

**Spontaneous release would become much rarer.** The curved nose is what lets the natural jiggling of the robot slide the box sideways into a sensor's field of view. With a flat front the box would stay centred in the blind spot and be pushed much further, so releases would be almost entirely **induced** — near obstacles and other boxes. The likely consequence is **fewer, larger heaps** and less scatter. Note explicitly that the lecture lists the robot's **shape** as one of the factors determining heap size and number.
</details>

**V4.** *"Define emergence and give the Didabots as an example."*

<details><summary>Answer</summary>

**Emergence** is *"the way complex systems and patterns arise out of a multiplicity of relatively simple interactions"* — it is central to the theories of integrative levels and of complex systems.

**Didabots as the example:** the global pattern is *boxes gathered into heaps*, which looks purposeful and has been called "cleaning up". The local rule is only *turn away from whatever a sensor detects*. Nothing in the robot represents a heap, a goal, or the arena. The pattern arises from the interaction of the control rule with the **physical morphology** (blind spot, curved nose) and the environment. Other examples from the course: **swarm intelligence**, ant colonies, and Conway's Game of Life gliders.
</details>

### ⚠️ TRAPS

- **Forgetting to say there is no clustering rule.** That is the entire point of the experiment.
- **Skipping the "more than one Didabot" sub-question.** It is named explicitly in two of the three wordings and it is worth its own marks — the answer is **induced release type 2**.
- **Only giving one release mechanism.** There are **two** for a single robot and **three** for several.
- **Not naming the four essential properties.** They are a numbered list on the slide and thus a numbered list of marks.

---

## Q12 · EA fitness diagrams 🔒
**Recurrence: 3/4. 5 points. TWO DIFFERENT DIAGRAMS — do not confuse them.**

### Asked as

- *"Draw the **distribution of fitness** before and after external selection with (µ+λ) and elitism."* — 2023 `qn-02` 13
- *"Given an EA with rank-based, elitism, (λ+µ) selection process. Draw diagrams depicting the **fitness of the population sorted by fitness** before and after the selection process."* — 2025 T6
- 2017 Q6 — the **performance graph** variant

**Read which one you were given.** "Sorted by fitness, before and after selection" = **Diagram A**. "Fitness over generations / over time" = **Diagram B**. They look nothing alike.

### DIAGRAM A — population sorted by fitness, before vs after external selection

**Axes:** $x$ = individual index, **sorted by fitness** (best on the left); $y$ = fitness $f$. Label both.

```
      BEFORE external selection                AFTER (mu + lambda), elitism, rank-based

  f                                        f
  ^                                        ^
  |  *                                     |  *
  |    *                                   |    *
  |      *                                 |      *
  |        *                               |        *
  |          *                             |          *
  |            *                           |          |
  |              *                         |          |  <- sharp cut
  |                *                       |          |
  |                  *                     |          |
  +---------------------------> index      +----------|----------------> index
   1                        P               1        mu                P
       all P individuals                     the worst lambda = P - mu
                                             are DISCARDED; the best mu
                                             survive UNCHANGED
```

**Write these four sentences with it:**

1. **Before:** the population sorted by fitness gives a **monotonically decreasing curve** from the best individual down to the worst.
2. **After:** external selection **"keeps the Best and discards the Losers"** — the worst $\lambda = P - \mu$ individuals are removed, so the curve is **truncated** at $\mu$ and **ends in a sharp cut**.
3. **The surviving part is identical to the left part of the "before" curve** — because the selection is **deterministic and rank-based with elitism**, no surviving individual has its fitness changed, and the best individual is guaranteed to survive.
4. **The mean fitness of the population rises**, but the **maximum is unchanged** — selection alone never creates a better individual, it only removes worse ones.

**If asked for the following steps too** (`sheet-08` asks for inheritance and mutation as well):

- **After inheritance/recombination:** the $\lambda$ empty slots are refilled with offspring whose fitness lies **mostly between the parent values**, so the curve is **restored to length $P$** but the new tail sits **below** the surviving parents.
- **After mutation:** the values are **spread out** again — some offspring get better, some worse — so the curve becomes **smoother and noisier**, and occasionally a mutant **exceeds** the previous best.

### DIAGRAM B — the performance graph

> The **performance graph** shows the development of the fitness $f^*(t)$ of the **best individual in each generation** with respect to time. It is **"the most important tool to monitor the optimization process of a working evolutionary algorithm."**

**Axes:** $x$ = time / generation $t$; $y$ = $f^*(t)$, the fitness of the best individual.

```
  f*(t)
    ^
    |                        ________________  <- slow increase (convergence)
    |                    ___/
    |                 __/
    |              __/
    |          ___/                             <- strong increase
    |      ___/
    |   __/
    |  /
    | /   <- initial situation
    +-------------------------------------> t

    Monotonically non-decreasing: it can NEVER go down.
```

**The three phases the lecture names:** *initial situation* → *strong increase* → *slow increase*.

**The rule you must state — this is what the question is really testing:**

> - For a **deterministic, rank-dependent elitism strategy $(\mu + \lambda)$, the performance graph will increase MONOTONICALLY.**
> - For a **probabilistic, non-elitism strategy, the performance graph can decrease**, but should show an increase in the long run.

**Why it is monotone** — say it explicitly, it is the marked reasoning:
> Because the $+$ strategy keeps the parents in the next generation and elitism guarantees the best individual survives, the best fitness at $t+1$ is at least the best fitness at $t$. It can therefore never decrease.

```
   (mu + lambda) with elitism          (mu , lambda) or non-elitism

   f*  ^      _____                    f*  ^        /\    ____
       |   __/                             |    /\_/  \__/
       |  /                                |   /   can drop when the
       | /   never decreases               |  /    parents are discarded
       +-----------------> t               +-----------------> t
```

### THE $(\mu+\lambda)$ vs $(\mu,\lambda)$ BLOCK

Straight from the slides:

- **$+$ (plus) strategy:** the next generation consists of **$\mu$ parents + $\lambda$ offspring — the parents survive.**
- **$,$ (comma) strategy:** the next generation consists of **only the $\lambda$ offspring — the parents are discarded.**

| | $(\mu + \lambda)$ | $(\mu , \lambda)$ |
|---|---|---|
| Parents | survive | discarded |
| Best fitness over time | **monotonically non-decreasing** | can decrease |
| Re-evaluations | saved (parents keep their fitness) | every individual is new |
| Risk | **stagnation** in a local optimum | loses good solutions |
| Best used when | fitness is static and reliable | **fitness drifts over time**, or escaping local optima matters |

**Named special cases from the slides:**
- **$(1+1)$** — one parent, one child, inheritance by **copying only** (no recombination), only mutation, rank-based deterministic external selection.
- **$(1+\lambda)$** — one parent, $\lambda$ offspring.
- **$(\mu+\lambda)$** — $\mu$ parents, $\lambda$ offspring, recombination + mutation + external selection, parents survive.
- **$(\mu,\lambda)$** — the same but parents are discarded.

### VARIANTS

**V1.** *"Draw the performance graph for a probabilistic, non-elitism strategy and explain the difference."*

<details><summary>Answer</summary>

```
  f*(t)
    ^          /\      ___/\____
    |     /\__/  \    /
    |    /        \__/
    |   /   <- can DECREASE, because the best individual
    |  /       is not guaranteed to survive the selection
    | /
    +---------------------------> t
```
Because selection is probabilistic and there is no elitism, **the current best individual can fail to be selected and be lost**, so $f^*(t)$ can drop. Over the long run it should still increase. The trade-off: the ability to lose the best is also the ability to **escape a local optimum**.
</details>

**V2.** *"Sketch the fitness distribution after MUTATION."*

<details><summary>Answer</summary>

```
   after selection + inheritance         after mutation

  f ^  *                               f ^  *
    |    *                               |   * *
    |      * *                           |     *  *
    |         * *                        |   *      * *
    |            * * *                   |        *   *  *
    +-----------------> index            +-----------------> index
    smooth, offspring cluster            SPREAD OUT and noisier;
    between parent values                a few mutants may exceed
                                         the previous best
```
Mutation is the **exploration** operator: it perturbs individuals randomly, widening the fitness spread. Most mutants are worse, a few are better — and those few are the only mechanism by which the population can exceed its current maximum.
</details>

**V3.** *"An EA has $P = 100$, $\mu = 20$. How many offspring are generated per generation, and what fraction of the population is discarded?"*

<details><summary>Answer</summary>

Keeping the population constant at $P$: $\lambda = P - \mu = 100 - 20 = \mathbf{80}$ offspring are generated from the 20 surviving parents, and $\lambda/P = 80/100 = \mathbf{80\,\%}$ of the population is discarded each generation. The **selection pressure** is $\mu/P = 20\%$ — a low $\mu/P$ means high pressure and fast but possibly premature convergence.
</details>

**V4.** *"Name the termination criteria for an EA."* (six on the slide)

<details><summary>Answer</summary>

By **performance of the best individual**; by **performance of a sub-population**; by **stagnation / development of the fitness improvement**; by **time**; by **number of generations**; by **choice of a human operator**.
</details>

**V5.** *"What are the two principles for initializing the first population?"*

<details><summary>Answer</summary>

1. **Start as good as possible** — use all a priori knowledge available, and try to avoid illegal genomes.
2. **Enough richness, enough diversity** — sample as much of the fitness landscape as possible and try to cover the complete search space.

These are in tension: seeding with known-good solutions reduces diversity, which risks premature convergence.
</details>

### ⚠️ TRAPS

- **Drawing the wrong diagram.** "Sorted by fitness, before/after selection" ≠ "fitness over generations". Read the axis words in the question.
- **Not labelling the axes.** An unlabelled sketch scores nothing.
- **Forgetting to say WHY the elitist $(\mu+\lambda)$ graph is monotone.** That sentence is the question.
- **Drawing the "after selection" curve as a shrunken copy.** It is the **same curve, truncated** — the survivors' fitness values do not change.

---

## Q13 · EA mutation probability ⚙️
**Recurrence: 3/4. 5 points. THREE different formulas — the question decides which.**

### Asked as — read these three side by side, they are NOT the same question

- *"Calculate the probability that **at least one element of a sequence / genome** is affected by a mutation."* — 2023 `qn-03` → **Formula ①**
- *"A parent $X(i)$ with a genome of $L$ bit has created $N$ offspring identical to the parent. The mutation operator modifies each of these $N$ offspring by flipping each of the $N \cdot L$ bits with a probability of $p$. Derive a formula for the probability $Q$ that **at least one of the $N$ new individuals is different to the parent**."* — 2023 `qn-02` 4 → **Formula ②**
- *"…parent selection selects only [the best] individual and creates exact copies to create $N$ new individuals. Each bit is mutated with probability $p = \frac{1}{L^2}$. Calculate and derive a formula for the probability $Q$ that in the new population **no individual is identical to the parent**."* — 2025 T13 → **Formula ③**

### THE THREE FORMULAS

**Start from the one building block and derive everything from it.** State it first:

> A single bit is **not** flipped with probability $(1-p)$. Bits are mutated **independently**, so a block of $m$ bits survives completely unchanged with probability $(1-p)^m$.
>
> **Symbols:** $p$ = probability that one bit is flipped; $L$ = number of bits in one genome; $N$ = number of offspring; $Q$ = the probability asked for.

**① At least one bit of ONE genome is affected** ($m = L$)

$$Q = 1 - (1-p)^{L}$$

> The complement of "at least one bit flips" is "no bit flips", which has probability $(1-p)^L$.

**② At least one of $N$ offspring differs from the parent** ($m = N\cdot L$)

$$Q = 1 - (1-p)^{N L}$$

> "At least one offspring differs" is the complement of "**every** offspring is identical", which requires **all $N \cdot L$ bits** to survive unchanged — probability $(1-p)^{NL}$.

**③ NO offspring is identical to the parent**

$$Q = \Bigl(1 - (1-p)^{L}\Bigr)^{N}$$

> One offspring is identical to the parent with probability $(1-p)^L$, so it **differs** with probability $1 - (1-p)^L$. The $N$ offspring mutate independently, so **all $N$ differ** with that probability raised to the $N$-th power.

**⚠️ ② and ③ are different and both have been asked.** ② is *"at least one differs"*; ③ is *"none is identical"* = *"all differ"*. Read the sentence twice before you write.

```
        "at least one differs"          "no one is identical"
        = NOT(all identical)            = ALL differ
        = 1 - (1-p)^(N*L)               = (1 - (1-p)^L)^N
```

### WORKED — 2025 T13 with $p = 1/L^2$

Substitute into ③:

$$Q = \left(1 - \left(1 - \frac{1}{L^{2}}\right)^{L}\right)^{N}$$

**Then simplify, which is what "calculate" asks for.** For large $L$, expand to first order:

$$\left(1-\frac{1}{L^{2}}\right)^{L} \approx 1 - L\cdot\frac{1}{L^{2}} = 1 - \frac{1}{L}$$

so

$$1 - \left(1-\frac{1}{L^{2}}\right)^{L} \approx \frac{1}{L} \qquad\Longrightarrow\qquad \boxed{\;Q \approx \left(\frac{1}{L}\right)^{N} = L^{-N}\;}$$

> **Interpret the result in one sentence — this earns the last mark:** with $p = 1/L^2$ the mutation rate is so low that each offspring has only about a $1/L$ chance of differing from its parent at all, so the probability that *none* of the $N$ offspring is a copy falls off as $L^{-N}$ — i.e. for any realistic $L$ and $N$, the new population is **almost certain to contain an exact copy of the parent**. That is a very weak mutation operator.

### SANITY CHECKS — do these in the margin, they catch sign errors

| Case | ① $1-(1-p)^L$ | ③ $(1-(1-p)^L)^N$ | Meaning |
|---|---|---|---|
| $p = 0$ | $0$ | $0$ | No mutation ⇒ nothing ever differs. ✔ |
| $p = 1$ | $1$ | $1$ | Every bit flips ⇒ every offspring is the exact complement, so all differ. ✔ (But there is **no diversity** — all offspring are identical to each other.) |
| $p = 0.5$ | $1 - 2^{-L}$ | $\approx 1$ | Each bit is randomised ⇒ pure random restart, no inheritance. |
| $p$ small | $\approx pL$ | $\approx (pL)^N$ | The useful regime: local search around the parent. |

### VARIANTS

**V1.** *"$L = 10$, $N = 4$, $p = 0.01$. Give ①, ② and ③ numerically."*

<details><summary>Answer</summary>

$(1-p) = 0.99$.
- $(0.99)^{10} = 0.9044$
- ① $Q = 1 - 0.9044 = \mathbf{0.0956}$ — one genome is affected ~9.6 % of the time.
- ② $Q = 1 - (0.99)^{40} = 1 - 0.6690 = \mathbf{0.3310}$ — at least one of the 4 offspring differs.
- ③ $Q = (1 - 0.9044)^{4} = (0.0956)^4 = \mathbf{8.35 \times 10^{-5}}$ — all four differ; very unlikely.

Note ② $\gg$ ③, as it must be: "at least one" is far easier than "all".
</details>

**V2.** *"Derive the probability that EXACTLY one bit of a genome of length $L$ is flipped."*

<details><summary>Answer</summary>

Choose which bit flips ($L$ ways), it flips with probability $p$, and the other $L-1$ bits must survive:

$$P(\text{exactly one}) = \binom{L}{1} p (1-p)^{L-1} = L\,p\,(1-p)^{L-1}$$

More generally, the number of flipped bits is **binomially distributed**:
$$P(k \text{ flips}) = \binom{L}{k} p^{k} (1-p)^{L-k}$$
</details>

**V3.** *"What value of $p$ makes exactly one bit flip per genome on average?"*

<details><summary>Answer</summary>

The expected number of flipped bits is $E = L\,p$. Setting $E = 1$ gives
$$p = \frac{1}{L}$$
This is the standard textbook default mutation rate, and it is worth contrasting with the exam's $p = 1/L^2$, which is a factor $L$ **weaker** — on average only $1/L$ bits flip per genome, i.e. most offspring are exact copies.
</details>

**V4.** *"How many distinct offspring can one-point crossover produce from two parents with genomes of $L$ genes?"*

<details><summary>Answer</summary>

The crossover point can sit in any of the $L-1$ gaps between genes, and each cut yields **two** complementary children, so

$$\#\text{offspring} = 2(L-1)$$

(The cuts before the first gene and after the last gene are excluded, since they just reproduce the parents.)
</details>

**V5.** *"What is a super-individual and how do you avoid one?"*

<details><summary>Answer</summary>

A **super-individual** is one individual so much fitter than the rest that, under fitness-proportional selection, it takes over almost the whole population within a few generations. The result is a **collapse of diversity** and premature convergence to whatever local optimum that individual sits in.

**Avoidance:** use **rank-based** selection instead of fitness-proportional (the shares then depend only on ordering, not on the size of the fitness gap); use **softmax with a high temperature $\tau$** to flatten the distribution; or **cap the number of offspring** any single parent may produce.
</details>

### ⚠️ TRAPS

- **The big one: ② vs ③.** *"At least one differs"* and *"no individual is identical"* are different formulas. Underline the phrase in the question before you start.
- **Forgetting to define $p$, $L$, $N$ and $Q$.** The 2017 paper explicitly demands "which variable means what".
- **Not substituting $p = 1/L^2$** when the question gives it. The question says "calculate", not just "derive".
- **Working forwards instead of via the complement.** Always compute "nothing happens" first, then subtract from 1.

---
---

# ASKED ON TWO OF THE FOUR PAPERS

---

## Q14 · Counting the possible rules of a CA ⚙️
**Asked on 2 of 4. 5 points. The numbers change every time — this is a pure recipe.**

### Asked as

- *"Calculate the number of possible rules and derive a formula for a CA with **$d=3$, $k=2$, $r=1$ Moore**."* — 2025 T9
- *"[Rule count for **$d=1$, $r=3$, $k=4$**]"* — 2017 Q8
- *"How long would it take to print all $Z$ possible rules for a 1-dim CA with **$k=4$ and $r=1$** at 100 rules per second? Set up a formula $Z = Z(r,k)$."* — `sheet-02` A1
- *"Write formulas for the number $Z$ of possible rules … a) all, b) peripheral $Z_p$, c) totalistic $Z_t$, d) with a silent state $Z_s$."* — `sheet-02` A5

### THE RECIPE — three lines, always the same three lines

**Keep $n$, $L$ and $Z$ strictly apart. Confusing $L$ with $Z$ is the standard way to lose this question.**

$$n = \text{size of the neighbourhood} \qquad L = k^{\,n} \qquad Z = k^{\,L}$$

- **$k$** = number of states one cell may take.
- **$n$** = number of cells consulted by the rule (**including the cell itself**).
- **$L$** = number of **lines in the rule table** — one per possible neighbourhood configuration. Each of the $n$ cells independently takes one of $k$ states ⇒ $k^n$ combinations.
- **$Z$** = number of **possible rules**. Each of the $L$ lines is filled independently with one of $k$ outputs ⇒ $k^L$.

**Step 1 — get $n$ from the geometry.** This is the only part that changes:

| Neighbourhood | $n$ | Example |
|---|---|---|
| $d=1$, radius $r$ | $n = 2r+1$ | $r=1 \Rightarrow 3$; $r=3 \Rightarrow 7$ |
| $d$-dim **Moore**, $r=1$ | $n = 3^{\,d}$ | $d=2 \Rightarrow 9$; $d=3 \Rightarrow 27$ |
| $d$-dim **von Neumann**, $r=1$ | $n = 2d+1$ | $d=2 \Rightarrow 5$; $d=3 \Rightarrow 7$ |
| $d$-dim Moore, radius $r$ | $n = (2r+1)^{d}$ | $d=2, r=2 \Rightarrow 25$ |

**Step 2 — plug into $L = k^n$. Step 3 — plug into $Z = k^L$.** Then state the magnitude in words.

### WORKED — 2017 Q8: $d=1$, $r=3$, $k=4$

$$n = 2r+1 = 2(3)+1 = 7$$
$$L = k^{n} = 4^{7} = 16\,384$$
$$Z = k^{L} = 4^{16\,384}$$

> In words: the neighbourhood consults 7 cells, the rule table has 16 384 lines, and there are $4^{16384}$ possible rules.

### WORKED — 2025 T9: $d=3$, $k=2$, $r=1$, Moore

$$n = 3^{\,d} = 3^{3} = 27$$
$$L = k^{n} = 2^{27} = 134\,217\,728$$
$$Z = k^{L} = 2^{\,2^{27}} = 2^{134\,217\,728}$$

> **Draw the neighbourhood** — a $3\times3\times3$ cube of cells, 27 including the centre. And say the magnitude: $Z$ is a power tower with roughly $4\times10^{7}$ decimal digits.

```
    3 x 3 x 3 Moore neighbourhood in d=3

         # # #          # # #          # # #
         # # #          # C #          # # #
         # # #          # # #          # # #
       back layer     middle layer   front layer
                                          n = 27
```

### THE FOUR RESTRICTED COUNTS

| | Formula | Derivation |
|---|---|---|
| **all rules** | $Z = k^{\,k^{2r+1}}$ | $L = k^{2r+1}$ lines, each independently one of $k$ outputs. |
| **peripheral** | $Z_p = k^{\,k^{2r}}$ | The centre is ignored, so only $2r$ cells matter ⇒ $k^{2r}$ lines. |
| **totalistic** | $Z_t = k^{\,n(k-1)+1}$ | Output depends only on the **sum**, which runs $0 \ldots n(k-1)$ ⇒ $n(k-1)+1$ lines. |
| **silent state** | $Z_s = k^{\,L-1}$ | One line (all-zero neighbourhood) is **forced** to 0, leaving $L-1$ free. |

**Sanity check with $d=1, r=1, k=2$:** $Z = 256$, $Z_p = 2^4 = 16$, $Z_t = 2^{3(1)+1} = 16$, $Z_s = 2^7 = 128$ — exactly half the rules have a silent state, as expected.

### VARIANTS

**V1.** *"$d=2$, $k=3$, $r=1$ Moore. How many rules?"*

<details><summary>Answer</summary>
$n = 3^2 = 9$; $L = 3^9 = 19\,683$; $Z = 3^{19\,683}$.
</details>

**V2.** *"$d=2$, $k=2$, $r=1$ von Neumann. How many rules, and how many are legal?"*

<details><summary>Answer</summary>
$n = 2d+1 = 5$; $L = 2^5 = 32$; $Z = 2^{32} \approx 4.3\times10^9$ ("4 Giga").

**Legal = symmetric AND silent.** The silent state fixes 1 of the 32 lines. Symmetry pairs up the neighbourhoods that are mirror images of each other; only the un-paired (self-mirrored) ones stay free. Give the method and note that the exact count depends on how many of the 32 configurations are self-symmetric — the marks are for the reasoning, not a memorized number.
</details>

**V3.** *`sheet-02` A1 — printing time for $k=4$, $r=1$ at 100 rules/second.*

<details><summary>Answer</summary>

$$Z(r,k) = k^{\,k^{2r+1}}, \qquad Z(1,4) = 4^{\,4^{3}} = 4^{64} = 2^{128} \approx 3.40\times10^{38}$$
$$T = \frac{Z}{100\ \mathrm{s^{-1}}} \approx 3.40\times10^{36}\ \mathrm{s} \approx 1.08\times10^{29}\ \text{years}$$

Roughly $10^{19}$ times the age of the universe. **The expected conclusion is the moral, not the number:** exhaustive search over CA rules is impossible in principle — which is exactly why Wolfram classified *behaviours* instead of enumerating rules.
</details>

### ⚠️ TRAPS

- **Confusing $L$ and $Z$.** Write all three lines, labelled.
- **Forgetting the centre cell** when counting $n$. Moore in $d=3$ is 27, not 26.
- **Not giving the derivation.** Both papers say "derive a formula" *and* asked for the value.

---

## Q15 · "A totalistic rule with a silent state is legal" — prove or disprove 🔒
**Asked on 2 of 4. 5 points. The answer is a three-step proof.**

### Asked as

- *"Is the following statement true or not? 'A totalistic rule with silent state is legal.'"* — 2025 T17
- *"Is a totalistic rule with a silent state always legal? (Proof)"* — 2023 `qn-02` 17
- *"Prove or disprove: **All totalistic rules are legal**, because they are symmetric and have a silent state."* — `sheet-02` A2 ← **different claim, different answer**

### THE DEFINITIONS — write these first, the proof is nothing without them

- **Silent state:** the rule has a silent state if the neighbourhood with **all cells set to 0** maps onto **0**.
- **Symmetric:** a neighbourhood and its **mirror image** yield the same next state.
- **Legal:** the rule is **symmetric AND has a silent state**. Both, not either.
- **Totalistic:** the next state depends **only on the sum** of the set cells in the neighbourhood.

### THE PROOF — exam version: **TRUE**

**Step 1 — what must be shown.**
> By definition a rule is legal $\iff$ it is symmetric **and** has a silent state. The silent state is given by assumption. So it remains only to show **totalistic $\Rightarrow$ symmetric**.

**Step 2 — totalistic $\Rightarrow$ symmetric.**
> A totalistic rule's output depends only on
> $$\mathrm{SUM}(t) = a_{i-r}(t) + \ldots + a_i(t) + \ldots + a_{i+r}(t)$$
> **Addition is commutative**, so any reordering of the neighbourhood cells — in particular **mirroring** — leaves the sum unchanged:
> $$\mathrm{SUM}(a_{i-r},\ldots,a_{i+r}) = \mathrm{SUM}(a_{i+r},\ldots,a_{i-r})$$
> Equal sums must give equal outputs, so a neighbourhood and its mirror image yield the same next state. That is exactly the definition of **symmetric**.

**Step 3 — conclude.**
> The rule is symmetric (Step 2) and has a silent state (assumption), therefore it is **legal**. $\blacksquare$

### ⚠️ THE SHEET VERSION IS A DIFFERENT CLAIM — answer: **DISPROVED**

*"All totalistic rules are legal"* drops the "with a silent state" condition.

- The **first half is true**: all totalistic rules **are** symmetric, by Step 2 above.
- The **second half is false**: nothing forces a totalistic rule to map $\mathrm{SUM}=0$ onto state 0.

**Counterexample** ($d=1, r=1, k=2$):

```
   SUM(t)     3   2   1   0
   a_i(t+1)   0   0   0   I     <- SUM = 0 maps to I
```

This rule is totalistic (it is defined purely on the sum) but has **no silent state**, so it is **not legal**. Hence "all totalistic rules are legal" is **disproved**.

> **In the exam: read which claim you were given, and say which one you are answering.** One sentence — *"The statement as given includes the silent state as a hypothesis, so I prove it true; without that hypothesis it would be false, by [counterexample]."* — covers both and is worth the extra mark.

### VARIANTS

**V1.** *"Is every legal rule totalistic?"*

<details><summary>Answer</summary>

**No.** Legal = symmetric + silent; totalistic is strictly **stronger** than symmetric. **Counterexample: rule 204**, the identity rule (output = centre cell):
```
 111  110  101  100  011  010  001  000
  I    I    0    0    I    I    0    0
```
It is symmetric ✔ and has a silent state ✔, so it is **legal** — but it is **not totalistic**, since $\mathrm{SUM}=2$ gives $110\to I$, $101\to 0$, $011\to I$, which are not all equal.

**The implication runs one way only: totalistic $\Rightarrow$ symmetric, but symmetric $\not\Rightarrow$ totalistic.**
</details>

**V2.** *"Is a peripheral rule with a silent state always legal?"*

<details><summary>Answer</summary>

**No.** Peripheral means the centre cell is ignored; it says nothing about mirror symmetry. **Counterexample** ($d=1,r=1,k=2$): a peripheral rule that maps left-neighbour-only, e.g. output $=$ the **left** neighbour's state. Then $100 \to I$ but its mirror $001 \to 0$, so it is **not symmetric** and therefore **not legal**, even though $000 \to 0$ gives it a silent state.
</details>

**V3.** *"Is Conway's Game of Life rule legal? Justify."*

<details><summary>Answer</summary>

**Yes.**
- **Silent state ✔** — an all-dead neighbourhood with a dead centre maps to dead, so an empty grid stays empty.
- **Symmetric ✔** — the rule depends only on *how many* neighbours are alive, never on *which* ones, so any mirroring or rotation gives the same result.
- Legal = symmetric + silent ⇒ **legal**. (The lecture states this outright.)

But note: **not peripheral** (the centre's own state matters at exactly 2 neighbours) and **not totalistic** — it is **outer-totalistic**.
</details>

### ⚠️ TRAPS

- **Asserting the answer without unfolding the definitions.** "Proof" means Steps 1–3.
- **Missing that the sheet's claim differs.** Underline whether "with a silent state" is present.
- **Forgetting commutativity is the actual reason.** That one word is the proof.

---

## Q16 · Wolfram's classes — III vs IV 🔒
**Asked on 2 of 4. 5 points. Always as a compare-and-contrast.**

### Asked as

- *"Explain what Wolfram's class 3 and class 4 are, how they differ and what they have in common."* — 2025 T15
- *"Explain the difference and similarities between Type 3 and 4 classes of CA."* — 2023 `qn-02` 12
- *"Name the 4 behaviours of CAs (Wolfram's classification) and describe their characteristics in your own words (max two sentences each)."* — `sheet-02` A6

### HOW THE CLASSIFICATION IS MADE — one free mark, say it first

> To determine the class, the CA is **initialised with a random pattern and iterated for a long time**; this is **repeated for several random initialisations**, and the typical resulting dynamics is then classified. The classes are to some extent **aligned with observations from nonlinear dynamical systems theory**.

### THE FOUR CLASSES

| Class | Name | Characteristic |
|---|---|---|
| **I** | **Homogeneous** | The CA reaches a **homogeneous state for all cells**, mostly the silent state. Everything dies out. |
| **II** | **Periodic** | **Periodic, oscillatory patterns**, including stable (fixed) patterns. |
| **III** | **Chaotic** | **Deterministic chaos** — no periodicity is observable. |
| **IV** | **Complex, Patterns, "Self Organisation"** | **Interesting structures evolve, persist, seem to interact, and generate new structures.** |

```
 CLASS I - Homogeneous            CLASS II - Periodic
 ####...##.#..##.#.               #..#..#..#..#..#.
 ..#.....#.....#..                #..#..#..#..#..#.
 .................                #..#..#..#..#..#.
 .................                #..#..#..#..#..#.
 dies to a uniform state          stable / oscillating local patterns


 CLASS III - Chaotic              CLASS IV - Complex
 #.##..#.#.###..#.                ....#.......##...
 ##.#.###..#..###                 ...#.#......##...
 #..####.#.##.#.#                 ....##.....##....
 .##.#..###.#..##                 .......#..##.....
 ###..##.#..###.#                 ......#.#..#.....
 random-looking for ever          localised structures persist,
 no periodicity, no structure     move, collide, create new ones
```

### THE ANSWER — similarities first, then differences

**Half the marks are in the "in common" half, which candidates skip. Do both.**

**What they have in common:**
- Both arise from **simple, local, deterministic rules** with no central control.
- Both are **aperiodic** — neither settles into a repeating global cycle, so neither is class I or II.
- Both look **irregular and complicated**, and neither can be predicted analytically: **the only way to know the state at time $t$ is to run the automaton**.
- Both are **sensitive to the initial configuration**.

**How they differ:**

| | **Class III — Chaotic** | **Class IV — Complex** |
|---|---|---|
| **Structures** | No persistent localised structures; uniformly random-looking everywhere. | **Localised structures form and persist** (e.g. gliders). |
| **Interaction** | Nothing to interact — disturbances just spread. | Structures **move, collide, interact, generate new structures**. |
| **Information** | Local information is **destroyed**, diffusing into noise. | Local information is **transported and processed** — a glider carries a bit. |
| **Position** | Fully disordered. | **Between order and chaos** — the "edge of chaos", between class II and III. |
| **Computation** | None. | Supports **universal computation** (Rule 110, Game of Life). |
| **Example** | Rule 30; the logistic map at $a=4$. | **Rule 110**; **Conway's Game of Life**; the **glider**. |

> **The one-sentence discriminator:** both are aperiodic and unpredictable, but class III destroys local structure into uniform noise, whereas class IV supports **persistent, moving, interacting structures** — which is what makes class IV capable of computation.

### VARIANTS

**V1.** *"Which class does the blinker belong to? And the glider?"*

<details><summary>Answer</summary>
The **blinker** is *"the archetype of a periodic **class II** behaviour"* — it oscillates with period 2. The **glider** is *"the prototypic **class IV** pattern"* — a persistent localised structure that travels and can interact. (Both phrases are the lecture's own.)
</details>

**V2.** *"Which Wolfram class does the r-pentomino show? Support with arguments."* (`sheet-03` A4)

<details><summary>Answer</summary>

**Class IV.**
- It runs for over a thousand generations of apparently chaotic activity, so it is **not class I** (it does not die out) and **not class II** (it does not settle quickly).
- It is **not class III** either, because it does **not** stay aperiodic for ever: it eventually settles into still lifes and oscillators **while emitting gliders**.
- Those gliders are the decisive evidence: **persistent, localised, propagating structures** are the defining feature of class IV and are absent from class III.

**Honest caveat worth including:** during its long transient it *looks* class III, so "class III during the transient, class IV overall" is a defensible answer — say which you mean and why. The marks are for the argument.
</details>

**V3.** *"Give the four classes with one CA example each."*

<details><summary>Answer</summary>

- **I — Homogeneous:** rule 0 (everything → 0); rule 255.
- **II — Periodic:** rule 4, rule 204 (identity, freezes the pattern); the blinker in Game of Life.
- **III — Chaotic:** rule 30; rule 90 from a random start.
- **IV — Complex:** **rule 110**; Conway's Game of Life.
</details>

### ⚠️ TRAPS

- **Only listing differences.** Both wordings explicitly ask what they have **in common**.
- **Saying class IV is "more random" than class III.** It is the opposite — class IV is *more structured*, sitting between order and chaos.

---

## Q17 · Self-Organized Criticality — the scaling law 🔒+⚙️
**Asked on 2 of 4. 5 points. Once as the formula, once as the diagram.**

### Asked as

- *"[Write and explain the SOC scaling law]"* — 2017 Q13
- *"Draw a diagram visualizing the **Gutenberg-Richter-Law** and define the variables you used."* — 2025 T5

### THE MOTIVATION — one sentence that frames everything

> **How large is a typical earthquake?** There are **a lot of small** earthquakes, **some** with medium strength, **a few large**, and **rare extreme** ones. There is no "typical" size — and that is what a scaling law expresses.

### ① THE SCALING LAW — the definition

> A function $f(x)$ obeys a **scaling law**, or is **scaling invariant**, if scaling the argument $x \to \lambda x$ gives
> $$f(\lambda x) = C(\lambda)\,f(x)$$
> where the scaling factor $C(\lambda)$ **does not depend on $x$**. In principle $C(\lambda)$ can be any function, but it is often simply $\lambda^{n}$ for an integer $n$.

### ② THE POWER LAW — the size distribution

> **How does the number of events $N(s)$ depend on the size $s$ of the event?**
> $$N(s) \sim \frac{1}{s^{\,b}} \qquad\Longrightarrow\qquad \log N(s) \sim -\,b \log s$$
>
> **Define every symbol:** $s$ = size / strength of an event; $N(s)$ = number (frequency) of events of that size; $b$ = the characteristic exponent.
>
> This is a **linearly decreasing dependency of the number of events on the strength, both in logarithmic scale** — so in a **log–log plot the graph is a straight, decreasing line**.

**Draw it — this is the diagram the exam wants:**

```
   log N(s)
      ^
      |  *
      |    *
      |      *           slope = -b
      |        *
      |          *
      |            *
      |              *
      |                *
      +-------------------------> log s

   Straight, DECREASING line in a log-log plot.
   Many small events, few large ones, no characteristic size.
```

### ③ GUTENBERG-RICHTER (1949, 1954) — the instantiated version, 2025 T5

> The Gutenberg-Richter law gives a statistical dependency between the number $N$ of earthquakes **with at least magnitude $M$**, and the magnitude $M$ (strength on a logarithmic scale):
> $$\log_{10} N = a - b\,M \qquad\Longleftrightarrow\qquad N = 10^{\,a - bM}$$
>
> **Symbols:** $N$ = number of earthquakes of at least magnitude $M$; $M$ = magnitude; $a$ = a constant setting the overall level (total seismicity of the region); $b$ = a constant **typically close to $b = 1.0$**, with $0.5 < b < 1.5$ reasonable in special environments.

```
   log10 N
      ^
    5 |  *
      |     *
    4 |        *
      |           *          slope = -b  (b ~ 1.0)
    3 |              *
      |                 *
    2 |                    *
      |                       *
    1 |                          *
      +---+---+---+---+---+---+---+---> M  (magnitude)
          2   3   4   5   6   7   8

   b ~ 1  =>  each unit of magnitude means
              TEN TIMES fewer earthquakes
```

> **Say the interpretation:** with $b \approx 1$, going up one unit of magnitude makes earthquakes about **ten times rarer**.

### ④ THE OTHER POWER LAWS ON THE SLIDES — one line each

| Law | Formula | What it relates |
|---|---|---|
| **Size distribution** | $N(s) \sim 1/s^{\,b}$ | number of events vs event size |
| **Temporal / inter-event-interval** | $N(t) \sim 1/t^{\,g}$ | number of events vs time between events |
| **Power spectrum** | $P(f) \sim 1/f^{\,a}$ | signal power vs frequency ("$1/f$ noise") |
| **Gutenberg-Richter** (1949/54) | $\log_{10} N = a - bM$, $b\approx1$ | earthquakes |
| **Zipf's Law** (1935) | $f(r) \sim 1/r^{\,\gamma}$, $\gamma \approx 1$ | word frequency vs its **rank** — the most frequent word occurs about twice as often as the second, three times as often as the third |
| **Zipf-Mandelbrot** | $f(r) \sim 1/(r+b)^{\gamma}$ | Zipf with an offset; $b=0$ gives Zipf exactly |
| **Lotka's Law** (1926) | $Y(x) = C/x^{\alpha}$, $\alpha \approx 2$ | number of authors vs number of publications |

**The named SOC example systems:** forest-fire model (Chen/Bak/Jensen 1990; Drossel/Schwabl 1992), **sandpile model (Bak, Tang, Wiesenfeld 1987)**, land slides (Fuji 1969), percolation theory (Broadbent & Hammersley 1957), earthquakes (Gutenberg & Richter), Zipf, Lotka, Auerbach (1913).

### ⑤ THE BTW SANDPILE — the algorithm, in case it is asked

> Each cell $z(x,y)$ holds the number of grains (or the local slope). Critical value **$C = 4$**, so stable cells have $z \in \{0,1,2,3\}$. Neighbourhood $r=1$, **von Neumann**.

```
 0: Initialize all positions (random or a special pattern)
 1: Choose a position (x,y) randomly
 2: Add a grain:  z(x,y) -> z(x,y) + 1
 3: If ALL z(x,y) < 4  GOTO step 1
 4: Take an unstable position and redistribute:
        z(x,y)   -> z(x,y) - 4
        z(x-1,y) -> z(x-1,y) + 1
        z(x+1,y) -> z(x+1,y) + 1
        z(x,y-1) -> z(x,y-1) + 1
        z(x,y+1) -> z(x,y+1) + 1
    Grains at the edge FALL OFF the playground and are lost.
 5: GOTO step 3   (repeat 4 until everything is stable)
```

> The redistribution can make neighbours unstable in turn, causing further topplings — **an avalanche**. The **sizes of these avalanches follow the power law**, and the system reaches this critical state **by itself**, with no parameter tuned — which is precisely what "**self-organized** criticality" means.

### VARIANTS

**V1.** *"Why is it called SELF-organized criticality?"*

<details><summary>Answer</summary>

Because the system **evolves naturally into the critical state through a self-organizational process**, with **no external parameter tuned to a critical value**. In the sandpile you only ever drop grains at random; the slope arranges itself at the critical angle. Contrast with a classical phase transition, where an experimenter must tune the temperature to $T_c$.
</details>

**V2.** *"Draw a diagram visualizing Zipf's Law and define your variables."*

<details><summary>Answer</summary>

Same shape as Gutenberg-Richter — a falling straight line in log–log:
```
   log f(r)
      ^
      |  *
      |     *
      |        *      slope = -gamma  (gamma ~ 1)
      |           *
      |              *
      +------------------> log r
```
**Symbols:** $r$ = the rank of a word in the frequency-sorted list; $f(r)$ = the frequency of that word; $\gamma$ = the characteristic exponent, very often $\approx 1$; $N$ = the number of words (size of the corpus).

**Statement:** the frequency of any word is **inversely proportional to its rank** — the most frequent word occurs about twice as often as the second, three times as often as the third, and so on.
</details>

**V3.** *"Prove that $f(x) = a\,x^{-\alpha}$ is scale invariant."*

<details><summary>Answer</summary>

Substitute $x \to \lambda x$:
$$f(\lambda x) = a(\lambda x)^{-\alpha} = a\,\lambda^{-\alpha} x^{-\alpha} = \lambda^{-\alpha}\bigl(a\,x^{-\alpha}\bigr) = \lambda^{-\alpha} f(x)$$
So $f(\lambda x) = C(\lambda) f(x)$ with $C(\lambda) = \lambda^{-\alpha}$, which **does not depend on $x$**. Hence $f$ obeys a scaling law. $\blacksquare$

**Interpretation:** rescaling the event size only rescales the count by a constant factor — the distribution **looks the same at every scale**, so there is **no characteristic event size**.
</details>

**V4.** *"Explain the forest-fire model and its control parameters."*

<details><summary>Answer</summary>

A **non-deterministic CA**: $d=2$, rectangular grid, $r=1$, **von Neumann**, $k=3$ with states **A** (empty/ashes), **T** (tree), **F** (burning tree/fire).

**Transitions:** fire turns into ashes; **spontaneous growth** at rate $p$; **spontaneous fire** at rate $f$; **induced fire** — a tree burns if at least one neighbour burns; **induced growth** — a tree grows if at least one neighbour is a tree, at rate $q$.

**Control parameters: $p$, $f$, $q$.** $q = 0$ (no induced growth) is a good setting to start from, and **interesting (fractal) behaviour arises when $f \ll p$**, e.g. $p/f = 100$.
</details>

### ⚠️ TRAPS

- **Drawing linear axes.** The whole point is that it is a straight line **in log–log**. Label the axes $\log N$ and $\log s$.
- **Not defining the variables.** 2025 T5 says "define the variables you used" — that is half the marks.
- **Forgetting $b \approx 1$.** The examiner wants exact values.

---
---

# ASKED ON ONE OF THE FOUR PAPERS

**Do not skip these.** Each paper takes ~17 of the ~21 pool questions, and which ones get dropped rotates. All four below are current lecture material.

---

## Q18 · The Ant Algorithm — the 4 phases 🔒
**⚠️ THIS QUESTION WAS MISSING FROM MY EARLIER POOL TABLE. It is on `qn-03` (2023) as a 5-pointer.**

### Asked as

- *"Ant Algorithm [5 Points] — **Describe the 4 phases of the Ant Algorithm.**"* — 2023 `qn-03`

### THE FRAME — one sentence

> The **Ant Algorithm** is a **method for discrete optimization**, inspired by observations of real ant colonies — in particular their **foraging behaviour** and how ants find **shortest paths between a food source and the nest**. First published by **M. Dorigo** and colleagues in **1991/1992**.

**Essential ingredients of an Ant System (AS):** multiple **cooperating agents**, simply structured; each has a **sensory system**, a method to **deposit pheromones (stigmergy)**, and a **simple mechanism to decide where to go**. **The pheromones evaporate after a while.**

### THE FOUR PHASES — the answer

```
  PHASE 1: RANDOM SEARCH        PHASE 2: FOOD FOUND

      N                              N
     /|\                            /|\
    / | \  ants leave in           / | \
   /  |  \ arbitrary directions,  /  |  \
  .   .   . dropping pheromone   .   .   *---[F]
                                          one ant reaches
                                          the food by chance

  PHASE 3: RETURN & REINFORCE   PHASE 4: POSITIVE FEEDBACK

      N                              N
      |                              |
      | winner returns along         ||  more ants take it,
      | its OWN trail, dropping      ||  each adding pheromone;
      | more pheromone -> that       ||  the other trails
      * trail is used TWICE          ||  EVAPORATE away
      |                              ||
     [F]                            [F]
```

**① Random search and pheromone deposition.**
> Ants leave the nest $N$ **heading into arbitrary directions**, searching for food. During their journey they **deposit pheromones along their pathway**. Ants without a prior pheromone trail are simply performing **random movements** — slow and inefficient, but it can be shown that there is a chance of even finding the **optimal** path.

**② Discovery of the food source.**
> **By chance, one of the ants reaches the source of food** while the others are still searching. It picks up some food.

**③ Return and reinforcement.**
> The successful ant **travels back to the nest following its own pheromone trail**, so it takes (almost) the same route back, **dropping more pheromone on the way**. Because this trail is **traversed twice — forth and back — it now carries a higher pheromone concentration** than the trails of the still-searching ants.

**④ Positive feedback (autocatalysis) and evaporation.**
> Other ants **sense the pheromone and base their movement on its concentration**: *the higher the concentration, the more likely an ant will take that path*, otherwise it follows an almost random route. So the most successful path gets a **higher probability of being chosen, more ants take it, and they further increase the concentration — positive feedback, an autocatalytic mechanism.** Meanwhile **the other pheromone trails decay** through evaporation.

### WHY EVAPORATION MATTERS — three reasons, straight from the slide

> The process of time-dependent evaporation is tricky:
> - it **enforces faster, and thereby shorter routes**;
> - it **can react to dynamic changes of the environment** — an exhausted food source, a changed path length;
> - it acts as a **virtual reset of unused trails**.

### EXPLORATION vs EXPLOITATION — the standard follow-up

> - Ants **performing random movements: exploration.**
> - Ants **following a trail, using knowledge acquired before: exploitation.** The more successful a path has been, the more likely it is taken — those trails are **local minima** of the underlying optimization problem.

### THE DISCRETE VERSION — for the "how is it an optimization method?" follow-up

> Transposing the ant algorithm to a discrete world is straightforward: the ants **travel along a graph**, where the nest and the food are two special nodes and the other nodes are connected by edges representing allowed routes. In each discrete time step an ant travels **one edge**; **pheromones are deposited on the edges reciprocal to the length of the edge**; **evaporation is implemented as an exponential decay**; and the **pheromone-dependent decision is implemented using a softmax / Boltzmann distribution**.

**Variants named on the slides:** Ant System (AS), Ant Colony System (ACS), Ant Colony Optimization (ACO), AntNet.

### VARIANTS

**V1.** *"What is stigmergy?"*

<details><summary>Answer</summary>

**Stigmergy** is indirect coordination through the **environment**: an agent modifies the environment (here, by depositing pheromone), and other agents respond to that modification rather than communicating directly. It is what lets simple agents cooperate **with no central control, no direct messages and no global map** — the pheromone field *is* the shared memory.
</details>

**V2.** *"Pheromone evaporates exponentially. If the concentration must fall to 10 % after 42 steps, what is the decay factor?"* (`sheet-06`)

<details><summary>Answer</summary>

Exponential decay: $\tau(t) = \tau_0\,\rho^{\,t}$, where $\tau_0$ is the initial concentration and $\rho$ the per-step decay factor. Require $\rho^{42} = 0.1$:
$$\rho = 0.1^{1/42} = 10^{-1/42} \approx \mathbf{0.9462}$$
So about **5.4 % of the pheromone evaporates per step**.
</details>

**V3.** *"Where do exploration and exploitation appear in the EA, the ant algorithm, and PSO?"* (asked directly on 2017 Q3 and in orals)

<details><summary>Answer</summary>

| | **Exploration** | **Exploitation** |
|---|---|---|
| **EA** | random initialization; **mutation** | selection, elitism, recombination of good parents |
| **Ant algorithm** | random movement of ants with no trail; pheromone **evaporation** | following high-concentration trails; pheromone reinforcement |
| **PSO** | the random factor $R$; inertia $w V_j$ keeping the old direction | the pull toward **personal best** and **global best** |
</details>

### ⚠️ TRAPS

- **Giving the four phases as a story with no structure.** Number them 1–4 — the question says "the 4 phases".
- **Omitting evaporation.** It is what makes the algorithm find the *shortest* path rather than just *a* path.

---

## Q19 · Particle Swarm Optimization 🔒+⚙️
**Asked on 1 of 4 (2017 Q10) — and it is the NEWEST material in the course (`lect-12`), which makes it more likely to return, not less.**

### Asked as

- *"[Write and explain the PSO **position** update formula]"* — 2017 Q10

### THE FRAME

> **Particle Swarm Optimization** is an Artificial-Life-inspired, **multi-hypothesis, meta-heuristic method for optimization**. Based on **C. Reynolds' Boids**, it was developed by **J. Kennedy, R. Eberhart and Y. Shi**, who added an **objective (a position) that the simulated individuals should reach**. The results were so successful that PSO became a well accepted optimization method. It is related to Evolutionary Algorithms, Particle Filters and Boids.

**Each particle $j$ has:** a **position $X_j$** in the search space $S$; a **velocity $V_j$** (its change in position); and a **memory** storing the best result it has found so far — its **personal best** $X_{j,pb}$ with $f(X_{j,pb})$ — and optionally the best of the group it belongs to, $X_{j,grb}$.

### ⚠️ THE VELOCITY UPDATE HAS **FOUR** TERMS IN THIS LECTURE

$$V_j \;\leftarrow\; w\,V_j \;+\; a\,R\,(X_{j,pb} - X_j) \;+\; b\,R\,(X_{gb} - X_j) \;+\; g\,R\,(X_{j,grb} - X_j)$$

$$\boxed{\,X_j \;\leftarrow\; X_j + V_j\,} \qquad \text{$\leftarrow$ this is the POSITION update 2017 Q10 asked for}$$

**Name every term — the slide does, and so must you:**

| Term | Meaning |
|---|---|
| $w\,V_j$ | **keep the old direction** (inertia / momentum) |
| $a\,R\,(X_{j,pb} - X_j)$ | **steer towards the personal best** |
| $b\,R\,(X_{gb} - X_j)$ | **steer towards the global best** |
| $g\,R\,(X_{j,grb} - X_j)$ | **steer towards the group best** |

**Define every symbol:**
- $X_j$ = position of particle $j$; $V_j$ = its velocity.
- $X_{j,pb}$ = personal best position of particle $j$; $X_{gb}$ = best position in the whole swarm; $X_{j,grb}$ = best position in $j$'s group.
- $w, a, b, g$ = control parameters, with $0.0 \le w \le 1.0$ and $0.0 \le a, b, g \le 4.0$.
- **$R$ = a random value in $[0 \ldots 1]$ — this is the exploration component**, so that particles do not follow identical trajectories.

**Typical values from the slide:** $P = 20 \ldots 40$ particles, $w = 1.0$, $a = 2.0$, $b = 2.0$, $g = 1.0$.

**The two common simplifications — worth a sentence:**
- **Usually no special group is defined**, and only personal best and global best are used: $g = 0.0$.
- **Sometimes the group is the spatial neighbourhood** and the global best is omitted: $b = 0.0$.

### THE MAIN LOOP

```
 Init: X_j , V_j , groups
 Main loop:
     calculate new velocity  V_j
     calculate new position  X_j  <-  X_j + V_j
     calculate new performance f(X_j)  , evaluate particle
     store new best performances: personal best / global best / group best
     Finish?
```

```
   PSO in the search space

        X_gb (global best)
          *
           \
            \  b*R*(X_gb - X_j)
             \
    X_j  O----+------>  new position
       /  \    \
      /    \    ` a*R*(X_j,pb - X_j)
   w*V_j    *
   inertia  X_j,pb (personal best)
```

### VARIANTS

**V1.** *"Name the swarm topologies."*

<details><summary>Answer</summary>

**Singletons** (no special topology, just single particles); **Ring** (cyclic, one-dimensional); **Grid** ($N$-dimensional regular structure, including a torus); **Mesh** (randomly connected particles); **Fully-connected**.

Within a group, **only the particle's own personal best and the information from a local neighbourhood** are used to compute the new velocity.
</details>

**V2.** *"How are position and velocity bounds handled?"*

<details><summary>Answer</summary>

- **Position bounds:** for most applications an area of the search space where results are expected can be determined a priori, so particle positions are restricted to it. Particles that "try to escape" can be handled by different philosophies: **bounce, reset to start, reset randomly, reset to the stored best**, …
- **Velocity bounds:** an **upper bound on the velocity** can be defined to restrict how far a particle moves per step.
</details>

**V3.** *"What is the difference between PSO and Boids?"*

<details><summary>Answer</summary>

They are **different paradigms with a different purpose** — the lecture flags this explicitly.
- **Boids** is a **simulation** of natural flocking: three steering rules, **no objective function**, and the goal is realistic-looking collective motion.
- **PSO** is an **optimization method**: it adds an **objective function** $f$ and a **memory of the best positions found** (personal / group / global best), and the swarm's motion is a search for the optimum, not an imitation of birds.

PSO is *based on* Boids — the velocity update is *"a weighted combination of 4 different aspects, comparable to the steering rules of Boids"*.
</details>

**V4.** *"What is $R$ for, and which term gives exploration vs exploitation?"*

<details><summary>Answer</summary>

$R$ is a **random value in $[0,1]$** redrawn each step, providing **stochastic weighting** so particles do not follow identical, deterministic trajectories — it is labelled **(exploration)** on the slide.

- **Exploration:** the random factor $R$, and the inertia term $w V_j$ which carries a particle past the current best.
- **Exploitation:** the pull toward $X_{j,pb}$ and especially $X_{gb}$, which concentrates the swarm on the best found so far.
</details>

### ⚠️ TRAPS

- **Giving only three terms.** This lecture's formula has **four** — the group-best term is there even though it is usually switched off with $g = 0$.
- **Giving only the velocity update.** 2017 Q10 asked for the **position** update: $X_j \leftarrow X_j + V_j$. Give both.
- **Confusing PSO with Boids.** Different purpose — see V3.

---

## Q20 · Reynolds' Boids 🔒
**Asked on 1 of 4 (2017 Q12). 5 points. Pure recall — three rules, three sketches.**

### Asked as

- *"[Name and explain the rules producing swarming behaviour]"* — 2017 Q12

### THE ANSWER — three rules, each one sentence plus a sketch

> **C. Reynolds' Boids** (1986) model how an individual boid manoeuvres, **based on the positions and velocities of its nearby flockmates**.

**① Separation — steer to avoid crowding local flockmates.**
**② Alignment — steer towards the average heading of local flockmates.**
**③ Cohesion — steer to move toward the average position of local flockmates.**

```
   SEPARATION                ALIGNMENT                 COHESION

     o    o                    ->    ->                  o   o
       \  /                      ->    ->                 \ /
    o <-()-> o                 ->  ()  ->              o -> () <- o
       /  \                      ->    ->                 / \
     o    o                    ->    ->                  o   o

   steer AWAY from            match the AVERAGE         steer TOWARD the
   nearby flockmates          HEADING of neighbours     AVERAGE POSITION
   (avoid collision)          (fly the same way)        (stay together)
```

**The two points that turn 3/5 into 5/5:**

- **All three rules use only a LOCAL neighbourhood** — each boid sees only its nearby flockmates, never the whole flock. There is **no leader and no global plan**.
- The flocking is therefore **emergent**: realistic collective motion arises from three simple local steering rules.

### CONTEXT — swarm intelligence, if the question is broader

> **Swarm intelligence (SI)** is the **collective behaviour of decentralized, self-organized systems**, natural or artificial. The expression was introduced by **Gerardo Beni and Jing Wang in 1989**, in the context of cellular robotic systems. SI systems consist of a population of **simple agents interacting locally** with one another and with their environment; the agents follow very simple rules and **although there is no centralized control structure**, local and partly random interactions **lead to the emergence of "intelligent" global behaviour, unknown to the individual agents**.
>
> **Natural examples:** ant colonies, bird flocking, animal herding, bacterial growth, fish schooling, microbial intelligence.

### VARIANTS

**V1.** *"How would you extend Boids so the flock moves toward a goal?"* (`sheet-11`)

<details><summary>Answer</summary>

Add a **fourth steering term** pulling each boid toward the target position (or toward the optimum of an objective function), and combine it with the three existing rules as a **weighted sum**:
$$\text{steer} = w_1\,\text{sep} + w_2\,\text{align} + w_3\,\text{coh} + w_4\,(X_{\text{goal}} - X_j)$$
The weights trade flock cohesion against goal-seeking. **This is exactly the step from Boids to PSO**: adding an objective turns a flocking simulation into an optimization method.
</details>

**V2.** *"How is obstacle avoidance added to Boids?"*

<details><summary>Answer</summary>

As a further steering term that **repels the boid from nearby obstacle surfaces**, weighted more strongly than the flocking rules so it dominates when a collision is imminent. Reynolds demonstrated this in 1986 with a **simulated boid flock avoiding cylindrical obstacles**. It is structurally the same as **separation**, applied to obstacles instead of flockmates.
</details>

**V3.** *"What happens if you remove each of the three rules in turn?"*

<details><summary>Answer</summary>

- **No separation** → boids collide and collapse onto a single point; the flock has no volume.
- **No alignment** → boids stay together but move incoherently, milling about rather than travelling as a flock.
- **No cohesion** → the flock disperses; boids drift apart and never form a group.

All three are needed: cohesion pulls in, separation pushes out, and alignment gives the group a common direction.
</details>

### ⚠️ TRAPS

- **Naming the rules without saying they are LOCAL.** That is the emergence point.
- **Confusing alignment with cohesion.** Alignment matches **heading/velocity**; cohesion matches **position**.

---

## Q21 · Subsumption architecture — suppression vs inhibition 🔒
**Asked on 1 of 4 (2025 T7). 5 points. Two mechanisms, two diagrams.**

### Asked as

- *"There are two mechanisms, how the higher levels of the subsumption architecture influence the lower level. **Describe and visualize them.**"* — 2025 T7

### THE FRAME

> The **Subsumption Architecture** was introduced by **Rodney A. Brooks (1985)** in *"A Robust Layered Control System for a Mobile Robot"* (A.I. Memo 864, MIT). Instead of decomposing a robot controller into **functional** modules (the classical **SMPA** chain: **S**ense → **M**odel → **P**lan → **A**ct), it decomposes it into **task-achieving behaviours** stacked as **levels of competence**.

```
   CLASSICAL SMPA (functional decomposition)

   sensors -> [Sense] -> [Model] -> [Plan] -> [Act] -> actuators
              one broken block breaks the whole chain


   SUBSUMPTION (task-achieving behaviours)

              +--> [ level 3: build maps        ] --+
              +--> [ level 2: explore           ] --+
   sensors ---+--> [ level 1: wander            ] --+--> actuators
              +--> [ level 0: avoid objects     ] --+
              each layer is a COMPLETE controller on its own
```

**Brooks' 8 levels of competence:** 0. avoid contact with objects — 1. wander aimlessly around without hitting things — 2. explore the world — 3. build a map and plan routes — 4. notice changes in the environment — 5. reason about the world — 6. formulate and execute plans changing the world — 7. reason about the behaviour of other objects.

**Layered control:** *"Control is layered, with higher level layers subsuming the lower levels."* If necessary or appropriate for the task, the higher layers **subsume the effect of the lower layers**, so higher-level behaviours can **dominate** lower-level ones.

> **The robustness argument — always worth a sentence:** if some part of the layered structure produces no commands (busy, damaged, …), **the lower levels remain operational and still implement a working controller**. That is the key advantage over SMPA, where one broken stage kills the whole chain.

**Module structure:** each module is a **finite state machine augmented with instance variables**, with **input lines, output lines and a reset**. Brooks designed them as FSMs explicitly so they are easy to implement in hardware. Modules connect into a **network**, and the signals between them correspond to **messages** between subtasks (e.g. `halt` sent to `motor`).

### ⭐ THE ANSWER — the two mechanisms

> Beside connecting output lines to input lines, **the output of a module can alter the signal on another connection by 2 methods:**

| | **Suppression** | **Inhibition** |
|---|---|---|
| **What it does** | **Overwriting** signal lines for $z$ time steps | **Cancelling** signals for $z$ time steps |
| **Acts on** | an **INPUT** line | an **OUTPUT** line |
| **Effect** | the suppressing signal **replaces** what was there | the inhibited signal is **blocked**; nothing gets through |
| **Symbol** | a circle marked **S** on the line | a circle marked **I** on the line |
| **The number in the circle** | the **time $z$** for which the effect lasts | the **time $z$** for which the effect lasts |

**Draw both — the question says "visualize":**

```text
 ================================================================
                     SUPPRESSION (Input)
 ================================================================
                                 
                   [ Higher Layer ]
                          |
                          | (Sends override signal)
                          v
                        ( S ) <--- Lasts for z time steps
                          |
  [ Normal Input ] -------+-------> [ Module ]
                          
  EFFECT: The normal input is disconnected. The signal from the 
          higher layer goes into the module instead.
 
 ================================================================
                     INHIBITION (Output)
 ================================================================
 
                   [ Higher Layer ]
                          |
                          | (Sends blocking signal)
                          v
                        ( I ) <--- Lasts for z time steps
                          |
  [ Module ] -------------+-------> [ X ] (NOTHING PASSES)
                          
  EFFECT: The module's normal output is blocked like a brick wall. 
          Nothing gets sent to the next layer or motors.
 ================================================================
```

> **The one-sentence discriminator:** **suppression replaces a signal on an input line; inhibition blocks a signal on an output line.** In both cases the number written inside the circle is the **number of time steps** the effect lasts.

### VARIANTS

**V1.** *"Why is subsumption more robust than SMPA?"*

<details><summary>Answer</summary>

In **SMPA** the modules form a **chain** — Sense → Model → Plan → Act — so **every module must work** for the robot to do anything; a failure anywhere leaves the robot inert.

In **subsumption**, **each layer is a complete controller by itself** that runs from sensors to actuators. If a higher layer is busy, damaged, or silent, **the lower layers keep operating** and the robot still avoids obstacles and wanders. Competence degrades gracefully instead of collapsing.
</details>

**V2.** *"Give an example of subsumption with two layers."*

<details><summary>Answer</summary>

- **Level 0 — avoid objects:** reads the proximity sensors and steers away from obstacles. Always running.
- **Level 1 — wander:** generates a random heading every few seconds and drives that way.

Level 1 **suppresses** level 0's input with its desired heading when the path is clear. When an obstacle appears, level 0's avoidance output **inhibits** the wander command for $z$ time steps so the robot turns away, then wandering resumes. The robot wanders *and* never collides, with no map and no planner.
</details>

**V3.** *"Name Brooks' requirements for a control system."*

<details><summary>Answer</summary>

Brooks' *"robotics wish list for Santa Claus"*: **Multiple Goals**, **Multiple Sensors**, **Robustness**, **Additivity** (being able to add new capabilities without redesigning what already works).
</details>

### ⚠️ TRAPS

- **Swapping them.** *Suppression = input = overwrite. Inhibition = output = cancel.* Memorize as **"S for Substitute, I for Interrupt"**.
- **Not visualizing.** The question says "describe **and visualize**". Two labelled diagrams.
- **Forgetting the number in the circle.** It is the **time constant $z$** — how many time steps the effect lasts.

---
---

# ⚠️ COVERAGE CHECK — every past-exam task, accounted for

All **69 tasks** across the four written papers map onto the 21 questions above. Nothing is left unsolved.

| Paper | Tasks | Where |
|---|---|---|
| **2017 (G)** — 17 tasks | Q1 GoL(10) · Q2 Didabots(10) · Q3 EA(10) · Q4 life · Q5 Wolfram no. · Q6 perf. graph · Q7 Langton · Q8 rule count · Q9 Braitenberg · Q10 PSO · Q11 L-System · Q12 Boids · Q13 SOC · Q14 von Neumann · Q15 Wheel · Q16 Fibonacci · Q17 glider | Q1, Q11, Q2, Q3, Q4, Q12, Q5, Q14, Q6, Q19, Q7, Q20, Q17, Q8, Q9, Q10, Q1 |
| **2023 `qn-02`** — 17 tasks | 1 GoL(10) · 2 Didabots(10) · 3 EA(10) · 4 EA mutation · 5 glider · 6 Wolfram 42 · 7 Braitenberg t1 · 8 sensor swap · 9 Wheel · 10 Langton · 11 von Neumann · 12 class III/IV · 13 fitness distr. · 14 life · 15 golden ratio · 16 L-System · 17 totalistic-legal | Q1, Q11, Q2, Q13, Q1, Q4, Q6, Q6, Q9, Q5, Q8, Q16, Q12, Q3, Q10, Q7, Q15 |
| **2023 `qn-03`** — 12 recorded | GoL(10) · EA(10) · Didabots(10) · EA mutation · von Neumann · life · Braitenberg t1 · Wolfram 42 · L-System · golden ratio · Wheel · **Ant Algorithm** | Q1, Q2, Q11, Q13, Q8, Q3, Q6, Q4, Q7, Q10, Q9, **Q18** |
| **2025 `qn-01`** — 18 tasks | T1 Wolfram rev.(10) · T2 EA(10) · T3 Langton · T4 Braitenberg · T5 Gutenberg-Richter · T6 EA fitness · T7 subsumption · T8 life · T9 rule count · T10 von Neumann · T11 Wheel · T12 glider · T13 EA mutation · T14 Braitenberg t1 · T15 classes · T16 L-System · T17 totalistic-legal · T18 Fibonacci | Q4, Q2, Q5, Q6, Q17, Q12, Q21, Q3, Q14, Q8, Q9, Q1, Q13, Q6, Q16, Q7, Q15, Q10 |

**Two corrections I made while checking this:**

1. **The Ant Algorithm (Q18) was missing from my earlier pool table.** It is a genuine 5-point task on `qn-03` (2023). The pool is **21 questions, not 20**.
2. **The PSO velocity formula in my earlier notes had three terms; the lecture has four** (it includes the group-best term $g\,R\,(X_{j,grb} - X_j)$). Corrected in Q19.

---

# THE FULL SELF-TEST — one pass over all 21

Cover every answer. Write them out on paper, timed. **This is a complete mock paper's worth of content: 90 minutes, ~90 points.**

1. Explain Game of Life in full and draw a glider moving to the lower left, $t=0..3$. **(10 min)**
2. Name and explain all parts and steps of an EA, plus pros and cons. **(10 min)**
3. Name 5 criteria of life. **(2 min)**
4. Write the rule table for Wolfram number 42 and classify it. **(4 min)**
5. Draw the 4 micro-behaviours of Langton's Ant, labelled. **(4 min)**
6. What happens if proximity sensors are swapped for distance sensors in a 3b? Draw it. **(4 min)**
7. Give an L-System producing `OAOAOAOAOAOAOAO` at $t=3$ from axiom `O`, with the expansion table. **(4 min)**
8. Name and explain 2 things von Neumann is associated with. **(3 min)**
9. Derive $\omega_1(P)$ for the Wheel of Fortune. **(4 min)**
10. Derive the relation between Fibonacci and the golden ratio, with a numeric table. **(4 min)**

11. Explain the Didabot experiment in full: purpose, result, the four essential properties, both release mechanisms, and what changes with more than one Didabot. **(10 min)**
12. Draw the fitness of the population sorted by fitness, before and after $(\mu+\lambda)$ external selection with elitism. Then draw the performance graph and say why it is monotone. **(5 min)**
13. Derive $Q$ for (a) at least one of $N$ offspring differing from the parent, and (b) no offspring being identical to the parent. Substitute $p = 1/L^2$ into (b). **(5 min)**
14. Derive the number of possible rules for a CA with $d=3$, $k=2$, $r=1$ Moore. **(4 min)**
15. Prove or disprove: "a totalistic rule with a silent state is legal". **(4 min)**
16. Explain Wolfram's class III and class IV — differences **and** similarities. **(4 min)**
17. Write the SOC scaling law, then draw and label the Gutenberg-Richter diagram, defining every variable. **(5 min)**
18. Describe the 4 phases of the Ant Algorithm. **(5 min)**
19. Give the PSO velocity **and** position update formulas, naming all four velocity terms and every symbol. **(4 min)**
20. Name and sketch Reynolds' three Boids rules. **(3 min)**
21. Describe **and visualize** the two mechanisms by which higher subsumption layers influence lower ones. **(4 min)**

**Total: ~85 minutes.** That is the real exam, at real speed.

---

# THE NIGHT-BEFORE SHORTLIST

If you only have time for one pass, drill these in this order — they are the highest points per minute:

1. **Q3** life criteria — 5 pt, pure list, 2 minutes.
2. **Q8** von Neumann — 5 pt, pure recall.
3. **Q20** Boids — 5 pt, three rules.
4. **Q21** subsumption — 5 pt, two diagrams, one discriminator sentence.
5. **Q5** Langton's Ant — 5 pt, four labelled sketches + the number 104.
6. **Q7** L-System — 5 pt, two rules + the expansion table.
7. **Q9** Wheel of Fortune — 5 pt, four-line derivation to $2/(P+1)$.
8. **Q10** Fibonacci — 5 pt, derivation + numeric table.
9. **Q1** Game of Life — up to 10 pt, spec + 23/3 + blinker + glider.
10. **Q2** EA — 10 pt, six parts + cycle + pros/cons + the recipe application.
11. **Q11** Didabots — 10 pt, six parts + one-vs-many.

That is **~70 points** from eleven questions.
