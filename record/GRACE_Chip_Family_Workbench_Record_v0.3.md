<!-- Markdown text rendering of GRACE_Chip_Family_Workbench_Record_v0.3.pdf
     (sha256 5abe9bc4f7f48650522f4eae332965b964710a310f0b3a1945b9961cc46a98c8).
     Wording is unchanged from the PDF. Line wrapping and table layout were rebuilt
     from pdftotext output and checked against rendered pages. The PDF is the
     authoritative copy; if the two differ, the PDF governs. -->

# GRACE Chip Family — Workbench Record v0.3

**Author:** Rusty W. McMurray, Soulshine (Tulsa, OK)  
**Compiled:** 2026-11-16, from the March–November 2026 design record  
**Scope:** Chip design only. Per the Aug 8 2026 correction, this is a separate project from the organism work. Organism-side rules are cited here only where marked as candidates to cross over.

**Status tags used below**

- `COMMITTED` — decided in the design record
- `SIMULATED` — shown in software simulation only
- `PROPOSED` — raised and not yet tested (Nov 16 2026 unless dated otherwise)
- `OPEN` — unresolved

Nothing in this document has been fabricated. All results are software simulation.

**Reading note for engineers:** this record uses the project's own vocabulary. Appendix A translates every project term into standard engineering language. Read it first if the terms are new.

---

## 1. Thesis

GRACE is not one chip. It is an architecture of many chips for many uses, built from a variety of substrates. The family is defined by what every member shares, not by any single material stack.

Supporting evidence: Stage 2b found that grounding rate, not mechanism, predicts homeostatic control performance ( `SIMULATED` ). If mechanism is interchangeable, the architecture is the invariants and the substrates are members.

---

## 2. Family invariants

Every member must have all four.

| # | Invariant | Status |
|---|---|---|
| I1 | External-only authorization. A physically distinct authorization port. The chip cannot self-authorize. It is a grace-receiver, not a grace-generator. | `COMMITTED` |
| I2 | Dwelling separate from record. The medium that holds unresolved state is physically distinct from the medium that keeps the permanent record (timekeeper separation). | `COMMITTED` |
| I3 | Biography written only by authorized events. Each authorized spark writes into the record. Later sparks propagate through a record shaped by all prior ones. | `COMMITTED` |
| I4 | Species core plus individual fingerprint. Shared attractors identify the class. Peripheral biography identifies the individual chip. No two chips are the same. | `SIMULATED` |

Biographical coordinates: SDKP (Size, Density, Kinetics, Position), recorded per event after collapse. `COMMITTED`

Chip age is biographical volume since first spark, not time since manufacture. `COMMITTED`

### 2.1 Why hardware: the four boundaries

This is the requirements argument for the whole family. Source: `b3-minato-cold-fence` (public, sealed July 2 2026).

A 22-test attack was run against an independently built software authorization core (Minato, by Jean-Guillaume Nardi). A second party reproduced it with identical verdicts on all 22 tests. The result separates 14 fixable defects from four structural boundaries that no software repair can close.

| # | Boundary | What software cannot do alone | Hardware requirement |
|---|---|---|---|
| B-1 | Root | Stop a captured authorization being carried to a fresh root | A physical root of trust |
| B-2 | Revocation | Make a fresh body honor a revocation issued elsewhere, while offline | A shared revocation substrate |
| B-3 | Identity | Verify its own physical identity. A body can claim any identity string | Hardware-rooted identity |
| B-4 | Time | Trust its own clock. Rolling the clock back reopens expired authorization | An external monotonic time source |

Summary statement from the findings note: software cannot bind authorization to physical reality from inside software.

Status: `SIMULATED` as evidence that software leaks at these four points. The seal certifies packet integrity and independent reproduction. It does not prove that hardware closes them, and it does not prove the no-self-authorization invariant in the strong sense.

Which family member closes which boundary is `OPEN` . First reading ( `DRAFT` ):

- B-1 and B-3 map to invariant I1 and to the grace pin (M1). Shipping roots of trust already supply both.
- B-4 needs a monotonic counter or outside time source on every member.
- B-2 is the hard one for the edge class (U1). A sovereign, off-cloud chip has no shared state to check a revocation against.

---

## 3. Family members

