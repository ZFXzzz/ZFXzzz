# Fengxin Zhou

**AI Infrastructure Engineer · Distributed LLM Serving and GPU Reliability**

I deploy and debug multi-node inference with vLLM and Ray on H20-3e and DGX Spark. My work covers CUDA runtime and build tooling, serving reliability, and reproducible latency and throughput measurement.

[Engineering portfolio · EN / 中文](https://zfxzzz.github.io/) · [Upstream contributions](#upstream-contributions) · [Runnable projects](#runnable-projects)

## Upstream contributions

| Project | Contribution | Evidence |
| --- | --- | --- |
| **FlashInfer** | Traced a CUDA 13 JIT sampler artifact to a CUDA 12.9 worker failure using build rules and ELF dependencies. Submitted a cross-major toolchain warning with two CPU regression tests. | [Issue #5145](https://github.com/flashinfer-ai/flashinfer/issues/5145) · [PR #5154](https://github.com/flashinfer-ai/flashinfer/pull/5154) |
| **vLLM** | Reproduced inflated benchmark peak concurrency with adjacent and sub-second requests. Submitted an event-based peak counter and four boundary cases. | [Issue #56653](https://github.com/vllm-project/vllm/issues/56653) · [PR #56675](https://github.com/vllm-project/vllm/pull/56675) |
| **SparkRing** | Documented how to diagnose a missing NVIDIA CDI refresh service and verify GPU device entries before retrying a DGX Spark deployment. | [PR #403](https://github.com/FujitsuPolycom/sparkring/pull/403) |

**Additional vLLM reports.** Proposed a DeepSeek V4.1 Flash tool-calling check after finding that plain chat passed while automatic tool selection failed. The report links my example and a community contributor's implementation. I also reported ambiguous SLA guidance that equates a startup KV-cache estimate with measured serving capacity. [Tool calling #69114](https://github.com/vllm-project/vllm/issues/69114) · [KV cache #69117](https://github.com/vllm-project/vllm/issues/69117)

## Runnable projects

| Repository | What you can inspect or run |
| --- | --- |
| **[LLM Serving Checks](https://github.com/ZFXzzz/llm-serving-checks)** | OpenAI-compatible tool-call validation, burst benchmarks, and offline JSON/JSONL/CSV comparison that flags workload differences. Includes synthetic fixtures, offline tests, and an Nginx cutover and rollback guide. |
| **[Agent Progress Guard](https://github.com/ZFXzzz/agent-progress-guard)** | A dependency-aware state machine for agent workflows. Synthetic-time tests cover empty results, dependency outages, and a task deadline that continues through an outage. |

Try the benchmark report with the included synthetic data:

```sh
git clone https://github.com/ZFXzzz/llm-serving-checks.git
cd llm-serving-checks
python benchmark_report.py examples/benchmark-summaries.csv
```

## Systems work

- **Distributed serving.** Brought up Kimi K3 across two 8-GPU H20-3e nodes with TP16/EP16. Diagnosed the CUDA toolchain mismatch on Ray workers and verified generation after recovery.
- **GPU and fabric reliability.** Brought up DeepSeek V4.1 Flash on four DGX Sparks with TP4/SIRCL. Checked RoCE GIDs, management connectivity, and container GPU discovery before API acceptance.
- **Performance validation.** Compare TTFT, TPOT, throughput, and success rate under explicit prompt length, output length, cache conditions, and client concurrency. See the [engineering case studies](https://zfxzzz.github.io/).
