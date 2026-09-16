# Engineering highlights

[Back to portfolio](../README.md)

These short case studies describe engineering problems and validation decisions without exposing source code, interfaces, implementation parameters, or private test data.

## Complete result checking across the host–FPGA boundary

**Problem:** A successful transport acknowledgement does not prove correct baseband computation, digital sample consumption, or complete result delivery.

**Approach:** Treat task acceptance, computation, consumption, result collection, and release as distinct observable stages. Compare the complete returned digital result against its reference instead of relying on a single status flag or a small sample of outputs.

**Evidence:** The accepted hardware batch completed all 18 tasks, with 450,000 complex I/Q sample pairs matching the reference. All tasks were read back and released.

**Discussion topics:** fixed-point checking, system-level observability, verification boundaries, and separating transport correctness from computation correctness.

## Lost responses without repeated work

**Problem:** A response can be lost after the hardware has acted. Blindly treating a retry as new work can duplicate execution or corrupt the host's view of a task.

**Approach:** Define bounded retry behavior and check both the returned result and the task lifecycle. Exercise deliberately missing responses rather than inferring retry safety from a successful nominal run.

**Evidence:** Specified commit, result-readback, and release response-loss cases completed without duplicate task execution in the accepted batch.

**Boundary:** These finite cases do not establish arbitrary interruption recovery or unattended recovery after power loss.

## Distinguishing a testbench race from a design defect

**Problem:** A control-component test failed around a backpressure sampling edge. A failing simulation alone did not identify whether the issue belonged to the design, synthesized behavior, or stimulus scheduling.

**Approach:** Preserve the failing evidence, compare RTL and synthesized-netlist behavior, and isolate the stimulus phase while retaining the production RTL and assertions.

**Evidence:** Correcting testbench stimulus timing resolved the race. The checked behavior then agreed across 49 interface scenarios in RTL and netlist simulation under two clock relationships; 82 Python tests also passed within the component's verification scope.

**Boundary:** Functional agreement does not establish formal equivalence or physical timing qualification.

## Keeping capability, candidate qualification, and release separate

**Problem:** An earlier board demonstration and later passing component tests can easily be combined into an unsupported claim that a new integrated release is ready.

**Approach:** Maintain explicit scope and evidence boundaries. Preserve the demonstrated baseline, verify changed components separately, and require updated-candidate qualification plus a fresh whole-system acceptance before release.

**Current outcome:** The hardware capability baseline is demonstrated; the reusable Version 1 workflow remains in progress. No release-complete or real-time wireless claim is made.

**Discussion topics:** regression planning, CDC/reset review, change-impact analysis, reproducibility, and acceptance criteria.

## Use of this portfolio

This is an independent laboratory project overview, not a statement of commercial deployment or employment history. The descriptions are project-level claims; they do not imply sole authorship of every tool or component. Third-party platforms and tools retain their own ownership and licensing.
