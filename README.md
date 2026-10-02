<div align="center">
  <img src="assets/TIP_Logo_Square.jpg" width="150" alt="TIP Logo">
  
  <p><b>PKLM Sandbox</b></p>

  <p>
    <a href="https://github.com/TheImmortalPython/pklm-sandbox/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-MIT-yellow.svg" alt="License: MIT"></a>
    <a href="https://github.com/TheImmortalPython/pklm-sandbox/actions"><img src="https://github.com/TheImmortalPython/pklm-sandbox/actions/workflows/ci.yml/badge.svg" alt="CI Status"></a>
    <img src="https://img.shields.io/badge/python-3.10%2B-blue.svg" alt="Python Version">
    <img src="https://img.shields.io/github/stars/TheImmortalPython/pklm-sandbox?style=social" alt="GitHub Stars">
  </p>
</div>

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