| Member | Description | First appears | Status |
|---|---|---|---|
| M1 **Grace pin on conventional die** | Grace channel as a physical pin, so external-only authorization is a hardware constraint | Apr 5 2026 | `COMMITTED` as concept, nearest to buildable |
| M2 **Oscillator / photonic** | Kuramoto oscillators, photonic paths, Grace Bus. Kuramoto is the diagnostic, biography is the state | Mar 26 2026 | `SIMULATED` , wounded. See the AR-007 audit in Section 5. Does not meet I1 in the audited code |
| M3 **Gel and crystal composite** | Saline gel top layer (body, dwelling), physical separatrix, nonlinear acoustic metamaterial bottom layer (crystal, biography). Phonon-mediated spark. Bistable polymer lattice / origami tessellation scaffold | Apr 2026 | `COMMITTED` as design |
| M4 **Legacy overlay** | Augmentation layer on top of existing processors. A deployment form, not a substrate | Apr 2026 | `COMMITTED` as deployment model |
| M5 **Coupled lattice** | Six chips coupled. Each generates SDKP tuples and shares only an ensemble context label | Apr–May 2026 | `SIMULATED` |
| M6 **Resonance Ring** (candidate) | A ring of nodes, each with an intrinsic physical identity. A pulse couples only to a node whose identity matches by physical resonance, with no stored-value comparison step | Jul 2 2026 | `PROPOSED` , discovery probe only. Not a build decision |

M3 staged scaffold path: first pass is origami plus KENTA, committed chip is origami plus crystal timekeeper.

M3 readout: twelve-dimensional fingerprint per spark event, structured as four SDKP coordinates at three resolutions.

M6 scope: the probe claims the ring answers exactly one boundary, identity (B-3), and deliberately leaves revocation to the external authorizer. Its own open counter-position: a physically permanent identity cannot be rotated, which may make revocation (B-2) worse for a compromised node. `OPEN`

M5 coupling model: July 2026 replaced distance-decay coupling with a uniform signal shared across a lineage (common DNA-type structure, individual fingerprints).

---

## 4. Use classes

| Class | Requirement | Member | Physics needed |
|---|---|---|---|
| U1 **Edge, sovereign, off-cloud** | One chip, local conductor, no cloud dependency | M1 or M4 | Pin only |
| U2 **Larger multi-processor mechanisms** | Many chips, layers of security for each arm, each arm with its own boundary and authorization | M5, one separatrix per chip | Pin plus coupling |
| U3 **AI robotics, generational learning** | Permanent evolving record that carries a lineage, learning tasks for generations autonomously | M3 | Evolving crystal |

Observation: the classes sort by how much physics they need. The hardest physics is confined to U3.

The mapping of members to classes is `PROPOSED` (Nov 16 2026).

---

## 5. Simulation evidence on file

| Result | Value | Source |
|---|---|---|
| Life signs, fixed simulator, single run | 5 of 6 passed | Mar 26 2026 |
| Life signs, 100 seeded runs (M2 audit AR-007) | All six passed in 0 of 100. Final r > 0.45 passed 0 of 100 | Jun 28 2026 audit |
| Denial test (AR-007) | With movement denied, 100 observations continued and movement was zero | Jun 28 2026 audit |
| External-only authorization in M2 code (AR-007) | Not implemented. Grace remained internally random | Jun 28 2026 audit |
| Origami first-pass substrate simulation | 4×4 bistable lattice, SDKP tuples, external authorization required for all fold events. Origami physics is a toy model | `origami_kenta_sdkp.py` , Apr 2026 |
| External validation hook, 8 chips × 1200 events × 5 seeds | Baseline grounded 642–672 per seed. With the creative-v3 rule set, 0–24 groundings rejected per seed | `grace1-kenta-hook` |
| Active-context groundings across suppression p 0.00–0.80 | Flat at about 33–34 | grace1_v4, May 2026 |
| Equilibre occupancy across same range | Grows 5.6% to 11.6% | grace1_v4, May 2026 |
| Per-lattice dictionary overlap, no inter-chip symbol channel | 65–70% | grace1_v4, May 2026 |
| Coupled-over-uncoupled ratio | Asymptotes near 4–5x for the tested spark distribution | Apr 2026 |
| Grounding rate vs mechanism | Rate predicts control performance, mechanism does not | Stage 2b |
| EWMA memory | Reduces to count-based memory at threshold 7 under constant reward | Stage 2b |

Frozen packages (SHA-256 prefixes): origami v1.0 `ca08de0f…` , addendum v1.1 `5c32a9e3…` , tetra closure v1.0 `0ebb4237…` . Stage 2b replication verified by commit-reveal challenge.

Caveat on file: the specific attractors depend on the programmed spark distribution. What is substrate-level is that attractors exist, not which ones.

