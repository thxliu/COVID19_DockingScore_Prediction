# COVID19_DockingScore_Prediction
# PROBLEM OVERVIEW
The traditional drug discovery process is expensive and time-consuming, so accelerating it is crucial in responding to emerging threats like SARS-CoV-2. This project aims to predict docking scores of candidate molecules against SARS-CoV-2 protein targets using machine learning, enabling high-throughput virtual screening and prioritization of the most promising compounds for experimental testing. 

# SOLUTION OVERVIEW
This solution takes advantage of machine learning (ML) based surrogate models to predict docking scores for 18 protein pockets. Key steps in the process include data preprocessing, modeling, evaluation, and prediction and ranking.

*Data Preprocessing*
Input molecules are represented as SMILES strings which are then converted in Morgan fingerprints (using RDKit’s MorganGenerator) to numerically encode the molecular structure. Morgan fingerprints are a type of circular fingerprint that represents the presence of substructures in a model. Each molecule is converted into a fixed-length bit vector (in this case 1024 bits but can be 2048 bits) where each bit represents if a particular substructure is present (1) or absent (0) in the molecule. Converting the SMILES strings into Morgan fingerprints is critical for models like Random Forests (used in this solution) that take numerical arrays to learn patterns in the molecular substructures that relate to docking scores. Morgan fingerprints are widely used in bioinformatics and cheminformatics due to their computing efficiency and effectiveness for predicting molecular properties.

*Modeling*
A Random Forest Regressor wrapped in a MultiOutputRegressor is used for docking score prediction across all 18 protein pockets simultaneously. The models are trained on a subset of experimental docking scores.

*Evaluation*
The model’s performance is assessed using mean absolute error (MAE) on a validation set. In general, the lower the MAE, the more accurate the predictions.

*Prediction and Ranking*
For each molecule, the model generates predicted docking scores per pocket. Molecules are then ranked by both pocket-specific scores and by the average across all pockets. In the predictions and rankings, the SMILES column represents the chemical structure of the molecule and the other columns represent the different pockets and their respective predicted docking scores. In general, lower docking scores indicate stronger binding affinity and thus, more effective interactions. Comparisons can be drawn between the molecules’ predicted scores across pockets to see which specific molecules are estimated as stronger candidates for experimental validation.

# MODELS USED
Two models are leveraged for this model.
RandomForestRegressor via scikit-learn
MultiOutputRegressor to handle multiple docking score targets simultaneously 
Input features: 1024-bit Morgan fingerprints converted from SMILES strings

# MIMINAL REPRODUCIBLE EXAMPLE/TUTORIAL

# DATA
Data used from Kaggle’s COVID-19 Bioinformatics Drug Target Challenge that can be found at https://www.kaggle.com/competitions/covid-19-bioinformatics-drug-target-challenge/overview. 

