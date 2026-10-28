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

## Overview & Architecture

PKLM Sandbox is a lightweight developer-tier tool for the `TheImmortalPython/pklm-sandbox` GitHub repository designed to test token-level constraint modeling and token-level guardrails. Operating directly on a model's token distribution during text generation via native Hugging Face `LogitsProcessor` integration, it eliminates external API dependency and runs entirely on-device for zero-leakage, network-isolated execution.

## Under the Hood

PKLM Sandbox operates by intercepting the model's token prediction pipeline before sampling occurs:

- **Token Interception:** It takes a list of vocabulary token IDs (`blocked_token_ids`) that you want to restrict.
- **Probability Masking:** During generation, it targets the score matrix and forces the log-probability of those banned tokens to negative infinity (`-float("inf")`).
- **Zero Probability Enforcement:** When the model applies softmax to these scores to select the next token, a score of `-inf` results in a 0% probability, ensuring the model never selects those paths.
- **Vectorized Performance:** Using PyTorch's native tensor indexing (`scores[:, self.blocked_token_ids] = -float("inf")`) avoids slow Python-level loops during inference, maintaining low-latency execution.

## Core Mechanics & Benefits

- **Zero-Drift Linguistic Containment:** Forces Large Language Models (LLMs) to strictly adhere to specific vocabularies, formats, or linguistic structures, preventing "hallucination drift" over long generations.
- **Lightweight Hugging Face Integration:** Plugs directly into existing transformers generation pipelines as a native `LogitsProcessor` without requiring massive rewrites of inference code.
- **Low-Overhead Guardrailing:** Dynamically modifies logits during generation rather than running complex external post-processing text validation scripts, serving as an efficient first line of defense.
- **Hard vs. Soft Token Restrictions:** Enables testing of both absolute blocking (setting a token's probability to zero) and relative biasing (nudging probabilities up or down to guide tone or style).
- **Vocabulary-Agnostic Debugging:** Operates directly on token IDs across completely different model architectures (such as Llama, Mistral, or Gemma) by mapping rules to specific tokenizers.
- **Deterministic Output Testing:** Isolates constraints during the logits phase to facilitate reliable unit testing and guarantee structural compliance (such as forcing valid JSON syntax).
- **Non-Stochastic AI Control:** Addresses the unpredictable nature of traditional text generation, removing the "gambling" element from LLM formatting outputs.

## Community Benefits & Enterprise Prototyping

- **Open-Source Accessibility:** Gives independent developers a completely free, open starting point to test token-level control without building complex custom logits interception code from scratch.
- **Safer AI Experimentation:** Acts as a safe testing ground for experimenting with rules that completely block harmful, repetitive, or broken token paths before a model ever goes live.
- **Bridging the Gap to Enterprise Tech:** Serves as a frictionless public playground to evaluate how structured constraints work firsthand before transitioning to enterprise tiers.

## Installation

To install locally from source:

```bash
pip install .

```

To pull and install directly from the repository for offline or edge tool deployments:

```bash
pip install git+https://github.com/TheImmortalPython/pklm-sandbox.git

```

## Quickstart & Usage

To apply the sandbox processor during generation, pass it into the `logits_processor` argument of the `.generate()` method using a `LogitsProcessorList`:

```python
from transformers import AutoModelForCausalLM, AutoTokenizer, LogitsProcessorList
from pklm_sandbox.processor import PKLMSandboxProcessor

# 1. Load model and tokenizer
tokenizer = AutoTokenizer.from_pretrained("gpt2")
model = AutoModelForCausalLM.from_pretrained("gpt2")

# 2. Instantiate your custom processor with the token IDs you want to block
sandbox_processor = PKLMSandboxProcessor(blocked_token_ids=[50256])

# 3. Add it to a LogitsProcessorList
processors = LogitsProcessorList([sandbox_processor])

# 4. Tokenize inputs and pass the processor to generate()
inputs = tokenizer("Hello, world!", return_tensors="pt")
outputs = model.generate(
    **inputs,
    max_new_tokens=50,
    logits_processor=processors
)

print(tokenizer.decode(outputs[0], skip_special_tokens=True))

## Example: Initialize processor with tokens to restrict

```python
processor = PKLMSandboxProcessor(blocked_token_ids=[50256])

```

## Enterprise and Production Deployments

This public repository (`pklm-sandbox`) contains only a basic developer-tier wrapper for testing and evaluation.

For high-stakes enterprise environments requiring the full **PKLM Core (`pklm-core`)** architecture—including custom token-level constraint modeling, heavy Pāṇinian kāraka rule engines (leveraging relational syntax mechanics inspired by traditional Sanskrit grammar frameworks), low-latency compiled binaries, and production SLAs—enterprise clients should reach out directly:

Contact: theimmortalpythonlabs@proton.me

---

> **Founder & Principal AI Architect:** Joshua St. Germain  
> **Enterprise Governance:** TheImmortalPython Labs (`theimmortalpythonlabs@proton.me`)  
> **Repositories:** `pklm-core` (Private) | `pklm-sandbox` | `determinism-runtime-core` (Private) | [the-nsai-guide](https://github.com/TheImmortalPython/the-nsai-guide)

---

## License

Distributed under the MIT License. See LICENSE for more information.
