<h1 align="center">dt6 to NIfTI converter</h1>

<p align="center">
  NIfTI maps of FA, MD, AD, RD and the Westin shape indices from the tensor fit stored in a dtiInit <code>dt6.mat</code>.
</p>

<p align="center">
  <a href="https://github.com/brainlife/abcd-spec"><img src="https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg" alt="ABCD Spec v1.1"></a>
  <a href="https://doi.org/10.25663/bl.app.48"><img src="https://img.shields.io/badge/Brainlife-bl.app.48-blue.svg" alt="Run on brainlife.io"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-lightgrey.svg" alt="MIT license"></a>
</p>

> 📍 **This branch, `1.0`, is the brainlife.io App dt6 To Nifti Converter** ([doi:10.25663/bl.app.48](https://doi.org/10.25663/bl.app.48)).

## 🧠 At a glance

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Converts a dtiInit dt6.mat tensor fit into NIfTI maps of FA, MD, AD, RD and the Westin shape indices (cl, cp, cs) with vistasoft.**

Loads dti/dt6.mat from a dtiInit output, recomputes the eigen-decomposition and writes FA, MD, AD, RD, cl, cp and cs as NIfTI images in the tensor datatype. Use it when a dtiInit output must be used by Apps that take a tensor datatype. Format conversion utility; no model is refitted from the DWI.

| | |
|---|---|
| 📥 **Inputs** | `neuro/dtiinit` |
| 📤 **Outputs** | `neuro/tensor` · `raw` |
| 🐳 **Container** | `brainlife/mcr:neurodebian1604-r2017a` |
| 🔗 **Run it** | [doi.org/10.25663/bl.app.48](https://doi.org/10.25663/bl.app.48) |

#### 📥 Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `0` | `neuro/dtiinit` | yes | dtiInit output directory containing dti/dt6.mat. |

#### 📤 Outputs

| Output | Datatype | Description |
|---|---|---|
| `0` | `neuro/tensor` | Tensor datatype with FA, MD, AD, RD, cl, cp and cs NIfTI maps. |
| `1` | `raw` |  |

<!-- brainlife-app:end -->

## 🚀 Running the App

The App runs from the [`1.0`](https://github.com/brainlife/app-dt6tonifti/tree/1.0) branch of this repository.

### ☁️ On brainlife.io

Open the App at [doi.org/10.25663/bl.app.48](https://doi.org/10.25663/bl.app.48), choose a `neuro/dtiinit` dataset from your project and press **Execute**. The App has no options. It loads `dti/dt6.mat`, recomputes the eigenvectors and eigenvalues with vistasoft's `dtiEig`, clips negative eigenvalues, and computes the tensor measures with `dtiComputeFA` and the Westin shape indices with `dtiComputeWestinShapes`. No model is refitted from the DWI. The maps are archived to your project as a `neuro/tensor` dataset, which can be used by Apps such as Tract Analysis Profiles.

### 💻 Locally

You need [Singularity/Apptainer](https://apptainer.org/). The App is a compiled MATLAB program (`compiled/main`, built from `main.m` with [vistasoft](https://github.com/vistalab/vistasoft) and [jsonlab](https://github.com/fangq/jsonlab)) and runs in the `brainlife/mcr:neurodebian1604-r2017a` container with the MATLAB Runtime R2017a.

1. Clone this repository and check out the App branch (`git checkout 1.0`).
2. Create `config.json` with the path to the dtiInit output directory:

   ```json
   {
       "dt6": "./input/dtiinit/"
   }
   ```

3. Run the App:

   ```bash
   ./main
   ```

### 🧪 Sample data

Download a dtiInit sample from brainlife.io with the [brainlife CLI](https://github.com/brainlife/cli):

```bash
npm install -g brainlife
bl login
mkdir input
bl dataset download 5a0dcb1216e499548135dd27 && mv 5a0dcb1216e499548135dd27 input/dtiinit
```

## 📦 Outputs

The App writes seven NIfTI images in the working directory, on the grid of the dtiInit tensors:

- `fa.nii.gz`, `md.nii.gz`, `ad.nii.gz`, `rd.nii.gz`: fractional anisotropy and mean, axial and radial diffusivity;
- `cl.nii.gz`, `cp.nii.gz`, `cs.nii.gz`: Westin linear, planar and spherical shape indices.

## 🩺 Troubleshooting

- **`output missing`**: `fa.nii.gz` was not written. Check that the input directory contains `dti/dt6.mat`.

## 📚 Citing

> [!TIP]
> If you use this App in your work, please cite the App, the software it builds on and brainlife.io (below). GitHub's **Cite this repository** button gives the App citation in APA and BibTeX.

- dt6 To Nifti Converter. brainlife.io App. [doi:10.25663/bl.app.48](https://doi.org/10.25663/bl.app.48)
- Hayashi S, Caron BA, Heinsfeld AS, et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. *Nature Methods* 21:809–813 (2024). [doi:10.1038/s41592-024-02237-2](https://doi.org/10.1038/s41592-024-02237-2)
- Avesani P, McPherson B, Hayashi S, et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. *Scientific Data* 6:69 (2019). [doi:10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

## 👥 Authors

- Brad Caron

**Contributors:** Soichi Hayashi, Franco Pestilli (project director)

## 💰 Funding

[![Wellcome-226486/Z/22/Z](https://img.shields.io/badge/Wellcome-226486%2FZ%2F22%2FZ-purple.svg)](https://wellcome.org/)
[![NIH-NINDS-U24NS140384](https://img.shields.io/badge/NIH_NINDS-U24NS140384-green.svg)](https://reporter.nih.gov/project-details/11261037)
[![NIH-NINDS-UM1NS132207](https://img.shields.io/badge/NIH_NINDS-UM1NS132207-green.svg)](https://reporter.nih.gov/project-details/11411328)
[![NIH-NIBIB-R01EB029272](https://img.shields.io/badge/NIH_NIBIB-R01EB029272-green.svg)](https://reporter.nih.gov/project-details/10262925)
[![NIH-NIBIB-R01EB030896](https://img.shields.io/badge/NIH_NIBIB-R01EB030896-green.svg)](https://reporter.nih.gov/project-details/10428625)
[![NIH-NIMH-R01MH126699](https://img.shields.io/badge/NIH_NIMH-R01MH126699-green.svg)](https://reporter.nih.gov/project-details/10460628)
[![NIH-NIDCD-R01DC020088](https://img.shields.io/badge/NIH_NIDCD-R01DC020088-green.svg)](https://reporter.nih.gov/project-details/11140284)
[![NSF-BCS-1734853](https://img.shields.io/badge/NSF_BCS-1734853-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1734853)
[![NSF-BCS-2203524](https://img.shields.io/badge/NSF_BCS-2203524-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2203524)
[![NSF-IIS-1636893](https://img.shields.io/badge/NSF_IIS-1636893-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1636893)
[![NSF-OAC-2148729](https://img.shields.io/badge/NSF_OAC-2148729-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2148729)
[![NSF-IIS-1912270](https://img.shields.io/badge/NSF_IIS-1912270-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1912270)
[![NSF-IIS-2148700](https://img.shields.io/badge/NSF_IIS-2148700-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2148700)
[![NSF-OAC-1916518](https://img.shields.io/badge/NSF_OAC-1916518-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1916518)

<sub>brainlife.io is publicly funded, and acknowledging that support helps keep it running. This App was developed with support from Wellcome, the U.S. National Institutes of Health (including the BRAIN Initiative BRAIN CONNECTS program: The Axonal Projectome EXchange, U24NS140384, and the Center for Mesoscale Connectomics, UM1NS132207) and the U.S. National Science Foundation.</sub>

## ⚖️ License

[MIT](LICENSE).
