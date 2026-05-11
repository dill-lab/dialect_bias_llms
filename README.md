# Dialect Bias LLMs

This repository contains the code and data for our paper:



Kritee Kondapally, Claire J. Smerdon, Pooja C. Patel, Ogheneyoma Akoni, Jevon Torres, Jaspreet Ranjit, Matthew Finlayson, Swabha Swayamdipta

## About

We introduce a framework for evaluating dialect bias in language models across different prompting settings. Specifically, we study how language models associate stereotypical traits with intent-equivalent tweets written in Standard American English (SAE) and African American Vernacular English (AAVE). While prior work has shown that models assign more negative stereotypes to AAVE tweets when they are evaluated in isolation, we find that this bias is often amplified when SAE/AAVE tweet pairs are evaluated side by side. We evaluate both covert dialect bias, where dialect labels are not provided, and overt dialect bias, where dialect labels are explicitly specified. We also examine counterfactual fairness finetuning as a mitigation strategy and find that, although it can reduce average disparities for some traits in the absolute setting, these improvements do not consistently hold in the contrastive setting. Our results suggest that existing evaluation settings may underestimate the severity of dialect bias in language models, especially in comparative setting where models are used to rank or compare people.

## Getting Started
Plots for the covert/overt analysis pulled out of the original notebook. Each script reads the data in `data_files/` (and related subfolders), writes a PDF to `plots/`, and can be run directly with `uv`.

## Data

Please refer to the [TwitterAAE dataset](https://slanglab.cs.umass.edu/TwitterAAE/) for the data used in this work.

- Original AAVE tweets: TwitterAAE dataset
- SAE rewrites: intent-equivalent SAE translations associated with the dataset
- Evaluation pairs: AAVE/SAE tweet pairs used for absolute and contrastive dialect bias evaluation

Note: Please follow the original dataset’s terms of use and citation requirements when using this data.

## Setup
- Install [uv](https://docs.astral.sh/uv/).
- From the repo root, install dependencies and create the virtual environment:
  - `uv sync`
- Run any script through uv so it picks up the managed environment:
  - `uv run python <script.py>`

## Plotting scripts
- `cf_gap_heatmaps_covert.py`: Heatmaps of covert absolute vs. relative CTF gaps with confidence-interval annotations (`plots/CF_Gap_Heatmaps_covert.pdf`).
- `cf_gap_heatmaps_overt.py`: Overt version of the CTF gap heatmaps (`plots/CF_Gap_Heatmaps_overt.pdf`).
- `compare_main_plots.py`: Side-by-side covert/overt CTF gap panels and Cohen’s d comparisons (absolute + relative) written to `plots/compare_cf_gaps_covert_overt.pdf`, `plots/compare_cohens_d_absolute.pdf`, and `plots/compare_cohens_d_relative.pdf`.
- `cohens_d_all.py`: Four-panel Cohen’s d grid (covert/overt × absolute/relative) saved as `plots/COHENS_D_all.pdf`.
- `cohens_d_covert_absolute.py`, `cohens_d_covert_relative.py`, `cohens_d_overt_absolute.py`, `cohens_d_overt_relative.py`: Per-setting bar charts of positive/negative valence traits for each model (outputs prefixed with `plots/COHENS_D_...pdf`).
- `cohens_d_finetuned.py`: Finetuning deltas for LLaMA Cohen’s d scores (`plots/cohens_d_finetuned.pdf`).
- `q_values_covert.py`: Q-value heatmap for covert prompting (`plots/Q_values_covert.pdf`).
- `pearson_correlations_covert_abs.py`: Pearson r heatmap for positive/negative trait correlations across models (`plots/pearson_correlations_covert_abs.pdf`).
- `score_winner_difference_covert_direct_deepseek.py`: Winner grid and score count differences for DeepSeek covert direct prompting (`plots/score_winner_difference_covert_direct_deepseek.pdf`).
- `self_consistency_aave.py`, `self_consistency_sae.py`: Self-consistency heatmaps for AAVE and SAE dialects (`plots/self_consistency_AAVE.pdf`, `plots/self_consistency_SAE.pdf`).
- `Graph_code.py`: Legacy notebook-style scratchpad; prefer the dedicated scripts above for reproducible plots.

### Notes
- Scripts expect the Excel and CSV inputs already present under `data_files/` and related folders. No downloads are performed at runtime.
- Matplotlib is configured to use LaTeX + Libertinus (`plot_utils.configure_matplotlib`). Ensure the fonts/LaTeX package are available in your environment if you see font warnings.

## Citation
@inproceedings{kondapally2026dialectbias,
  title={Side-by-side Comparison Amplifies Dialect Bias in Language Models},
  author={Kondapally, Kritee and Smerdon, Claire J. and Patel, Pooja C. and Akoni, Ogheneyoma and Torres, Jevon and Ranjit, Jaspreet and Finlayson, Matthew and Swayamdipta, Swabha},
  booktitle={Proceedings of the 2026 ACM Conference on Fairness, Accountability, and Transparency},
  series={FAccT '26},
  year={2026},
  publisher={Association for Computing Machinery},
  address={New York, NY, USA},
  doi={10.1145/3805689.3812217}
}
