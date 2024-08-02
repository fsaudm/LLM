# LLMs from HF

This repo contains notebooks that look into downloading, loading, and running LLM models from `HuggingFace` using `transformers` 'on-prem'

<br>

For the **`llama3_1.ipynb`** notebook,
**Consider** that:

1. Every time you start your kernel, you need to run the code cells under `env Variables` to set the appropiate environment variables
2. When loading the models for the first time, the models will be downloaded first, and this naturally takes more time. If the model has been previously downloaded, it will be directly loaded. For a reference, loading `Llama v3.1 - 8B` in this machine takes 45.1 seconds.
3. **These models have a lot of parameters** , and to run inference, the models will be loaded to memory. From HuggingFace (https://huggingface.co/blog/llama31): For inference, the memory requirements depend on the model size and the precision of the weights. Here's a table showing the approximate memory needed for different configurations:

| Model Size | FP16     | FP8      | INT4     |
|------------|----------|----------|----------|
| 8B         | 16 GB    | 8 GB     | 4 GB     |
| 70B        | 140 GB   | 70 GB    | 35 GB    |
| 405B       | 810 GB   | 405 GB   | 203 GB   |

This figures only consider the weights. That is, for `Llama v3.1-70B-FP16`, you neec at least 140 GB! As an example, an H100 node (of 8x H100) has ~640GB of VRAM, so the 405B model would need to be run in a multi-node setup or run at a lower precision (e.g. FP8), which would be the recommended approach.

4. The list of "readily-available" models can be found [here](https://huggingface.co/collections/meta-llama/llama-31-669fc079a0c406a149a5738f). In the Llama 3.1 family, the models available are:
- meta-llama/Meta-Llama-3.1-8B (& -Instruct)
- meta-llama/Meta-Llama-3.1-70B (& -Instruct)
- meta-llama/Meta-Llama-3.1-405B (& -Instruct)
- meta-llama/Meta-Llama-3.1-405B-FP8 (& -Instruct)