# EXAM DAY PLAN — reading order

**Thursday 30 July 2026, 12:00–14:00, Hörsaal X, University Bonn Main Building.**

All question numbers refer to **`notes/qbank.md`**.

---

## CONFIRMED EXAM FORMAT

| | |
|---|---|
| **Duration** | **90 minutes** (10 less than the past papers) |
| **Maximum points** | **90** (10 less than the past papers) |
| **Structure** | **2 questions × 10 points + 14 questions × 5 points = 16 questions** |
| **Pass threshold** | **45 points (50 %)** |
| **Pace** | exactly **1 minute per point** — a 5-pointer gets 5 minutes, a 10-pointer gets 10 |

**What this changes versus the past papers:** 2017 and 2023 had **three** 10-pointers; this paper has **two**. So one of the big questions that used to be worth 10 has either dropped to 5 or vanished. There is **no spare time** — at 1 min/point you cannot overrun anywhere.

---

## THE TARGET

**Pass = 45 points. That is confirmed.** The rest of the scale is not stated anywhere in your materials, so:

| Grade | Estimated points | Basis |
|---|---|---|
| **4.0 (pass)** | **45 / 90** | **confirmed by the examiner** |
| 3.0 | ~59 / 90 (65 %) | inferred |
| 2.3 | ~68 / 90 (75 %) | inferred |
| **2.0** | **~72–75 / 90 (80–83 %)** | **inferred** |
| 1.0 | ~86–90 / 90 (95 %+) | inferred |

> The two commonest German schemes — the 12-step table (2.0 at 80 %) and the straight linear one (2.0 at 83 %) — both land in the **72–75** band once 45 is fixed as the pass mark. **Aim at 75 so a 2.0 survives a couple of dropped marks.**

**In questions answered, 75 points means:** **both 10-pointers + 11 of the 14 five-pointers.** You can afford to lose three small questions completely.

---

## ⭐ THE ARITHMETIC THAT DECIDES YOUR PLAN

There are **21 questions in the pool** but only **16 on the paper** — five get dropped, and which five rotates.

**The ten 4/4 questions have appeared on every paper.** Count what they alone are worth on a 2×10 + 14×5 paper:

| | Slots | Points |
|---|---|---|
| **EA** (Q2) — a 10-pointer on **all four** past papers | 1 × 10 | 10 |
| One more 10-pointer from {Game of Life, Didabots, Wolfram-reverse} | 1 × 10 | 10 |
| Life criteria, Wolfram number, Langton, **Braitenberg ×2**, L-System, von Neumann, Wheel of Fortune, Fibonacci | 9 × 5 | 45 |
| | | **≈ 65** |

> **Mastering only the ten 4/4 questions gets you to roughly 65 points — a comfortable pass, around a 2.7–3.0.** You then need **two or three more small questions** from the next tier to clear 2.0. That is the whole strategy.

**And note: Q2 (EA) is near-certainly one of the two 10-pointers.** It has been a 10-pointer on four papers out of four. It is the single highest-value item in the bank.

---

## PART 1 — READ THESE FIRST (85 points of material, ~2 h 50)

| # | Q | Topic | Pts | Min | Cum. pts | Recurrence |
|---|---|---|---|---|---|---|
| **1** | Q3 | 5 criteria of life | 5 | 8 | 5 | 4/4 |
| **2** | Q20 | Boids — 3 rules | 5 | 6 | 10 | 1/4 |
| **3** | Q8 | von Neumann ×2 | 5 | 10 | 15 | 4/4 |
| **4** | Q7 | L-System `OAOA…O` | 5 | 10 | 20 | 4/4 |
| **5** | Q4 | Wolfram number — **forward only** | 5 | 12 | 25 | 4/4 |
| **6** | Q5 | Langton's Ant | 5 | 12 | 30 | 4/4 |
| **7** | Q2 | **EA full + applied — near-certain 10-pointer** | 10 | 25 | 40 | 4/4 |
| **8** | Q1 | **Game of Life** | 10 | 20 | 50 | 4/4 |
| **9** | Q6 | Braitenberg — **TWO slots** (§Q6a, §Q6b, §Q6c) | 10 | 15 | 60 | 4/4 |
| **10** | Q9 | Wheel of Fortune | 5 | 12 | 65 | 4/4 |
| **11** | Q10 | Fibonacci ↔ golden ratio | 5 | 12 | **70** | 4/4 |
| **12** | Q11 | **Didabots** | 10 | 20 | 80 | 3/4 |
| **13** | Q15 | Totalistic + silent ⇒ legal | 5 | 8 | **85** | 2/4 |

**Item 7 moved up.** EA is now studied *before* Game of Life, because it is the one question that has been a 10-pointer on every single paper and there are only two 10-pointers left.

**Items 1–6 are 30 points in under an hour.** Do those first no matter what happens.
**Items 1–11 are the ten 4/4 questions = ~65–70 points ≈ a safe pass with room.**

---

## PART 2 — THE REMAINING NINE (in this order, as time allows)

