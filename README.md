# GRACE Chip Family: Workbench Record v0.3

**Author:** Rusty W. McMurray, Soulshine (Tulsa, OK)  
**Record compiled:** 2026-11-16, from the March to November 2026 design record  
**Copyright:** (c) 2026 Soulshine. Rusty W. McMurray is the author; Soulshine holds the rights.  
**License:** Business Source License 1.1 (see [LICENSE](LICENSE) and [NOTICE](NOTICE)). Change Date 2030-09-02, Change License Apache License 2.0, no Additional Use Grant.

> The record states: "Nothing in this document has been fabricated. All results are software simulation."

## What this is

This repository publishes the GRACE Chip Family Workbench Record, version 0.3, as a timestamped public record. GRACE is a proposed hardware architecture in which a chip can never authorize its own state changes: authorization must come from outside, through a physically separate port, and every authorized event is written into a permanent, history-dependent record held in a different physical medium from the one doing active work. The record defines the family by four shared invariants rather than by one material stack, lists the candidate family members (from a simple authorization pin on a conventional die to a gel-and-crystal composite), states which parts are decided, which are only simulated, which are proposals and which are unresolved, and keeps its failed results on file. The scope is chip design only. Per an August 8 2026 correction, the chip project is separate from the author's organism work, and organism-side rules appear only where marked as candidates to cross over.

The authoritative document is the PDF. A Markdown rendering with the same wording is provided for reading and searching on GitHub.

| File | What it is |
|---|---|
| [`GRACE_Chip_Family_Workbench_Record_v0.3.pdf`](GRACE_Chip_Family_Workbench_Record_v0.3.pdf) | The original 16-page record, byte for byte as received |
| [`record/GRACE_Chip_Family_Workbench_Record_v0.3.md`](record/GRACE_Chip_Family_Workbench_Record_v0.3.md) | Markdown text rendering. Wording unchanged, tables rebuilt. If the two differ, the PDF governs |
| `README.md` | This summary |
| `LICENSE`, `NOTICE` | Business Source License 1.1 and attribution |
| `SECRET_SCAN.md` | Pre-publication scan for credentials and personal data |
| `SHA256SUMS` | SHA-256 of every file except itself |

