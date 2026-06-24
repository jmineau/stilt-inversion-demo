# Inverse modeling with STILT, in Python

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/jmineau/stilt-inversion-demo/blob/main/inverse_modeling_with_stilt.ipynb)

A live-demo notebook touring three small, composable Python packages that cover
the STILT inverse-modeling pipeline from meteorology to posterior flux, with a
look at the Salt Lake Valley methane inversion they were built for.

Click the badge above to run it on Google Colab. Everything installs and
downloads itself, so there is no local setup and no CHPC access needed. It even
runs a one-off STILT footprint live (pystilt bundles the HYSPLIT engine).

| stage | package | what it does |
|---|---|---|
| meteorology | [`arlmet`](https://github.com/jmineau/arl-met) | reads/writes ARL-packed met as `xarray`, and fetches it cropped from NOAA |
| transport | [PYSTILT](https://github.com/jmineau/PYSTILT) | runs STILT in Python (pip `pystilt`, import `stilt`), producing trajectories and footprints |
| inversion | [`fips`](https://github.com/jmineau/fips) | assembles and solves the linear Bayesian inverse problem |
| application | [`slv`](https://github.com/jmineau/slv) | an example of wrapping the pystilt and fips pipeline (SLV CH4) |

The footprint is the hinge. It is STILT's output, and it is also a row of the
inverse problem's Jacobian. Staying in Python means you never leave `xarray` and
`pandas` from the met file to the posterior.

### Contents

- `inverse_modeling_with_stilt.ipynb`, the notebook (open it in Colab).
- `data/`, small bundled inputs: a footprint and trajectory sample (the fallback
  if a given Colab cannot run the live STILT run).

### Running locally instead of Colab

```bash
pip install "fips[flux]" "arlmet[sources]"
jupyter lab inverse_modeling_with_stilt.ipynb
```

James Mineau, Lin group, University of Utah. james.mineau@utah.edu
