<!-- solve-problem:cc1b1594-809d-4f85-ba9a-6f537dc7bbd0 -->
# Deterministic NC for general perfect matching

A [Tangle Solve problem](https://solve.tangle.tools/problems/cc1b1594-809d-4f85-ba9a-6f537dc7bbd0).

## What is the problem?

Determine whether the general graph perfect matching problem is in deterministic NC. Precisely: given an undirected graph G = (V, E) with n vertices and m edges, construct an algorithm running on a PRAM (or equivalent parallel model) with poly(n) processors in O(polylog n) time that (a) outputs a perfect matching of G if one exists, or (b) correctly reports that none exists — all deterministically, with no random bits. Complexity class NC = ⋃_k NC^k means parallel time O(log^k n) with polynomially many processors. The problem is known to be in randomized RNC via the isolation lemma; the question is whether the randomness can be removed. By the standard "sequential-parallel equivalence" for matching (Borodin–von zur Gathen–Hopcroft: NC algorithms imply efficient serial algorithms, and vice versa a decimation-style reduction), a decision/parallel-search NC algorithm exists iff one can count or otherwise deterministically "isolate" matchings. A related formulation: find a weight assignment to edges making the minimum-weight perfect matching unique — this is the deterministic isolation lemma problem, itself open.

## Why does it matters?

It would derandomize one of the oldest RNC-complete problems and resolve a flagship case of the RNC vs. NC question. Perfect matching is a subroutine throughout combinatorial optimization (assignment, flow decompositions, market clearing); an NC algorithm would put these in deterministic polylog depth. It is also tightly coupled to the circuit complexity of matching and to the permanent/determinant divide, so progress here would illuminate core questions in derandomization.

## What's already known?

- RNC: Mulmulee–Vazirani–Vazirani (1987) gave an RNC algorithm via the isolation lemma and the Tutte matrix: assign random poly(n)-bit weights, isolate a unique minimum-weight perfect matching, and compute it from the rank profile of a polynomial matrix. The only randomness used is the isolation.
- Deterministic quasi-NC: Svensson and Tarnawski (2017) gave a deterministic algorithm with Õ(log^{O(1)} n)... specifically polylogarithmic depth but quasi-polynomially many processors (NC with n^{polylog n} processors), by derandomizing isolation for bipartite graphs via an elaborate recursive/margin-based scheme (building on an FPGA-style hierarchy), then reducing general graphs to bipartite via a "doubling" gadget (Fenner–Gurjar–Thierauf for bipartite came first, 2016).
- Bipartite case: Fenner, Gurjar, Thierauf (STOC 2016) — deterministic isolation for bipartite perfect matching, hence quasi-NC.
- Reductions: NC matching ⟺ NC isolation for the class; general graphs reduce to bipartite in NC (via Tutte-matrix / Thorup's work, and the ST paper's reduction).
- The known approaches fall short because the quasi-NC isolation schemes blow up processor counts exponentially in recursion depth; no poly-size witness of isolation is known. (Also known: perfect matching decision is in SPL for bipartite graphs — Allender, Reinhardt, Zhou.)

## What would count as solving it?

1. A deterministic isolation lemma for general graphs: an NC-computable (polylog depth, poly work) edge-weighting of any graph guaranteeing a unique minimum-weight perfect matching — this plus MVV yields NC.
2. Directly: an explicit NC algorithm (O(log^k n) time, n^O(1) processors) outputting a perfect matching or reporting none, with a correctness proof.
3. Negative/unconditional direction (harder variant): a proof that deterministic NC matching implies something believed false, e.g., an unlikely circuit-class collapse — unlikely to be required; the standard acceptance criterion is a constructive algorithm with full proofs.
Partial credit variants: NC^k for fixed k, or deterministic isolation with quasi-polynomial bit-length weights but NC computation — these would be incremental, not solving.

## How to start

1. Read MVV (1987) §on the isolation lemma and the Tutte-matrix algorithm first — everything routes through "if we could isolate deterministically, we'd be done."
2. Read Fenner–Gurjar–Thierauf (2016) to understand the bipartite deterministic isolation technique (based on bit-level weight constructions from studies of the perfect matching polytope / short paths in the matching polytope graph), then Svensson–Tarnawski (2017) for the general-graph reduction and where quasi-polynomial blowup enters.
3. Natural attack: find a polylog-depth analogue of the "decoupling/margin" isolation, or an NC procedure for navigating the matching polytope (weight manipulation via Newton-like steps).
4. Main obstacle: isolation requires breaking symmetry among exponentially many perfect matchings; known constructions need quasi-polynomial weight bit-length or recursive depth. A good exercise: try to isolate in bipartite graphs with only polynomial bit-length weights in NC.

## Key references

- K. Mulmuley, U. V. Vazirani, V. V. Vazirani, "Matching is as easy as matrix inversion," Combinatorica 7 (1987) 105–113. RNC perfect matching via the isolation lemma and Tutte-matrix rank computation. https://doi.org/10.1007/BF02579206
- S. Fenner, R. Gurjar, T. Thierauf, "Bipartite perfect matching is in quasi-NC," STOC 2016. First deterministic isolation (quasi-NC) for bipartite matching. https://doi.org/10.1145/2897518.2897565
- O. Svensson, J. Tarnawski, "The matching problem in general graphs is in quasi-NC," FOCS 2017. Extends deterministic isolation to general (non-bipartite) graphs, giving quasi-NC. https://doi.org/10.1109/FOCS.2017.52
- E. Allender, K. Reinhardt, S. Zhou, "Isolation, matching, and counting," CCC 1999. Places bipartite perfect matching in SPL, a complexity-class lens on isolation. https://doi.org/10.1109/CCC.1999.766260
- R. Gurjar, T. Thierauf on linear matroid intersection in quasi-NC (2017/2020) — extensions showing where the technique reaches. (verify exact venue)

## Warnings

- Do not conflate decision ("does a perfect matching exist") with search; for NC they are equivalent via standard decimation, but the interesting derandomization is isolation.
- The isolation lemma cannot be fully derandomized by naive weight assignments: small-weight weightings provably fail on some graphs; the bottleneck is genuinely combinatorial.
- The Svensson–Tarnawski result gives quasi-polynomial processors, not just polylog time — many misread it as solving the problem. It does not.
- Also distinct from the parallel complexity of max-flow or approximate matching; read carefully which variant a paper addresses.
- Whether NC requires NC^k for small k is a separate refinement; the open problem is existence of any fixed k.

---
*`ALGO-000121` · unverified*

## Acceptance guidance

1. A deterministic isolation lemma for general graphs: an NC-computable (polylog depth, poly work) edge-weighting of any graph guaranteeing a unique minimum-weight perfect matching — this plus MVV yields NC.
2. Directly: an explicit NC algorithm (O(log^k n) time, n^O(1) processors) outputting a perfect matching or reporting none, with a correctness proof.
3. Negative/unconditional direction (harder variant): a proof that deterministic NC matching implies something believed false, e.g., an unlikely circuit-class collapse — unlikely to be required; the standard acceptance criterion is a constructive algorithm with full proofs.
Partial credit variants: NC^k for fixed k, or deterministic isolation with quasi-polynomial bit-length weights but NC computation — these would be incremental, not solving.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/cc1b1594-809d-4f85-ba9a-6f537dc7bbd0?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000121.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000121)
