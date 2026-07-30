# Phase 1 — Life & Cellular Automata

**Covers:** `lect-01` (Natural & Artificial Life, Langton's Ant), `lect-02` (Cellular Automata in 1D, Wolfram), `lect-03` (Cellular Automata in 2D, Conway's Game of Life)
**Sheets solved:** `sheet-01`, `sheet-02`, `sheet-03`
**Pool questions covered:** 7 of ~20 — life criteria, Langton's Ant, Wolfram number (forward *and* reverse), rule counting, totalistic-legal proof, Wolfram class III vs IV, Game of Life
**Budget:** ~4.5 h

### Drawing conventions — fix these now and use them all exam long

State them once at the top of your exam script, then never explain them again:

```
.  = dead cell / white cell / state 0
#  = alive cell / black cell / state I
^ > v <  = Langton's Ant, showing its heading (N, E, S, W)
```

- **Always label your axes and time steps.** Write `t=0`, `t=1`, … above or beside every grid. An unlabelled grid earns nothing.
- **Always draw the grid lines** for Game of Life and 2-dim CA. Loose dots are ambiguous; a ruled box is not.
- **For 1-dim CA, space runs horizontally and time runs downward.** That is the lecture's convention and the examiner reads it that way.

---

## PART 1 — Natural Life and Artificial Life (`lect-01`)

### 1.1 What Artificial Life is

> **CONTEXT — not directly a pool question**, but it supplies the opening sentence of several answers and is `sheet-01` Assignment 1.

Artificial Life (AL) is the study of life-like behaviour in artificial systems. Chris Langton's 1989 phrasing is the one to quote, because Goerke uses it verbatim:

- Artificial Life is **"life made by man rather than by Nature"** (C. Langton, 1989).
- The field is trying to move from studying **"life as we know it"** to studying **"life as it could be"**.

That second slogan is the one that scores. It says AL is not restricted to carbon-based, Earth-evolved biology; it asks what *any* possible living system could look like.

**Strong vs weak Artificial Life** — this is `sheet-01` Assignment 1, and it is a clean 5-point answer:

| | **Strong Artificial Life** | **Weak Artificial Life** |
|---|---|---|
| **Goal** | To really create artificial lifeforms — to make life out of non-living material. | To identify the properties, principles and circumstances of life. |
| **Claim** | The artefact **is** alive. | The artefact **simulates** the conditions and the behaviour of life. |
| **Working level** | Mainly molecular. | Mainly simulation. |
| **Who works there** | Chemists, synthetic biologists. | Most AL researchers, including this lecture. |

> **The one-sentence version to write:** Strong AL wants to *create* life out of non-living matter and works on a molecular basis, whereas weak AL wants to *understand* life by simulating its conditions and behaviour, and makes no claim that the simulation is alive.

Everything in this course — cellular automata, Game of Life, L-Systems, evolutionary algorithms, Braitenberg vehicles — is **weak** AL.

**Context only, never examinable:** the Golem legend, von Kempelen's chess-playing Turk (1769, a hoax with a human inside), Vaucanson's Digesting Duck (1735), Jaquet-Droz's Writer (1738), and the Faust quotation. One sentence of awareness is the most these are worth.

---

### 1.2 The criteria of life

> **POOL 4/4 — 2017 Q4, `qn-02` 14, `qn-03`, `qn-01` T8.** Also orals C and H. **Five points, and the cheapest five on the paper.**

The exact wordings that have been used:

- *"Name 5 attributes, commonly used to define natural life."* (2025 T8)
- *"Name 5 common criteria for life mentioned at the beginning of the lecture."* (2023, `qn-02` 14)
- *"Name 5 properties commonly associated with life."* (2023, `qn-03`)

**The single most important thing about this question: give a NAMED LIST, not a paragraph.** Five bullet points, each a noun plus one clause of explanation. A flowing paragraph containing the same five ideas scores worse, because the marker is counting items.

#### The lecture's starting position

Write this as your first line, because it frames the whole answer and costs one sentence:

> There is **no commonly accepted definition** of life in the literature. Instead there are many attempts, each based on a **set of criteria** that must be fulfilled; these sets differ in size, quality and kind, some omit relevant aspects, and some contradict each other. Remarkably, most people answer "is XXXX alive?" instantly and agree with each other, even though a concise definition remains difficult.

#### The list to memorise — the DTV "common criteria"

`lect-01` gives several competing lists. The one it labels *"here is one set of common criteria"* is from the German **DTV Atlas zur Biologie**, and this is the safest to quote because it is the list the question means by "mentioned at the beginning of the lecture":

1. **Existence in space and time** — a living thing occupies a definite place and persists over a definite period.
2. **Reproduction** — it produces new individuals of its own kind.
3. **Metabolism** — it takes in, converts and releases matter and energy.
4. **Phylogenetic development** — the species evolves across generations.
5. **Ontogenetic development** — the individual develops through a life cycle.
6. **Growth** — it increases in size and complexity over its lifetime.
7. **Movement out of itself** — it moves under its own power, not only when pushed.
8. **Reaction as a consequence to the environment** — it responds to external stimuli.
9. **Decay, death** — its existence ends.
10. **Storage of information about oneself** — it carries a description of itself (the genome).

**Pick any five and explain each in one clause.** If you want the five that are hardest to argue with, take **metabolism, reproduction, growth, reaction to the environment, and movement out of itself** — these five also appear in the Freedictionary definition, so they are doubly safe.

#### The two backup lists (know they exist; quote one only if asked for a *specific* source)

**Koshland's 7 pillars** (Daniel E. Koshland Jr., *Science*, 22 March 2002) — something is alive if it has:

1. a **program** to make copies of itself;
2. **adaptation and evolution** through mutation and selection;
3. a **complex, highly organised, compartmentalised structure**;
4. the **ability to take energy from its environment**;
5. **regeneration systems** that replace its own parts;
6. **responsiveness** to environmental stimuli through feedback;
7. numerous **metabolic reactions**, separated from each other.

**The Freedictionary's five functions** — metabolism, growth, reproduction, response to stimuli, adaptation to the environment, all *originating from within the organism*. That last phrase matters: it is what excludes a river or a fire.

#### The follow-up you must be ready for: border cases

The natural next question — and it is `sheet-01` Assignment 4 — is to sort items as living or not. Have **one border case and its reason** ready:

| Item | Verdict | Why it is a border case |
|---|---|---|
| **Virus** | Border | It reproduces and carries information about itself, but has **no metabolism of its own** and can replicate only inside a host cell. |
| **Crystal** | Not living | It grows and has a highly organised structure, but has **no metabolism, no reproduction of a self-description, and no reaction to stimuli**. |
| **Fire** | Not living | It consumes fuel, grows, moves and reacts — it fails on **reproduction of a self-description** and **information storage**. |
| **Mule** | Border | It has every criterion **except reproduction** — a mule is sterile. This is the classic argument against treating any single criterion as necessary. |
| **River Rhine / language / anthill** | Not living (individually) | The lecture uses these to show that "movement", "growth" and "adaptation" alone are far too weak. |

> **The deeper point the lecture ends on, worth one closing sentence:** perhaps we do not need a strict binary YES/NO categorisation at all, and a **soft transition** between living and not-living would serve better.

#### ✅ `sheet-03` Assignment 8 — *"Discuss which criteria of living are not fully met by Conway's Game of Life?"*

Answer it against your list of five:

- **Metabolism — not met.** Game of Life cells do not take in, convert or release energy or matter; there is no energy budget at all.
- **Growth (ontogenetic development) — not met.** An individual pattern does not develop through a life cycle; it either persists, oscillates, moves, or dies.
- **Phylogenetic development — not met.** There is no mutation and no selection, so no evolution of the population of patterns.
- **Reaction to the environment — only trivially met.** A cell "reacts" to its neighbours, but there is no environment external to the automaton and no adaptation.
- **Reproduction — partly met.** A glider gun genuinely produces new gliders, and self-replicating patterns exist, so this criterion is the one Game of Life comes closest to satisfying.
- **Existence in space and time, movement out of itself, information storage — met.** Patterns occupy positions, gliders move under their own rule, and the configuration is its own description.

> Conclusion sentence: Game of Life satisfies the *structural* and *dynamic* criteria but fails the *energetic* and *evolutionary* ones, which is exactly why it is **weak** Artificial Life.

#### ✅ `sheet-01` Assignments 2 and 3

- **A2** (cite a definition not from the lecture) and **A3** (choose 4–6 criteria you find most feasible) are **admission-only**; A3's *reasoning* is however good exam rehearsal — argue for metabolism, reproduction and information storage as necessary, and admit that movement and growth are not.

---

### 1.3 Langton's Ant

> **POOL 4/4 — 2017 Q7, `qn-02` 10, `qn-03`, `qn-01` T3.** Two variants have been asked; **learn both**.

The exact wordings:

- *"Name the 4 micro behaviors of Langton's Ant and give a short scribble visualization for each of them."* (2025 T3 — **note "for each of them": four separate drawings are required**)
- *"Explain the 4 steps of microbehaviour of Langton's Ant, support your explanation by a drawing of each step."* (2023, `qn-02` 10)
- *"Compare the resulting patterns and behavior … starting on a uniform white plane vs a uniform black plane."* (2017 Q7, = `sheet-01` Assignment 6)

#### The definition — say all of this before you draw

Langton's Ant is a **2-dimensional, rectangular grid** in which:

- each **cell** has a binary state $\{O, I\}$, equivalently $\{$white, black$\}$;
- the **ant** has a spatial position $(x,y)$ **and a heading** from $\{N, E, S, W\}$;
- the ant can **move** one cell in its heading, **turn** by $+90°$ or $-90°$, and **flip** the state of the cell it stands on.

The rule is two lines:

- **At a white cell:** turn **90° right**, flip the cell, move forward one step.
- **At a black cell:** turn **90° left**, flip the cell, move forward one step.

#### The four micro-behaviours — **scan → turn → flip → move**

