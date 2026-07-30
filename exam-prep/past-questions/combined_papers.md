# Artificial Life (Nils Goerke): Combined Exam Protocols

Sources merged into this file:

| Source file | Term | Type |
|---|---|---|
| ALife_10_SS.pdf | SS 2010 | 6 separate oral protocols |
| ALife_17_SS.pdf | SS 2017 | 1 written exam (8.8.17) |
| ALife_20_SS.pdf | SS 2020 | 1 oral protocol |

All question and answer text below is reproduced word for word from the originals. Spelling, typos, mixed German/English and inconsistent notation are left exactly as written. Nothing has been rewritten, shortened or merged. Redundancy is handled by the topic index in Part 0, which maps every recurring topic to the protocols it appears in, so no text had to be deleted.

---

## Part 0: Topic Index (redundancy map)

Protocol codes used below:

- **A** = SS 2010, handwritten Masterprüfung protocol
- **B** = SS 2010, 2010/08/07 protocol (grade 1.0)
- **C** = SS 2010, Prüfungsprotokoll AL SS2010 (Note 1,0)
- **D** = SS 2010, Magdalena Reichel, 27 July 2010 (Note 1.0)
- **E** = SS 2010, 2010/07/27 protocol (Note 1,0)
- **F** = SS 2010, Beowulf Siegert
- **G** = SS 2017 written exam, 8.8.17
- **H** = SS 2020 oral protocol

| Topic | Appears in |
|---|---|
| Cellular Automata / Wolfram notation | A, C, E, G |
| Game of Life (glider, blinker, glider gun, Turing equivalence) | E, G |
| Digital filters (1st / 2nd derivative, convolution) | B, C, D, F |
| Braitenberg Vehicles (3a, 3b, 3c, obstacle avoidance) | B, D, E, G, H |
| Didabots | F, G, H |
| Evolutionary Algorithms (cycle, operators, termination) | A, B, C, D, F, G, H |
| Ant Algorithm | B, D |
| L-Systems / Lindenmayer Systems | A, G, H |
| Predator-prey / Lotka-Volterra / activator-inhibitor | A, E |
| Self-Organizing Criticality, scaling law, sandpile, earthquakes | C, E, G, H |
| Fixed points / graphical iteration | D, F |
| Boids / swarm behaviour | F, G |
| Particle Swarm Optimization | G, H |
| Definitions of life / characterisation of the field | C, G, H |
| Differential equations, exponential ansatz | B |
| Mutation probability calculation over N genomes / L bits | A, F |
| John von Neumann aspects | G |
| Fibonacci vs logistic growth | G |
| Wheel of Fortune | G |

---

# Part 1: SS 2010 protocols (ALife_10_SS.pdf)

## Protocol A: Handwritten Masterprüfung protocol

> Handwritten German original. Transcribed as legibly as possible; one item is ambiguous in the manuscript and is marked.

Prüfungsprotokoll
Artificial Life 2010
Masterprüfung

Fragen:

1) Was ist ein ZA?

2) Was ist L-System

3) Berechnen sie die Wahrscheinlichkeit, dass keine Änderung bei N Genomen, L Ports [handwriting ambiguous, most likely "L Bits"], Bitflip p auftritt.

4) Erläutern sie Aktivator/Inhibitor am Bsp.: Lotka-Volterra

5) Schritte EA

---

## Protocol B: 2010/08/07, Nils Goerke (grade 1.0)

2010/08/07
Artificial Life
Nils Goerke

1) braitenberg
- type 3b?
-> drew robot & explained distance/proximity sensors, inhibitory & crossed connections to motors, behavior: obstacle avoidance
- behaviour when facing wall diagonally?
-> explanation
- how to stop at fixed distance from obstacle?
-> after struggling a bit: 3a like build up + drew mapping of sensor to motor values
- type 3c?
-> rough explanation: sensors for light, temperature, oxygen, ..., complex connections, both positive & negative, both crossed & direct

