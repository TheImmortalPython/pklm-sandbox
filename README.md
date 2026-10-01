# PKLM Sandbox (pklm-sandbox)

Official open-source sandbox for PKLM Core, featuring lightweight Hugging Face logits processing and zero-drift linguistic containment.

## Installation

pip install .

## Quickstart

Integrate the sandbox processor into your local pipeline:

from transformers import AutoModelForCausalLM, AutoTokenizer
from pklm_sandbox.processor import PKLMSandboxProcessor

processor = PKLMSandboxProcessor(blocked_token_ids=[50256])

## Example: Initialize processor with tokens to restrict

processor = PKLMSandboxProcessor(blocked_token_ids=[50256])

## Enterprise and Production Deployments

This public repository contains only a basic developer-tier wrapper for testing and evaluation.

For high-stakes enterprise environments, custom token-level constraint modeling, heavy Paninian karaka rule engines, low-latency compiled binaries, and production SLAs, enterprise clients should reach out directly:

Contact: theimmortalpythonlabs@proton.me

## License

Distributed under the MIT License. See LICENSE for more information.