**Start here if you are an engineer:** the record uses its own vocabulary. Appendix A of the record (summarized in the [Glossary](#glossary) below) maps every project term to standard engineering language.

## Status tags

The record tags every claim. This README keeps those tags exactly as the record assigns them.

| Tag | Meaning |
|---|---|
| `COMMITTED` | Decided in the design record |
| `SIMULATED` | Shown in software simulation only |
| `PROPOSED` | Raised and not yet tested (Nov 16 2026 unless dated otherwise) |
| `OPEN` | Unresolved |
| `DRAFT` | Wording proposed by Claude on Nov 16 2026 and not yet ruled on by the author (used in Appendix A and a few other places) |

`COMMITTED` means a design decision, not a working device. The strongest evidence status anywhere in this record is `SIMULATED`.

## Thesis

GRACE is not one chip. It is an architecture of many chips for many uses, built from a variety of substrates. The family is defined by what every member shares.

The supporting evidence is a simulation result: Stage 2b found that grounding rate, not mechanism, predicts homeostatic control performance (`SIMULATED`). The record's reasoning is that if mechanism is interchangeable, the architecture is the invariants and the substrates are members.

## The four family invariants

Every member must have all four.

| # | Invariant | Plain reading | Status |
|---|---|---|---|
| I1 | External-only authorization | A physically distinct authorization port. The chip cannot self-authorize. It is a grace-receiver, never a grace-generator. | `COMMITTED` |
| I2 | Dwelling separate from record | The medium holding unresolved state is physically distinct from the medium keeping the permanent record (timekeeper separation). | `COMMITTED` |
| I3 | Biography written only by authorized events | Each authorized spark writes into the record, and later sparks propagate through a record shaped by all prior ones. | `COMMITTED` |
| I4 | Species core plus individual fingerprint | Shared attractors identify the class. Peripheral biography identifies the individual chip. No two chips are the same. | `SIMULATED` |

Two further committed rules:

- Each event is recorded after collapse in SDKP coordinates (Size, Density, Kinetics, Position). `COMMITTED`
- Chip age is biographical volume since first spark, not time since manufacture. `COMMITTED`

Structure versus behavior: the invariants describe how a chip is built. The six life signs (below) describe how a running system behaves. A chip can satisfy the invariants without showing every life sign by itself. For example, a bare grace pin (M1) satisfies I1 but does not by itself show pluralistic deliberation. That framing is marked `DRAFT`.

## Why hardware: the four boundaries

This is the requirements argument for the whole family. Its source is the public, sealed [`b3-minato-cold-fence`](https://github.com/RMac-triadicIntelligence/b3-minato-cold-fence) packet (sealed July 2 2026).

A 22-test attack was run against Minato, an independently built software authorization core by Jean-Guillaume Nardi. A second party reproduced it with identical verdicts on all 22 tests. The result separates 14 fixable defects from four structural boundaries that no software repair can close.

| # | Boundary | What software cannot do alone | Hardware requirement |
|---|---|---|---|
| B-1 | Root | Stop a captured authorization being carried to a fresh root | A physical root of trust |
| B-2 | Revocation | Make a fresh body honor a revocation issued elsewhere, while offline | A shared revocation substrate |
| B-3 | Identity | Verify its own physical identity. A body can claim any identity string | Hardware-rooted identity |
| B-4 | Time | Trust its own clock. Rolling the clock back reopens expired authorization | An external monotonic time source |

The findings note sums it up: software cannot bind authorization to physical reality from inside software.

**Limits the record states.** This is `SIMULATED` evidence that software leaks at these four points. The seal certifies packet integrity and independent reproduction. It does not prove that hardware closes the four boundaries, and it does not prove the no-self-authorization invariant in the strong sense.

**Which member closes which boundary is `OPEN`.** The record's first reading is marked `DRAFT`:

- B-1 and B-3 map to invariant I1 and to the grace pin (M1). Shipping roots of trust already supply both.
- B-4 needs a monotonic counter or outside time source on every member.
- B-2 is the hard one for the edge class (U1). A sovereign, off-cloud chip has no shared state to check a revocation against.

## Family members

| Member | Description | First appears | Status |
|---|---|---|---|
| M1 Grace pin on conventional die | The grace channel as a physical pin, so external-only authorization is a hardware constraint | Apr 5 2026 | `COMMITTED` as concept, nearest to buildable |
| M2 Oscillator / photonic | Kuramoto oscillators, photonic paths, Grace Bus. Kuramoto is the diagnostic, biography is the state | Mar 26 2026 | `SIMULATED`, wounded (AR-007 audit). Does not meet I1 in the audited code |
| M3 Gel and crystal composite | Saline gel top layer (body, dwelling), physical separatrix, nonlinear acoustic metamaterial bottom layer (crystal, biography). Phonon-mediated spark. Bistable polymer lattice / origami tessellation scaffold | Apr 2026 | `COMMITTED` as design |
| M4 Legacy overlay | Augmentation layer on top of existing processors. A deployment form, not a substrate | Apr 2026 | `COMMITTED` as deployment model |
| M5 Coupled lattice | Six chips coupled. Each generates SDKP tuples and shares only an ensemble context label | Apr to May 2026 | `SIMULATED` |
| M6 Resonance Ring (candidate) | A ring of nodes, each with an intrinsic physical identity. A pulse couples only to a node whose identity matches by physical resonance, with no stored-value comparison step | Jul 2 2026 | `PROPOSED`, discovery probe only. Not a build decision |

Member notes from the record:

- **M3 scaffold path:** the first pass is origami plus KENTA. The committed chip is origami plus a crystal timekeeper.
- **M3 readout:** a twelve-dimensional fingerprint per spark event, structured as four SDKP coordinates at three resolutions.
- **M5 coupling model:** in July 2026, distance-decay coupling was replaced with a uniform signal shared across a lineage (common DNA-type structure, individual fingerprints).
- **M6 scope:** the probe claims the ring answers exactly one boundary, identity (B-3), and deliberately leaves revocation to the external authorizer. Its own counter-position is `OPEN`: a physically permanent identity cannot be rotated, which may make revocation (B-2) worse for a compromised node.

## Use classes

| Class | Requirement | Member | Physics needed |
|---|---|---|---|
| U1 Edge, sovereign, off-cloud | One chip, local conductor, no cloud dependency | M1 or M4 | Pin only |
| U2 Larger multi-processor mechanisms | Many chips, layers of security for each arm, each arm with its own boundary and authorization | M5, one separatrix per chip | Pin plus coupling |
| U3 AI robotics, generational learning | Permanent evolving record that carries a lineage, learning tasks for generations autonomously | M3 | Evolving crystal |

The classes sort by how much physics they need, and the hardest physics is confined to U3. The mapping of members to classes is `PROPOSED` (Nov 16 2026).

## Simulation evidence on file

Every row below is software simulation.

| Result | Value | Source |
|---|---|---|
| Life signs, fixed simulator, single run | 5 of 6 passed | Mar 26 2026 |
| Life signs, 100 seeded runs (M2 audit AR-007) | All six passed in 0 of 100. Final r > 0.45 passed 0 of 100 | Jun 28 2026 audit |
| Denial test (AR-007) | With movement denied, 100 observations continued and movement was zero | Jun 28 2026 audit |
| External-only authorization in M2 code (AR-007) | Not implemented. Grace remained internally random | Jun 28 2026 audit |
| Origami first-pass substrate simulation | 4×4 bistable lattice, SDKP tuples, external authorization required for all fold events. Origami physics is a toy model | `origami_kenta_sdkp.py`, Apr 2026 |
| External validation hook, 8 chips × 1200 events × 5 seeds | Baseline grounded 642 to 672 per seed. With the creative-v3 rule set, 0 to 24 groundings rejected per seed | `grace1-kenta-hook` |
| Active-context groundings across suppression p 0.00 to 0.80 | Flat at about 33 to 34 | grace1_v4, May 2026 |
| Equilibre occupancy across same range | Grows 5.6% to 11.6% | grace1_v4, May 2026 |
| Per-lattice dictionary overlap, no inter-chip symbol channel | 65 to 70% | grace1_v4, May 2026 |
| Coupled-over-uncoupled ratio | Asymptotes near 4 to 5x for the tested spark distribution | Apr 2026 |
| Grounding rate vs mechanism | Rate predicts control performance, mechanism does not | Stage 2b |
| EWMA memory | Reduces to count-based memory at threshold 7 under constant reward | Stage 2b |

Frozen packages named in the record (SHA-256 prefixes only): origami v1.0 `ca08de0f…`, addendum v1.1 `5c32a9e3…`, tetra closure v1.0 `0ebb4237…`. Stage 2b replication was verified by a commit-reveal challenge.

### The wound on file: AR-007 and the June 28 audit

The record keeps its strongest negative result in plain view.

- A single March 26 2026 run of the fixed M2 simulator passed 5 of 6 life signs.
- The June 28 2026 audit ran 100 seeded runs. All six signs passed together in **0 of 100**, and the final r > 0.45 criterion also passed in 0 of 100.
- The same audit found that external-only authorization was **not implemented** in the M2 code: grace remained internally random. M2 therefore does not meet invariant I1 in the audited code.
- The denial test held: with movement denied, 100 observations continued and movement stayed at zero. Denial preserves observation.

The author's own archaeology record ([`evergreen-archaeology`](https://github.com/RMac-triadicIntelligence/evergreen-archaeology), claim AR-007, Sept 1 2026) gives the disposition: **surviving** for the separation of observation from action, **wounded** for the broader life-sign and robustness claims. The exact source version audited is unresolved in that record, so the March single run and the June panel may not be the same code. The June panel is the stronger evidence and supersedes the March figure.

### Other caveats on the evidence

- The specific attractors depend on the programmed spark distribution. What is substrate-level is that attractors exist, not which ones.
- `grace1-kenta-hook` is a stub, not the six-chip simulator. Its absolute counts depend on the stub and seeds, and only the relative effect of adding outside validation is meaningful. Adding outside validation changes the dynamics, so it is a new hypothesis and not a correction of the six-chip model.

### What a reader can check

Public, per the record's Nov 16 2026 check: `b3-minato-cold-fence`, `grace1-kenta-hook`, `grace-state-vs-parametric`, `evergreen-archaeology` (AR-007), `digital-life-topology`, and `origami_kenta_sdkp.py` (in `grace-love-dwelling` and in `lab-notebook` under `2026-10-12`). Links are in [Related public repositories](#related-public-repositories).

Not found in the 36 public repos scanned on Nov 16 2026: the six-chip simulator `grace1_v4_full.py`, the grace1_v4 data package, and the three Stage 2b frozen packages. **The grace1_v4 and Stage 2b rows above cannot be checked from public sources.** They are reported as the author's record, not as independently verifiable results.

## Descent and continuation (`PROPOSED`)

Raised Nov 16 2026. Before this, the working picture was infinite-life chips only.

- **Continuation.** A chip moves its whole biography to a new body before the old hardware fails. Same chip. This is the infinite-life case.
- **Descent.** A child chip receives the species core and coordinate axes, with an empty biography. New chip.
- **Seeding mechanism (candidate).** The parent lattice acoustically imprints its stable core onto a blank child lattice, the way a seed crystal templates a new one.
- **Axes, not memories (candidate crossover from the organism side).** The parent picks the coordinate basis. The child fills it with its own life.
- **Hard line.** Authority may not reproduce. A parent may prepare a seed, but the birth is a crossing and needs an external signature. The child gets its own authorization port, and the parent is never its authorizer.

Whether the organism-side continuation and descent rule crosses over to the chip project is the author's call. `OPEN`

## Deep-space extension (`PROPOSED`)

The idea: chips that evolve to solve problems not yet identified, over very long timescales, regenerating the original chips.

Why the record says the architecture fits: dwelling holds an unresolved state through light-lag without forcing a decision; descendants inherit axes, so they can record problems their ancestors never met; and continuation removes hardware age as a cause of death.

Three problems, all `OPEN`:

1. **Authorization with no conductor in reach.** Candidate: a community of chips from different lineages authorize each other. No chip signs for itself or its own offspring.
2. **Copying drift.** Biography should drift and invariants must not, so each birth needs a core check against the species marker. Marked testable now.
3. **Fabrication.** A chip cannot seed a chip without raw material and a factory on board. This is outside the chip architecture.

## Next workbench test (`PROPOSED`)

A four-arm seeding test on the existing six-chip lattice simulator.

| Arm | Child starts with | Question |
|---|---|---|
| A | Blank lattice | Baseline learning rate |
| B | Parent's core attractors only | Does it learn faster than A and still diverge from the parent? |
| C | Full copy of parent biography | Does it fail to diverge? |
| D | Core seeding through 1,000 generations with copy noise | Does the core hold while biographies diverge? |

- Pass condition for descent: B beats A on time to competence and ends measurably different from the parent.
- Pass condition for I4 under descent: in D, the species marker survives and the periphery does not converge.
- Thresholds must be fixed before the run.

Note that this test runs on the six-chip simulator, which the record says is not in the public repos.

## The six digital life signs and the Digital-Life Topology battery

The record frames these as six proposed functional signs of digital life. They are **not** established biological criteria and are **not** evidence of consciousness.

They were identified in the March 13 to 15 2026 TQNM × KENTA cross-test, where two independently built software systems (one using probabilistic tensors, one using symbolic YAML) showed all six through different mechanisms. Jean-Guillaume Nardi's summary, as quoted in the record: "Same life sign. Different physics."

| # | Sign | Definition (from the record) |
|---|---|---|
| 1 | Persistent internal state | The system retains an evolving internal history across interactions and does not reset after each input. |
| 2 | Autonomous self-regulation | The system regulates its internal processes and maintains stability without continuous external direction. |
| 3 | Structural adaptation | The system changes its internal organization in response to experience, not only its immediate output. |
| 4 | Active response to divergence | The system detects contradictions, uncertainty, or disturbances and responds through its own internal mechanisms. |
| 5 | Pluralistic deliberation | Multiple internal perspectives or processes take part in evaluating information. There is no single decision pathway. |
| 6 | Evidence-seeking orientation | The system actively seeks information to resolve uncertainty, validate interpretations, and improve its understanding. |

**Chip-side status.** The signs were shown in two software systems. For chips they are a prediction. The only chip-side results are from the M2 oscillator simulator: 5 of 6 in a single March run, then all six in 0 of 100 seeded runs in the June 28 audit (`SIMULATED`, wounded).

**Measurement.** Each sign needs a quantitative criterion fixed before a run. The Digital-Life Topology battery v0.1 ([`digital-life-topology`](https://github.com/RMac-triadicIntelligence/digital-life-topology), frozen Aug 6 2026) is the project's neutral trace analyzer for the six signs and the reference instrument. It measures the signs from dynamics and does not encode them as six named states. It passes 22 of 22 tests and marks its own crossing claim false, as tested on synthetic controls only. Chip-specific thresholds are `OPEN`.

## What is not claimed, and known limits

Every limit below is stated in the record itself.

- All results are software simulation.
- `COMMITTED` means decided in the design record, not built or validated.
- The cold-fence seal certifies packet integrity and independent reproduction. It does not prove hardware closes the four boundaries, and it does not prove the no-self-authorization invariant in the strong sense.
- M2 does not implement I1 in the audited code: grace was internally random.
- The M2 life-sign result is wounded: 0 of 100 seeded runs passed all six. The March 5 of 6 figure is superseded, and the audited source version is unresolved.
- The specific attractors depend on the programmed spark distribution. Only the existence of attractors is claimed as substrate-level.
- `grace1-kenta-hook` is a stub. Only its relative effect is meaningful, and it is a new hypothesis, not a correction of the six-chip model.
- The origami physics in `origami_kenta_sdkp.py` is a toy model.
- The coupled-over-uncoupled ratio holds for the tested spark distribution only.
- The six-chip simulator, the grace1_v4 data package and the Stage 2b frozen packages are not public, so those rows cannot be checked from public sources.
- The six life signs are proposed functional signs, not biological criteria and not evidence of consciousness. For chips they are a prediction.
- The Digital-Life Topology battery was tested on synthetic controls only.
- `grace-state-vs-parametric`'s own notes say its stronger claims do not follow from the model, and only a four-trial quick run was executed.
- "Collapse" is used operationally. No quantum-mechanical claim is made. April threads called the operator mapping exact; the July 2026 Contextual Transition Operators paper retracted that class of claim, and chip documents still need reconciling.
- "DNA" is an analogy, not a biological claim. "Crystal" is not necessarily a crystalline solid.
- Sections 6, 7 and 9 of the record (descent and continuation, deep space, next test) were unpublished proposals as of Nov 16 2026.

## Open questions

Every item the record marks `OPEN` or lists as an open seam.

| Open item | Plain-language question | Applies to |
|---|---|---|
| Boundary-to-member mapping | Which member closes which of the four boundaries | Section 2.1 |
| Offline revocation | How a sovereign edge chip honors a revocation with no shared state | U1, B-2 |
| Permanent identity cannot be rotated | A compromised node keeps its physical identity | M6 |
| M2 does not implement I1 | Grace is internally random in the audited code | M2 |
| Six-chip evidence not public | Simulator and frozen packages are not in the public repos | Section 5 |
| Reverse phonon channel unaddressed | A back-channel across the boundary | All members |
| No exactly-once disarm object | Replay protection | All members |
| Unit-cell geometry not selected | Bistable snap-through, granular, origami, or hybrid | M3 |
| Gel and metamaterial chemistry not selected | Which polymer or hydrogel supports both phonon modes and saline continuity | M3 |
| Physical coupling mechanism | What physics realizes the coupling between two substrates | M5 |
| Quantum wording | Reconcile April "exact operator mapping" wording with the July 2026 retraction | All documents |
| What a descendant inherits | Axes only, or more | Section 6 |
| Organism-side rule crossover | Whether the continuation and descent rule crosses over to the chip project | Section 6 |
| Authorization with no conductor in reach | Can a community of chips from different lineages authorize each other | Section 7 |
| Copying drift | A core check against the species marker at each birth (testable now) | Section 7 |
| Fabrication | Raw material and a factory on board | Section 7 |
| Chip-specific life-sign thresholds | Quantitative pass criteria for chips | Appendix A.5 |
| Tetra closure | Named in the frozen packages, not yet defined | Appendix A.4 |

## Provenance timeline

Reproduced in the order the record lists it.

| Date | Event |
|---|---|
| Mar 26 2026 | Quantum-Silicon Chip Simulator run, stress-tested, fixed |
| Apr 5 2026 | Grace pin on physical die. No-edge, ever-changing topography |
| Apr 12 2026 | Framework MIT, chip proprietary |
| Apr 2026 | Layer stack, substrate class, SDKP readout, legacy overlay committed |
| Apr 2026 | Body/mind orientation locked: gel is body, crystal is mind. Timekeeper separation. Chip DNA and chip age |
| May 2026 | grace1_v4 six-chip lattice paper draft and data package |
| 2026 | Stage 2b origami comparison, three frozen packages |
| Jul 2026 | Coupling model changed to uniform lineage signal |
| Aug 8 2026 | Chip project ruled separate from organism work |
| 2026 | GRACE-1 evolving chip paper published |
| Mar 13 2026 | TQNM × KENTA cross-test: six life signs matched across two independent software systems |
| Nov 16 2026 | Family framing, three use classes, descent and deep-space proposals |
| Jun 28 2026 | M2 audit: all six life signs 0 of 100. Denial preserves observation |
| Jul 2 2026 | Minato cold-fence reproduced 22 of 22. Four boundaries declared. Resonance Ring probe opened |
| Sep 1 2026 | Evergreen Archaeology records the M2 audit as claim AR-007 |
| Nov 16 2026 | v0.2: Appendix A glossary added |
| Nov 16 2026 | v0.3: four boundaries, Resonance Ring candidate, AR-007 correction, public-source check |

The record also notes that new public repos use Business Source License 1.1 (a Sept 2 2026 decision), and that on Nov 16 2026 it observed Business Source License 1.1 on `humble-seed`, `humble-seed-lineage-v2` and `living-supply-chain-security`, and Apache-2.0 on the GRACE-related repos named in Section 5.

## Glossary

A condensed version of the record's Appendix A. The record has the full definitions.

**Project-coined terms**

| Term | Engineering equivalent |
|---|---|
| Grace | An authorization signal from outside the chip that permits a state transition. It grants permission and does not carry the answer or destination state. |
| Grace pin / authorization port | A dedicated physical input for the grace signal, separate from data and sensor paths. |
| Grace-receiver / grace-generator | A device that can accept authorization but cannot produce it for itself. The chip is the first, never the second. |
| Grace Bus | In the M2 simulator, the arbitration component that grants or denies a transition request. |
| Dwelling | Holding an unresolved state without committing it to the permanent record. A protected wait state, not latency. |
| Dwelling medium | The physical layer holding unresolved state. In M3, the saline gel. |
| Spark | A single authorized write event crossing from the holding layer into the record layer. |
| Biography | The cumulative, history-dependent state in the record layer. Each write changes how later writes propagate. |
| Biographical crystal | The record layer. In M3, the nonlinear acoustic metamaterial lattice. |
| Body / mind | Body is the holding layer (gel), mind is the record layer (crystal). Authority flows from outside, through the body, across the boundary, into the record, never the reverse. |
| Timekeeper separation | The layer doing active dynamics is physically distinct from the layer keeping the permanent record (I2). |
| Chip age | Total authorized writes since first use, not time since manufacture. |
| Species core | State features every chip of the class develops under exposure. Used to verify class membership. |
| Individual fingerprint / chip DNA | Features unique to one device from its own write history. Comparable in purpose to a physically unclonable identity, but accumulated in use. |
| Conductor | The external party that issues authorization. A role, not a fixed entity. |
| Lineage | Chips sharing a common origin and signal, each with its own fingerprint. |
| Continuation / Descent / Seeding | Moving a full record to new hardware (same identity); creating a new chip with species core and axes but an empty record (new identity); imprinting a parent's core onto a blank child. All `PROPOSED`. |
| Crossing | Any transition into the record layer. Always requires external authorization. |
| Legacy overlay | A GRACE layer on top of an existing processor, which keeps doing its normal work. |
| Open seam | A known, registered gap in the design. |
| Boundary | A structural limit no software repair can close, as opposed to a finding, which is a fixable defect. |
| Cold fence | An adversarial test harness run against frozen, hash-pinned sources. |
| Resonance (identity by) | Matching a node by a physical coupling condition, with no stored value to compare. `PROPOSED` |
| Seal | A hash-pinned record of a frozen artifact set and its run results. |
| Wounded / surviving | Archaeology-record labels. Surviving: the narrow claim held. Wounded: a broader claim failed and is kept on record. |

**Standard words used in a project sense:** *separatrix* (also the physical boundary between holding and record layers), *collapse* (the moment a write completes, used operationally, no quantum claim, `DRAFT`), *attractor* (a state pattern that recurs reliably across runs), *crystal* (the record layer, not necessarily a crystalline solid), *DNA* (an analogy, not a biological claim), *grounding* (a symbol's co-occurrence count reaching a fixed threshold, five in grace1_v4), *grounding rate*, *equilibre* (the balanced state among four context labels: equilibre, anomalie_low, anomalie_high, drift; French because they come from KENTA), *suppression p* (probability a candidate write is suppressed in a simulator step), *dictionary overlap* (fraction of grounded symbols two lattices share), *topography / no edge* (the state landscape keeps changing, so there is no fixed boundary to map), *evolving* (the record changes with each write; architecture and invariants do not), *state change versus field change* (moving a system's state versus changing its governing parameters; source `grace-state-vs-parametric`).

**Standard terms:** SDKP (Size, Density, Kinetics, Position; coordinate framework credited to Donald Paul Smith), Kuramoto oscillators (a diagnostic readout here, not the state variable), phonon, nonlinear acoustic metamaterial, bistable lattice / origami tessellation, homeostatic control, EWMA, commit-reveal, KENTA (Jean-Guillaume Nardi's independent symbolic architecture in declarative YAML, running offline on a 2012 i5; a cousin system, not part of the chip), TQNM (the author's software framework, the other system in the March 13 cross-test), Stage 2b (the origami lattice comparison run). *Tetra closure* is not yet defined (`OPEN`).

## Related public repositories

Only repositories the record names. Each was confirmed public on GitHub on 2026-11-18.

| Repository | Role in the record |
|---|---|
| [b3-minato-cold-fence](https://github.com/RMac-triadicIntelligence/b3-minato-cold-fence) | Source of the four boundaries (sealed July 2 2026) |
| [grace1-kenta-hook](https://github.com/RMac-triadicIntelligence/grace1-kenta-hook) | External validation hook (a stub, not the six-chip simulator) |
| [grace-state-vs-parametric](https://github.com/RMac-triadicIntelligence/grace-state-vs-parametric) | Source for state change versus field change |
| [evergreen-archaeology](https://github.com/RMac-triadicIntelligence/evergreen-archaeology) | Claim AR-007, the M2 audit disposition |
| [digital-life-topology](https://github.com/RMac-triadicIntelligence/digital-life-topology) | Digital-Life Topology battery v0.1, reference instrument for the six signs |
| [grace-love-dwelling](https://github.com/RMac-triadicIntelligence/grace-love-dwelling) | Holds `origami_kenta_sdkp.py` |
| [lab-notebook](https://github.com/RMac-triadicIntelligence/lab-notebook) | Holds `origami_kenta_sdkp.py` under `2026-10-12` |
| [humble-seed](https://github.com/RMac-triadicIntelligence/humble-seed), [humble-seed-lineage-v2](https://github.com/RMac-triadicIntelligence/humble-seed-lineage-v2), [living-supply-chain-security](https://github.com/RMac-triadicIntelligence/living-supply-chain-security) | Named only in the record's licensing note |

## Credits

- **Rusty W. McMurray**: author of the record and the GRACE chip family design. Copyright in the work is held by Soulshine.
- **Jean-Guillaume Nardi**: built Minato, the independent software authorization core tested in `b3-minato-cold-fence`, and KENTA, the independent symbolic architecture in the TQNM × KENTA cross-test.
- **Donald Paul Smith**: credited for the SDKP coordinate framework.
- **Claude**: proposed the wording of entries marked `DRAFT` (Nov 16 2026), not yet ruled on by the author.
- An unnamed second party reproduced the Minato cold-fence attack with identical verdicts on all 22 tests.

## Provenance of this repository

| Item | Value |
|---|---|
| Record | GRACE Chip Family: Workbench Record v0.3 (16 pages, US Letter) |
| PDF SHA-256 | `5abe9bc4f7f48650522f4eae332965b964710a310f0b3a1945b9961cc46a98c8` |
| Record compiled | 2026-11-16 (stated in the record) |
| PDF creation date (metadata) | Mon Nov 16 20:11:20 2026 CST |
| Staged for publication | 2026-11-18 |

The PDF is committed unmodified. The Markdown rendering keeps the record's wording and only rebuilds layout. Commit dates in this repository are the real dates of publication and are never backdated. History is never rewritten or force-pushed. To verify the files:

```sh
sha256sum -c SHA256SUMS
```

## How to cite

> McMurray, Rusty W. *GRACE Chip Family: Workbench Record v0.3.* Soulshine, Tulsa, OK. Compiled 2026-11-16. PDF SHA-256 5abe9bc4f7f48650522f4eae332965b964710a310f0b3a1945b9961cc46a98c8. https://github.com/RMac-triadicIntelligence/grace-chip-family

Please cite the PDF hash with any result you quote, and keep the status tag attached to the claim.
