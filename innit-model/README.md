# en-or-not v1 model reference

The v1 model artifacts are published at
[huggingface.co/Mitchins/en-or-not](https://huggingface.co/Mitchins/en-or-not).

This directory keeps the model configuration and metadata used by the Python
package. The public model repository contains the ONNX and SafeTensors files,
the reproducible OOD set, its provenance manifest, and the current evaluation
figures.

## Model contract

- Architecture: `TinyByteCNN_EN`
- Parameters: 156,642
- Input: UTF-8 bytes, maximum 256 bytes per chunk
- Classes: `NOT-EN`, `EN`
- Task: binary English detection

The model is not a general language identifier. See the model repository for
limitations, provenance, and evaluation details.
