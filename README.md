# Project 1 (Option 3: Mamba-2 on CPU + Mamba-3 bonus): individual contribution of Rishabh

**Member 1: Setup, measurements, plotting and report (spec steps 1–5)**

GitHub repository: https://github.com/hhiten10/ldls-project-1

Team: Rishabh (Member 1), Himanshu (Member 2), Aditya Sai Teja B (Member 3). The full per-member split is in
`Project-1/CONTRIBUTIONS.md` once all three folders are merged.

## Work completed
- Set up the environment and built llama.cpp CPU-only at a pinned commit (WSL2, OpenMP, one thread per physical core).
- Downloaded, converted and quantized Mamba-2 1.3B/2.7B, Mamba-1 1.4B and the Llama-3.2-1B base model under the spec's quantization rules.
- Recorded the hardware and measured memory bandwidth (STREAM + own read-only kernel): 30.5 GB/s read at 8 threads, saturated by 3–4 cores.
- Correctness: perplexity on a fixed text sample and sample generations for every model, with peak RSS logged.
- Ran all benchmark sweeps (prefill vs prompt length, decode vs context, thread scaling, threads × context), 3 repetitions each, with swap and AC-power guards.
- Wrote the analysis/plotting script that turns the raw runs into the summary CSVs and plots.
- Assembled the README and the 4-page report, and recorded the talk.

## Key results
- Mamba-2 1.3B Q4 decode 18.2 → 18.1 tok/s from 0 to 32k context (flat); Llama-3.2-1B falls 29.5 → 3.7 tok/s by 16k.
- Prefill: Mamba-2 1.3B 122 → 128 tok/s (512 → 32k); Llama 205 → 90 tok/s.
- Decode stops scaling at 3–4 threads (bandwidth bound); prefill keeps scaling to 8 cores.

## My files
| File | What it does |
|---|---|
| `scripts/00_setup_venv.sh` | Python venv (CPU torch, gguf, plotting) |
| `scripts/01_build.sh` | llama.cpp CPU-only build at the pinned commit |
| `scripts/env.sh` | shared paths, thread pinning, model list |
| `scripts/run_logged.sh` | runs any stage with a timestamped log |
| `scripts/02_get_models.sh` | download, convert (lossless 16-bit) and quantize Mamba-1/2 models, disk guard |
| `scripts/02b_llama_base.sh` | Llama-3.2-1B base conversion + Q4_K_M |
| `scripts/03_hw_stream.sh` | hardware record + STREAM / read-bandwidth sweep |
| `scripts/tools/readbw.c` | read-only bandwidth microbenchmark |
| `scripts/tools/cpu_freq_logger.ps1` | CPU frequency / AC-power logger during runs |
| `scripts/04_correctness.sh` | perplexity on the fixed text sample + peak RSS |
| `scripts/04b_samples.sh` | sample generations for every model |
| `scripts/05_sweep.sh` | prefill / decode / thread / context sweeps, 3 repetitions, swap guard |
| `scripts/run_all_timed.sh` | end-to-end pipeline driver |
| `scripts/run_final.sh` | final rerun of analysis stages |
| `scripts/run_battery_fix.sh` | redo of runs that overlapped off-AC windows |
| `scripts/run_rest.sh` | rerun after pipeline crash fixes |
| `scripts/run_gaps.sh` | requirement-audit reruns (base Llama, cross sweep) |
| `scripts/08_analyze.py` | aggregates raw runs into summary CSVs and draws the main-study plots |
| `README.md` | project README: hardware, models, reproduce commands, headline results |
| `.gitignore` | build outputs and transient files |
| `docs/llama_cpp_commit.txt` | pinned llama.cpp commit |
| `report/report.html` | 4-page report source |
| `report/report.pdf` | 4-page report (with repository link) |
| `presentation video.mp4` | recorded 10-minute talk |

Results: `results/hw/`, `results/correctness/`, `results/raw/`, `results/llama_instruct/`, `results/summary_runs.csv`, `results/summary_cross.csv`
Plots: `plots/decode_vs_context.png`, `plots/prefill_vs_prompt.png`, `plots/thread_scaling.png`

Report sections: §1 Hardware, §2 Models & correctness, §3 Results. Talk: slides 1–4.

Totals: 18 code files, 679 lines of code (non-blank), 456 result files, 3 plots, 483 files in all.

## How this zip fits with the other two
`Project-1/` holds my files at their repository paths. Copying the `Project-1/` folders from all three members' zips
into one folder gives the complete repository; `Project-1/README.md` (Member 1) then explains how to rerun everything.