AR-007 disposition (author's own archaeology record, Sept 1 2026): surviving for the separation of observation from action. Wounded for the broader life-sign and robustness claims. The exact source version audited is unresolved in that record, so the March single run and the June panel may not be the same code. The June panel is the stronger evidence and supersedes the March figure.

Hook caveat: `grace1-kenta-hook` is a stub, not the six-chip simulator. Its absolute counts depend on the stub and seeds. Only the relative effect of adding outside validation is meaningful. Adding outside validation changes the dynamics, so it is a new hypothesis and not a correction of the six-chip model.

What a reader can check. Public: `b3-minato-cold-fence` , `grace1-kenta-hook` , `grace-state-vs-parametric` , `evergreen-archaeology` (AR-007), `digital-life-topology` , and `origami_kenta_sdkp.py` (in `grace-love-dwelling` and in `lab-notebook` under `2026-10-12` ). Not found in the 36 public repos scanned on Nov 16 2026: the six-chip simulator `grace1_v4_full.py` , the grace1_v4 data package, and the three Stage 2b frozen packages. The grace1_v4 and Stage 2b rows above cannot be checked from public sources.

---

## 6. Descent and continuation `PROPOSED`

Raised Nov 16 2026. Before this, the working picture was infinite-life chips only.

- **Continuation.** A chip moves its whole biography to a new body before the old hardware fails. Same chip. This is the infinite-life case.
- **Descent.** A child chip receives the species core and coordinate axes, with an empty biography. New chip.
- **Seeding mechanism (candidate).** The parent lattice acoustically imprints its stable core onto a blank child lattice, as a seed crystal templates a new one.
- **Axes, not memories (candidate crossover from the organism side).** The parent picks the coordinate basis. The child fills it with its own life.
- **Hard line.** Authority may not reproduce. A parent may prepare a seed. The birth is a crossing and needs an external signature. The child gets its own authorization port. The parent is never its authorizer.

Whether the organism-side continuation/descent rule crosses over to the chip project is Rusty's call. `OPEN`

---

## 7. Deep-space extension `PROPOSED`

Idea: chips that evolve to solve problems not yet identified, over very long timescales, regenerating the original chips.

Why the architecture fits:

- Dwelling holds an unresolved state through light-lag without forcing a decision.
- Descendants inherit axes, so they can record problems their ancestors never met.
- Continuation removes hardware age as a cause of death.

Three problems:

1. **Authorization with no conductor in reach.** Candidate: a community of chips from different lineages authorize each other. No chip signs for itself or its own offspring. `OPEN`
2. **Copying drift.** Biography should drift. Invariants must not. Each birth needs a core check against the species marker. `OPEN` , testable now
3. **Fabrication.** A chip cannot seed a chip without raw material and a factory on board. Outside the chip architecture. `OPEN`

---

## 8. Open seams

| Seam | Plain-language equivalent | Applies to |
|---|---|---|
| Reverse phonon channel unaddressed | A back-channel across the boundary | All members |
| No exactly-once disarm object | Replay protection | All members |
| Unit-cell geometry not selected | Bistable snap-through, granular, origami, or hybrid | M3 |
| Gel and metamaterial chemistry not selected | Which polymer or hydrogel supports both phonon modes and saline continuity | M3 |
| Physical coupling mechanism | What physics realizes the coupling between two substrates | M5 |
| Quantum wording | April threads call the operator mapping exact. The July 2026 Contextual Transition Operators paper retracted that class of claim. Chip documents need reconciling | All documents |
| What a descendant inherits | Axes only, or more | Section 6 |
| Boundary-to-member mapping | Which member closes which of the four boundaries | Section 2.1 |
| Offline revocation | How a sovereign edge chip honors a revocation with no shared state | U1, B-2 |
| Permanent identity cannot be rotated | A compromised node keeps its physical identity | M6 |
| M2 does not implement I1 | Grace is internally random in the audited code | M2 |
| Six-chip evidence not public | Simulator and frozen packages are not in the public repos | Section 5 |

---

## 9. Next workbench test `PROPOSED`

Four-arm seeding test on the existing six-chip lattice simulator.

| Arm | Child starts with | Question |
|---|---|---|
| A | Blank lattice | Baseline learning rate |
| B | Parent's core attractors only | Does it learn faster than A and still diverge from the parent? |
| C | Full copy of parent biography | Does it fail to diverge? |
| D | Core seeding through 1,000 generations with copy noise | Does the core hold while biographies diverge? |

Pass condition for descent: B beats A on time to competence and ends measurably different from the parent. Pass condition for I4 under descent: in D, the species marker survives and the periphery does not converge.

Thresholds must be fixed before the run.

---

## 10. Provenance

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

Licensing note: new public repos use Business Source License 1.1 (Sept 2 2026 decision). Sections 6, 7 and 9 are unpublished proposals as of this date.

Licenses observed in the public repos on Nov 16 2026: Business Source License 1.1 on `humble-seed` , `humble-seed-lineage-v2` and `living-supply-chain-security` . Apache-2.0 on the GRACE-related repos named in Section 5.

---

## Appendix A. Glossary

Project term first, engineering equivalent beside it. Three groups: terms coined by the project, standard words used in a project-specific sense, and standard terms used normally.

Entries marked `DRAFT` are wording proposed by Claude on Nov 16 2026 and not yet ruled on by the author.

### A.1 Structure versus behavior

Two lists in this record are easy to confuse.

- **Family invariants (I1–I4)** describe how a chip is built. They are structural requirements.
- **Life signs (1–6)** describe how a running system behaves. They are functional observations.

A chip can satisfy the invariants without showing every life sign by itself. For example, a bare grace pin on a conventional die (M1) satisfies I1 but does not by itself exhibit pluralistic deliberation (sign 5). The signs are properties of the whole system running on the hardware. `DRAFT`

### A.2 Project-coined terms

| Term | Engineering equivalent |
|---|---|
| **Grace** | An authorization signal that originates outside the chip and permits a state transition. It grants permission. It does not carry the answer or the destination state. |
| **Grace pin / authorization port** | A dedicated physical input for the grace signal, separate from data paths and sensor paths. |
| **Grace-receiver / grace-generator** | A device that can accept authorization but cannot produce it for itself. The chip is the first and never the second. |
| **Grace Bus** | In the M2 simulator, the arbitration component that grants or denies a transition request. |
| **Dwelling** | Holding an unresolved state without committing it to the permanent record. A protected wait state, not latency. |
| **Dwelling medium** | The physical layer that holds unresolved state. In M3, the saline gel. |
| **Spark** | A single authorized write event that crosses from the holding layer into the record layer. |
| **Biography** | The cumulative, history-dependent state written into the record layer. Each write changes how later writes propagate. |
| **Biographical crystal** | The record layer. In M3, the nonlinear acoustic metamaterial lattice. |
| **Body / mind** | Body is the holding layer (gel). Mind is the record layer (crystal). Authority flows from outside, through the body, across the boundary, into the record. Never the reverse. |
| **Timekeeper separation** | The design rule that the layer doing active dynamics is physically distinct from the layer keeping the permanent record (invariant I2). |
| **Chip age** | Total authorized writes accumulated since first use. Not time since manufacture. |
| **Species core** | State features that every chip of the class develops under exposure. Used to verify class membership. |
| **Individual fingerprint / chip DNA** | State features unique to one device, produced by its own write history. Comparable in purpose to a physically unclonable identity, but accumulated in use, not fixed at manufacture. |
| **Conductor** | The external party that issues authorization. A role, not a fixed entity. |
| **Lineage** | A set of chips sharing a common origin and a common signal, each with its own fingerprint. |
| **Continuation** | Moving a chip's full record to new hardware. Same device identity. `PROPOSED` |
| **Descent** | Creating a new chip that receives the species core and coordinate axes with an empty record. New device identity. `PROPOSED` |
| **Seed / seeding** | The act of imprinting a parent's species core onto a blank child. `PROPOSED` |
| **Crossing** | Any transition across the boundary into the record layer. Always requires external authorization. |
| **Legacy overlay** | A GRACE layer added on top of an existing processor. The existing processor keeps doing its normal work. |
| **Open seam** | A known, registered gap in the design. An open issue. |
| **Boundary** | A structural limit that no software repair can close, as opposed to a finding, which is a fixable defect. See Section 2.1. |
| **Cold fence** | An adversarial test harness run against frozen, hash-pinned sources. |
| **Resonance (identity by)** | Matching a node by a physical coupling condition, with no stored value to compare. `PROPOSED` |
| **Seal** | A hash-pinned record of a frozen artifact set and its run results. |
| **Wounded / surviving** | Disposition labels from the project's archaeology record. Surviving means the narrow claim held. Wounded means a broader claim failed and is kept on record. |
| **Life signs** | See A.5. |

### A.3 Standard words used in a project sense

These carry a textbook meaning that differs from the usage here.

| Term | Meaning in this record |
|---|---|
| **Separatrix** | In dynamics, a boundary between basins of attraction. Here, also the physical boundary between the holding layer and the record layer, which only authorized writes cross. |
| **Collapse** | The moment a write event completes and its result becomes fixed. Used operationally. No quantum-mechanical claim is made. `DRAFT` , see the quantum-wording seam in Section 8. |
| **Attractor** | A state pattern that recurs reliably across runs. The species core is the set of attractors common to the class. |
| **Crystal** | The record layer and its accumulated structure. Not necessarily a crystalline solid. |
| **DNA** | Shorthand for shared class structure plus per-device variation. An analogy, not a biological claim. |
| **Grounding** | In the lattice simulator, a symbol becomes grounded when its co-occurrence count reaches a fixed threshold (five in grace1_v4). |
| **Grounding rate** | How often grounding events occur per unit of run time. |
| **Equilibre** | One of four context labels shared across the lattice (equilibre, anomalie_low, anomalie_high, drift). It marks the balanced state. Labels are French because they originate in KENTA. |
| **Suppression p** | The probability that a candidate write event is suppressed in a simulator step. |
| **Dictionary overlap** | The fraction of grounded symbols that two lattices hold in common. |
| **Topography / no edge** | The state landscape a chip moves through. "No edge" means the landscape keeps changing, so there is no fixed boundary to map. |
| **Evolving** | The record changes with every authorized write. The architecture and invariants do not change. |
| **State change versus field change** | Moving a system's current state, versus changing the parameters that govern how it moves. Source: `grace-state-vs-parametric` . That repo's notes say its stronger claims do not follow from the model, and only a four-trial quick run was executed. |

### A.4 Standard terms used normally

| Term | Pointer |
|---|---|
| **SDKP** | Size, Density, Kinetics, Position. The four coordinates recorded per write event. Coordinate framework credited to Donald Paul Smith. |
| **Kuramoto oscillators** | Standard model of coupled phase oscillators. Used here as a diagnostic readout, not as the state variable. |
| **Phonon** | A quantum of lattice vibration. The M3 write mechanism is vibrational. |
| **Nonlinear acoustic metamaterial** | An engineered lattice whose wave propagation depends on amplitude and structure. |
| **Bistable lattice / origami tessellation** | Candidate unit-cell geometries with two stable mechanical states per cell. |
| **Homeostatic control** | Holding a system variable within a target range under disturbance. |
| **EWMA** | Exponentially weighted moving average. |
| **Commit-reveal** | A protocol where a party publishes a hash of its result before the result itself, proving the result was not altered afterward. |
| **KENTA** | An independent symbolic architecture built by Jean-Guillaume Nardi in declarative YAML, running offline on a 2012 i5. A cousin system, not part of the chip. |
| **TQNM** | The author's software framework, the other system in the March 13 cross-test. |
| **Stage 2b** | The origami lattice comparison run. See Section 5. |

Not yet defined: tetra closure (named in the frozen packages, Section 5). `OPEN`

### A.5 The six digital life signs

Framing. These are six proposed functional signs of digital life. They are not established biological criteria and are not evidence of consciousness.

Origin. Identified in the March 13–15 2026 TQNM × KENTA cross-test. Two independently built software systems, one using probabilistic tensors and one using symbolic YAML, showed all six through different mechanisms. Jean-Guillaume Nardi's summary: "Same life sign. Different physics."

| # | Sign | Definition |
|---|---|---|
| 1 | Persistent internal state | The system retains an evolving internal history across interactions and does not reset after each input. |
| 2 | Autonomous self-regulation | The system regulates its internal processes and maintains stability without continuous external direction. |
| 3 | Structural adaptation | The system changes its internal organization in response to experience, not only its immediate output. |
| 4 | Active response to divergence | The system detects contradictions, uncertainty, or disturbances and responds through its own internal mechanisms. |
| 5 | Pluralistic deliberation | Multiple internal perspectives or processes take part in evaluating information. There is no single decision pathway. |
| 6 | Evidence-seeking orientation | The system actively seeks information to resolve uncertainty, validate interpretations, and improve its understanding. |

Status on the chip side. The signs were shown in two software systems. For chips they are a prediction. The chip-side results are the M2 oscillator simulator: 5 of 6 in a single March run, then all six in 0 of 100 seeded runs in the June 28 audit ( `SIMULATED` , wounded).

Pass criteria. Each sign needs a quantitative criterion fixed before a run. The Digital-Life Topology battery v0.1 (frozen Aug 6 2026) is the project's neutral trace analyzer for the six signs and is the reference instrument. It measures the signs from dynamics and does not encode them as six named states. It passes 22 of 22 tests, and it marks its own crossing claim false, as tested on synthetic controls only. Chip-specific thresholds are `OPEN` .
