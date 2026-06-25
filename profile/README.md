<div align="center">

<a href="https://smedjan.dev"><img src="https://raw.githubusercontent.com/smedjan/smedjan/main/docs/banner.png?v=2" alt="SMEDJAN — pure-Rust LLM engine. Own the stack." width="840"></a>

**A pure-Rust LLM training &amp; inference engine — own the whole stack, from tokenizer to served checkpoint. Metal + CUDA. Zero Python, zero PyTorch, zero cloud.**

[**Website**](https://smedjan.dev) · [**Engine**](https://github.com/smedjan/smedjan) · [**crates.io**](https://crates.io/crates/smedjan) · [**Docs**](https://smedjan.dev/docs)

</div>

---

*Smedjan* is Swedish for "the smithy" — the forge where you make your own tools. Every line of code, every GPU kernel, every byte of the model lives in one repo: ~45K lines of Rust whose entire dependency tree is `clap`, `rand`, `memmap2`, `byteorder`, plus the GPU FFI bindings.

### What's inside

- **One binary, the whole pipeline** — `tokenizer → prepare → train → distill → sft → dpo → quantize → export-gguf → generate`. No glue scripts, no handoff between frameworks, no step that secretly needs Python.
- **Two GPU backends, one codebase** — Metal on Apple Silicon, CUDA on NVIDIA, selected at compile time. Train on a Mac, resume on an H100, same checkpoint format.
- **Built from scratch** — hand-written tape-based autograd; an RMSNorm / RoPE (NTK + YaRN) / GQA / SwiGLU decoder; alternative mixers (linear attention, SSM/Mamba-2, RWKV, MLA, block-sparse); MoE routing; AdamW + Muon/NorMuon; speculative decoding; Q4/Q8 quantization; safetensors + GGUF interop.
- **Measured, not extrapolated** — on an M1 Mac mini (16 GB) the 45M `medium` model runs **~5,090 tok/s** inference and **~1,150 tok/s** training; the hardware simdgroup-MMA path is ~1.3–1.4× the scalar fallback. On an RTX 4090, forward inference reaches **~70,000 tok/s**. Reproduce with `smedjan bench`.

### See it run

The headline on **[smedjan.dev](https://smedjan.dev)** is written live, in your browser, by a 295K-parameter Smedjan model compiled to WebAssembly — no server, no API. The engine demoing itself.

### Get started

```bash
git clone https://github.com/smedjan/smedjan.git
cd smedjan && cargo build --release      # Metal (macOS / Apple Silicon) by default
```

<sub>MIT-licensed · one engineer's engine · contributions welcome</sub>