2) ant algorithm
-> goal: find shortest paths, principle: use "ants" to sample surrounding, ants leave pheromones, choices of ants influenced by pheromones
- what about ant colony algorithm?
- application?
-> find good connections in the internet
- how?
-> could only guess, probably by sending packages and recording their path

3) digital filters, give one example and try to explain the values.
- filter for first derivative
-> 1/2 * [-1, 0, 1]
- why these values?
-> discrete approximation of dx/dt = lim_{h->0}(f(x+h)-f(x))/h by calculating discrete differences of the function values and dividing by the step size (here symmetric differences: dx/dt ~= (x_{i+1} - x_{i-1}) / 2
- filter for second derivative (with five values)?
-> 1/12 [-1,16,30,16,-1]
- why is this filter symmetric?
-> same principle to approximate first derivative from function applied to first derivative itself
- how does one apply these filters to actual (discrete) function values?
-> by convolving the function values with the filter kernel

4) apply the exponential ansatz to the differential equation ax''' + bx'' + cx' = 0
-> x(t) = x_0*exp(-idt)
-> calculate derivatives x'(t) = ..., x''(t) = ..., x'''(t) = ...
-> insert into equation
- how to solve? what are we looking for?
-> want to determine parameters x_0 and d in x(t)
-> solve: rule out x(t) = 0 and divide by x(t) => gain two results for d using pq-formula (plus one solution for d = 0)
- what about case x(t) = 0?
-> implies the only solution x_0 = 0 (because exp(...) != 0)
- what is the total number of solutions?
-> counted solutions: four...
- I claim that there is an infinite amount of solutions. How come?
-> arbitrary linear combinations of complex exponentials also solve this kind of DEQ

5) evolutionary algorithms
- explain principle, function & design for an example application of your choice
-> short introduction of this optimization approach with relation to natural evolution, selection, survival of the fittest
-> multi hypothesis approach, genome as one possible solution in search space, population of genomes, exploitation & exploration
-> drew circle scheme for EAs + explained each step, chose example of radar antennas developed by NASA with the help of EAs
-> initialisation, fitness function, combination (= exploitation), mutation (=exploration), termination
- most time consuming part? justify claims for example of population of n=100 individuals.
-> fitness evaluation (because fitness function can be quite expensive to evaluate)
- ok, now rule out that trivial answer.
-> external selection: sorting nlogn, parent selection: determine combination partners (can be up to n*n), mutation: n times arbitrarily complex operations, e.g. generation of random numbers
- costs for recombing genomes using mu+lambda, 1+lambda, ... strategies
- example: 100 bit genome, mutation?
-> flip single (random) bit
-> flip all bits with certain probability
- costs?
-> 100 random numbers
- when to terminate?
-> observe best fitness values
- what would this look like in a graph?
-> plotted example fitness of best individual over time
- what important characteristic does the curve have?
-> monotonically rising function because of exploitation
- further termination criteria?
-> fixed number of iterations
-> fixed time
- what about observing fitness of whole population?
-> wait until fitness values over whole population are approximately the same

grade: 1.0

---

## Protocol C: Prüfungsprotokoll AL SS2010, Note 1,0

Prüfungsprotokoll AL SS2010
Note 1,0

1. Charakterisieren sie das Forschungsgebiet Artificial Life und nennen sie die Themen der Vorlesung.
2. Geben sie den zellulären Automaten an, der mit der Dim=1, k=2, r=2, nach der sogenannten Wolframnotation die Nummer 65538 = (2^16 + 2) hat.
3. Erläutern sie anhand des Gutenberg-Richter Gesetz was man unter dem Skalengesetz versteht.
4. Erläutern sie Aufbau und Funktion eines Digitalen Filters am Beispiel der ersten Räumlichen Ableitung.
5. Beschreiben sie Ziel und Vorgehensweise von Evolutionären Algorithmen an einem selbst gewählten Beispiel.

