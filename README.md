# Fengxin Zhou

**AI Infrastructure · Distributed LLM Inference**

I build and debug vLLM deployments across GPU nodes. My work focuses on serving reliability, CUDA runtime diagnostics, and reproducible latency and throughput benchmarks.

[Engineering portfolio (EN)](https://zfxzzz.github.io/?lang=en) · [工程作品集](https://zfxzzz.github.io/?lang=zh) · [Upstream contributions](#upstream-contributions) · [Runnable projects](#runnable-projects)

## Upstream contributions

- **FlashInfer · CUDA JIT diagnostics.** Traced a CUDA 12.9 worker failure to a CUDA 13-built sampler that required `libcudart.so.13`. Submitted a toolchain mismatch warning and two CPU regression tests. [Issue #5145](https://github.com/flashinfer-ai/flashinfer/issues/5145) · [PR #5154](https://github.com/flashinfer-ai/flashinfer/pull/5154)
- **vLLM · Benchmark correctness.** Reproduced peak-concurrency overcounting caused by second-level buckets. Submitted an event-based counter and four boundary tests. [Issue #56653](https://github.com/vllm-project/vllm/issues/56653) · [PR #56675](https://github.com/vllm-project/vllm/pull/56675)
- **SparkRing · Deployment troubleshooting.** Documented how to diagnose a missing NVIDIA CDI refresh service and verify GPU device entries before retrying a DGX Spark deployment. [PR #403](https://github.com/FujitsuPolycom/sparkring/pull/403)
- **vLLM · Deployment validation.** Reported a gap in DeepSeek V4.1 Flash automatic tool-call verification and provided a sample check. A community contributor opened the follow-up PR. Separately, reported that the benchmark guide recommended a KV-cache sizing estimate as an SLA limit. [Tool-calling Issue #69114](https://github.com/vllm-project/vllm/issues/69114) · [Community PR #69131](https://github.com/vllm-project/vllm/pull/69131) · [Capacity Issue #69117](https://github.com/vllm-project/vllm/issues/69117)

## Runnable projects

- **LLM Serving Checks.** Check structured tool calls, run concurrent bursts, and compare saved JSON, JSONL, or CSV benchmarks with workload differences flagged. [Repository and quick start](https://github.com/ZFXzzz/llm-serving-checks) · [Nginx cutover guide](https://github.com/ZFXzzz/llm-serving-checks/blob/main/docs/nginx-backend-cutover.md)
- **Agent Progress Guard.** A Python state machine that pauses the no-progress timer during a dependency outage while enforcing the task deadline. Includes synthetic-time tests. [Repository and tests](https://github.com/ZFXzzz/agent-progress-guard)

## Systems work

- **Kimi K3 on two 8-GPU H20-3e nodes.** Brought up vLLM with Ray and verified generation after recovering from a CUDA runtime mismatch. In one C32 synthetic run with 8,192 requested input tokens and a 512-token output budget, **32/32 requests completed** at **314.46 aggregate output tok/s** and **2.92 s mean TTFT**. [Deployment and benchmark case study](https://zfxzzz.github.io/?case=k3&lang=en)
- **DeepSeek V4.1 Flash on four DGX Sparks.** Brought up a TP4 deployment with SparkRing/SIRCL. Restored worker management connectivity and verified RoCE GIDs, container GPU discovery, and API readiness. [CDI troubleshooting contribution](https://github.com/FujitsuPolycom/sparkring/pull/403)
