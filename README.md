# The ESKAPE model: open-source antibiotic discovery for everyone

### Overview

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

### Repository Contents
- Processed training datasets
- Prediction datasets
- Predictions on 12 million "in-stock" molecules from the ZINC15 chemical database
- "db" folder containing trained models and canonicalized training data for local predictions using the ESKAPE model

### Try the ESKAPE model yourself!
The ESKAPE model website can be found [here](https://eskape.mcmaster.ca/). The website has a maximum input of 100 molecules. To run the ESKAPE model locally (with no input limit), download the "db" folder and follow the instructions at https://github.com/raphenya/eskape-model-standalone.
