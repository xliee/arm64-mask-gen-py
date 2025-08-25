# ARM64 Mask Generator - Python Wrapper

[![PyPI version](https://badge.fury.io/py/arm64-mask-gen-py.svg)](https://badge.fury.io/py/arm64-mask-gen-py) [![CI](https://github.com/xliee/arm64-mask-gen-py/actions/workflows/CI.yml/badge.svg)](https://github.com/xliee/arm64-mask-gen-py/actions/workflows/CI.yml)

A PyO3 wrapper around the [`arm64-mask-gen`](https://github.com/xliee/arm64-mask-gen) Rust library, providing Python bindings for ARM64 assembly pattern and mask generation.

## Features

- **Fast Pattern Generation**: Rust-powered ARM64 assembly to byte pattern conversion
- **Python Integration**: Seamless integration with Python-based reverse engineering tools
- **IDA Pro Compatible**: Designed for use with the [IDA Mask Plugin](https://github.com/xliee/ida_mask_plugin)
- **Template Support**: Flexible template syntax with wildcard placeholders

## 📦 Installation

### Option 1: Install from PyPI (Recommended)
```bash
pip install arm64-mask-gen-py
```

### Option 2: Build from Source
1. Install Rust.

2. Install Maturin:
```bash
pip install maturin
```

3. Clone and build:
```bash
git clone https://github.com/xliee/arm64-mask-gen-py
cd arm64-mask-gen-py
maturin develop --release
```

### Option 3: Build for IDA Pro
For IDA Pro integration, build against IDA's Python interpreter:
```bash
maturin develop --release --interpreter /path/to/ida/python
```

## 🚀 Quick Start

```python
import arm64_mask_gen_py

# Generate pattern and mask from ARM64 assembly template
pattern, mask = arm64_mask_gen_py.make_r2_mask("BL #?")

print(f"Template: BL #?")
print(f"Pattern : {pattern}")  # 00000094
print(f"Mask    : {mask}")     # 000000fc
```

## 📖 Examples

### Basic Usage
```python
import arm64_mask_gen_py

# Branch with Link instruction (any target)
pattern, mask = arm64_mask_gen_py.make_r2_mask("BL #?")
# Result: pattern="00000094", mask="000000fc"

# Move immediate with wildcard
pattern, mask = arm64_mask_gen_py.make_r2_mask("MOV X3, #?")
# Matches any MOV X3, #immediate instruction

# Load with specific register
pattern, mask = arm64_mask_gen_py.make_r2_mask("LDR X0, [X1]")
# Exact match for LDR X0, [X1]
```

### Error Handling
```python
import arm64_mask_gen_py

try:
    pattern, mask = arm64_mask_gen_py.make_r2_mask("INVALID_INSTRUCTION")
except Exception as e:
    print(f"Failed to generate pattern: {e}")
```

### Command Line Testing
Run the included example script:
```bash
python examples/sample_use.py "BL #?"
python examples/sample_use.py "MOV X3, #?"
```

## 🔧 API Reference

### `make_r2_mask(template: str) -> tuple[str, str]`

Generates a byte pattern and mask from an ARM64 assembly template.

**Parameters:**
- `template` (str): ARM64 assembly instruction with optional wildcards (`#?` for immediate values)

**Returns:**
- `tuple[str, str]`: A tuple containing `(pattern, mask)` as hexadecimal strings

**Raises:**
- `Exception`: If the template cannot be parsed or assembled

## 🛠️ Development

### Building
```bash
# Development build
maturin develop

# Release build
maturin develop --release

# Build wheel
maturin build --release
```

### Testing
```bash
# Run example
python examples/sample_use.py

# Test different templates
python examples/sample_use.py "ADD X0, X1, X2"
python examples/sample_use.py "STR X0, [SP, #?]"
```

## 🔗 Related Projects

- **Core Library**: [arm64-mask-gen](https://github.com/xliee/arm64-mask-gen) - Rust implementation
- **IDA Plugin**: [ida_mask_plugin](https://github.com/xliee/ida_mask_plugin) - IDA Pro integration
- **PyPI Package**: [arm64-mask-gen-py](https://pypi.org/project/arm64-mask-gen-py/) - Published wheel

## 📋 Requirements

- **Python**: 3.7+
- **Rust**: For building from source
- **Platform**: Linux, macOS, Windows

## 📝 License

Licensed under the MIT License. See [LICENSE](LICENSE) for details.

---

*Flexible ARM64 pattern generation for Python*
