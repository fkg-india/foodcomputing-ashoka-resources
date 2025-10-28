# Feature-by-feature coverage (2/1/0)

|                        # | Feature                                              | MILK  | Corel | Action-Graph |
| -----------------------: | ---------------------------------------------------- | :---: | :---: | :----------: |
|  **Entities & metadata** |                                                      |       |       |              |
|                        1 | Ingredient names                                     |   2   |   2   |      2       |
|                        2 | Quantities + units (structured)                      |   1   |   2   |      2       |
|                        3 | Ingredient form/modifiers                            |   1   |   1   |      2       |
|                        4 | Tools/utensils modeled                               |   2   |   1   |      2       |
|                        5 | Yield / servings                                     |   0   |   2   |      0       |
|                        6 | Nutrition metadata                                   |   0   |   0   |      0       |
|                        7 | Provenance / traceability                            |   1   |   0   |      2       |
|    **Process & actions** |                                                      |       |       |              |
|                        8 | Typed action taxonomy                                |   2   |   0   |      2       |
|                        9 | **Transfer** modeled distinctly                      |   2   |   0   |      2       |
|                       10 | **Plate / Serve**                                    |   2   |   0   |      1       |
|                       11 | Partial transfers / granularity                      |   1   |   0   |      1       |
|                       12 | Tool manipulation / settings                         |   2   |   0   |      2       |
|                       13 | Outcome/doneness checks                              |   2   |   0   |      2       |
|                       14 | Loops / iteration                                    |   0   |   0   |      0       |
|                       15 | Ingredient alternatives / notes                      |   0   |   0   |      0       |
|   **Temporal & thermal** |                                                      |       |       |              |
|                       16 | Absolute time                                        |   1   |   2   |      2       |
|                       17 | Time ranges & relative timing                        |   0   |   1   |      2       |
|                       18 | Timers / synchronization semantics                   |   0   |   0   |      2       |
|                       19 | Numeric temperature                                  |   1   |   2   |      2       |
|                       20 | Qualitative heat levels                              |   1   |   1   |      1       |
|                       21 | Temperature ramps / curves                           |   0   |   0   |      2       |
|                       22 | Cooling / resting states                             |   2   |   0   |      2       |
|      **Graph & control** |                                                      |       |       |              |
|                       23 | Concurrency constructs                               |   0   |   0   |      2       |
|                       24 | Interjections / nested relative actions              |   0   |   0   |      2       |
|                       25 | DAG guarantee                                        |   0   |   0   |      2       |
|                       26 | Environment modeling (container, location, geometry) |   1   |   0   |      2       |
| **Validation & tooling** |                                                      |       |       |              |
|                       27 | Static validation (usedef / unit checks)             |   0   |   2   |      1       |
|                       28 | Corpus / annotation availability                     |   2   |   0   |      0       |
|                       29 | Authoring/editor or export tooling                   |   1   |   2   |      0       |

**Legend:** 2 = explicit / first-class; 1 = implicit/partial; 0 = unsupported.

**Notes linking scores to sources (representative):**

- MILK defines a compact, typed action set and a container-based world state; time/temps typically appear as strings or via checks (e.g., `set`, `chefcheck`), and there’s no concurrency construct.

- Corel provides explicit syntax for times (`|…|`) and temperatures (`<…>`), rich ingredient/serving metadata, and editor validations, but leaves environments, transfers, and concurrency to prose.

- The Action-Graph DSL explicitly models PROCESS/TRANSFER/PLATE, environments (container + location + optional geometry), concurrency with merges, relative timing/interjections, temperature ramps, and implicit-but-recoverable PPC provenance.

## Totals & coverage

| DSL              | Explicit (2) | Implicit (1) | Missing (0) | Score (out of 58) |  Coverage |
| ---------------- | -----------: | -----------: | ----------: | ----------------: | --------: |
| **MILK**         |            9 |            9 |          11 |            **27** | **46.6%** |
| **Corel**        |            7 |            4 |          18 |            **18** | **31.0%** |
| **Action-Graph** |           19 |            4 |           6 |            **42** | **72.4%** |

*(Higher % = broader first-class coverage of explicit and implicit recipe semantics.)*

## Justifications

- **Corel** excels at author-friendly numerics and metadata (units, temps, times, yields) and strong editor checks, but intentionally omits procedural structure (environment, transfer, concurrency), so explicit coverage is narrower outside of I/O and metadata.

- **MILK** offers a compact predicate inventory and a world model via container relations, with useful control-style predicates (`set`, `leave`, `chefcheck`, `serve`). Lack of first-class time/temperature fields and no concurrency mean many features are only implicitly representable.

- **Action-Graph DSL** targets procedural fidelity: explicit separation of state change (PROCESS) and spatial change (TRANSFER), explicit environments, concurrency and relative timing/interjections, temperature ramps, and implicit-but-reconstructible PPCs. This yields the highest explicit coverage across categories.
