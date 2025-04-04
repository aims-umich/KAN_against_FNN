# Kolmogorov Arnold Networks (KAN) Performance and Accuracy Comparison With FNN
The dataset and codes which have been used while analyzing the performance of KANs in nuclear engineering applications. 

## Paper

Erdem, O. F., Panczyk, N. R., Radaideh, M. I. (2025). Interpretable Machine Learning Regression for Nuclear Applications with Kolmogorov-Arnold Networks (KAN). In Mathematics & Computation (M&C) 2025, Denver, CO. https://www.ans.org/meetings/mc2025/session/view-3016/#paper_9161

## 🛠️ Environment Installation

To set up the environment for this project, follow these steps:

```bash
# 1. Create a new conda environment with Python 3.9
conda create -n KAN_env python=3.9

# 2. Activate the environment
conda activate KAN_env

# 3. Install the requirements
pip install -r requirements.txt

# 4. Install Jupyter and Papermill for notebook execution
pip install jupyter papermill
```

## How to generate the results

The files have been separated to 3 parts. CHF KAN (1), HTGR KAN (2) and SHAP and Diagonal Validations (3). The contents of these parts are outlined below. For each folder, running the accompanying Jupyter Notebook files would create the KAN and FNN models, and export their outputs for diagonal validation plots. The folders contents are explained below:

- Step 1: Run the model trainer and prediction generator codes in the directory "KAN_against_FNN/CHF_KAN". 

```bash
nohup papermill KAN_CHF_6-6-1_KAN.ipynb KAN_CHF_6-6-1_KAN_out.ipynb &
```

- Step 2: Run the diagonal validation plotter in the directory "KAN_against_FNN/CHF_KAN/Results". 

```bash
nohup papermill create_diagonal_validation_plot.ipynb create_diagonal_validation_plot_out.ipynb &
```

- Step 3: Run the model trainer and prediction generator codes in the directory "KAN_against_FNN/HTGR_KAN". 

```bash
nohup papermill KAN_HTGR_8-4.ipynb KAN_HTGR_8-4_out.ipynb &
```

- Step 4: Run the diagonal validation plotter in the directory "KAN_against_FNN/HTGR_KAN/Results". 

```bash
nohup papermill create_diagonal_validation_plot.ipynb create_diagonal_validation_plot_out.ipynb &
```

- Step 5: Run the explainable AI tools in the directory "KAN_against_FNN/SHAP_and_Diagonal_Validations". 

```bash
nohup papermill chf_all.ipynb chf_all_out.ipynb &
nohup papermill htgr_all.ipynb htgr_all_out.ipynb &
nohup papermill shap_kan_chf.ipynb shap_kan_chf_out.ipynb &
nohup papermill shap_kan_htgr.ipynb shap_kan_htgr_out.ipynb &
```

In each problem, KAN models and FNN models have been tuned for the problems. The best models have been compared for their training times and accuracies.

## Dataset Information

1) Critical Heat Flux (CHF) synthetic data. This dataset is based on that produced by the NEA in [CDZ24]. The NEA dataset was generated from vertical water-cooled uniformly heated tubes, producing 24576 samples from 59 different sources of measurement. The dataset was collected over experimental measurements spanning 60 years of CHF data collection methods such as visual identification, physical burnout, changes in the test section resistances, and the usage of thermocouples. The input parameters collected include: test section diameter, heated length, pressure, mass flux, fluid input temperature, outlet equilibrium quality are the input parameters of the problem. CHF is the single output parameter which is being predicted with KAN and FNN models. The dataset has been imported from PyMaise. As the original dataset is confidential, a synthetic version designed to mimic the behavior of the real data is used in this research. It consists of 2500 samples, 2000 training samples and 500 testing samples. These were generated by adding random noise to the experimental data. More information can be found at: https://pymaise.readthedocs.io/en/latest/stubs/pyMAISE.datasets.load_chf.html

2) HTGR Micro Reactor data. This data consists of 751 samples of 8 inputs and 4 outputs. Each input parameter corresponds to a control drum angle in a different octant in the HTGR. The output parameters correspond to neutron fluxes in quadrants of the HTGR. This data set is based on the HOLOS-Quad reactor design. This reactor implements modular construction where separate units can be transported independently and assembled at the plant. The HOLOS-Quad core is a 8 cylindrical control drums control a 22 MWt high-temperature gas-cooled microreactor (HTGR). More information can be found at: https://pymaise.readthedocs.io/en/latest/stubs/pyMAISE.datasets.load_HTGR.html
