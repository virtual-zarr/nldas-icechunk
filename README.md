# LNDAS-icechunk

## Dependency management

This repo uses [uv](https://docs.astral.sh/uv/) as package/project manager.


### Running Jupyter Notebooks on the NASA VEDA hub

To reproduce results in the notebooks, you need to build a custom kernel with 

```
uv sync
uv run bash
python -m ipykernel install --user --name=lndasenv --display-name="LNDAS-VENV"
```

Then select the "LNDAS-VENV" kernel on the upper right corner drop-down in your notebook (you might have to refresh the browser to see it). 

### Running scripts

You can run the scripts with 
```
uv run <scriptname>
```