**zu 1.**

- strong, weak AL erklären
- Themen der Vorlesung: SOC, dynamische Systeme, Selfreplication, Räuber-Beute Systeme, CA, GOL, Roots of complex behaviour (Braitenberg vehikel...), L-Systems, EA,...

**zu 2.**

- Tabelle malen
- 2 Übergänge zur 1:

| a_i(t) | 10000 | ... | 00001 | 0 |
|---|---|---|---|---|
| a_i(t+1) | 1 | 0 | 1 | 0 |

- legal? -> symm. + ruhiger Zustand -> ja
- peripheral? -> Nein
- totalistisch? -> Nein
- Größe der Tabelle: 2^5 = 32
- wie sieht die Regel aus? mit einem seed:

```
...000010000...
...001000100...
...100000001...
```

- typischer weise aber mit rnd. seed.

**zu 3.**

```
N(s)=1/s^alpha
log(N(s))=log(1/s^alpha)=log(1) - log(s^a)=log(1) - a *log(s)= c - a* log(s)
```

- Diagram malen
- Zipfsches Gesetz
- Sandhaufenmodell
- Fire-Forest Model

**zu 4.**

- Zeitdiskrete Funktion
- erste Abl: 1/2 * [-1,0,1] ≙ dx/dt
- Diagram malen, am besten Parabel, denn dort ist der Filter = der ersten Ableitung! also Herleitung.

```
dx/dt = 1/2 * (x(i+1) - x(i-1)) symmetrisch

Vektoriell: x'(i) = 1/2 (-1 0 1)^T * (x(i-1) x(i) x(i+1))^T
```

- Digitale Filter werden bei in der Digitalen Signalverarbeitung und der Bildverarbeitung verwendet.
- Anwendung durch Faltung.
(Herr Goerke hätte hier auch noch weiter gefragt, also wie das genau Funktioniert... Fouriertransformation, Gaussfilter, Kantenfilter usw.)

**zu 5.**

- Beispiel aussuchen, Herr Goerke schlägt aber auch eines vor wenn man keine Idee hat.
Beispiel: Schokoladenherstellung (Firma Mars)
- EA Cycle malen
- Genom: reeller Vektor mit 40 Einträgen, Prozentual oder numerische Werte.
- bzgl. Bsp alle Punkte im Cycle erklären. zb welche Fitness eval., External select strategie, Parent Select, Inheritance, Mutation, wie und warum.
- was ist am „teuersten" in unserem EA -> Schokolade probieren, extrem Zeitintensiv.
- wann fertig?-> nach ca 20-30 verschiedenen Schokoladen schmecken alle sehr ähnlich (Mensch beendet den EA)
- warum überhaupt EA? zb. bzgl. TSP.
Fitness des besten Individuums über die Zeit auftragen: man kann sehen dass EA nach t/2 ein Ergebnis liefert welches sich nur geringfügig vom Ergebnis zum Zeitpunkt t unterscheidet. Die meisten anderen Algorithmen zb. Dijkstra liefern nur unausgewertete Daten wenn man sie einfach so abbricht.

---

## Protocol D: Magdalena Reichel, 27 July 2010, Note 1.0

Prüfung zur VL Artificial Life
Dozent: Nils Goerke
Sommersemester 2010
Prüfer: Nils Goerke, Beisitzer: Marcel Missura
Prüfling: Magdalena Reichel, Note:1.0

July 27, 2010

Herr Dr. Goerke hat – wie immer – 5 Fragen vorbereitet, die er mir erstmal der Reihe nach vorliest. Davon sind 4 relativ schnell zu beantworten, während die letzte Frage deutlich umfangreicher konzipiert ist. D.h. die ersten Fragen decken fast nur Wissen aus der Vorlesung ab, während man für die 5. evtl ein bisschen Transferleistung erbringen muss. Deswegen bearbeitet man die Fragen am besten auch in der vorgegebenen Reihenfolge (obwohl man sich theoretisch wohl auch eine andere Reihenfolge aussuchen kann).

