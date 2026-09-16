# Validation summary

[Back to portfolio](../README.md)

Status snapshot: 2026-09-15. This page separates the demonstrated hardware baseline from later component verification and unfinished delivery work.

## 1. Hardware capability baseline

The finite acceptance batch used 16 saved OAI-derived downlink tasks and two synthetic controls. Linux submitted the tasks over Ethernet; the AX7A200B FPGA performed the digital processing, consumed the resulting samples digitally, and returned the complete results.

| Check | Recorded outcome |
| --- | --- |
| Task completion | 18 of 18 |
| Full I/Q result comparison | 450,000 complex sample pairs; all matched bit for bit |
| Result collection and release | All 18 tasks read back and released |
| Deliberately lost responses | Specified commit, readback, and release retries completed without duplicate execution |

Reference-result checking and request/response review were used to cross-check the batch. The evidence covers actual FPGA computation, rather than a software-emulated FPGA response.

The task source was saved data. This run did not establish a live OAI scheduler-to-FPGA real-time path. Complete readback correctness is not a throughput or radio-deadline benchmark. The digital sample-consumption result is not proof of DAC output, ADC capture, wireless reception, or HARQ acknowledgement.

## 2. Later control-component verification

A separate component for the controlled initialization/run workflow was verified offline:

- 82 Python tests passed.
- 49 interface scenarios were exercised in RTL simulation and synthesized-netlist simulation, each under two clock relationships.
- The four runs agreed on the checked interface behavior.
- Coverage included handshake ordering, backpressure, clock stoppage, reset behavior, and invalid or stale requests.
- Synthesized synchronizer and reset structures were reviewed alongside the functional results.

This means **49 unique scenarios across four runs**, not 196 unique scenarios. It is component-level evidence, not a fresh hardware acceptance of the integrated system.

A simulation race was isolated using controlled comparisons. The testbench stimulus timing was corrected without changing production RTL or weakening the assertions. Failed-run evidence was retained rather than relabeled as a pass.

Synthesized-netlist simulation is not formal equivalence, routed timing closure, physical CDC/RDC signoff, or board qualification.

## 3. Delivery milestones

| Milestone | Status |
| --- | --- |
| Demonstrate the finite Linux–FPGA digital capability | Complete for the accepted hardware baseline |
| Define the Version 1 scope and record the baseline candidate | Complete; not a released package |
| Integrate the controlled run workflow and qualify its updated candidate | In progress |
| Execute fresh whole-system acceptance through the delivery workflow | Pending |
| Finalize the delivery package, instructions, and sign-off | Pending |

Earlier acceptance does not automatically qualify a modified candidate. New control-component results do not change the status of the hardware baseline, and cannot substitute for the new whole-system run.

## 4. Evidence and disclosure

The engineering workspace retains detailed test records and version associations. This public repository contains only a manually curated summary; it does not distribute source, payloads, raw output vectors, build artifacts, or the underlying receipts.

Readers therefore cannot independently reproduce or audit every result from this repository alone. Claims are limited to the recorded project tests, not independent certification or product qualification.

## 5. Outside the demonstrated scope

- Arbitrary NR configurations, complete uplink/downlink PHY coverage, or multi-user operation.
- Replacement of the live software PHY or guaranteed radio-slot deadlines.
- Analog/RF loopback, over-the-air interoperability, or a complete wireless base station.
- Continuous full-rate sample streaming, environmental qualification, or long-term production reliability.
- ASIC physical implementation or tapeout readiness.

These boundaries are part of the result, not exceptions to an otherwise unrestricted claim.
