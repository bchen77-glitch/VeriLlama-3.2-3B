# VeriLlama-3.2-3B

VeriLlama-3.2-3B is a fine-tuned **Meta Llama 3.2 3B** model for **Verilog code generation and RTL design assistance**.

This project adapts Llama 3.2 3B to generate synthesizable Verilog code from natural language prompts and module specifications. The model is trained using parameter-efficient fine-tuning (LoRA/QLoRA) on Verilog datasets and evaluated with simulation-based verification.

---

## Project Motivation

Writing Verilog RTL manually can be time-consuming, especially for repetitive digital design tasks such as:

- Counters
- FSMs
- Arithmetic circuits
- Multiplexers
- Registers
- Parameterized modules

General-purpose LLMs often struggle with:

- Verilog syntax correctness
- Hardware semantics
- Testbench compatibility
- Compilation errors

This project aims to improve Verilog generation quality by fine-tuning Llama 3.2 3B on hardware design datasets.

---

## Features

- Fine-tuned on Verilog datasets
- Natural language → Verilog generation
- Supports parameterized RTL modules
- LoRA-based efficient training
- Automated simulation verification using Icarus Verilog
- Compatible with local inference

---

## Model Architecture

Base Model:

- `meta-llama/Llama-3.2-3B`

Fine-tuning Method:

- LoRA / QLoRA

Frameworks:

- Hugging Face Transformers
- PEFT
- Unsloth
- PyTorch

Verification Tool:

- Icarus Verilog (`iverilog`)

---

## Dataset

Training data includes:

- Public Verilog datasets
- RTL benchmark problems
- Instruction-response formatted Verilog examples

Example format:

```json
{
  "instruction": "Generate a 4-bit synchronous counter with reset.",
  "output": "module counter(...); ..."
}
