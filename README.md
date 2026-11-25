# Power Spectral Density (PSD)

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Computes the power spectral density of raw MEG/EEG data with MNE-Python's Welch method, saving per-channel PSD tables for gradiometers, magnetometers and EEG and PSD plots.**

Reads an MNE raw file and runs mne.time_frequency.psd_welch separately for each channel type present (grad, mag, eeg) between fmin and fmax, with configurable time window, FFT length, overlap, window and averaging. PSDs are stored in dB as TSV tables (channels x frequencies) and plotted with MNE and with a manual plot. Use it to inspect spectral content or as input to peak-frequency Apps.

| | |
|---|---|
| 📥 **Inputs** | `neuro/meeg/mne/raw` |
| 📤 **Outputs** | `neuro/meeg/psd` ×3 · `raw` |
| 🐳 **Container** | `brainlife/mne:0.23dev` |
| ⚙️ **Resources** | 4 CPUs · 64 GB memory · 1 h walltime |
| 🔗 **Run it** | [doi.org/10.25663/brainlife.app.530](https://doi.org/10.25663/brainlife.app.530) |

#### 📥 Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `megfif` | `neuro/meeg/mne/raw` | yes | Raw MEG/EEG recording (MNE raw, FIF). |

#### 📤 Outputs

| Output | Datatype | Description |
|---|---|---|
| `out_grad` | `neuro/meeg/psd` | PSD table (TSV, channels x frequencies, dB) for gradiometer channels. |
| `out_mag` | `neuro/meeg/psd` | PSD table (TSV, channels x frequencies, dB) for magnetometer channels. |
| `out_eeg` | `neuro/meeg/psd` | PSD table (TSV, channels x frequencies, dB) for EEG channels. |
| `out_figs` | `raw` | PSD figures (PNG) produced with MNE and with a manual plot. |

<details>
<summary><b>⚙️ Parameters</b> (12)</summary>

| Parameter | Type | Default | Description |
|---|---|---|---|
| `fmin` | number | `0` | Min frequency of interest. |
| `fmax` | number | `100` | Max frequency of interest. |
| `tmin` | number |  | Min time of interest. |
| `tmax` | number |  | Max time of interest. |
| `n_fft` | number | `4096` | The length of FFT used, must be >= n_per_seg. The segments will be zero-padded if n_fft > n_per_seg. If n_per_seg is None, n_fft must be <= number of time points in the data. |
| `n_overlap` | number | `2000` | The number of points of overlap between segments. Will be adjusted to be <= n_per_seg. |
| `n_per_seg` | number |  | Length of each Welch segment (windowed with a Hamming window). Defaults to None, which sets n_per_seg equal to n_fft |
| `window` | string | `hamming` | Windowing function to use. See scipy.signal.get_window(). |
| `proj` | boolean | `false` | Apply SSP projection vectors. |
| `reject_by_annotation` | boolean | `true` | Whether to omit bad segments from the data before fitting. If True (default), annotated segments whose description begins with 'bad' are omitted. If False, no rejection based on annotations is performed. |
| `picks` | string | `None` | Channels to include. In lists, channel type strings (e.g., [meg, eeg]) will pick channels of those types, channel name strings (e.g., [MEG0111, MEG2623]) will pick the given channels. When you use a list, don't forget to use the square brackets. Can also be the string values “all” to pick all channels, or “data” to pick data channels. None will pick all data channels. Note that channels in info['bads'] will be included if their names are explicitly provided. |
| `average` | enum | `mean` | How to average the segments. - If 'mean (default), calculate the arithmetic mean. - If 'median', calculate the median, corrected for its bias relative to the mean. - If 'None', returns the unaggregated segments. Options: `mean`, `median`, `None`. |

</details>

📚 **References used by this App:**
- Avesani P et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. Sci Data 6:69 (2019). [doi:10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)
- Gramfort A et al. MEG and EEG data analysis with MNE-Python. Frontiers in Neuroscience 7:267 (2013). [doi:10.3389/fnins.2013.00267](https://doi.org/10.3389/fnins.2013.00267)

<!-- brainlife-app:end -->

[![Abcdspec-compliant](https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg)](https://github.com/brain-life/abcd-spec)
[![Run on Brainlife.io](https://img.shields.io/badge/Brainlife-bl.app.530-blue.svg)](https://doi.org/10.25663/brainlife.app.530)

Brainlife App to compute Power Spectral Density (PSD) on MEG files using MNE-Python Welch method `mne.time_frequency.psd_welch` function

## app-peak-frequency documentation

2) Input file is:
    * `meg/fif` meg data file
5) Ouput files are:
    * A series of files `.tsv` file containing the PSD, 
    for gradiometers (grad), magnetometers (mag) and electroencephalography (eeg)
    acording to the channels types contained in raw meg data
    * a plot of the PSD for all channels (grad, mag, eeg) using MNE-Python function
    * a plot of the PSD for all channels (grad, mag, eeg) manually implemented (for reproducibility purposes) 

## Authors
- Guiomar Niso (guiomar.niso@ctb.upm.es)

## Citations
We kindly ask that you cite the following articles when publishing papers and code using this code. 

*- brainlife.io Publishing and Apps:*

Avesani, P., McPherson, B., Hayashi, S. et al. **The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services**. Sci Data 6, 69 (2019). https://doi.org/10.1038/s41597-019-0073-y

*- MNE-Python package:* 

Gramfort A, Luessi M, Larson E, Engemann DA, Strohmeier D, Brodbeck C, Goj R, Jas M, Brooks T, Parkkonen L, and Hämäläinen MS.  **MEG and EEG data analysis with MNE-Python**. Frontiers in Neuroscience, 7(267):1–13, 2013. https://doi.org/10.3389/fnins.2013.00267

## Funding Acknowledgement
brainlife.io is publicly funded and for the sustainability of the project it is helpful to Acknowledge the use of the platform. We kindly ask that you acknowledge the funding below in your publications and code reusing this code.

[![NSF-BCS-1734853](https://img.shields.io/badge/NSF_BCS-1734853-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1734853)
[![NSF-BCS-1636893](https://img.shields.io/badge/NSF_BCS-1636893-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1636893)
[![NSF-ACI-1916518](https://img.shields.io/badge/NSF_ACI-1916518-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1916518)
[![NSF-IIS-1912270](https://img.shields.io/badge/NSF_IIS-1912270-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1912270)
[![NIH-NIBIB-R01EB030896](https://img.shields.io/badge/NIH_NIBIB-R01EB030896-green.svg)](https://grantome.com/grant/NIH/R01-EB030896-01)


#### MIT Copyright (c) 2021 brainlife.io The University of Texas at Austin and Indiana University