This is the answer to the 4/4 question, and each of the four needs its own sketch. Memorise the order: **scan, turn, flip, move.**

```
   (1) SCAN                 (2) TURN                (3) FLIP                (4) MOVE

   . . . . .              . . . . .              . . . . .              . . . . .
   . . . . .              . . . . .              . . . . .              . . . . .
   . . ^ . .              . . > . .              . . > . .              . . # > .
   . . . . .              . . . . .              . . . . .              . . . . .
   . . . . .              . . . . .              . . . . .              . . . . .
       ^                      ^                      ^                      ^
   read the state         turn 90° R because    invert the cell        step one cell
   of the cell the        the cell was WHITE    under the ant          forward along
   ant stands on          (90° L if BLACK)      (white -> black)       the new heading
```

Write one sentence under each panel:

1. **Scan** — the ant reads the state of the cell it is currently standing on. This is the only input it ever gets; it has no other sensor and no memory.
2. **Turn** — the ant rotates **90° to the right if the cell is white** and **90° to the left if the cell is black**. Only the heading changes here; the position does not.
3. **Flip** — the ant inverts the state of the cell it is standing on: white becomes black, black becomes white. This is the ant's only way of writing to the world.
4. **Move** — the ant advances exactly one cell in its (new) heading.

> **Marking tip:** the turn direction depends on the colour, and that dependency is the single most likely thing to be marked. Put "white ⇒ right, black ⇒ left" in words next to the drawing, not just in the picture.

#### The first four steps, drawn — practise this exactly

Start on an all-white plane, ant at the centre facing **North**.

```
  t=0                t=1                t=2                t=3                t=4

. . . . .          . . . . .          . . . . .          . . . . .          . . . . .
. . . . .          . . . . .          . . . . .          . . . . .          . . . . .
. . ^ . .          . . # > .          . . # # .          . . # # .          . . ^ # .
. . . . .          . . . . .          . . . v .          . . < # .          . . # # .
. . . . .          . . . . .          . . . . .          . . . . .          . . . . .

ant on white       flipped it to      flipped it to      flipped it to      the 2x2 block
facing N           black, turned      black, turned      black, turned      is closed; the
                   R to E, moved      R to S, moved      R to W, moved      ant now stands
                   one cell E         one cell S         one cell W         on BLACK again
```

At $t=4$ the ant is back where it started, on a **black** cell, so at the next step it turns **left** instead of right and the neat square breaks open. That is the moment the pattern stops being trivial — a good sentence to write.

#### The three macroscopic phases (uniform white plane)

> This is `sheet-01` Assignment 5 and the second half of several exam answers. **Use the lecture's numbers.**

```
 number of
 black cells
     ^
     |                                                    /
     |                                                  /  <- Phase 3: HIGHWAY
     |                                                /       perfectly regular,
     |                                              /         repeating, unbounded
     |                         ~~~~~~~~~~~~~~~~~~~/
     |                    ~~~~~                          <- Phase 2: CHAOTIC
     |               ~~~~~                                  irregular growth,
     |          ~~~~                                        no visible structure
     |    /\/\/                                          <- Phase 1: SYMMETRIC
     |  /                                                   small, near-symmetric
     +--+--------------------+------------------------------> t
        ~420                ~10 000
```

| Phase | Roughly when | What it looks like |
|---|---|---|
| **1 — Symmetric growth** | up to step **≈ 420** | The pattern is small and **almost symmetric**; each step is easy to follow by hand. |
| **2 — Chaotic growth** | ≈ step **400 to 10 000** | The region keeps growing but **no structure is distinguishable**; the lecture calls it **deterministic chaos** — irregular, yet not random at all. |
| **3 — Highway** | from ≈ step **10 000** onwards | A **highly structured, repetitive pattern (the "highway")** suddenly emerges, is **persistent**, and repeats with a **cycle time of 104 steps**, carrying the ant off to infinity in a fixed diagonal direction. |

> ⚠️ **Number check.** `lect-01` says phase 1 runs to *about step 420* and phase 2 from *about 400 to 10 000*. Some sources (and an earlier version of my own notes) say "the first 500 steps". **Quote the lecture: ≈420, ≈10 000, and highway period 104.** The 104 is the number most likely to be marked, so make sure it appears.

Add the lecture's own comment, which is worth a mark on an "explain" question:

> Although the rule is simple and every single step is comprehensible, the **short-term behaviour is hard to impossible to predict**, and the **mid-term behaviour resists prediction entirely**. The only way to know the state of the grid after a given time $t$ is to **run the simulation** and watch it. This is the essential lesson: determinism does not imply predictability.

#### ✅ Variant: white plane vs black plane — 2017 Q7 (= `sheet-01` A6)

*"Compare the resulting patterns and behaviour that Langton's Ant shows for case A: starting on a uniform white plane, with case B: starting on a uniform black plane."*

**The answer is that the two are mirror images of each other, with identical statistics.**

- The rule is **colour-symmetric**: swapping the two colours swaps "turn right" with "turn left" and leaves everything else untouched.
- Therefore, starting on an all-**black** plane produces exactly the **mirror image** (left–right reflected) of the all-white trajectory.
- **All three phases still occur, in the same order, at the same step counts**, and the highway still has **period 104** — it simply runs off in the mirrored diagonal direction.
- The colours of the trail are inverted: where case A leaves black marks on white, case B leaves white marks on black.

```
   Case A: start on WHITE          Case B: start on BLACK
   first turn is RIGHT             first turn is LEFT

        . . . . .                       # # # # #
        . . # > .                       # # . < #
        . . . . .                       # # # # #

   highway heads one way           highway heads the mirrored way
   -- same 3 phases, same ~420 / ~10 000 / period 104 --
```

> **One-sentence answer:** Because the rule is symmetric under exchanging the two cell states, case B is the mirror image of case A — the same three phases occur at the same times and the highway still has period 104, only reflected and with inverted colours.

#### ✅ `sheet-01` Assignment 7 — starting on a checkerboard (a lovely, drawable result)

*"Imagine Langton's Ant starting in a white square of an (infinite) checkerboard. Depict the first 8 steps."*

On a checkerboard the colours alternate, so the ant alternates **right, left, right, left, …** and the result is a **perfectly regular diagonal staircase** — no chaos, no highway, just a straight march to infinity.

```
  checkerboard, ant starts on a white cell facing N:

  . # . # . #          each pair of steps = one diagonal move NE
  # . # . # .
  . # . # . #                 step 1: white -> turn R (N->E), flip, move E
  # . # . # .                 step 2: black -> turn L (E->N), flip, move N
  . # . # ^ .                 step 3: white -> turn R (N->E), flip, move E
  # . # . # .                 step 4: black -> turn L (E->N), flip, move N
                              ... and so on, for ever

  trace after 8 steps:        the ant has advanced 4 cells NE and left
                              a diagonal trail of inverted cells behind it
        . . . . o
        . . . o .             o = cells the ant flipped
        . . o . .
        . o . . .
        o . . . .
```

- **The behaviour is purely periodic in its micro-behaviour** (a two-step cycle: turn right, turn left) and the ant escapes to infinity along a straight diagonal.
- This also answers **`sheet-01` A10** (*"Is there a starting configuration that generates pure periodic behaviour?"*): the checkerboard gives a perfectly regular, non-chaotic trajectory, so the answer is that **the initial configuration, not the rule, decides whether the behaviour is chaotic**.

#### ✅ `sheet-01` Assignment 8 — why is Langton's Ant a 2-dim Turing machine?

Map it onto the formal definition of a Turing machine, term by term — this is what "refer to the formal definition" means:

| Turing machine | Langton's Ant |
|---|---|
| **Tape** | The 2-dimensional grid (a tape with two dimensions instead of one). |
| **Tape alphabet** | $\{$white, black$\}$, i.e. $\{O, I\}$. |
| **Read/write head** | The ant. |
| **Head position** | The ant's cell $(x,y)$. |
| **Internal state** | The ant's **heading** $\{N, E, S, W\}$ — four states. |
| **Transition function** | The two rules: read the symbol, **write** the flipped symbol, **change state** (turn), **move** one cell. |
| **Halting state** | **None** — the ant never halts. |

- Gajardo, Moreira and Goles (2000) proved that the movement of a **single** Langton's Ant can implement **any Boolean function**, which is the formal statement of its computational power.

#### The RL generalisation (one extra sentence, sometimes asked)

Extend the ant to $k>2$ cell states, e.g. $k=3$ with states $\{0,1,2\}$; on every move the state is **increased by one, cyclically**. The rule is then written as a **string of turn directions**, one letter per state:

- **Langton's original ant is `RL`** — turn **R**ight on state 0 (white), **L**eft on state 1 (black).
- Other rules named in the lecture: `RLR`, `LLRR`, `RRLLLRLLLRRR`. Different strings give wildly different long-term behaviour — some produce highways, some produce symmetric growth for ever, some fill space chaotically.

#### 📝 Drill — Langton's Ant

Draw, blind, on paper: **(a)** the four micro-behaviour panels with captions; **(b)** the $t=0..4$ evolution on a white plane; **(c)** the three-phase sketch with ≈420, ≈10 000 and period 104 marked. Target: 5 minutes total.

---

## PART 2 — Cellular Automata in one dimension (`lect-02`)

### 2.1 What a Cellular Automaton is — the five-part definition

> **FOUNDATION.** Not asked alone, but every CA question begins by assuming it, and the 10-point Game-of-Life question expects you to open with it.

