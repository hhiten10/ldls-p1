# Contributions

Repository: https://github.com/hhiten10/ldls-p1

Three members, each owning one part of the pipeline end to end: the code, the results and plots it produced,
the report sections and the slides presented in the talk.

## Member 1 (Rishabh): setup, measurements, plotting, report (spec steps 1–5)

| | |
|---|---|
| Setup and build | `scripts/00_setup_venv.sh`, `scripts/01_build.sh`, `scripts/env.sh`, `scripts/run_logged.sh` |
| Models | `scripts/02_get_models.sh`, `scripts/02b_llama_base.sh` |
| Hardware | `scripts/03_hw_stream.sh`, `scripts/tools/readbw.c`, `scripts/tools/cpu_freq_logger.ps1` |
| Correctness | `scripts/04_correctness.sh`, `scripts/04b_samples.sh` |
| Sweeps and pipeline | `scripts/05_sweep.sh`, `scripts/run_all_timed.sh`, `scripts/run_final.sh`, `scripts/run_battery_fix.sh`, `scripts/run_rest.sh`, `scripts/run_gaps.sh` |
| Plotting | `scripts/08_analyze.py` (all main-study plots and summary CSVs) |
| Repo and docs | `README.md`, `.gitignore`, `docs/llama_cpp_commit.txt` |
| Report and talk | `report/report.html` → `report/report.pdf`, talk recording |
| Results | `results/hw/`, `results/correctness/`, `results/raw/`, `results/llama_instruct/`, `results/summary_runs.csv`, `results/summary_cross.csv` |
| Plots | `decode_vs_context`, `prefill_vs_prompt`, `thread_scaling` |
| Report sections | §1 Hardware, §2 Models & correctness, §3 Results |
| Slides | 1–4 |

## Member 2 (Himanshu): profiling, roofline, own experiment, Mamba-3 reference (spec steps 6–8, bonus steps 1–2)

| | |
|---|---|
| Profiler | `scripts/01b_build_prof.sh`, `scripts/tools/make_op_profile_patch.py`, `docs/ggml-op-profile.patch`, `scripts/07_profile.sh` |
| Roofline and gap analysis | `scripts/06_roofline.py`, `scripts/10_gap.py` |
| Experiment | `scripts/09_experiment.sh`, `docs/experiment_preregistration.md`, `report/experiment.md` |
| Mamba-3 reference | `bonus/ref/mamba3_ref.py`, `bonus/ref/mamba3_model_ref.py`, `bonus/ref/ppl_check.py`, `bonus/ref/verify_ref.py` |
| Slide deck and docs | `report/slides_new.pptx`, `CONTRIBUTIONS.md` |
| Results | `results/profile/`, `results/experiment/`, `results/roofline.csv`, `results/roofline_bytes.txt`, `results/summary_ops.csv`, `results/summary_roofline.csv`, `results/summary_gap.csv` |
| Plots | `threads_x_context`, `op_breakdown`, `predicted_vs_measured` |
| Report sections | §4 Profiling, §5 Roofline, §6 Own experiment |
| Slides | 5–8 |

## Member 3 (Aditya Sai Teja B, @aditya25058): Mamba-3 kernels and ggml operator, MIMO answer, PARAM Rudra (Rudra reference run, bonus steps 3–7)

| | |
|---|---|
| Traces | `bonus/ref/make_trace.py`, `bonus/ref/upstream_refs.py` (copied from the official Mamba repository) |
| Kernels | `bonus/kernel/m3.h`, `bonus/kernel/m3_kernels.cpp`, `bonus/kernel/main.cpp`, `bonus/kernel/build.sh` |
| ggml operator | `bonus/ggml/ggml_driver.cpp`, `bonus/ggml/build.sh` |
| Timing and bonus plots | `bonus/run_bench.sh`, `bonus/analyze_bonus.py` |
| Write-up | `report/bonus_mamba3.md` |
| Rudra | `rudra/setup_login.sh`, `rudra/reference.sbatch` |
| Results | `results/bonus/`, `results/rudra/` |
| Plots | `bonus_step_time`, `bonus_roofline`, `bonus_errors` |
| Report sections | §7 Rudra, §8 Mamba-3 bonus, §9 What we learned |
| Slides | 9–12 |
