arm64_mask_gen_py

PyO3 wrapper around [`arm64-mask-gen`](https://github.com/xliee/arm64-mask-gen) to expose pattern:mask generation to Python (used by the IDA plugin).

Build (recommended with maturin):

1. Install maturin:

```bash
   pip install maturin
```

2. Build & install into your current Python:

```bash
   maturin develop --release
```

## License

Licensed under the MIT License. See [LICENSE](LICENSE) for details.