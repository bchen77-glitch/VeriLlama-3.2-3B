# VeriLlama-3.2-3B

VeriLlama-3.2-3B is a fine-tuned **Meta Llama 3.2 3B** model designed for **Verilog RTL code generation** from natural language descriptions.

This project improves hardware code generation reliability by combining:

- LLM fine-tuning
- Verilog dataset training
- RTL generation
- Simulation-based verification

The model takes natural language hardware specifications and generates synthesizable Verilog code for digital circuit design tasks.

---

## Project Overview

Traditional LLMs often struggle with hardware design tasks because Verilog requires:

- Strict syntax correctness
- Hardware semantic understanding
- Timing logic awareness
- Functional verification

This project addresses these issues by fine-tuning Llama 3.2 3B on Verilog-specific datasets and validating generated RTL through simulation.

---

## Features

- Natural language → Verilog generation
- Fine-tuned Llama 3.2 3B model
- Parameter-efficient fine-tuning (LoRA/QLoRA)
- RTL code generation
- Automated verification using Icarus Verilog
- Local inference support

---

## Tech Stack

- Python
- PyTorch
- Hugging Face Transformers
- PEFT
- Unsloth
- Icarus Verilog
- Verilog HDL

---

## Dataset

This project uses Verilog-related datasets for supervised fine-tuning:

- RTLLM dataset
- VerilogEval benchmark
- GitHub Verilog dataset
- Custom instruction-response formatting

Example training format:

```json
{
  "instruction": "Generate a 4-bit synchronous counter with reset.",
  "output": "module counter(...); ..."
}
```

---

## Training Setup

### Create environment

```bash
conda create -n verillama python=3.10
conda activate verillama
```

### Install dependencies

```bash
pip install torch transformers datasets peft trl unsloth
```

### Train model

```bash
python train.py
```

---

## Inference Example

```python
from transformers import AutoTokenizer, AutoModelForCausalLM

model_path = "./VeriLlama-3.2-3B"

tokenizer = AutoTokenizer.from_pretrained(model_path)
model = AutoTokenizer.from_pretrained(model_path)

prompt = """
Generate Verilog code for a 4-bit synchronous counter with reset.
"""

inputs = tokenizer(prompt, return_tensors="pt")

outputs = model.generate(
    **inputs,
    max_new_tokens=300
)

print(tokenizer.decode(outputs[0]))
```

---

## Example Generation

### Input Prompt

```text
Generate Verilog code for a parameterized ternary adder tree with five inputs and one clocked output.
```

### Generated Output

```verilog
module ternary_adder_tree #(parameter WIDTH = 8)(
    input clk,
    input [WIDTH-1:0] a,b,c,d,e,
    output reg [WIDTH-1:0] out
);

always @(posedge clk) begin
    out <= (a+b+c) + (d+e);
end

endmodule
```

---

## Verification Flow

Generated RTL is validated using Icarus Verilog simulation:

```bash
iverilog testbench.v design.v
vvp a.out
```

Verification checks:

- Syntax correctness
- Compilation success
- Functional correctness

---

## Experimental Results

| Metric | Result |
|----------|----------|
| Compilation Success Rate | XX% |
| Functional Pass Rate | XX% |
| Pass@1 | XX% |

> Replace these values with your actual experiment results.

---

## Project Structure

```bash
VeriLlama-3.2-3B/
│
├── dataset/
├── training/
├── evaluation/
├── inference/
├── saved_model/
├── README.md
└── requirements.txt
```

---

## Future Improvements

- Improve functional correctness
- Expand Verilog dataset size
- Add SystemVerilog support
- Integrate formal verification
- Deploy as hardware coding assistant

---

## Author

**Boruei Chen**

GitHub: https://github.com/bchen77-glitch/VeriLlama-3.2-3B

---

## License

This project follows Meta Llama licensing requirements.
Please ensure compliance before commercial use.