A Cellular Automaton is a **discrete model of information processing** — discrete in **space, time and value** — and **deterministic**. CAs are often called **NON-von-Neumann computers**, because their architecture is not the classical von Neumann architecture. (The irony worth one sentence: the first scientific work on them was von Neumann's own, *"Theory and Organisation of Complicated Automata"*, 1949, with Stanislav Ulam and Arthur Burks. **Stephen Wolfram** began the systematic study of the 1-dimensional case in **1982**.)

**A Cellular Automaton consists of exactly five things. Memorise this list — it is the skeleton of every CA answer:**

1. **A lattice of cells** — a regular grid with a specific topology. $d=1$ is a chain of adjacent cells; $d=2$ is a rectangular grid covering the plane; $d>2$ is possible but very unusual.
2. **A neighbourhood** — the set of cells whose states are consulted, normally those within a **radius $r$** of the cell.
3. **A finite set of states (an alphabet)** — of size $k$. Very often $k=2$ with $\{0, I\}$, sometimes called $\{$dead, alive$\}$. States need not be numbers; they may be letters, items or colours.
4. **An initial state** — the states of all cells at $t=0$.
5. **A rule (transition rule)** — determining the next state of a cell from the states of its neighbourhood.

Two properties to state alongside:

- The rule is applied **synchronously**: every cell is updated for $t+1$ **at the same time**, using **only** states from $t$. (Never update in place — that is the classic implementation bug and a classic exam trap.)
- A CA is **homogeneous** if all cells obey the same rule, have the same neighbourhood and the same set of states.

#### The neighbourhood in $d=1$, drawn

```
  d=1, r=1                       d=1, r=2

   ... [i-1][ i ][i+1] ...        ... [i-2][i-1][ i ][i+1][i+2] ...
        \____ ___/                      \________ ________/
             V                                   V
        n = 3 cells                         n = 5 cells
```

- The neighbourhood of cell $i$ is $\{\,i-r,\ \ldots,\ i-1,\ i,\ i+1,\ \ldots,\ i+r\,\}$.
- **The cell $i$ itself is part of its own neighbourhood.**
- The neighbourhood **without** the cell itself is called the **periphery**.
- The size is
  $$n = 2r + 1$$
  where $r$ is the neighbourhood radius and $n$ the number of cells consulted. Typical values are $r=1$ and $r=2$; $r=0$ is unusual but explicitly allowed.

#### The three usual initialisations

1. **By random** — every cell's state is set randomly. (This is what you use to determine the Wolfram *class*.)
2. **As a seed** — exactly one cell is set, all others are 0.
3. **An initial pattern** chosen for investigation.

---

### 2.2 The rule table, and counting rules

> **POOL 2/4 — 2017 Q8, `qn-01` T9.** Also `sheet-02` Assignments 1 and 5.

#### The rule as a table

For $d=1, r=1, k=2$ the neighbourhood has $n = 2\cdot1+1 = 3$ cells, each with $k=2$ possible states, so there are $2^3 = 8$ possible neighbourhood configurations. The rule must map **each** of them to one output state. **Always write the eight patterns in descending binary order** — this ordering is what makes the Wolfram number work:

```
 neighbourhood at t:   111   110   101   100   011   010   001   000
                        |     |     |     |     |     |     |     |
 new state a_i(t+1):    o7    o6    o5    o4    o3    o2    o1    o0
```

Drawn the way the lecture draws it, with cells:

```
  ###   ##.   #.#   #..   .##   .#.   ..#   ...
   |     |     |     |     |     |     |     |
   o7    o6    o5    o4    o3    o2    o1    o0
```

#### Counting the rules — the derivation the exam wants

Two quantities, and you must keep them apart, because confusing $L$ with $Z$ is the standard way to lose this question:

$$L = k^{\,n} = k^{\,2r+1} \qquad\qquad Z = k^{\,L} = k^{\,k^{2r+1}}$$

- $k$ is the number of states one cell may take.
- $n = 2r+1$ is the number of cells in the neighbourhood.
- $L$ is the number of **lines in the rule table** — one line per possible neighbourhood configuration. There are $k$ choices for each of the $n$ neighbourhood cells, hence $k^n$ combinations.
- $Z$ is the number of **possible rules**. Each of the $L$ lines can be filled **independently** with any of the $k$ output states, so there are $k$ choices repeated $L$ times, hence $k^L$.

**Worked check, $d=1, r=1, k=2$:** $n = 3$, $L = 2^3 = 8$, $Z = 2^8 = 256$. There are 256 rules — this is why Wolfram numbers run 0…255.

**The lecture's other examples:**

- $d=1, r=2, k=2$: $n = 5$, $L = 2^5 = 32$, $Z = 2^{32} = 4$ Giga.
- $d=1, r=2, k=8$: $L = 8^5 = 32768$, $Z = 8^{32768}$.

> The point the lecture draws from this, worth a closing sentence: the number of rules is **tremendous even in the one-dimensional case**, so investigating or testing all rules systematically is **by no means thinkable**.

#### Neighbourhood sizes in higher dimensions — needed for the 2025 variant

| Neighbourhood | Size $n$ | Example |
|---|---|---|
| $d=1$, radius $r$ | $n = 2r+1$ | $r=1 \Rightarrow n=3$ |
| $d$-dim **Moore**, $r=1$ | $n = 3^{\,d}$ | $d=2 \Rightarrow n=9$; $d=3 \Rightarrow n=27$ |
| $d$-dim **von Neumann**, $r=1$ | $n = 2d+1$ | $d=2 \Rightarrow n=5$; $d=3 \Rightarrow n=7$ |

Generally, a $d$-dimensional Moore neighbourhood of radius $r$ has $n = (2r+1)^d$ cells.

#### ✅ 2017 Q8 — rule count for $d=1$, $r=3$, $k=4$

$$n = 2r+1 = 2\cdot 3 + 1 = 7$$
$$L = k^{\,n} = 4^{7} = 16\,384$$
$$Z = k^{\,L} = 4^{16\,384}$$

Write all three lines, and say what each is: 7 cells in the neighbourhood, 16 384 lines in the rule table, and $4^{16384}$ possible rules.

#### ✅ 2025 T9 — *"Calculate the number of possible rules and derive a formula for a CA with $d=3$, $k=2$, $r=1$ Moore."*

$$n = 3^{\,d} = 3^{3} = 27$$
$$L = k^{\,n} = 2^{27} = 134\,217\,728$$
$$Z = k^{\,L} = 2^{\,2^{27}} = 2^{134\,217\,728}$$

- The neighbourhood is a $3\times3\times3$ cube of cells, hence $27$ — **draw the cube** and say "$3\times3\times3$, including the centre cell".
- Note the answer is a **power tower**: $Z$ has about $4\times10^7$ decimal digits. Saying so out loud shows you understand the magnitude, which is the point of the question.

#### ✅ `sheet-02` Assignment 1 — the printing-time variant

*"How long would it take to print all $Z$ possible rules for a 1-dim CA with $k=4$ and $r=1$, at 100 rules per second? Set up a formula $Z=Z(r,k)$."*

$$Z(r,k) = k^{\,k^{2r+1}}, \qquad Z(1,4) = 4^{\,4^{3}} = 4^{64} = 2^{128} \approx 3.40\times 10^{38}$$
$$T = \frac{Z}{100\ \text{s}^{-1}} \approx 3.40\times10^{36}\ \text{s} \approx 1.08\times10^{29}\ \text{years}$$

That is roughly $10^{19}$ times the age of the universe. **The expected conclusion is not the number but the moral:** exhaustive search over CA rules is impossible in principle, which is why Wolfram classified *behaviours* instead of enumerating rules.

#### ✅ `sheet-02` Assignment 5 — the four restricted counts

Derive each; do not just quote it.

| | Formula | Why |
|---|---|---|
| **a) all rules** | $Z = k^{\,k^{2r+1}}$ | $L = k^{2r+1}$ lines, each independently filled with one of $k$ states. |
| **b) peripheral** | $Z_p = k^{\,k^{2r}}$ | The centre cell is ignored, so the neighbourhood effectively has $2r$ cells, giving $k^{2r}$ table lines. |
| **c) totalistic** | $Z_t = k^{\,n(k-1)+1} = k^{\,(2r+1)(k-1)+1}$ | The output depends only on the **sum**, which runs from $0$ to $n(k-1)$ — that is $n(k-1)+1$ distinct sums, i.e. $n(k-1)+1$ table lines. |
| **d) silent state** | $Z_s = k^{\,L-1} = k^{\,k^{2r+1}-1}$ | One line (the all-zero neighbourhood) is **forced** to output 0, leaving $L-1$ free lines. |

Sanity-check with $d=1,r=1,k=2$: $Z=256$, $Z_p = 2^{4} = 16$, $Z_t = 2^{3\cdot1+1} = 2^4 = 16$, $Z_s = 2^{7} = 128$ — exactly half of all rules have a silent state, which is the expected answer.

---

### 2.3 Rule properties

> **POOL 2/4 — `qn-01` T17, `qn-02` 17** (the totalistic-and-silent proof). Also `sheet-02` A2 and A4, and `sheet-03` A2.

Wolfram proposed five terms for grouping rules. **Learn the definitions verbatim; the proof question is won or lost on the definitions.**

| Property | Definition | Test |
|---|---|---|
| **Silent state** | A rule has a silent state if the neighbourhood with **all cells unset (state 0)** is mapped onto state **0**. | Look at the last line, $00\ldots0 \to ?$ |
| **Symmetric** | A rule is symmetric if a neighbourhood and its **mirror image** yield the same next state. | For $r=1$: check the pairs $(110, 011)$ and $(100, 001)$. The patterns $111$, $010$, $101$, $000$ are their own mirror image, so they are automatically fine. |
| **Legal** | A rule is legal if it is **symmetric AND has a silent state**. Both, not either. | Do the two tests above. |
| **Peripheral** | A rule is peripheral if the **state of the cell itself does not influence** the result — only the periphery matters; the centre is "don't care". | For $r=1$: check that $111{\to}101$, $110{\to}100$, $011{\to}001$, $010{\to}000$ each give the **same** output. |
| **Totalistic** | A rule is totalistic if **only the sum of the set cells in the neighbourhood** determines the next state. | Group the lines by $\text{SUM}$ and check each group is constant. |

