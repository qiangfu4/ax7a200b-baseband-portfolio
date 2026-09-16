# Linux–FPGA Digital Baseband & DFE

An AX7A200B / Artix-7 engineering portfolio focused on digital design, baseband processing, and evidence-driven hardware validation.

[中文说明](README.zh-CN.md) · [Validation summary](docs/validation-summary.md) · [Engineering highlights](docs/engineering-highlights.md)

## The result

A Linux host sends saved, OAI-derived downlink tasks over Ethernet. The FPGA performs a restricted NR baseband and digital front-end (DFE) processing chain, consumes the resulting samples digitally, and returns the complete I/Q results for reference comparison.

**Hardware baseline demonstrated:** 18 of 18 tasks completed, with all 450,000 complex I/Q sample pairs matching the reference results bit for bit.

This is a finite laboratory digital-processing demonstration, not a complete real-time 5G base station. The reusable Version 1 delivery workflow is still in progress.

## System at a glance

Linux task preparation → Ethernet transport → FPGA baseband / DFE → digital sample consumption → full-result readback and validation

The demonstrated processing scope includes channel coding, rate matching, resource-grid generation, OFDM, and DFE. Saved task replay is separate from live OAI scheduling or replacement of OAI's software PHY.

## What was demonstrated

| Evidence | Result | Scope |
| --- | --- | --- |
| Hardware task batch | 16 saved OAI-derived tasks + 2 synthetic controls passed | Finite, restricted downlink profile |
| Full output comparison | 450,000 complex I/Q sample pairs matched | Complete batch readback, not selected samples |
| Deliberate response loss | Tested retries completed without duplicate execution | Specified commit, readback, and release cases |
| New control-component verification | 82 Python tests; 49 interface scenarios across four simulation runs | RTL and synthesized netlist, under two clock relationships; separate from the hardware baseline |

These are project-recorded results, not an independent certification. The [validation summary](docs/validation-summary.md) explains the evidence boundaries.

## Engineering focus

- **FPGA / digital design:** RTL integration, clock-domain crossings, reset behavior, handshakes, backpressure, and synthesis-aware debugging.
- **Baseband / DFE:** fixed-point reference comparison and end-to-end digital processing correctness within a defined profile.
- **Linux–hardware integration:** finite task lifecycle, Ethernet request/response behavior, bounded retries, complete result collection, and resource release.
- **Verification:** model-to-RTL comparison, synthesized-netlist simulation, negative tests, fault injection, and retained pass/fail evidence.

Project toolset: Verilog / SystemVerilog, Python, Tcl, Vivado / XSim, Icarus Verilog, Yosys, Linux, and Git.

## Current status

The hardware capability baseline is complete. Follow-on work is integrating a controlled initialization and run workflow, qualifying its updated hardware candidate, and preparing a fresh end-to-end acceptance run and delivery package. **Version 1 has not been released.**

Not demonstrated by the results above: arbitrary NR profiles, real-time PHY replacement, over-the-air interoperability, analog/RF loopback, production reliability, or ASIC tapeout readiness.

## About this repository

This is a documentation-only portfolio for FPGA, digital-design, and baseband engineering discussions. It intentionally publishes outcomes, engineering topics, and validation boundaries—not implementation details.

RTL, host source, bitstreams, netlists, detailed interfaces and parameters, raw test payloads, I/Q vectors, logs, and private environment information are not distributed here. Consequently, this repository is not a buildable or independently reproducible release. The original engineering repository and its history remain separate.

OpenAirInterface (OAI) is a third-party project. Its use as a task source does not imply affiliation, endorsement, or interoperability certification. Board and tool names identify the project environment only.

Status snapshot: **2026-09-15**. Maintainer: [qiangfu4](https://github.com/qiangfu4).
