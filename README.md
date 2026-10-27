<div align="center">
  <img src="assets/TIP_Logo_Square.jpg" width="150" alt="TIP Logo">
  
  <p><h1>PKLM Sandbox</h1></p>

  <p>
    <a href="https://github.com/TheImmortalPython/pklm-sandbox/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-MIT-yellow.svg" alt="License: MIT"></a>
    <a href="https://github.com/TheImmortalPython/pklm-sandbox/actions"><img src="https://github.com/TheImmortalPython/pklm-sandbox/actions/workflows/ci.yml/badge.svg?branch=main" alt="CI Status"></a>
    <img src="https://img.shields.io/badge/python-3.10%2B-blue.svg" alt="Python Version">
    <img src="https://img.shields.io/github/stars/TheImmortalPython/pklm-sandbox?style=social" alt="GitHub Stars">
  </p>
</div>

Official open-source sandbox for PKLM Core, featuring lightweight Hugging Face logits processing and zero-drift linguistic containment.

## Community Benefits

PKLM Sandbox benefits the AI community by solving immediate friction points for developers building deterministic, safe software:

* **Open-Source Accessibility:** Gives independent developers a completely free, open starting point to test token-level control without needing to build complex custom logits interception code from scratch.
* **Safer AI Experimentation:** Acts as a safe testing ground for **zero-drift linguistic containment**. It lets engineers experiment with rules that completely block harmful, repetitive, or broken token paths before a model ever goes live.
* **Bridging the Gap to Enterprise Tech:** Serves as a public playground to evaluate how structured constraints work firsthand, demonstrating the mechanics behind its private enterprise counterpart, **PKLM Core**.

## Installation

To install locally from source:

```
pip install .
```

To pull and install directly from the repository for offline or edge tool deployments:

```
pip install git+https://github.com/TheImmortalPython/pklm-sandbox.git
```

## Quickstart

Integrate the sandbox processor into your local pipeline:

```
from transformers import AutoModelForCausalLM, AutoTokenizer
from pklm_sandbox.processor import PKLMSandboxProcessor

processor = PKLMSandboxProcessor(blocked_token_ids=[50256])
```

## Example: Initialize processor with tokens to restrict

```
processor = PKLMSandboxProcessor(blocked_token_ids=[50256])
```

## Enterprise and Production Deployments

This public repository (`pklm-sandbox`) contains only a basic developer-tier wrapper for testing and evaluation. 

For high-stakes enterprise environments requiring the full **PKLM Core (`pklm-core`)** architecture—including custom token-level constraint modeling, heavy Paninian karaka rule engines, low-latency compiled binaries, and production SLAs—enterprise clients should reach out directly:

Contact: theimmortalpythonlabs@proton.me

---
> **Founder & Principal AI Architect:** Joshua St. Germain  
> **Enterprise Governance:** TheImmortalPython Labs (`theimmortalpythonlabs@proton.me`)  
> **Repositories:** `pklm-core` (Private) | `pklm-sandbox` | `determinism-runtime-core` (Private) | [the-nsai-guide](https://github.com/TheImmortalPython/the-nsai-guide)

---

## License

Distributed under the MIT License. See LICENSE for more information.