The sum is
$$\text{SUM}(t) = a_{i-r}(t) + \ldots + a_{i-1}(t) + a_i(t) + a_{i+1}(t) + \ldots + a_{i+r}(t)$$
and for $k>2$, or for non-numeric states, **SUM typically denotes the number of cells that are "set"** — that is, not in the silent state.

A totalistic rule's table is short, because it is indexed by the sum, not by the pattern:

```
  d=1, r=1, k=2                 d=1, r=2, k=2
  SUM(t)     3  2  1  0         SUM(t)     5  4  3  2  1  0
  a_i(t+1)   I  0  0  I         a_i(t+1)   I  0  I  0  0  I
```

**Why the "silent state" matters conceptually:** when all cells of the CA are unset, the CA **remains calm** — the silent state persists, so an empty universe stays empty. Without it, an empty grid would spontaneously light up everywhere.

#### ✅ THE PROOF QUESTION — `qn-01` T17 / `qn-02` 17 / `sheet-02` A2

*"Is the following statement true or not? 'A totalistic rule with silent state is legal.'"* (2025 T17)
*"Is a totalistic rule with a silent state always legal? (Proof)"* (2023)
*"Prove or disprove: All totalistic rules are legal, because they are symmetric and have a silent state."* (`sheet-02` A2 — **note the different claim**)

**Answer to the exam version: TRUE.** Write the proof as three numbered steps — that structure is what earns the marks:

1. **What must be shown.** By definition, a rule is **legal** if and only if it is **symmetric** and **has a silent state**. The silent state is given by assumption. So it remains only to show that **totalistic $\Rightarrow$ symmetric**.
2. **Totalistic $\Rightarrow$ symmetric.** A totalistic rule's output depends **only** on $\text{SUM}(t)$, the sum over the neighbourhood cells. Addition is **commutative**, so any reordering of the neighbourhood cells — in particular **mirroring** it — leaves the sum unchanged:
   $$\text{SUM}(a_{i-r},\ldots,a_{i+r}) = \text{SUM}(a_{i+r},\ldots,a_{i-r})$$
   Equal sums must map to equal outputs, so a neighbourhood and its mirror image yield the same next state. That is exactly the definition of **symmetric**.
3. **Conclude.** The rule is symmetric (step 2) and has a silent state (assumption), therefore it is **legal**. $\blacksquare$

> ⚠️ **The `sheet-02` version is a different claim and the answer is different.** It asserts *all* totalistic rules are legal "because they are symmetric **and have a silent state**". The first half is true — **all** totalistic rules are symmetric, by step 2 above. The second half is **false**: nothing forces a totalistic rule to map $\text{SUM}=0$ to state $0$. **Counterexample:** the $d=1,r=1,k=2$ totalistic rule with table $\text{SUM}=3{\to}0,\ 2{\to}0,\ 1{\to}0,\ 0{\to}I$ is totalistic but maps the empty neighbourhood to $I$, so it has **no** silent state and is **not legal**. Hence *"all totalistic rules are legal"* is **disproved**, while *"a totalistic rule **with** a silent state is legal"* is **proved**. Read which one you were asked, and say which one you are answering.

#### ✅ `sheet-02` Assignment 4 — classify eight Wolfram numbers

*"Depict the tables for the ($d=1, r=1, k=2$) rules given by the decimal Wolfram numbers (0, 17, 42, 51, 110, 165, 204, 243), and classify each as legal, symmetric, totalistic or peripheral."*

Convert each number to 8 bits and read them against `111 110 101 100 011 010 001 000`:

| Rule | Binary | 111 | 110 | 101 | 100 | 011 | 010 | 001 | 000 | silent | symm. | legal | periph. | totalistic |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| **0** | 00000000 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | ✔ | ✔ | ✔ | ✔ | ✔ |
| **17** | 00010001 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 1 | ✘ | ✘ | ✘ | ✘ | ✘ |
| **42** | 00101010 | 0 | 0 | 1 | 0 | 1 | 0 | 1 | 0 | ✔ | ✘ | ✘ | ✘ | ✘ |
| **51** | 00110011 | 0 | 0 | 1 | 1 | 0 | 0 | 1 | 1 | ✘ | ✔ | ✘ | ✘ | ✘ |
| **110** | 01101110 | 0 | 1 | 1 | 0 | 1 | 1 | 1 | 0 | ✔ | ✘ | ✘ | ✘ | ✘ |
| **165** | 10100101 | 1 | 0 | 1 | 0 | 0 | 1 | 0 | 1 | ✘ | ✔ | ✘ | ✔ | ✘ |
| **204** | 11001100 | 1 | 1 | 0 | 0 | 1 | 1 | 0 | 0 | ✔ | ✔ | ✔ | ✘ | ✘ |
| **243** | 11110011 | 1 | 1 | 1 | 1 | 0 | 0 | 1 | 1 | ✘ | ✘ | ✘ | ✘ | ✘ |

Show your working for at least one, since the sheet says *"your solution shall show how the Wolfram numbers and the table are connected"*. Useful identities to mention:

- **Rule 0** maps everything to 0 — it satisfies every property trivially, which makes it the ideal sanity check.
- **Rule 51** is "**invert the centre cell**" — symmetric (the neighbours are irrelevant), but $000 \to I$, so no silent state and **not legal**.
- **Rule 165** is "**XNOR of the two neighbours**" — the centre is ignored, so it is **peripheral**, and it is symmetric; but $000 \to I$, so not legal. It is the bitwise complement of rule 90.
- **Rule 204** is the **identity** (output = centre cell). Symmetric and silent, hence **legal**, but obviously not peripheral.
- **Rule 110** is the famous one: a **class IV** rule, later proved **Turing-complete**. Worth naming.

---

### 2.4 The Wolfram number

> **POOL 4/4 — 2017 Q5, `qn-02` 6, `qn-03`, `qn-01` T1 (as a 10-pointer).** Also `sheet-02` A4, orals A, C, E. **Learn it in both directions.**

The exact wordings:

- *"Give a rule table for the Wolfram number $42_D$ with $d=1$, $r=1$, $k=2$."* (2023, `qn-02` 6)
- *"Write down the ruleset for the Wolfram number $42_D$."* (2023, `qn-03`)
- *"Name all possible Wolfram Numbers that produce the following $d=1,k=2,r=1$ patterns. Explain how you calculated the numbers."* (2025 T1, **10 points** — the reverse direction)

#### The definition

For $d=1$, $r=1$, $k=2$ the right-hand side of the rule table is a binary vector of $L=8$ entries, so there are $Z = 2^8 = 256$ rules and a binary numbering suggests itself. **Each output state is identified with a power of 2**, with the neighbourhood $111$ carrying the **most significant bit**:

```
 neighbourhood:  111   110   101   100   011   010   001   000
                  |     |     |     |     |     |     |     |
 weight:         2^7   2^6   2^5   2^4   2^3   2^2   2^1   2^0
                 128    64    32    16     8     4     2     1
```

The lecture's own worked example, **rule 90**:

```
 111  110  101  100  011  010  001  000
  0    I    0    I    I    0    I    0

 = 0*128 + 1*64 + 0*32 + 1*16 + 1*8 + 0*4 + 1*2 + 0*1
 = 64 + 16 + 8 + 2
 = 90_D  =  0I0II0I0_B  =  5A_HEX
```

#### ✅ Forward direction — write the table for $42_D$

Work it explicitly; the marks are in the working, not the answer.

$$42 = 32 + 8 + 2 = 2^5 + 2^3 + 2^1$$

So the bits at weights $2^5$, $2^3$ and $2^1$ are set — which are the neighbourhoods $101$, $011$ and $001$:

```
 42_D = 0 0 1 0 1 0 1 0_B

 neighbourhood at t:  111  110  101  100  011  010  001  000
 new state a_i(t+1):   0    0    I    0    I    0    I    0

 drawn as cells:

   ###   ##.   #.#   #..   .##   .#.   ..#   ...
    |     |     |     |     |     |     |     |
    .     .     #     .     #     .     #     .
```

**Then classify it, because the follow-up is standard and free:**

- **Silent state?** $000 \to 0$. **Yes.**
- **Symmetric?** Check the mirror pairs: $110 \to 0$ but $011 \to I$. **No.**
- **Legal?** Needs symmetric *and* silent. **No** — it fails symmetry.
- **Totalistic?** $\text{SUM}=2$ arises from $110{\to}0$, $101{\to}I$, $011{\to}I$ — not constant. **No.**
- **Peripheral?** $111 \to 0$ but $101 \to I$, so the centre matters. **No.**

> Rule 42 has a silent state and nothing else. Say exactly that.

#### ✅ Reverse direction — 2025 T1, the 10-point version

*"Name all possible Wolfram Numbers that produce the following patterns (three rows: $t=0$, $t=1$, $t=2$). Explain how you calculated the numbers."*

⚠️ The protocol did not preserve the actual grids, so **the specific numbers cannot be reproduced here.** What matters is the method, which transfers to whatever picture appears. Learn the procedure:

**The method, in five steps:**

1. **Write the three rows one under the other**, aligned by column, and mark the cell positions.
2. **For every cell of row $t{+}1$, read off its neighbourhood in row $t$** (the cell itself plus one neighbour on each side). Each such reading gives you one **constraint**: "neighbourhood $abc$ must map to output $o$".
3. **Collect the constraints in the standard 8-row table.** Several cells usually give the *same* neighbourhood — check they agree; if two cells give the same neighbourhood but different outputs, **no rule produces the picture** and that is the answer.
4. **Count the unconstrained lines.** If the picture pins down $m$ of the 8 neighbourhoods, then $8-m$ lines are free, and each can be $0$ or $I$ independently, so there are
   $$2^{\,8-m}$$
   Wolfram numbers consistent with the picture.
5. **Report them properly.** Write the fixed bits, mark the free ones with $\times$, and then either list all $2^{8-m}$ numbers or give them as "base number $+$ any subset of these weights".

