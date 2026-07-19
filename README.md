# en-or-not

Fast binary English-versus-non-English text detection.

This repository is the code and training/provenance companion associated with
the current `en-or-not` v1 model. It is the implementation repository used to
produce and ship v1. The model artifacts are published at
[Hugging Face](https://huggingface.co/Mitchins/en-or-not). The released model
is the only version currently supported.

## What it does

`en-or-not` predicts one of two classes:

- `EN`
- `NOT-EN`

It does not identify the specific non-English language. The model processes
raw UTF-8 bytes, with a 256-byte input limit per chunk.

The implementation supports ONNX Runtime for fast CPU inference and TinyGrad
for a small-dependency fallback. The Python package and import namespace remain
`innit-detector` and `innit` for v1 compatibility; `en-or-not` is the project
and model name.

## Install

```bash
pip install innit-detector
```

For the ONNX backend:

```bash
pip install 'innit-detector[onnx]'
```

## CLI

```bash
innit "Hello world!"
innit "Hello" "Bonjour" "你好" "Привет"
innit --json "Hello world!"
innit --download
```

## Python API

```python
from innit import InnitClient, InnitClientConfig

client = InnitClient(InnitClientConfig(backend="onnx"))
result = client.classify("Hello world!")

print(result["is_english"])
print(result["confidence"])
```

## v1 model and evaluation

The v1 model is available from the
[en-or-not model repository](https://huggingface.co/Mitchins/en-or-not).
That repository includes the published 17,544-example OOD set, its provenance
manifest, and the measured evaluation results.

The current OOD result is:

```text
17007/17544 correct = 96.9391%
```

The original 99.94% validation result remains a reported training-pipeline
figure. The training data split and original evaluator are not included here,
so it should not be read as general accuracy. The historical 14-example
synthetic challenge set is diagnostic only and is not used for the published
OOD figure.

## Training and data provenance

The model's documented training sources are described in
[DATA_SOURCES.md](DATA_SOURCES.md). This repository contains the implementation,
model integration, and provenance notes associated with v1; the original
training run itself is not reproduced by the package test suite.

The published OOD set uses a separate, pinned Tatoeba export and is documented
in the Hugging Face model repository. It is source-level OOD relative to the
documented training sources, not a guarantee of zero lexical overlap with
undisclosed training artifacts.

## Development

```bash
pip install -e '.[onnx,dev]'
pytest
ruff check .
```

## License

MIT License. See [LICENSE](LICENSE).
