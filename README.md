[![Abcdspec-compliant](https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg)](https://github.com/soichih/abcd-spec)
[![Run on Brainlife.io](https://img.shields.io/badge/Brainlife-bl.app.48-blue.svg)](https://doi.org/10.25663/bl.app.48)

# app-dt6tonifti

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

**Converts a dtiInit dt6.mat tensor fit into NIfTI maps of FA, MD, AD, RD and the Westin shape indices (cl, cp, cs) with vistasoft.**

Loads dti/dt6.mat from a dtiInit output, recomputes the eigen-decomposition and writes FA, MD, AD, RD, cl, cp and cs as NIfTI images in the tensor datatype. Use it when a dtiInit output must be used by Apps that take a tensor datatype. Format conversion utility; no model is refitted from the DWI.

Run it on brainlife.io: [https://doi.org/10.25663/bl.app.48](https://doi.org/10.25663/bl.app.48)

| Input | Datatype | Required | Description |
|---|---|---|---|
| `0` | `neuro/dtiinit` | yes | dtiInit output directory containing dti/dt6.mat. |

| Output | Datatype | Description |
|---|---|---|
| `0` | `neuro/tensor` | Tensor datatype with FA, MD, AD, RD, cl, cp and cs NIfTI maps. |
| `1` | `raw` |  |

Runtime: container `brainlife/mcr:neurodebian1604-r2017a`.

<!-- brainlife-app:end -->

This app will take a dt6 and create tensor (FA,MD,AD,RD) and Westin Shape Indices (cl, cp, cs) nifti images from a dt6.mat structure. First, a dt6.mat structure will be loaded and eigenvectors and eigenvalues will be extracted using Vistasoft's dtiEig function. The negative eigenvalues are then clipped to 0. Finally, tensors and Westin Shape indices nifti images are computed by using Vistasoft's dtiComputeFA and dtiComputeWestinShapes functions. This is all performed by running the main script.

### Authors
- Brad Caron (bacaron@iu.edu)

### Contributors
- Soichi Hayashi (hayashi@iu.edu)
- Franco Pestilli (franpest@indiana.edu)

### Funding
[![NSF-BCS-1734853](https://img.shields.io/badge/NSF_BCS-1734853-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1734853)
[![NSF-BCS-1636893](https://img.shields.io/badge/NSF_BCS-1636893-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1636893)

## Running the App 

### On Brainlife.io

You can submit this App online at [https://doi.org/10.25663/bl.app.48](https://doi.org/10.25663/bl.app.48) via the "Execute" tab.

### Running Locally (on your machine)

1. git clone this repo.
2. Inside the cloned directory, create `config.json` with something like the following content with paths to your input files.

```json
{
        "dt6": "./input/dtiinit/"
}
```

### Sample Datasets

You can download sample datasets from Brainlife using [Brainlife CLI](https://github.com/brain-life/cli).

```
npm install -g brainlife
bl login
mkdir input
bl dataset download 5a0dcb1216e499548135dd27 && mv 5a0dcb1216e499548135dd27 input/dtiinit
```


3. Launch the App by executing `main`

```bash
./main
```

## Output

The main outputs of this App are nifti images of the tensors and Westin Shape indices. These can then be used in app-tractanalysisprofiles.

#### Product.json
The secondary output of this app is `product.json`. This file allows web interfaces, DB and API calls on the results of the processing. 

### Dependencies

This App requires the following libraries when run locally.

  - singularity: https://singularity.lbl.gov/
  - VISTASOFT: https://github.com/vistalab/vistasoft/
  - SPM 8: https://www.fil.ion.ucl.ac.uk/spm/software/spm8/
  - jsonlab: https://github.com/fangq/jsonlab.git