**Worked illustration of the reporting format.** Suppose the picture constrains five lines and leaves $110$, $010$ and $001$ free:

```
 neighbourhood:  111  110  101  100  011  010  001  000
 output:          0    x    I    0    I    x    x    0
 weight:         128   64   32   16    8    4    2    1

 fixed part  = 32 + 8 = 40
 free weights = 64, 4, 2   ->  2^3 = 8 possible rules

 the 8 numbers = 40, 42, 44, 46, 104, 106, 108, 110
                 (40 + any subset of {64, 4, 2})
```

**Two remarks that earn marks:**

- Say **why** cells at the edges of the pattern give constraints too: an all-white region tells you $000 \to 0$, which is usually the first constraint you can extract.
- Say explicitly that the free lines are free **because the given initial pattern never presents those neighbourhoods** — the picture simply contains no information about them.

#### The $r=2$ variant (oral C — be ready, it is easy if you saw it coming)

Oral C asked for $d=1, k=2, \mathbf{r=2}$ with Wolfram number $\mathbf{65538}$.

- $n = 2r+1 = 5$, so the table has $L = 2^5 = \mathbf{32}$ lines, not 8, and there are $Z = 2^{32}$ rules.
- $65538 = 65536 + 2 = 2^{16} + 2^{1}$.
- So **exactly two** of the 32 lines output $I$: the ones at weights $2^{16}$ and $2^{1}$. Index the 32 neighbourhoods from $11111$ (weight $2^{31}$) down to $00000$ (weight $2^0$); weight $2^{16}$ is the neighbourhood whose binary index is $16 = 10000_B$, and weight $2^1$ is index $1 = 00001_B$.
- **The moral to state:** the Wolfram numbering is not restricted to $r=1$; it is just "read the output column as a base-$k$ number", and the table simply gets longer.

#### Rule 90 evolution from a seed — a drawing worth practising

Rule 90 is **XOR of the two neighbours** (the centre is ignored, so rule 90 is **peripheral**). From a single seed it draws the **Sierpiński triangle**, which is the standard illustration of self-similarity emerging from a trivial rule:

```
 t=0    . . . . . . . # . . . . . . .
 t=1    . . . . . . # . # . . . . . .
 t=2    . . . . . # . . . # . . . . .
 t=3    . . . . # . # . # . # . . . .
 t=4    . . . # . . . . . . . # . . .
 t=5    . . # . # . . . . . # . # . .
 t=6    . # . . . # . . . # . . . # .
 t=7    # . # . # . # . # . # . # . #
```

---

### 2.5 Boundary conditions

> **⚪ LOW PRIORITY — never on a written paper.** Know the first four by name and one sentence; the last three are explicitly "specialised applications". Do not spend more than 5 minutes here.

Real CAs have finite grids, so something must be said about the edges. The lecture lists seven, and calls **the first four the typical ones**:

1. **Virtually infinite (no boundary)** — make the grid larger than the space you expect to need, or enlarge it on demand. Reasonable when the initial state is a seed or a small pattern; needs smart memory management.
2. **Periodic / cyclic topology** — wrap the grid around, gluing each edge to the opposite one. Easiest to implement: do all index arithmetic **modulo** the grid size. In $d=1$ a **line becomes a ring**; in $d=2$ a **rectangle becomes a torus**; in $d=3$ a block becomes a hyper-torus.
3. **Fixed boundary** — set the border cells to a predefined value and never update them. The border must be at least $r$ cells thick so no neighbourhood contains an undefined cell. Using the **silent state** is often the good choice.
4. **Random boundary** — a special case of fixed, with random values.
5. **Adiabatic boundary (copy/mirror)** — extend the grid by $r$ cells that mirror the cells just inside the boundary.
6. **Open boundary (absorbing)** — signals leave and do not return.
7. **Closed boundary (reflecting)** — signals bounce back.

The last three "require deeper knowledge of the dynamical properties being modelled" and appear only in specialised applications such as diffusion processes or soliton behaviour.

```
   d=1 cyclic:  the chain closes into a ring

        [0]-[1]-[2]-[3]-[4]
         |                 |
         +-----------------+     index arithmetic mod 5
```

---

### 2.6 Wolfram's four classes of behaviour

> **POOL 2/4 — `qn-02` 12, `qn-01` T15.** Also `sheet-02` A6. The question is almost always **class III vs class IV**.

The exact wordings:

- *"Explain the difference and similarities between Type 3 and 4 classes of CA."* (2023, `qn-02` 12)
- *"Explain what Wolfram's class 3 and class 4 are, how they differ and what they have in common."* (2025 T15)

#### How the classification is made — say this first, it is an easy mark

To determine the class of a CA, the automaton is **initialised with a random pattern and iterated for a long time**; this is **repeated for several random initialisations**, and the typical resulting dynamics is then classified. The classes are **to some extent aligned with observations from nonlinear dynamical systems theory**.

#### The four classes, with sketches

```
 CLASS I - Homogeneous            CLASS II - Periodic
 ####...##.#..##.#.               #..#..#..#..#..#.
 ..#.....#.....#..                #..#..#..#..#..#.
 .................                #..#..#..#..#..#.
 .................                #..#..#..#..#..#.
 .................                #..#..#..#..#..#.
 everything dies to one           settles into stable or
 uniform state (mostly silent)    oscillating local patterns


 CLASS III - Chaotic              CLASS IV - Complex / Self-Organisation
 #.##..#.#.###..#.                ....#.......##...
 ##.#.###..#..###                 ...#.#......##...
 #..####.#.##.#.#                 ....##.....##....
 .##.#..###.#..##                 .......#..##.....
 ###..##.#..###.#                 ......#.#..#.....
 random-looking for ever,         localised structures persist,
 no periodicity, no structure     move, collide and create new ones
```

| Class | Name | Characteristic |
|---|---|---|
| **I** | **Homogeneous** | The CA reaches a **homogeneous state for all cells**, mostly the silent state. Everything dies out. |
| **II** | **Periodic** | **Periodic, oscillatory patterns**, including stable (fixed) patterns. Structures are local and repeat. |
| **III** | **Chaotic** | **Deterministic chaos** — no periodicity is observable. |
| **IV** | **Complex, Patterns, "Self Organisation"** | **Interesting structures evolve, persist, seem to interact, and generate new structures.** |

#### ✅ The answer to "class III vs class IV"

Structure it as **similarities, then differences** — the question always asks for both, and half the marks sit in the "in common" half that candidates skip.

**What they have in common:**

- Both arise from **simple, local, deterministic rules** with no central control.
- Both are **aperiodic** — neither settles into a repeating global cycle, so neither is class I or class II.
- Both look **irregular and complicated** to the eye, and neither can be predicted analytically; the only way to know the state at time $t$ is to run the automaton.
- Both are **sensitive to the initial configuration**.

**How they differ:**