Es bietet sich an, zu den jeweiligen Fragen ein paar Skizzen zu machen (z.B. Braitenberg-Vehikel und die entsprechenden Funktionen aufmalen, Bildchen für Ant Algo malen usw.).

**1. Frage: Wie realisiert man Hindernisvermeidung mit Braitenberg-Vehiklen?**

Vehikel hinmalen (3b). Wand hinmalen (erklären, warum 3b ausweicht). Funktion hinmalen (Nähe → Inhibition. Monoton steigende Funktion)

- Vergleichen Sie 2a, 3b (3b ist insgesamt vorzuziehen, weil wir in der Nähe von Hindernissen lieber abbremsen als beschleunigen. Ausserdem ist eine Abbremsung einer Maximalgeschwindigkeit technisch leichter zu realisieren, als eine immer höhere Beschleunigung)
- Wie verhindert man in der Ecke stecken bleiben? (Stochastische Komponente, Funktion extrem genug bauen, Gedächtnis...)
- Was kann passieren wenn Sie nur die Funktion anpassen? (er wollte aufs Hin- und Herpendeln hinaus)
- Malen Sie dieses Verhalten in ein Diagramm (Achsen: Zeit → Winkel. Funktion: Oszillierendes Verhalten)
- Und was ist das? (2 Fixpunkte → Bifurkationsdiagramm)
- Kann man so ein Vehikel auch so einstellen, dass es einem Hindernis folgt? (Ja. 3b. Inhibition sollte genau 100% sein, wenn die gewünschte Distanz erreicht.)

**2 Frage: Erläutern Sie das Konzept eines Digitalen Filters**

- wie sieht z.B. der für 1. Abl aus?
- Grafische Erklärung, für die erste Ableitung.
- 5 Punkt für 1. Abl?
- 2. Abl?
- Integrieren?
- Interpolation? (→ Moving Average)
- Extrapolation? (geht grundsätzlich auch mit Linearkombi von Vorgängern)

**3. Frage: Erklären Sie den Ant Algorithm**

Hab das Prinzip mithilfe von zwei Bildern erklärt: erst den Prozess der Selbstverstärkung mithilfe von Pheromonen im freien Gelände, dann für den diskretisierten Fall, bei dem nur eine endliche Menge von Wegen zur Auswahl steht.

- Einsatzgebiete? (Kürzeste Wege, insbesondere Internet)
- warum ausgerechnet Internet? (Weil sich da Situation ständig ändert und AntAlgo toll ist, um sich dynamisch anzupassen)

**4. Frage: Berechnen Sie analytisch den Fixpunkt der Funktion x_{i+1} = ax_i(2 − x_i)**

- Lösen (0 nicht vergessen;))
- Prinzip der Grafischen Iteration an einem Beispiel erklären
- Mathematisch erklären, warum die Grafische Iteration so geht

**5. Frage: GAs an einem Beispiel erklären**

Einsatzgebiet: Optimierungsprobleme, bei denen wir die Funktion selbst nicht kennen oder komplett untersuchen können. Mein Beispiel: wir haben Zutaten und wollen einen tollen Kuchen backen, haben aber natürlich keine Funktion die uns jede Zutatenmenge auf ein Grad an Leckerheit abbildet. Also müssen wir ausprobieren. (Denkt euch ruhig ein einfaches Beispiel aus; Ich musst dann alle anderen Fragen – Codierung, Fitnessfunktion usw. – in Bezug auf dieses konkrete Kuchen-Beispiel beantworten!)

GAs bieten ein Framework dafür, bei solchen komplexen Optimierungsproblemen eine hohe Exploration der Fitnessoberfläche zu erreichen und gleichzeitig die guten Umgebungen stark zu Exploiten.

