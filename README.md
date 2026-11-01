# Engines for models you own, and tools that take binaries apart.

Local inference on hardware I already have, matching decompilation, and agents that do the
boring parts of both. Everything here is meant to run offline, on consumer cards, with the
source in plain sight and the measurements in the README.

[![Followers](https://img.shields.io/github/followers/giveen?style=flat-square&logo=github&label=followers&color=30363d)](https://github.com/giveen?tab=followers)
![Public repos · 69](https://img.shields.io/badge/public%20repos-69-30363d?style=flat-square)
![Originals · 28](https://img.shields.io/badge/originals-28-30363d?style=flat-square)
![C++ · Rust · Python · Go · TS](https://img.shields.io/badge/C%2B%2B%20%C2%B7%20Rust%20%C2%B7%20Python%20%C2%B7%20Go%20%C2%B7%20TS-offline--first-8b5cf6?style=flat-square)

## Things I'd point you at first

| Repo | What it is | ★ |
|---|---|---|
| [**decomp.anything**](https://github.com/giveen/decomp.anything) `Python` | Point an AI agent at something you own and take it apart. Agents write C/C++ against the real binary, the original compiler builds it, the result is checked byte for byte. Games, PE and ELF binaries, apps, firmware, plain files. | [![★](https://img.shields.io/github/stars/giveen/decomp.anything?style=flat-square&logo=github&label=)](https://github.com/giveen/decomp.anything) |
| [**ninfer-studio**](https://github.com/giveen/ninfer-studio) `TS` | Native Linux and Windows desktop app (Tauri 2) that turns an inference server binary into a product: per-GPU presets, Hugging Face model management, streaming chat with vision, an agentic coding harness, live token and VRAM metrics. | [![★](https://img.shields.io/github/stars/giveen/ninfer-studio?style=flat-square&logo=github&label=)](https://github.com/giveen/ninfer-studio) |
| [**KernelOPT**](https://github.com/giveen/KernelOPT) `Rust` | Dispatch-aware, agentic GPU-kernel optimization. Point it at a kernel, a directory, or a whole model; it runs a profile → plan → edit → verify → gate loop until each kernel is faster or the budget runs out. Your working tree is never touched. | [![★](https://img.shields.io/github/stars/giveen/KernelOPT?style=flat-square&logo=github&label=)](https://github.com/giveen/KernelOPT) |
| [**late-sast**](https://github.com/giveen/late-sast) `Go` | Autonomous security auditor. One command, one repo in, one report out — graph-first taint tracing in a Docker sandbox with live exploit verification, so a finding is proven reachable instead of merely suspicious. | [![★](https://img.shields.io/github/stars/giveen/late-sast?style=flat-square&logo=github&label=)](https://github.com/giveen/late-sast) |
| [**Decapybara**](https://github.com/giveen/Decapybara) `C++` | Open-source C++20 and CUDA reconstruction of a closed inference server, targeting Qwen3.8-27B on RTX 5090 Blackwell. *"The source will be published later"* — later is now. | [![★](https://img.shields.io/github/stars/giveen/Decapybara?style=flat-square&logo=github&label=)](https://github.com/giveen/Decapybara) |
| [**golight**](https://github.com/giveen/golight) `Go` | Open-source worship presentation software, built to 1:1 parity with SongShow Plus 9.3 Ultra. Wails desktop app. | [![★](https://img.shields.io/github/stars/giveen/golight?style=flat-square&logo=github&label=)](https://github.com/giveen/golight) |

## By area

### Inference engines and quantization

The engines themselves, and the work of squeezing a model onto one GPU.

- [**spite**](https://github.com/giveen/spite) `Rust` — one engine, your model, your card: a single Rust host that loads any GGUF file and runs it on the hardware you have. No cloud, no subscription, nothing leaving the machine.
- [**ninfer-ext**](https://github.com/giveen/ninfer-ext) `C++` — high-performance single-GPU inference for selected checkpoints and cards. **Retired 2026-10-22:** the tree still builds and serves everything documented, it is simply not being worked on. Its README carries the head-to-head measurements against basalt for Qwen3.8-Flash-Next NVFP4 at 262k context on one RTX 5090.
- [**llama-cpp-turboquant-hybrid**](https://github.com/giveen/llama-cpp-turboquant-hybrid) `C++` — hybrid speculative decoding for llama.cpp: composes MTP (multi-token prediction) and DFlash (block diffusion) draft paths into a single decoder pass, with per-token provenance so each backend's acceptance stats stay separate.
- [**OSCAR-llamacpp**](https://github.com/giveen/OSCAR-llamacpp) `C++` — INT2 KV cache for Qwen3 and Gemma 4; the Metal path runs INT2+f16 KV on-GPU with fused mixed-precision flash-attention kernels. Pre-built `*-rot-kv.gguf` models on Hugging Face.

### Reverse engineering

- [**decomp.anything**](https://github.com/giveen/decomp.anything) `Python` — the matching-decompilation workbench above, plus an optional REA MCP bridge for binaries with no original build to match.
- [**NanoHound**](https://github.com/giveen/NanoHound) `Python` — lightweight in-memory Active Directory attack-path explorer, built on NiceGUI and NetworkX.

### Security and detection

- [**zap-extension-aitrafficanalyst**](https://github.com/giveen/zap-extension-aitrafficanalyst) `Java` — OWASP ZAP add-on that feeds live request/response pairs into the official ZAP LLM add-on for OWASP-first analysis. Provider-agnostic, local or remote, no model config of its own.
- [**DS-Stalker**](https://github.com/giveen/DS-Stalker) `Python` — recursive enumeration of paths exposed by publicly readable `.DS_Store` files.
- [**SnaffleSnap**](https://github.com/giveen/SnaffleSnap) `PowerShell` — parses Snaffler output into colour-coded HTML reports sorted by severity.

## What I work in

**C++/CUDA** and **Rust** for anything that has to hold a model in VRAM. **Python** for
reverse-engineering and analysis plumbing. **Go** for single-binary tools. **TypeScript**
with Tauri when the thing needs a GUI. Linux throughout, NVIDIA throughout.

## Measure first, then claim

Most of what I post carries the numbers that justified it: tokens per second at a stated
context depth, byte-for-byte match status, before-and-after kernel timings. When a project
stops being worth the time I say so at the top of its README and leave the tree building,
rather than letting it rot quietly.

## About the forks

41 of my 69 public repos are forks and they stay labelled as forks. Some I run and patch
for my own hardware; a few carry a handful of my commits. They are here because this is
where my working copies live, not because I wrote them — read the parent repo before
crediting me with any of it. One note on the star of the show: **decomp.anything** is an
independent fork of [decomp.wtf](https://github.com/i12bp8/decomp.wtf) by Sam Wolfs
(MIT, upstream discontinued). I continued and extended it, and the credit belongs where
it is due.
