# Timing Games on Ethereum: Who Pays for Waiting?

Code and derived data to reproduce every figure, table, and number in the paper.

## Quick start (offline, no database access needed)

```bash
pip install -r requirements.txt
jupyter notebook timing_games.ipynb   # run all cells
```

With no credentials set, the notebook runs in offline mode and reads all
inputs from `data/`. It writes figures to `fig/`, LaTeX tables to the working
directory, and every number quoted in the paper to `numbers.json`.

## Data

All raw data come from [Xatu](https://github.com/ethpandaops/xatu), an open
Ethereum dataset maintained by ethPandaOps. `data/` holds the result of every
query the notebook makes, restricted to October 2024 - October 2026:

| File | Content |
|---|---|
| `cache_sentry.parquet` | observations per sentry and month (sentry selection) |
| `cache_sentry_median.parquet` | per-sentry median propagation time by month |
| `cache_arr.parquet` | per-slot median propagation time across retained sentries |
| `cache_prop.parquet` | proposer validator index per observed block |
| `cache_nodes.parquet` | validator index -> operator label |
| `cache_mev.parquet` | MEV-Boost payment and block status per slot |
| `cache_bid.parquet` | arrival time of the winning bid per slot |
| `cache_block_meta.parquet` | block size, gas used, and blob count per slot |
| `cache_attestation.parquet` | head-vote counts per slot (from 2025-05-14) |
| `cache_balance_monthly.parquet` | monthly average and total effective balance |
| `cache_eb_end.parquet` | effective balance per validator at the end of the window |
| `cache_burden_3200_4000.parquet` | head-correct votes per operator on late vs. on-time blocks |
| `cache_late_inclusion.parquet` | attestations included two or more slots late, per slot |

## Re-pulling the raw data

Set `XATU_USER` and `XATU_PASSWORD` for the ethPandaOps ClickHouse endpoint
(access is provided by ethPandaOps), delete the cache files you want to
refresh, and rerun. Some queries also use a local Xatu mirror on
`localhost:8123`. A full re-pull takes several hours.

## License

Code: MIT. Derived data: CC BY 4.0.