- Kreis malen (Init → Fitness Eval → External Selection...)
- Codierungsmöglichkeiten diskutieren (In meinem Fall: die Zutaten als Menge, Bitstring, Vektor von Integern ... codieren.)
- Abbruchbedingungen diskutieren (Anzahl Iterationen, Zeit, Geld, gewünschte Qualität erreicht, Stagnation der Qualität, Superindividuum, ...)
- Mutationsoperatoren aufzählen / erklären (Bitflip, eine Zutat zufällig verändern, kleine Zufallsvariable addieren ...)
- Crossoveroperatoren aufzählen / erklären (1- oder n-Point-Crossover. In diesem konkreten Fall sogar sinnvoll, in anderen Fällen (z.B. TSP) nicht, weil dann ungültige Lösungen entstehen)
- (μ + λ), (μ, λ) Erklären. Vorteile bzw. Nachteile? (meistens ist (μ + λ) vorzuziehen, weil dann Qualität monoton steigend ist, außerdem ist Speicherplatz heutzutage billig und es gibt keinen Grund, die paar besten aus der letzten Generation nicht zu behalten)
- welche Werte würden Sie in ihrem Beispiel für μ und λ wählen? (μ < λ z.B. mu = 10, λ = 90)
- wie viele Fitnessfunktionsauswertungen brauchen wir denn so? (bei μ + λ weniger, weil ein paar Werte behalten werden können, die man schon in der letzten Runde berechnet hat)
- und bei einem zeitlichen Drift im Funktionswert? (Dann hilft auch die +-Strategie nix mehr; wenn die Leute schneller ihre Meinung ändern als wir eine neue Generation von Kuchen backen, müssen wir jedes Mal alle Kuchen – also auch die bereits bewerteten – nochmal probieren lassen)
- Welche Plots schauen wir uns während der ganzen Zeit an? (1. Rang → Fitness, für die Selektion 2. Generation → Min / Mean / Max der Fitness, für den Abbruch)

**Bemerkungen:** Herr Goerke ist relativ nett, hat aber eine sehr festgelegte Vorstellung, worauf er jeweils hinaus will (war zumindest bei mir bei den ersten vier Fragen so). Man sollte die einzelnen Punkte also möglichst genau so präsentieren, wie sie in der Vorlesung genannt wurden.

Der Stoff der Vorlesung ist zwar relativ gering, man sollte ihn aber umso genauer können. Z.B. wollte er bei den Filtern nicht nur die Idee an sich wissen, sondern wirklich die genauen Werte für einzelne Filter.

Außerdem sollte man sich nicht von Herrn Goerkes „Pokerface" aus dem Konzept bringen lassen. Ich war z.B. die ganze Zeit sehr unsicher, obwohl ich meistens richtig lag, einfach weil man bei diesem Prüfer wenig Feedback während der Prüfung darüber bekommt, ob das bisher gesagte halbwegs sinnvoll oder völliger Unsinn war.

Viel Glück!

---

## Protocol E: 2010/07/27, Nils Goerke, Note 1,0

2010/07/27
Nils Goerke
Pruefungsprotokoll Artificial Life

Zunächst die Frage, ob ich mich gesundheitlich in der Lage fühle. Dann hat er mir den Zettel mit 5 Fragen gezeigt, und die Fragen vorgelesen, und mir gesagt wenn ich möchte kann ich die Reihenfolge bestimmen, die wären aber in Etwa nach Schwierigkeit sortiert.

1) Zelluläre Automaten (z.B. d=1, r=2, k=2)
- Zeigen wie ein Zustand dargestellt wird
- Übergang (synchron) erklären, Regeln
- Wie kann man eine Regel darstellen (Wolfram-Notation, von Binär in Dezimal umrechnen erwähnen, nicht machen)

