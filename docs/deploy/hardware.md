# 所需硬件配置

运行 WeClone（尤其是模型微调阶段）对硬件有较高要求，**重点在于显存（VRAM）**。不建议在集成显卡或仅使用 CPU 的环境下运行，推荐使用带有独立 GPU 的设备，或租用云端 GPU 服务。

项目默认使用 [`Qwen2.5-7B-Instruct`](https://www.modelscope.cn/models/Qwen/Qwen2.5-7B-Instruct) 模型，并采用 **LoRA** 方法进行微调，显存需求约为 **16GB**。

下表列出了不同模型规模与微调方法所需的显存估算（数据来源于 [LLaMA Factory](https://github.com/hiyouga/LLaMA-Factory)）：

| 微调方法                        | 精度 (bits) | 7B 模型 | 14B 模型 | 30B 模型 | 70B 模型 | `x`B 模型 |
| ------------------------------- | ----------- | ------- | -------- | -------- | -------- | --------- |
| Full (`bf16` / `fp16`)          | 32          | 120GB   | 240GB    | 600GB    | 1200GB   | `18x` GB  |
| Full (`pure_bf16`)              | 16          | 60GB    | 120GB    | 300GB    | 600GB    | `8x` GB   |
| Freeze / LoRA / GaLore / APOLLO | 16          | 16GB    | 32GB     | 64GB     | 160GB    | `2x` GB   |
| QLoRA                           | 8           | 10GB    | 20GB     | 40GB     | 80GB     | `x` GB    |
| QLoRA                           | 4           | 6GB     | 12GB     | 24GB     | 48GB     | `x/2` GB  |
| QLoRA                           | 2           | 4GB     | 8GB      | 16GB     | 24GB     | `x/4` GB  |

::: tip
显存 ≥16GB：推荐使用默认的 LoRA 微调方案。
显存 <16GB：可考虑切换至 QLoRA 或选择更小参数量的模型。
:::

此外，请预留至少 **20GB 以上硬盘空间**，以存储模型文件、中间结果和缓存数据。

如果你希望启用 QLoRA 微调方式，请查阅后续章节 “[修改配置文件](override-settings.md)” 了解如何切换微调策略。