# PKLM Sandbox (`pklm-sandbox`)

Official open-source sandbox for **PKLM Core**, featuring lightweight Hugging Face logits processing and zero-drift linguistic containment.

## Quickstart

Integrate the sandbox processor into your local pipeline:

```python
from transformers import AutoModelForCausalLM, AutoTokenizer
from pklm_sandbox.processor import PKLMSandboxProcessor

# Example: Initialize processor with tokens to restrict
processor = PKLMSandboxProcessor(blocked_token_ids=[50256]) # Example token ID