2) Räuber-Beute Systeme als Differentialgleichung
- Wie kann man es aufschreiben
- Er bot an es als Differenzengleichung zu machen, habe ich auch gemacht
- N_i+1=N_I(a-b P_i)
- P_i+1 = P_i + P_i(c N_i - d)
- Lotka-Volterra, Diagramm skizzieren, Phasenverschiebung (pi/2) angeben

3) Braitenberg
- 3b Vehikel beschreiben
- 3b Verhalten an einer Wand beschreiben
- 3a Vehikel beschreiben
- 3a mit negativem Antrieb wenn man näher als d kommt beschreiben, Sensordiagramm (Gerade mit Nulldurchgang bei d) zeichnen.

4) SOC
- Erdbeben
- Sandhaufenmodell
- Skalengesetz

5) Game of Life
- Wie ist GoL definiert
- Wie funktioniert es
- Glider (Klasse? ->IV)
- Blinker (3 Kästchen in einer Reihe)
- Glidergun grob beschreiben
- Was passiert mit gegeneinander feuernden (Kollision erzeugt evnentuell neue Objekte)
- Turing Äquivalenz zeigen (NAND konstruieren)

Gegen Ende noch etwas Diskussion ob man aus GameOfLife denn praktisch Computer bauen könnte, was aber nicht mehr um die Bewertung ging wie ich hinterher gesagt bekam.

Note 1,0

---

## Protocol F: Beowulf Siegert

Vorlesung: Artificial Life, SoSe 2010, Nils Goerke
Name: Beowulf Siegert

1. Erklären sie Boids und erläutern sie 3 Regeln wie man Schwarmverhalten erzeugen kann.
NF: Wie kann man mit Boids Hindernisse umfliegen?

2. Erläutern sie die Funktionsweise eines Digitalen Filters anhand der 1. Ableitung
NF: Woher kommen die Zahlen [-1/2, 0 1/2], motivieren sie diese Parameter.
NF: Nennen sie die 1. Ableitung mit 5 Werten anstatt 3.

3. Analytische Fixpunkt-Errechnung der Funktion x_i+1 = a*x*(2-x)+b
NF: Wie erkennt man Fixpunkte grafisch?

4. Was passiert wenn man das Didabot experiment anstatt mit nur einem, mit mehreren Didabots startet?
NF: Ist die Form des "Kopfes" des Didabots wichtig?

5. Erläutern sie welche Methoden der Rekombination und Mutation die Diversität und das Erzeugung des Superindividuums beeinträchtigen.
NF: Welche Rekombinationen gibt es?
NF: Welche Mutationen gibt es?
NF: Was ist ein Superindividuum?
NF: Begünstigt es die Divrsität wenn man ein Genom aus 640 bits besteht, welches widerrum 10 64 bit Zahl aneinander gehangen hat...und man zufällig ein bit davon flippt?
NF: Wenn man jedes bit mit Wahrscheinlichkeit 0.001 flippt?
NF: Wahrschenilichkeit 0.5?
NF: Wahrscheinlichkeit 1?

---

# Part 2: SS 2017 written exam (ALife_17_SS.pdf)

Artificial Life exam 8.8.17
--> 100 minutes for 100 points
--> Wants explanations for all answers including formulas (which variable means what?)
--> 17 questions, first three worth 10 points(2 pages free space), rest worth 5(half page free space).

1) Details on Conways Game of Life. Pattern given (three black squares in a horizontal row). Supposed to draw next two steps and explain how the Game of Life works, why the pattern changes in which way and so on.

2) Didabot experiment: Explain the setup, the robots task, the observed behavior, the circumstances that led to this behavior. Difference between experiment with a single Didabot vs experiment with multiple identical Didabots?

3) Explain Evolutionary Algorithms in full detail: Every aspect of them, how they contribute, how the whole thing works. Then explain how the two principles a) Exploration and b) Exploitation contribute to Evolutionary Algorithms.

4) Name 5 common aspects of definitions for "life".

5) Give a rule table for the Wolfram number 42D with d=1, r=1, k=2.