| # | Q | Topic | Pts | Min | Cum. pts | Recurrence |
|---|---|---|---|---|---|---|
| **14** | Q16 | Wolfram class III vs IV | 5 | 8 | 90 | 2/4 |
| **15** | Q13 | EA mutation probability | 5 | 12 | 95 | 3/4 |
| **16** | Q21 | Subsumption — suppress vs inhibit | 5 | 8 | 100 | 1/4 |
| **17** | Q4 | Wolfram number — **reverse** | +5 | 15 | 105 | 4/4 |
| **18** | Q12 | EA fitness / performance diagrams | 5 | 12 | 110 | 3/4 |
| **19** | Q14 | Rule counting for given $d,k,r$ | 5 | 10 | 115 | 2/4 |
| **20** | Q18 | Ant Algorithm — the 4 phases | 5 | 10 | 120 | 1/4 |
| **21** | Q17 | SOC scaling law + Gutenberg-Richter | 5 | 12 | 125 | 2/4 |
| **22** | Q19 | PSO — velocity **and** position update | 5 | 12 | 130 | 1/4 |

**Full sweep: ~4 h 30.** The cumulative column passes 90 because only 16 of the 21 pool questions appear — covering 130 points of material means that whichever 90 show up, you are ready.

**Items 14–16 are the cheapest three in Part 2 (21 minutes for 15 points of material).** If you finish Part 1 with any time left, do those before anything else — they are what lift 65 to 2.0 territory.

---

## Why this order and not straight recurrence order

**① Q6 Braitenberg is worth 10 points, not 5.** Both 2023 and 2025 asked it **twice on the same paper**. Use the routing table at the top of Q6 — §Q6a stochastic component, §Q6b sensor swap, §Q6c obstacle avoidance — and write only the one you were asked.

**② Q20 Boids is #2 despite appearing on only one paper.** Three rules, one sketch each, six minutes. Nothing else returns 5 points that fast. Same logic puts Q21 subsumption at #16.

**③ Q4-reverse is deferred to #17** even though it was the 10-pointer in 2025. Forward Wolfram (#5) earns most of the credit anyway, and if the reverse version appears, the forward method plus *"count the unconstrained lines, the answer is $2^{8-m}$ numbers"* earns substantial partial credit for a fraction of the study time.

**④ Q17 SOC and Q19 PSO are last** — each needs a carefully labelled diagram and neither has ever been worth more than 5 points.

---

## If you fall behind

- **Items 1–11 = the ten 4/4 questions ≈ 65–70 points in ~2 h 20. That is the floor worth defending.** It clears the 45-point pass mark with a wide margin.
- **The least-bad sacrifice is #12 Didabots.** It is the only 10-pointer ever *absent* from a paper (missing in 2025) — and with only two 10-pointers this year, its odds are lower still.
- **Never sacrifice #7 EA or #8 Game of Life.** They are the two likeliest 10-pointers on the paper.

---

## In the exam room

**Pace: 1 minute per point, and there is no slack.** 5-pointer = 5 minutes. 10-pointer = 10 minutes.

1. **Read all 16 questions first (3 minutes).** Identify the two 10-pointers.
2. **Do every 5-pointer you know cold, first.** Fourteen small questions at 5 points each are 70 of the 90 points — they matter far more than the two big ones.
3. **Then the two 10-pointers**, ~10 minutes each.
4. **If a question stalls, leave it and move on.** At 1 min/point, two minutes lost on a 5-pointer is 2 points of another question gone.

**Two habits worth more than another question:**

**① Name the mechanism even when you cannot finish the calculation.** Write the formula, substitute, show the method. A blank sub-part scores zero; a named mechanism with a wrong number does not.

**② Write the exact values.** The 2017 paper states outright: *"Wants explanations for all answers including formulas (which variable means what?)"*

| Value | Where |
|---|---|
| **104** | Langton's Ant highway period |
| **≈420 / ≈10 000** | Langton's phase boundaries |
| **23/3** (= S23/B3) | Game of Life rule, in Goerke's notation |
| **period 30, 36 cells, 36×9** | Gosper's Glider Gun |
| **29 states, ~150 000 cells** | von Neumann Universal Constructor |
| **151 steps, 86 cells, $k=8$, 219 entries** | Langton's Loop |
| **5 cells, period 15** | Chou-Reggia Loop (smallest known) |
| **$\varphi = 1.618033988$, $\rho = 0.618033988$** | golden ratio |
| **137.51°** | golden angle |
| **1, 3, 3.44949, 3.56995, 4** | logistic-map thresholds |
| **$b \approx 1.0$** | Gutenberg-Richter |
| **$\omega_1 = 2/(P+1)$** | rank-based Wheel of Fortune |
| **$\lambda \approx 1.303577$** | Conway's constant (Look-and-Say) |

---

## Final checks before you walk in

- [ ] Can you draw a **glider in a named diagonal** and verify the direction with one hand-evolved step?
- [ ] Can you write **five criteria of life as a numbered list**, not a paragraph?
- [ ] For the EA design question, can you name **both** selection steps — $(\mu+\lambda)$ + elitism for external, tournament-or-rank for parent — **each with a because-clause**?
- [ ] Do you know **"at least one offspring differs"** $= 1-(1-p)^{NL}$ and **"no offspring is identical"** $= \left(1-(1-p)^L\right)^N$ are different formulas?
- [ ] Do you know **suppression = input = overwrite**, **inhibition = output = cancel**?
- [ ] For von Neumann, are your **two aspects non-overlapping** (Universal Constructor + the neighbourhood, not + "cellular automata")?
- [ ] Bring a **ruler** — every grid and log–log plot is worth drawing straight and labelled.
