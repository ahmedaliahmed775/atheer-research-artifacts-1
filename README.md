# Atheer Simulation Evaluation Artifact

This repository is a **reproducibility artifact** for the simulation-based evaluation of the "Atheer" system as described in **Section VI** of the research paper.

This repository aims to enable researchers and developers to reproduce and confirm the published results, ensuring scientific transparency and reliability.

## 📄 Reproducible Results

This repository reproduces (from the same simulation run) the following figures and tables from the research paper:

*   **Fig. 6** — Transaction Success Rate vs Load (Mean ± 95% CI)
*   **Fig. 7** — P95 End-to-End Latency vs Load (Mean ± 95% CI)
*   **Table IV** — Aggregated Performance Summary (Mean ± 95% CI)
*   **Table V** — Failure Breakdown at Max Load (50 TPS) (%)

> **Scope Note:** This artifact currently evaluates **S1 vs S2 (Network-only)**:
> 
> *   S1: Public Internet
> *   S2: Private APN (Atheer)
> 
> The parameters used are defined in `atheer_sim.py` (see `SCENARIOS`, `LOAD_POINTS_TPS`, etc.).

## 📂 Repository Layout

*   `atheer_sim.py` — Main Discrete-Event Simulation (SimPy) file + plotting + table export.
*   `requirements.txt` — List of required Python dependencies.
*   `tools/build_paper_tables.py` — Optional helper tool to build paper tables from a raw CSV file.
*   `configs/paper.yml` — **Documentation mirror** of the paper scenario setup (the current code does **not** directly read YAML files).
*   `docs/` — Contains additional documentation, including `REPRODUCE.md`, `MODEL_ASSUMPTIONS.md`, and `PARAMETERS.md`.

## ⚙️ Requirements

*   Python 3.10+ (recommended)
*   Dependencies listed in `requirements.txt`:
    *   `simpy>=4.1`
    *   `numpy>=1.24`
    *   `pandas>=2.0`
    *   `matplotlib>=3.7`
    *   `jinja2>=3.1`

## 🚀 Quick Start

To reproduce the results, follow these steps:

1.  **Install Dependencies:**

    ```shell
    python -m venv .venv

    # For Windows:
    .venv\Scripts\activate

    # For Linux/macOS:
    source .venv/bin/activate

    pip install -r requirements.txt
    ```

2.  **Run the Simulation:**

    Run the simulation from the repository root:

    ```shell
    python atheer_sim.py
    ```

    If you are running on a headless server (no GUI), you can force a non-interactive Matplotlib backend:

    ```shell
    # For Linux/macOS:
    export MPLBACKEND=Agg

    # For Windows PowerShell:
    # setx MPLBACKEND Agg
    ```

## 📊 Expected Outputs

Running `python atheer_sim.py` will create an `outputs/` folder and write timestamped files within it:

*   **Raw per-transaction CSV file:**
    *   `outputs/atheer_simulation_results_YYYYMMDD_HHMMSS.csv`
*   **Figures (Plots):**
    *   `outputs/figure_success_rate_ci_YYYYMMDD_HHMMSS.png`
    *   `outputs/figure_p95_latency_ci_YYYYMMDD_HHMMSS.png`
*   **Summary Tables:**
    *   `outputs/agg_long_YYYYMMDD_HHMMSS.csv`
    *   `outputs/agg_wide_YYYYMMDD_HHMMSS.csv`
    *   `outputs/table_wide_YYYYMMDD_HHMMSS.tex`
*   **Failure Breakdown (at max load, e.g., 50 TPS):**
    *   `outputs/failure_breakdown_YYYYMMDD_HHMMSS.csv`

## 📝 Optional: Build Paper Tables from an Existing Raw CSV

If you already have a raw simulation CSV and wish to generate paper-ready tables, use the following command:

```shell
python tools/build_paper_tables.py \
  --raw outputs/atheer_simulation_results_YYYYMMDD_HHMMSS.csv \
  --out paper_artifacts
```

This will write the table artifacts into the `paper_artifacts/` folder.

## 🐛 Troubleshooting

*   **Matplotlib issue on headless servers:** If you encounter issues when running the simulation on a headless server, ensure that the Matplotlib backend is set as described in the "Run the Simulation" section above.

## 🤝 Contributing

Contributions to improve this repository are welcome. Please read `CONTRIBUTING.md` (if available) for guidelines on how to contribute.

## 📚 Citation

If you use this software/repository in your research work, please cite it. GitHub reads the `CITATION.cff` file to display the "Cite this repository" option.

## ⚖️ License

This project is licensed under the MIT License. See the `LICENSE` file for more details.

## 📧 Contact

For inquiries or support, please contact the authors via the email address mentioned in the research paper or by opening an Issue in this repository.