6) Draw the typical fitness function (performance graph) for an evolutionary algorithm with: determinism, rank-based, elitism, (μ+λ)-strategy and no mutation for parents.

7) Compare the typical behavior for Langtons Ant on uniform black rectangles with the one on uniform white rectangles.

8) Derive the formula to calculate the quantity H of rules for a Cellular Automata with 1-dimension, r=3, k=4, then calculate the result for the given parameters.

9) Explain a Braitenberg Vehicle that is able to do obstacle avoidance. Draw a scenerie (with vehicle and obstacle!) that demonstrates your explanation.

10) Particle-Swarm-Optimization: Write and explain the formula to update a position Xi at time t for a particle i.

11) Develope the Lindenmayer-System with max. 4 rules that starts with O at time t=0 and generates the below string at t=3. Also write all previous timesteps.
t=3: OAOAOAOAOAOAOAO

12) Name and explain the rules that lead to the swarming behavior of Boids.

13) Write down and explain the formula of the Scaling Law for Self-Organizing Criticality Systems. You can give an example that supports your explanation.

14) Name and explain two aspects of Artificial Life that are connected with John von Neumann.

15) What is the task of the Wheel of Fortune mechanism in evolutionary algorithms?

16) Think of the two growth processes a) Fibonacci Sequence b) Logistic Growth. Give both formulas and compare how both behave.

17) Draw the 5-segment cellular automata that is called a glider. Its supposed to move to the lower right corner of the given space. Draw all 4 timesteps!

---

# Part 3: SS 2020 oral protocol (ALife_20_SS.pdf)

Artificial Life – Oral exam protocol
Examiner: Dr. Nils Goerke
Summer 2020

The protocol might not be complete but the questions here cover most of what was talked about.

Dr. Goerke was a very nice examiner and I felt like I was able to influence the topics of the exam a bit, but also he also made sure to cover a few different topics. When mentioning certain key words, he would ask about it and he also helped with further question when I did not get immediately what he wanted to hear.

During the discussion after the exam, Dr. Goerke summed up the whole exam including my answers so I could understand his grading.

Questions marked with "Extra:" were exceeding the content of the lecture and did not impact the grading much.

- Name 4 paradigms that were covered in the lecture and choose one of them to start with.

**Braitenberg Vehicles**

- What is the idea and purpose of Braitenberg Vehicles?
- What is the difference between type 3a and 3b?
- What is the difference between type 3 and 4?
- Extra: What is the difference between type 4 and 5?
- How does type 3b obstacle avoidance work?

**Didabots**

- What is the idea, the setup and the result of the experiment? What is the reason for the result?
- What happens if multiple Didabots are used and does the result change?

**Particle Swarm Optimization**

- What is the idea and purpose of PSO? How does it work?
- What is the formula for recalculating the velocity of an individual?
- Where in this formula are exploration and exploitation implemented?
- Why is PSO so popular?

**Evolutionary Algorithms**

- Why are EAs so popular?
- Draw the performance graph for a deterministic, fitness proportional, elitism, (λ + µ) strategy and explain it.
- Where in the EA cycle are exploration and exploitation implemented?
- Name strategies for a probabilistic selection strategy and choose one of them to explain.
- Why does one want to use probabilistic strategies?
- What is a super-individual?

**Lindenmayer Systems**

- What is the idea and purpose of Lindenmayer Systems?
- Give a simple example of a Lindenmayer System. (I choose the LS modeling population growth with rules C → A, A → CA from the lecture.)
- Which sequence does this implement? Give a formula for a more realistic modeling of population growth and explain it.

**Self-Organizing Criticality**

- Explain SOC using the example of earthquakes.
- Extra: What exactly is the self-organizing to criticality part in earthquakes? (Energy build-up)
- Which values exactly are related to each other?
- How do the two values depend on each other, e.g. in a diagram?

**Definitions of Life**

- Name 3 common criteria for life mentioned at the beginning of the lecture.
