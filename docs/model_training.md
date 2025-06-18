# Data processing and model training
Instructions for processing screening data and training and models from (paper)

## Data pre-processing
### Sanitization
Each training dataset was sanitized, meaning SMILES that could not be parsed by RDKit were removed. The sanitization script does this by converting each SMILES into a graph using RDKit, then converting them back. Any graphs that could not be converted into a SMILES was removed.

### Binarization
All training datasets were binarized based on growth inhibition using a cut-off of the mean of the data minus one standard deviation. Compounds above this cut-off were labeled 0 (inactive) and those below were labeled 1 (active).

### Deduplication
The training set has some repeated molecules, as well as some different salts of the same active compound, which would appear the same to RDKit (after salts are removed). Duplicated compounds with the same activity score (0 or 1) are all removed except for one. Duplicated compounds with different activity scores are all removed to avoid confusing the model.

## Model training
Three model types were trained on each pathogen dataset.
- Chemprop
- Chemprop-RDKit
- random forest

All models were trained on random splits using a 10-fold cross-validation scheme. Here, each model is an ensemble of ten models trained on different subsets of the training data. All model types were trained via Chemprop V1.

### Chemprop
Chemprop models are directed-message passing neural networks (D-MPNNs).

### Chemprop-RDKit
Chemprop-RDKit models retain the same architecture as Chemprop models, except 200 computable RDKit features are concatenated onto the output of the GNN before being fed into the FFNN.

### Random forest
Random forest models are ensemble of decision trees.

## Model evaluation
Each model was evaluated using area under the receiver-operating characteristic curve (AUROC) and area under the precision recall curve (AUPRC). These metrics are computed throughout training, however, the following steps were taken to manually plot ROC and PRC.
