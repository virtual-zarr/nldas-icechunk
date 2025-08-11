# LNDAS-icechunk

## Dependency management

This repo uses [uv](https://docs.astral.sh/uv/) as package/project manager.


### Running Jupyter Notebooks on the NASA VEDA hub

To reproduce results in the notebooks, you need to build a custom kernel with 

```
uv sync
uv run bash
python -m ipykernel install --user --name=nldasenv --display-name="NLDAS-VENV"
```

Then select the "NLDAS-VENV" kernel on the upper right corner drop-down in your notebook (you might have to refresh the browser to see it). 

### Running scripts

You can run the scripts with 
```
uv run <scriptname>
```

### Benchmark timings
See the `notebooks/benchmark.ipynb` for the code. I ran these on a 16 core/64 GB server on the VEDA JupyterHub. I did not randomize the points, but instead aimed that every point is on a different spatial chunk. This should be the worst case scenario, and more regional cases should run faster than these times.

- Single point: *2min 11s*
- 5 points: *6min 37s*
- 10 points: *10m 24s*
