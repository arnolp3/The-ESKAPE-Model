# The ESKAPE model: open-source antibiotic discovery for everyone

The ESKAPE Model is a machine learning-based resource to facilitate discovery of novel antibiotics against the ESKAPE pathogens, a group of multidrug-resistant bacteria that are responsible for the majority of hospital-acquired infections. These pathogens have been identified by the World Health Organization as priority pathogens for the research and development of new treatments.

The ESKAPE Model predicts the antibacterial activity of inputted molecules against each of the following ESKAPE pathogens:

- EF - Enterococcus faecium
- SA - Staphylococcus aureus
- KP - Klebsiella pneumoniae
- AB - Acinetobacter baumannii
- PA - Pseudomonas aeruginosa
- BW - Escherichia coli (wildtype)
- DKO - Escherichia coli (hyperpermeable and efflux deficient)

Models were trained on in-house growth inhibition screening datasets against common laboratory strains of each pathogen. A total of 21 models were trained - three model architectures for each pathogen:

- Random forest using Morgan fingerprints
- Chemprop graph neural network
- Chemprop with RDKit features

**Input file:**

Prepare a CSV file containing SMILES (one per row) with the column heading "smiles", similar to example below.

smiles
C[C@H]1CN(C[C@@H](C)N1)c1c(F)c(N)c2c(c1F)n(cc(C(O)=O)c2=O)C1CC1
CN1CCN(CC1)c1c(F)cc2c3c1SCCn3cc(C(O)=O)c2=O

**Output:**

Prediction scores from each of the 21 models are computed for each molecule. A prediction score is a value between 0 and 1 that denotes how confident the model is that a molecule is antibacterial. Predicted antibacterial molecules will have prediction scores closer to 1, while predicted non-antibacterial molecules will have prediction scores closer to 0.

For any input compounds that were tested against the ESKAPE pathogens during training data acquisition, this tool will additionally output the experimental optical density (OD) values in the "validated" row. OD is a measure of bacterial cell growth, where a high OD means the bacteria grew in the presence of the compound, and a low OD means the compound was able to inhibit the growth of the bacteria. For reference, an OD less than 0.06 denotes full growth inhibition. All OD values were normalized by plate based on the interquartile mean.

Several metrics are also calculated for each compound:


**Sum of PS:** Sum of prediction scores from all pathogen models for one compound. This metric can be used to prioritize broad-spectrum antibacterial compounds.

**PPF:** The ratio of the highest prediction score for a compound (PS1) to the second highest (PS2). This metric can be used to prioritize pathogen-prioritized antibacterial compounds.

**Molecular weight:** Size of the molecule in g/mol

**clogP:** Calculated octanol-water partition coefficient, where high clogP values mean the compound is more lipophilic. clogP is an important metric for solubility and bioavailability.

**TNN:** The TNN similarity measures the structural similarity (value between 0-1) of an input molecule to the most similar molecule (nearest neighbour) from the training set. TNN similarity closer to 1 indicates the molecules are more similar (TNN similarity = 1 means the molecules are equal). Predictions on compounds that are more similar to the training set are likely to be more accurate. Nearest neighbor SMILES from the training set are included in the TSV.

View your results on the reports page or download them as a TSV file.

**Interpretation:**

While all models were trained on the same datasets using the same training scheme, the three model types differ in terms of architecture and molecular representation. Prediction scores for the same molecule and pathogen will therefore vary based on the model type. Note that prediction scores do not correlate directly with likelihood of activity or potency, but rather represent model confidence.

The ESKAPE model website can be found [here](https://eskape.mcmaster.ca/). The website has a maximum input of 100 molecules. Instructions to run the ESKAPE model locally (with no input limit) can be found in this repository.

## Installation
Use of the ESKAPE model requires installation of Chemprop V1. Instructions for installing Chemprop V1 can be found [here](https://github.com/chemprop/chemprop-v1-old-branches?tab=readme-ov-file#installation).

## Repository Contents
- Running the ESKAPE Model locally
