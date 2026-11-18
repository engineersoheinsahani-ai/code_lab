# CHANGE REPORT - code-team improve wave
- date: 2026-10-26   model: openai/gpt-oss-120b   improve iterations: 7   kept batches: 0   reverted batches: 3
- NOTE: patches the integrity guard REFUSED (tests/, data/, outputs/, logs/, results/, provenance tools) are recorded in AUDIT.md and are deliberately NOT listed below as changes - they never happened.
- entry: python3 src/main.py --n-seeds 1
- regress_tol: 0.005 (a gated metric worsening by more than this reverts the whole batch)
- runtime_tol: 0.15 (wall-clock band; a batch that moves NO metric beyond its band is NEUTRAL and reverted - nothing was proven either way)
- the FINAL numbers come from ONE run: {"ts": "2026-10-25T07:16:30", "log": "pipeline_v8_20261025_064113.log", "runtime_s": 2119.0, "entry": "python3 src/main.py --n-seeds 1"}
- BASELINE metrics: {"r2_primary": 0.6453, "rmse_primary_kbtu": 33149.0, "r2_weighted": 0.6736, "cov90_pct": 90.1, "r2_eui_derived": 0.656, "r2_ensemble": 0.6539, "logo_mean_r2": 0.6973, "pop_calib_bias_pct": -5.77, "cov80_pct": 78.9, "cov95_pct": 95.6, "oof_stacked_r2": 0.7628, "val_r2_log": 0.7724, "tl_ablation_r2": 0.6421, "runtime_s": 2119.0}
- FINAL (best accepted) metrics: {"r2_primary": 0.6453, "rmse_primary_kbtu": 33149.0, "r2_weighted": 0.6736, "cov90_pct": 90.1, "r2_eui_derived": 0.656, "r2_ensemble": 0.6539, "logo_mean_r2": 0.6973, "pop_calib_bias_pct": -5.77, "cov80_pct": 78.9, "cov95_pct": 95.6, "oof_stacked_r2": 0.7628, "val_r2_log": 0.7724, "tl_ablation_r2": 0.6421, "runtime_s": 2119.0}

## Kept changes
- (none)

## Reverted changes (regression, NEUTRAL, inert or crash)
- iter 1 [speed and memory optimisation (CPU-first; the ARENA_DEVICE switch must keep working)] `src/model_selection.py` - Suppresses LightGBM training logs to reduce I/O overhead and -> runtime_s: 2047.0 -> 2102.5 (-2.71%)
- iter 2 [speed and memory optimisation (CPU-first; the ARENA_DEVICE switch must keep working)] `src/model_selection.py` - Suppresses redundant eval_set deprecation warnings by explic -> runtime_s: 2047.0 -> 2286.7 (-11.71%)
- iter 3 [speed and memory optimisation (CPU-first; the ARENA_DEVICE switch must keep working)] `src/model_selection.py` - Prevents XGBoost eval_metric conflict warnings and ensures c -> runtime_s: 2047.0 -> 2234.8 (-9.17%)

Input data was never modified (owner law); the data seal was verified before and after
every run and every patch batch. Every kept change alters what the manuscript must describe:
the writers read this file and report the FINAL protocol, not the older one.
NUMBER PROVENANCE: results-pool/metrics.json carries `src_run` (the log file, timestamp and
wall-clock of the single run the numbers came from) and `runout_from` (which artefacts were
shipped alongside them). The writers must cite ONLY that deposit, and must not mix its
numbers with tables from any other run in code-lab/outputs/.
