# Entropy Market Filter and Portfolio Allocation

Final project package for the Shannon-entropy market filter and dynamic portfolio-allocation analysis.

## Repository contents

- `unified_entropy_portfolio.ipynb`: complete executable analysis.
- `data/`: prepared input datasets used by the notebook.
- `outputs/`: generated CSV results and figures from the latest successful run.
- `Messina_Florio.pdf`: final project report.

## Reproduce the analysis

Create a Python environment, install the dependencies, and execute the notebook from the repository root:

```powershell
python -m pip install -r requirements.txt
python -m jupyter nbconvert --to notebook --execute --inplace --ExecutePreprocessor.timeout=3600 unified_entropy_portfolio.ipynb
```

The notebook reads the files in `data/` and writes the reproducible results to `outputs/`.
