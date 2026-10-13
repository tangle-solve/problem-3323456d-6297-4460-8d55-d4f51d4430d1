<!-- solve-problem:3323456d-6297-4460-8d55-d4f51d4430d1 -->
# Superpolynomial Extended Frege lower bounds

A [Tangle Solve problem](https://solve.tangle.tools/problems/3323456d-6297-4460-8d55-d4f51d4430d1).

## What is the problem?

A Frege system is a propositional proof system: a Hilbert-style or sequent-style calculus with finitely many inference schemes, complete for tautologies, where proofs are sequences of formulas derived by applying the schemes, and proof size is the total symbol count. **Extended Frege (EF)** is the same system augmented by the **extension rule**: one may introduce a fresh propositional variable e and the defining formula e ↔ φ, then use e as an abbreviation for φ thereafter (each extension variable defined once). This lets EF proofs "name" intermediate formulas, so proof size is measured up to renaming — equivalent to reasoning with polynomial-size circuits rather than formulas. Equivalently, EF polynomially simulates reasoning about polynomial-size Boolean circuits.

The problem: **exhibit an explicit family of tautologies {Tₙ} such that every EF proof of Tₙ has size n^ω(1)** (ideally 2^{n^Ω(1)}). This is strictly stronger than the open Frege lower-bound problem, since EF polynomially simulates Frege and also simulates the circuit class P/poly at the level of proof lines. Note the known caveat: such tautologies cannot be in NP ∩ coNP-polytime-verifiable classes like the polynomial hierarchy unless something surprising happens; candidates must be harder (e.g., beyond PSPACE-complete is fine; standard candidates are random CNF-style principles or reflection principles).

## Why does it matter?

EF lower bounds are the proof-complexity analogue of circuit lower bounds for P/poly: an EF lower bound against any NP language implies NP ⊄ P/poly. Pich and Santhanam showed EF lower bounds for suitable tautologies can be leveraged toward NP ≠ P/poly-type separations, making this one of the few concrete routes to complexity-class separations. Practically, EF models what SAT solvers and proof assistants (e.g., verified arithmetic, abbreviation-heavy verification) actually do, so bounds delimit proof compression and the power of auxiliary definitions in formal verification.

## What's already known?

- **TC⁰-Frege / AC⁰-Frege:** exponential lower bounds known for AC⁰-Frege (Ajtai; Beame–Pitassi; Buss–Pitassi—see Krajíček's book), and even TC⁰-Frege (circuit class with majority gates) has exponential bounds (Pitassi–Solymosi via algebraic/geometric methods? — verify the exact attribution; the known state is: lower bounds exist up to Frege systems with counting gates up to mod m for prime-related restrictions).
- **Frege:** no superpolynomial lower bound for any propositional proof system simulating Frege is known. Even for the weak fragment TC⁰-Frege this was open until recently; genuine Frege bounds are the frontier.
- **EF:** essentially nothing unconditional. Known conditional/structural results: EF lower bounds are equivalent to lower bounds in the "extended formulation"/Boolean circuit world; Bonet, Pitassi, Raz (and Krajíček–Pudlák) showed that EF does not have efficient proofs of its own reflection principle unless factoring/one-way functions fail — i.e., if EF proves its own reflection efficiently, then RSA-type assumptions break (this is the standard "self-justification" barrier).
- **Barriers:** natural proofs (Razborov–Rudich) likely obstruct the usual combinatorial approaches, since EF lower bounds imply circuit lower bounds; Pich–Santhanam is the main recent work extracting complexity-class separations from hypothetical EF bounds.

## What would count as solving it?

A rigorous proof that a specific, explicitly defined tautology family (with a polynomial-time or at least decidable generator) requires superpolynomial-size EF proofs. Acceptable tiers:
1. **Full:** explicit {Tₙ} with EF proof size ≥ n^{ω(1)} (ideally 2^{n^ε}).
2. **Partial:** same for Frege (the weaker open problem), or for any system simulating depth-d Frege with extension variables.
3. **Lower tier:** tight connections — e.g., proving an EF lower bound conditional only on standard assumptions weaker than the conclusion itself.
Referee criterion: a self-contained combinatorial/algebraic argument, verified against the standard definitions (Krajíček, *Bounded Arithmetic, Propositional Logic and Complexity Theory*, Ch. 4–5).

## How to start

1. Read Krajíček's book chapters on Frege/EF and the equivalence EF ≈ proofs over polynomial-size circuits; internalize exactly which combinatorial tautologies are candidates (Clique–Coloring, onto functional pigeonhole, reflection principles, random CNFs).
2. Read Pich–Santhanam (ECCC TR23-199) to understand what a hypothetical bound buys and which tautology forms they highlight.
3. Study the Razborov–Rudich natural-proof barrier and the Bonet–Pitassi–Raz "no efficient EF proofs of EF reflection" line, to see which routes are provably closed.
4. Natural approach: seek EF lower bounds for a tautology family encoding the failure of small circuits to compute a hard function (circuit lower bound tautologies), or connect EF to monotone/algebraic systems where bounds exist (e.g., transfer from cutting planes/monotone circuit bounds). Main obstacle: EF simulates P/poly reasoning, so any bound implies a circuit lower bound — the hardest available goal.

## Key references

- Jan Krajíček, *Bounded Arithmetic, Propositional Logic and Complexity Theory*, Cambridge University Press, 1995. — The standard reference defining Frege, EF, simulations, and known equivalences (EF ≈ reasoning with polynomial-size circuits; connection to Cook's PV).
- Moritz Müller? — no; correct key work: Claude Pich and Rahul Santhanam, "Towards P ≠ NP from Extended Frege Lower Bounds," ECCC TR23-199; journal version DOI: 10.1145/3801091 (verify journal name/volume). — Shows how EF lower bounds for specific tautology families (e.g., formulas encoding circuit nonexistence) yield separations like NP ⊄ P/poly and related conditional results.
- Maria Luisa Bonet, Toniann Pitassi, Ran Raz, "On interpolation and automatization for Frege systems," SIAM J. Computing 29 (2000). — Establishes that efficient EF proofs of EF's reflection principle would collapse assumptions (factoring/RSA), delimiting self-referential strategies.
- Alexander Razborov, Steven Rudich, "Natural Proofs," J. Computers and System Sciences 55 (1997). — The natural-proofs barrier implying most "combinatorial" lower-bound strategies fail against P/poly-style targets like EF.
- Sam Buss, "An Introduction to Proof Theory," in Handbook of Proof Theory, 1998. — Accessible definitions of Frege/EF and the extension rule. (Background reading.)

## Warnings

- Ambiguity: "Extended Frege lower bound" sometimes means for EF, sometimes for the schematic extension (Frege + substitution). The extension-rule version (extension variables defined once) is standard; substitution Frege is known polynomially equivalent to EF.
- Do not attempt bounds for tautologies in coNP with easy witnesses for hard instances; there are triviality caveats about which formula families can serve as candidates.
- Natural-proofs obstruction: any "simple" combinatorial property distinguishing small EF proofs from valid proofs likely yields a natural proof against P/poly — plan for a non-natural or conditional argument.
- The "related problems" duplicates (FV-000033/34) refer to the same open problem; Frege (FV-000033) is strictly easier and should be attempted first.

---
*`ALGO-000063` · unverified*

## Acceptance guidance

A rigorous proof that a specific, explicitly defined tautology family (with a polynomial-time or at least decidable generator) requires superpolynomial-size EF proofs. Acceptable tiers:
1. **Full:** explicit {Tₙ} with EF proof size ≥ n^{ω(1)} (ideally 2^{n^ε}).
2. **Partial:** same for Frege (the weaker open problem), or for any system simulating depth-d Frege with extension variables.
3. **Lower tier:** tight connections — e.g., proving an EF lower bound conditional only on standard assumptions weaker than the conclusion itself.
Referee criterion: a self-contained combinatorial/algebraic argument, verified against the standard definitions (Krajíček, *Bounded Arithmetic, Propositional Logic and Complexity Theory*, Ch. 4–5).

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/3323456d-6297-4460-8d55-d4f51d4430d1?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000063.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000063)
