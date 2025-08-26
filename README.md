# NLDAS-icechunk

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

### Benchmark timings
See the `notebooks/benchmark.ipynb` for the code. I ran these on a 16 core/64 GB server on the VEDA JupyterHub. I did not randomize the points, but instead aimed that every point is on a different spatial chunk. This should be the worst case scenario, and more regional cases should run faster than these times.

- Single point: *2min 11s*
- 5 points: *6min 37s*
- 10 points: *10m 24s*

### Usage 

You can load the virtual icechunk store into xarray like this:

>[! WARN]
>The current location of the store does not have list access and will not work at the moment!!! Ill update this as soon as it is fixed.

```python
import icechunk
import xarray as xr
import zarr

storage = icechunk.s3_storage(
    bucket='veda-eis-nldas',
    prefix='icechunk-test/NLDAS3-test2/',
    # anonymous=True,
    from_env=True,
)

virtual_credentials = icechunk.containers_credentials(
    {
        "s3://nasa-waterinsight/NLDAS3/forcing/daily/": icechunk.s3_anonymous_credentials()
    }
)
    
repo = icechunk.Repository.open(
    storage=storage,
    authorize_virtual_chunk_access=virtual_credentials,
)

session = repo.readonly_session('main')
ds = xr.open_zarr(session.store, consolidated=False, zarr_version=3)
ds
```

> Note the location of the store is not final yet!