| | **Class III — Chaotic** | **Class IV — Complex** |
|---|---|---|
| **Structures** | No persistent localised structures; the pattern is uniformly random-looking everywhere. | **Localised structures form and persist** — coherent objects like gliders. |
| **Interaction** | Nothing to interact; disturbances simply spread. | Structures **move, collide, interact, and generate new structures**. |
| **Information** | Local information is destroyed — it diffuses into noise. | Local information is **transported and processed** — a glider carries a bit from one place to another. |
| **Position** | Fully disordered. | **Between order and chaos** — the "edge of chaos", between class II and class III. |
| **Computation** | No computation. | Supports **universal computation** (Rule 110; Conway's Game of Life). |
| **Example** | Rule 30, and the logistic map at $a=4$. | **Rule 110**, and **Conway's Game of Life**. |

> **The one-sentence discriminator to write:** both are aperiodic and unpredictable, but class III destroys local structure into uniform noise, whereas class IV supports **persistent, moving, interacting structures** which is what makes class IV capable of computation.

#### ✅ `sheet-02` Assignment 6 — explain the four classes to a non-expert, max two sentences each

- **Class I — Homogeneous.** Whatever you start with, the whole grid collapses to a single uniform state, usually all-empty. It is the CA equivalent of everything dying out.
- **Class II — Periodic.** The grid settles into small local patterns that either stay frozen or blink between a few configurations for ever. Nothing new ever happens after the settling.
- **Class III — Chaotic.** The grid keeps changing in a way that looks random for ever, with no repetition and no recognisable objects, even though the rule is completely deterministic.
- **Class IV — Complex.** Recognisable structures appear, survive, travel across the grid and collide to make new structures, so the automaton sits between frozen order and pure noise — and this is the class in which computation becomes possible.

---

## PART 3 — Cellular Automata in two dimensions & Conway's Game of Life (`lect-03`)

### 3.1 Two-dimensional CAs

> **FOUNDATION** for the Game of Life question. The 2-dim neighbourhood drawing is worth memorising because it also appears in the rule-count question.

**History, one sentence:** although Wolfram investigated the 1-dim case intensively, the **original idea from Stanislav Ulam (1940) and John von Neumann was a 2-dimensional cellular automaton**. In the 1950s and 60s CAs were the basis for a series of analogue computers, and in **1969 Konrad Zuse** published (from 1940s ideas) *"Rechnender Raum"*, proposing that the laws of nature are discrete and work like a CA.

#### The two neighbourhoods — draw these exactly

```
     r = 1, von Neumann              r = 1, Moore

         . # .                          # # #
         # C #                          # C #
         . # .                          # # #

      n = 2d+1 = 5 cells             n = 3^d = 9 cells
      (C plus the 4 edge-           (C plus all 8 surrounding
       adjacent neighbours)          cells, edges and corners)
```

- **von Neumann**: the cell plus the four cells sharing an edge. In $d$ dimensions with $r=1$, $n = 2d+1$.
- **Moore**: the cell plus all eight cells sharing an edge **or a corner**. In $d$ dimensions with $r=1$, $n = 3^d$.
- A **larger radius** requires a more precise definition of which cells count; for $r=2$ Moore the neighbourhood is the full $5\times5$ block, $n=25$.

CAs extend easily to **higher dimensions** (e.g. 3-dim), to **different tilings** (triangles or hexagons in 2-dim), or even to a **non-uniform neighbourhood** (a graph). **Only the definition of the neighbourhood and the rule has to be adjusted accordingly** — that sentence is the whole point of the extension slide.

#### Applications of CAs (a one-line list, occasionally asked as a warm-up)

Growth of crystals; population dynamics; modelling and predicting traffic situations; modelling urban city development; modelling diffusion processes; generating "close to real" patterns; modelling forest fires.

**Majority-voting CA** — the lecture's simple 2-dim example: $d=2$, rectangular grid, $r=1$ **Moore**, $k=4$. The cell changes to **the majority of the states present in its neighbourhood**.

#### Non-deterministic CAs

As an extension of the classical deterministic rule, **the transition from one state to the next can have a stochastic component**: instead of one guaranteed successor state, a state goes to one of several successors with given probabilities $a$, $b$, $1-(a+b)$.

```
                 a
        a_i(t) -----> a_i(t+1)
           |    b
           +-------> a'_i(t+1)
           |  1-(a+b)
           +-------> (unchanged)
```

This is what makes the forest-fire model possible, since spontaneous growth and spontaneous ignition are probabilistic events.

---

### 3.2 The forest-fire CA

> **⚪–🟡 Low-to-medium priority here** — the *SOC* aspect belongs to Phase 2 (`lect-06`), but the **CA definition** is `lect-03` and `sheet-03` A1 asks about it directly. Teach it once, here.

**Definition:** $d=2$, rectangular grid, $r=1$, **von Neumann** neighbourhood, $k=3$, a **non-deterministic** cellular automaton.

**The three states:**

- **A** — empty / ashes
- **T** — tree
- **F** — burning tree / fire

**The five transitions — this is the answer to "explain the forest-fire model":**

```
        spontaneous growth (p)        induced fire
   A ---------------------------> T ---------------------> F
   ^                              ^  (a tree burns if at    |
   |                              |   least one neighbour   |
   |    induced growth (q)        |   burns)                |
   |  (a tree grows if at least   |                         |
   |   one neighbour is a tree)   |    spontaneous fire (f) |
   |                              +-------------------------+
   |                                                        |
   +--------------------------------------------------------+
                     fire turns into ashes
```

1. **Fire turns into ashes:** $F \to A$, deterministically, every step.
2. **Spontaneous growth:** $A \to T$ with probability $p$.
3. **Spontaneous fire:** $T \to F$ with probability $f$ (lightning).
4. **Induced fire:** a tree burns if **at least one neighbour burns**.
5. **Induced growth:** a tree grows if **at least one neighbour is a tree**, with rate $q$.

**The control parameters are $p$, $f$ and $q$.** The lecture's guidance:

- $q = 0$ (no induced growth) is a **good setting to start from**.
- **Interesting (fractal) behaviour arises when $f \ll p$**, e.g. $p/f = 100$.

(References: Drossel & Schwabl 1992, *"Self-organized critical forest-fire model"*; Chen, Bak & Jensen 1990.)

#### ✅ `sheet-03` Assignment 1

*"Take the 2-dim forest fire CA with a low rate for spontaneous growth $p \ll 1.0$ and a large induced growth rate $q = 1.0$. Discuss the effect of the rate for spontaneous fire on $Z$, the number of trees, for very small, medium and large values."*

With $q = 1.0$, any tree instantly seeds its neighbours, so **the forest regrows explosively from any surviving tree** and the forest density is governed almost entirely by how often fires start.

| $f$ | Effect on $Z$ (number of trees) |
|---|---|
| **Very small** ($f \ll p$) | The forest fills the grid almost completely, so **$Z$ is large and close to the maximum** for long stretches. But because induced growth has made the forest fully connected, a single lightning strike burns **essentially everything**, so $Z$ collapses to near zero and then refills. The result is **huge fluctuations** and a **power-law distribution of fire sizes** — this is the self-organised critical regime the lecture is aiming at. |
| **Medium** | Fires start often enough to **fragment the forest** into patches before they can merge. $Z$ settles around an **intermediate equilibrium** with moderate fluctuations, and typical fire sizes are moderate — big enough to matter, small enough not to be global. |
| **Large** | Trees ignite almost as soon as they appear, so the forest **never builds up**; $Z$ stays **very low and nearly constant**. The dynamics are dominated by ignition, spatial correlations never form, and there are no large avalanches. |

```
   Z (trees)
     ^
 max |####  ####  ####          <- f very small: nearly full, then
     |#  #  #  #  #  #             catastrophic collapse, refill
     |
     |  ~~~~~~~~~~~~~~~~        <- f medium: intermediate equilibrium
     |
     |____________________      <- f large: forest never establishes
     +---------------------> t
```

> **The point to state:** the interesting, critical, fractal behaviour lives at **$f \ll p$**, exactly where the separation of time scales between slow growth and fast burning is largest.

---

### 3.3 Conway's Game of Life

> **POOL 4/4 — 2017 Q1 (10 pt) & Q17, `qn-02` 1 (10 pt) & 5, `qn-03` (10 pt), `qn-01` T12.** Also oral E, and `sheet-03` A2/A3/A4/A5/A7/A8.
> **This is the single most reliable question on the paper. It has been a 10-pointer on three of four papers.**

The exact wordings:

- *"Explain all parts of Conway's Game of Life with the example of a blinker."* (2023, `qn-03`, **10 pt**)
- *"Explain the Game of Life, every detail of it. Draw the next 2 steps of this pattern and explain the rules of the GoL."* (2023, `qn-02` 1, **10 pt**)
- *"Draw a Game of Life pattern (Glider) that moves to the lower left corner. Draw 4 steps of this pattern."* (2023, `qn-02` 5)
- *"Within the Game of Life there is a pattern called glider. Give an example that moves to the lower-right and draw the 4 time-steps."* (2025 T12 — the paper supplied four $7\times7$ grids labelled $t{=}0 \ldots t{=}3$)

#### The specification — open every answer with this

John H. Conway, British professor of mathematics, proposed it in **1970**. It is **probably the most popular 2-dimensional cellular automaton**.

Conway's Game of Life is a **Cellular Automaton** defined on:

- $d = 2$ — a **2-dimensional rectangular grid**;
- $r = 1$ — a **Moore neighbourhood** (and Moore **periphery**, because the rule distinguishes the cell from its neighbours);
- $k = 2$ — **binary states** for each cell: $O$ = dead, $I$ = alive;
- **the rule is legal** (it is symmetric and has a silent state);
- and the rule **implements concepts from population dynamics**: birth, survival, death from overcrowding, and death from loneliness.

> Getting $d$, $r$, $k$ and "the rule is legal" onto the page **before** you state the rule is what separates a 10/10 from a 7/10. The question says "every detail of it".

#### The rule — Goerke writes it as 23/3

**The lecture's notation is `23/3`, equivalently `S23/B3`:** a cell **S**urvives with 2 or 3 neighbours, and a new cell is **B**orn with 3 neighbours. Spell out all three clauses:

- **Birth:** a cell is born if **exactly 3** neighbouring cells are alive.
- **Survival:** a living cell survives if **2 or 3** neighbouring cells are alive.
- **Death:** a living cell dies **from overcrowding** if **more than 3** neighbours are alive, or **from loneliness** if **fewer than 2** neighbours are alive.

#### The rule as a table — draw this, it is the "every detail" evidence

The lecture presents the rule as two rows indexed by $S_a(t)$, the **number of living cells in the periphery** (the 8 surrounding cells):

```
   S_a(t)                8   7   6   5   4   3   2   1   0
   ------------------------------------------------------------
   if a(t) is DEAD:      O   O   O   O   O   I   O   O   O    <- birth at exactly 3
   if a(t) is ALIVE:     O   O   O   O   O   I   I   O   O    <- survival at 2 or 3
                         \_______________/   \___/   \____/
                            overcrowding    survive  loneliness
```

#### ✅ `sheet-03` Assignment 2 — classify the Game of Life rule

*"Characterize the rule of Conway's Game of Life with respect to: silent state, totalistic, symmetric, peripheral, legal."*

| Property | Verdict | Reason |
|---|---|---|
| **Silent state** | **Yes** | An all-dead neighbourhood has $S_a = 0$ and a dead centre, and maps to dead. An empty grid stays empty. |
| **Symmetric** | **Yes** | The rule depends only on *how many* neighbours are alive, never on *which* ones, so any mirroring or rotation of the neighbourhood gives the same result. |
| **Legal** | **Yes** | Legal $=$ symmetric **and** silent state, and both hold. This is why the lecture states "the rule is legal". |
| **Peripheral** | **No** | The centre cell's own state matters: with exactly 2 living neighbours, a **living** cell survives but a **dead** cell stays dead. |
| **Totalistic** | **No — but outer-totalistic** | A strictly totalistic rule depends only on the **total** sum including the centre. Here total $=4$ arises both from (alive, 3 neighbours) $\to$ **alive** and from (dead, 4 neighbours) $\to$ **dead**, so the total sum does not determine the output. It **is** *outer-totalistic* (semi-totalistic): it depends on the centre state plus the **sum of the periphery** — which is exactly what the two-row table above shows. |

> ⚠️ **This is the one place where a careless "yes, totalistic" loses marks.** State the distinction: **not totalistic, but outer-totalistic.** The two-row table is your proof.

#### The blinker — the 10-point example from `qn-03`

Three cells in a row yield a **periodic structure oscillating with period 2**, called the **Blinker**. The lecture calls it **"the archetype of a periodic class II behaviour"** — use that phrase.

```
      t=0            t=1            t=2  (= t=0)

   . . . . .      . . . . .      . . . . .
   . . . . .      . . # . .      . . . . .
   . # # # .      . . # . .      . # # # .
   . . . . .      . . # . .      . . . . .
   . . . . .      . . . . .      . . . . .
```

**Walk the marker through the reasoning cell by cell — that is what "explain all parts with the example of a blinker" is asking for:**

- The **centre cell** has **2 living neighbours**, so it **survives**.
- The **two end cells** have only **1 living neighbour** each, so they **die of loneliness**.
- The cells **directly above and below the centre** are dead but have **exactly 3 living neighbours** (the three cells of the row), so they are **born**.
- Every other cell has at most 2 living neighbours and stays dead.
- Result: the horizontal bar becomes a vertical bar. By the same argument the vertical bar becomes horizontal again, so **the pattern has period 2**.

#### The glider — draw all four steps, in the direction you were asked for

The **Glider** is **the prototypic class IV pattern**. State its three properties:

- a glider consists of **5 living cells**;
- in **4 steps** it moves **one cell in a diagonal direction**;
- after 4 time steps the **original shape is reconstructed in an adjacent position**, although **all five cells have changed state** in the meantime — so the shape recurs but **the pattern is NOT periodic** (the lecture makes this point explicitly, and even asks "would you consider it to be the same Glider?").

**Glider moving to the LOWER RIGHT** (2017 Q17, 2025 T12) — verified step by step:

```
     t=0              t=1              t=2              t=3              t=4

  . . . . . .      . . . . . .      . . . . . .      . . . . . .      . . . . . .
  . . # . . .      . . . . . .      . . . . . .      . . . . . .      . . . . . .
  . . . # . .      . # . # . .      . . . # . .      . . # . . .      . . . # . .
  . # # # . .      . . # # . .      . # . # . .      . . . # # .      . . . . # .
  . . . . . .      . . # . . .      . . # # . .      . . # # . .      . . # # # .
  . . . . . .      . . . . . .      . . . . . .      . . . . . .      . . . . . .

                                                                   t=4 is t=0 shifted
                                                                   one cell right AND
                                                                   one cell down
```

**Glider moving to the LOWER LEFT** (2023, `qn-02` 5) — the horizontal mirror image:

```
     t=0              t=1              t=2              t=3              t=4

  . . . . . .      . . . . . .      . . . . . .      . . . . . .      . . . . . .
  . . . # . .      . . . . . .      . . . . . .      . . . . . .      . . . . . .
  . . # . . .      . . # . # .      . . # . . .      . . . # . .      . . # . . .
  . . # # # .      . . # # . .      . . # . # .      . # # . . .      . # . . . .
  . . . . . .      . . . # . .      . . # # . .      . . # # . .      . # # # . .
  . . . . . .      . . . . . .      . . . . . .      . . . . . .      . . . . . .

                                                                   t=4 is t=0 shifted
                                                                   one cell LEFT and
                                                                   one cell down
```

> **How to get the direction right under pressure:** the glider "points" in the direction it travels. In the $t=0$ shape above, the single top cell sits **above the far end of the three-cell bar**, and the glider moves toward the **opposite** corner from that single cell's overhang. Safest method in the exam: draw your $t=0$, **hand-evolve one step**, and check the centre of mass has moved the way you want. If it hasn't, mirror your $t=0$ and you are done — one minute well spent.

#### The other named patterns — one line each

**Still lifes (stable class II patterns):** Block, Tub, Loaf, Hive, Hook, Snake.

```
   Block        Tub          Snake
   . . . .      . # . .      . . . . . .
   . # # .      # . # .      . # # . # .
   . # # .      . # . .      . # . # # .
   . . . .      . . . .      . . . . . .
```

**Oscillators, period 2:** Blinker, Toad, Beacon.

```
   Toad                     Beacon
   . . . . . .              . . . . . .
   . . # # # .              . # # . . .
   . # # # . .              . # # . . .
   . . . . . .              . . . # # .
                            . . . # # .
```

**Other oscillators named in the lecture:** **Caterer** (period 3 — the **smallest oscillator known with period 3**), **Eight** (period 8), **Pentadecathlon** (period 15).

**Methuselahs — long-lasting patterns:** **Acorn**, **Rabbits**, **r-pentomino**, **Diehard**, **Pi-heptomino**.

```
   r-pentomino
   . . . . .
   . . # # .
   . # # . .
   . . # . .
   . . . . .
```

**Other rules (the lecture lists them to show 23/3 is not special):** 2/3, 3/3, 13/3, 23/3, 34/3, 35/3, 236/3, 135/35, 1357/1357.

#### ✅ `sheet-03` Assignment 4 — what Wolfram class is the r-pentomino?

**Answer: class IV.** Support it:

- The r-pentomino runs for over a **thousand generations** of apparently chaotic activity before stabilising — so it is not class I (it does not die out) and not class II (it does not settle quickly into a short cycle).
- It is **not class III** either, because it does **not** remain aperiodic for ever: it eventually settles into a fixed collection of **still lifes and oscillators** while **emitting gliders**.
- The decisive evidence is those gliders: **persistent, localised structures that travel and can interact** are the defining feature of class IV, and are absent from class III.
- Game of Life as a whole is the standard example of a **class IV** automaton, and the r-pentomino is its standard demonstration.

> **Honest caveat to include in the answer:** during its long transient the r-pentomino *looks* class III, and a defensible answer says "class III behaviour during the transient, class IV overall". Say which you mean and why — the marks are for the argument.

---

### 3.4 Gosper's Glider Gun and computational universality

> **Part of the 4/4 Game of Life question, and `sheet-03` A3 asks it outright.** This is the "so what" of the whole Game of Life block, and it is the natural closing paragraph of a 10-point answer.

#### The story, told in four sentences

1. Conway **doubted that a Game of Life pattern could grow infinitely**, and offered **\$50** to the first person to find one.
2. In **1970**, **Bill Gosper** (an MIT mathematician) found such a pattern and collected the \$50.
3. Gosper's pattern is an **oscillator with a cycle length of 30 steps** which constantly changes shape, and during each cycle a **5-cell sub-structure is left over** — and that leftover is **a Glider**.
4. Therefore **every cycle a Glider is produced**, the glider leaves, and the population grows without bound.

#### The structure

The **Glidergun** is composed of **4 elements**, consisting of **36 cells** in a **$36 \times 9$ bounding box**, with a **cycle length of 30 time steps**.

- Two **blocks**, one on the left and one on the right, implement **two stoppers** that limit the structure.
- The two other elements **approach each other, collide, turn around, and separate again**; when they reach the stoppers they are **reflected** and the cycle starts over.
- The collision produces the **5-cell remainder shaped like a glider**, which starts to move and **leaves the gun** — heading to the **lower right**.

```
   Gosper Glider Gun -- schematic (36 x 9 bounding box, period 30)

   +--------------------------------------------------+
   | ##                                          ##   |
   | ##      <-- shuttle -->      <-- shuttle -->##   |
   | stopper    two structures approach, collide,     |
   | (block)    turn around, separate, reflect        |  glider
   |                                                  |    \
   |            collision leaves a 5-cell remainder ----->   \
   |            = a GLIDER, emitted every 30 steps            v
   +--------------------------------------------------+    lower right
```

#### ✅ `sheet-03` Assignment 3 — *"What has been proven by the development of Gosper's Glider Gun?"*

Answer it in **two layers**, because there are two distinct results:

1. **Directly: unbounded growth is possible in Game of Life.** The gun emits one glider every 30 steps for ever, so the number of living cells grows without bound. This settled Conway's own conjecture in the negative and won the \$50.
2. **Consequently: Game of Life is computationally universal (Turing-complete).** This is the answer worth the marks, and the chain is:
   - **Streams of Gliders can be regarded as information streams — a single Glider is a single bit.**
   - Gliders **interfere when they collide** with other gliders and with specially shaped structures; depending on the **phase** at collision they can be **erased, delayed, reflected or doubled**.
   - By these means it is possible to construct Game of Life structures that act as **Boolean gates: AND, OR, NOT, NAND, NOR, XOR**.
   - **Glider guns are the motors** of complex Game of Life constructions, and **streams of gliders are the information carriers and the tools** of Game of Life machinery.
   - A gate set including **NAND** is functionally complete, and with an unbounded supply of gliders you have unbounded memory — hence a universal computer can be built inside Game of Life.

> **Oral E asked directly for a NAND construction.** You are not expected to draw a working NAND gate; you are expected to explain **why one can exist**: colliding glider streams implement the gate, the gun supplies the input stream, and the collision outcome depends on phase.

Two supporting facts the lecture adds, each worth a clause: colliding gliders are **"the universal tools to construct and destroy other structures in Game of Life"**, and the final result of a collision is **typically hard to predict**, so gate construction takes "a lot of effort and a lot of Game of Life experience".

#### ✅ `sheet-03` Assignment 5 — how many 5-cell configurations can the gun produce?

*"Imagine an exam question asking to depict a 5-cell configuration for Conway's Game of Life that has been produced by Gosper's Glider gun. How many correct configurations exist?"*

**Answer: 4.**

- The only 5-cell structure the gun produces is a **glider**, and the gun emits them all in the **same direction** (lower right), so orientation is fixed.
- A glider passes through **4 distinct phases** before reproducing its shape one cell along the diagonal.
- Those four phases are four **different** 5-cell configurations (up to translation).
- Hence **4 correct answers exist** — and any of the four grids drawn in §3.3 above would be accepted.

> If you also count the translation as "different", there are infinitely many; say explicitly that you are counting **up to translation**, which is what the question means.

#### ✅ `sheet-03` Assignment 7 — the smallest pattern that dies in one update

*"What is the smallest configuration (fewest living cells) that will completely die out in a single update? To make this non-trivial, at least one cell must die from overcrowding (four or more neighbours)."*

**Start from the counting argument, which is the part that certainly earns marks:**

- To have a cell die of **overcrowding** it needs **at least 4 living neighbours**, so together with itself the pattern needs **at least 5 living cells**. **5 is therefore the lower bound.**
- With exactly 5 cells, one cell $C$ must have all other 4 as neighbours. Those 4 must **also** die, so each needs $\le 1$ or $\ge 4$ living neighbours; each already has $C$, so each must have **no other** live neighbour — i.e. the four must be **pairwise non-adjacent**.
- Among the 8 cells of $C$'s Moore neighbourhood, the only 4 that are pairwise non-adjacent are **the four diagonal corners**. So the unique 5-cell candidate is the **X-pentomino**:

```
      # . #
      . # .        C (centre) has 4 neighbours -> dies of overcrowding
      # . #        each corner has 1 neighbour -> dies of loneliness
```

- **All five cells do indeed die.** Under the reading "all initially living cells die", the **X-pentomino with 5 cells is the answer, and 5 is provably minimal**.

> ⚠️ **Honest caveat — check which reading your marker wants.** Under the stricter reading "the grid becomes completely empty", the X-pentomino **fails**: the four edge cells $(\pm 1, 0)$ and $(0, \pm 1)$ are each dead with **exactly 3** living neighbours, so **four new cells are born**. Under that stricter reading no 5-cell solution exists, and the minimum is larger. **State the ambiguity, give the X-pentomino with its minimality proof, and note the births.** That is a complete answer; pretending the births do not happen is not. This assignment has never appeared on a written paper, so do not spend more time on it.

#### ✅ `sheet-03` Assignment 6 — an application not from the lecture

Admission-only (it demands a citation). One safe answer: **CA-based lattice-gas / lattice-Boltzmann fluid simulation**, where each cell holds discrete particle velocities and the rule enforces collision and streaming, recovering the Navier-Stokes equations in the macroscopic limit. Not examinable.

---

## PART 4 — Past-exam tasks for Phase 1, solved

Every Phase-1 task from all four written papers, with the answer as I would write it on paper.

| Paper | Task | Where the answer is |
|---|---|---|
| 2017 Q1 (10 pt) | Explain Game of Life, evolve the pattern | §3.3 — spec + 23/3 + rule table + blinker |
| 2017 Q4 | 5 criteria of life | §1.2 |
| 2017 Q5 | Wolfram number $42_D$ | §2.4 |
| 2017 Q7 | Langton's Ant, white plane vs black plane | §1.3 |
| 2017 Q8 | Rule count $d{=}1, r{=}3, k{=}4$ | §2.2 |
| 2017 Q17 | Glider to the lower right, 4 steps | §3.3 |
| `qn-02` 1 (10 pt) | Game of Life, every detail + 2 steps | §3.3 |
| `qn-02` 5 | Glider to the **lower left**, 4 steps | §3.3 |
| `qn-02` 6 | Rule table for $42_D$ | §2.4 |
| `qn-02` 10 | Langton's Ant, 4 micro-behaviours + drawings | §1.3 |
| `qn-02` 12 | Wolfram class III vs IV | §2.6 |
| `qn-02` 14 | 5 criteria of life | §1.2 |
| `qn-02` 17 | Totalistic + silent $\Rightarrow$ legal? | §2.3 |
| `qn-03` | Game of Life via the blinker (10 pt) | §3.3 |
| `qn-03` | Wolfram number $42_D$; 5 properties of life | §2.4, §1.2 |
| `qn-01` T1 (10 pt) | **All** Wolfram numbers producing a picture | §2.4 (reverse method) |
| `qn-01` T3 | Langton's Ant, 4 micro-behaviours + scribbles | §1.3 |
| `qn-01` T8 | 5 attributes of natural life | §1.2 |
| `qn-01` T9 | Rule count $d{=}3, k{=}2, r{=}1$ Moore | §2.2 |
| `qn-01` T12 | Glider to the lower right, 4 time steps | §3.3 |
| `qn-01` T15 | Wolfram class 3 and 4 | §2.6 |
| `qn-01` T17 | "A totalistic rule with silent state is legal" | §2.3 |

---

## EXAM-READY CHECKLIST — Phase 1

Tick each only when you can produce it **blind, on paper, inside the time**.

**Life (≈5 min)**
- [ ] Five named criteria of life, each with a one-clause explanation.
- [ ] The opening sentence: there is no commonly accepted definition, only sets of criteria.
- [ ] One border case (virus / mule / crystal / fire) and why it fails.
- [ ] Strong vs weak AL in one sentence each.

**Langton's Ant (≈5 min)**
- [ ] Four micro-behaviours **scan → turn → flip → move**, four separate labelled sketches.
- [ ] "White ⇒ turn right, black ⇒ turn left", written in words.
- [ ] Three phases with ≈420, ≈10 000, **highway period 104**.
- [ ] The white-plane vs black-plane answer: mirror image, same phases, same period.

**1-dim CA (≈10 min)**
- [ ] The five components of a CA, listed.
- [ ] $n = 2r+1$, $L = k^n$, $Z = k^L$ — with each symbol named.
- [ ] Both worked rule counts: $4^{16384}$ and $2^{2^{27}}$.
- [ ] The five rule properties, defined.
- [ ] The totalistic + silent ⇒ legal proof, in three steps.
- [ ] Wolfram number $42_D$ table, forward, plus its classification.
- [ ] The reverse-Wolfram method and the $2^{8-m}$ counting argument.
- [ ] Class III vs class IV: similarities **and** differences.

**2-dim CA & Game of Life (≈15 min)**
- [ ] von Neumann vs Moore neighbourhood, drawn, with $n = 2d+1$ and $n = 3^d$.
- [ ] Game of Life spec: $d{=}2$, $r{=}1$ Moore, $k{=}2$, **rule is legal**.
- [ ] The rule **23/3** with all four clauses (birth, survival, overcrowding, loneliness).
- [ ] The two-row rule table indexed by $S_a(t) = 8\ldots0$.
- [ ] The blinker, $t=0,1,2$, with the cell-by-cell reasoning.
- [ ] A glider, 4 steps, **in both diagonal directions**.
- [ ] GoL rule classification: silent ✔, symmetric ✔, legal ✔, peripheral ✘, totalistic ✘ (**outer**-totalistic).
- [ ] Gosper gun: period 30, 36 cells, $36\times9$ ⇒ unbounded growth ⇒ gliders as bits ⇒ Boolean gates ⇒ universality.
- [ ] Forest-fire CA: $k=3$ states, five transitions, parameters $p, f, q$.

---

## ACTIVE-RECALL QUIZ — Phase 1

Answer on paper before reading on.

**Q1.** A CA has $d=2$, a Moore neighbourhood with $r=1$, and $k=3$ states. How many lines does its rule table have, and how many such rules exist?

**Q2 (drawing).** Draw the four micro-behaviours of Langton's Ant, labelled, and state the turn rule in words.

**Q3.** Write the rule table for Wolfram number $110_D$ ($d{=}1, r{=}1, k{=}2$) and say whether it is legal.

**Q4 (drawing).** Draw a Game of Life glider at $t=0$ that will travel to the **upper left**, and give the $t=1$ grid.

**Q5.** Is every legal rule totalistic? Prove or give a counterexample.

**Q6.** Name the three phases of Langton's Ant on a white plane, with their approximate step counts and the highway's period.

---

### Answers

**A1.** A Moore neighbourhood in $d=2$ with $r=1$ has $n = 3^d = 3^2 = 9$ cells. So the rule table has
$$L = k^{\,n} = 3^{9} = 19\,683 \text{ lines},$$
and the number of possible rules is
$$Z = k^{\,L} = 3^{19\,683}.$$

**A2.** See §1.3. The four panels are **scan** (read the cell under the ant), **turn** (90° **right** if the cell is **white**, 90° **left** if **black**), **flip** (invert the cell), **move** (one step along the new heading). The turn rule in words is the marked part.

**A3.** $110 = 64+32+8+4+2 = 2^6+2^5+2^3+2^2+2^1$, so:

```
 111  110  101  100  011  010  001  000
  0    I    I    0    I    I    I    0
```

It **has a silent state** ($000 \to 0$) but is **not symmetric** ($100 \to 0$ while its mirror $001 \to I$), so it is **not legal**. Rule 110 is the class IV rule later proved Turing-complete.

**A4.** Take the lower-right glider from §3.3 and rotate it by 180° (equivalently, mirror it both horizontally and vertically):

```
     t=0                    t=1

  . . . . . .            . . # . . .
  . # # # . .            . # # . . .
  . # . . . .            . # . # . .
  . . # . . .            . . . . . .
  . . . . . .            . . . . . .
  . . . . . .            . . . . . .
```

The centre of mass has moved up and to the left, confirming the direction. (In the exam, always verify with one hand-evolved step exactly like this.)

**A5.** **No.** Legal means symmetric **and** having a silent state; totalistic is a strictly stronger condition than symmetric. **Counterexample:** rule **204**, the identity rule (output $=$ centre cell), is symmetric and has a silent state, hence legal — but it is **not totalistic**, since $\text{SUM}=2$ arises from $110 \to I$, $101 \to 0$ and $011 \to I$, which are not all equal. Note the implication runs the other way: **totalistic $\Rightarrow$ symmetric**, but symmetric $\not\Rightarrow$ totalistic.

**A6.** **Phase 1 — symmetric growth**, up to about step **420**: small, almost symmetric patterns. **Phase 2 — chaotic growth**, from about step **400 to 10 000**: continued growth with no distinguishable structure, described as deterministic chaos. **Phase 3 — highway**, from about step **10 000** onwards: a highly structured, persistent, repetitive pattern with a **cycle time of 104 steps** that carries the ant off to infinity.

---

## WHAT TO DO NEXT

1. **Close the book and reproduce the checklist items on paper.** Time yourself: 5-point items in 5 minutes, the Game of Life item in 10.
2. **Redraw the glider in all four diagonal directions** until the direction check takes under a minute. This alone has been worth 5 points on three of four papers.
3. **Say "Quiz me on Phase 1"** if you want to be tested before moving on, or **"Teach Phase 2"** to continue with von Neumann, the self-replicating loops, L-Systems, Fibonacci and self-organised criticality.
