# Structure-Activity Insights via Molecular Embeddings and Clustering of FDA-Approved and Natural Compounds
# Description

This study presents a hybrid computational framework that independently evaluates transformer-based ChemBERTa embeddings and classical molecular fingerprints to improve the unsupervised clustering and supervised classification of bioactive compounds.

# Findings

A curated set of 2016 FDA approved drugs was encoded using 768-dimensional ChemBERTa embedding, while four conventional fingerprints (Morgan, AtomPair, Topological Torsion, and RDKit) are computed and concatenated to construct a high-dimensional feature matrix. Both embedding-based and fingerprint-based descriptors are employed across five unsupervised clustering algorithms: K-Means, Gaussian Mixture Models, Spectral Clustering, Agglomerative Clustering, and HDBSCAN. Ensemble consensus clustering, coupled with hyperparameter optimization, was used to generate robust and reproducible cluster assignments. Notably, ChemBERTa embedding yielded 10 well-defined clusters with silhouette score of 0.6956. 

# Implementation

Step-by-step instructions to run the pipeline of the project and obtain the results as described in the paper

# Generation of Chemberta embeddings

A dataset of 2016 FDA approved drugs ('Dataset_2016.csv') has been subjected to generate 768-bit Chemberta embeddings as 
molecular features (ChemBERTa_Ensemble_Clustering.ipynb)

# Generation of Fingerprints

The dataset of 2016 FDA approved drugs ('Dataset_2016.csv') has been subjected to generate five different types of fingerprints (Morgan, AtomPair, Topological Torsion, and RDKit) and generate a consensus datase of nearly 6500-bits after preprocessing as molecular features (Fingerprint_Ensemble_Clustering.ipynb)

# Clustering using Chemberta embeddings

Using the Chemberta 768-bit embeddings dataset, five clustering algorithms (K-Means, HDBSCAN, Spectral Clustering, Agglomerative Clustering, and GMM) are individually modelled and then integrated into a consensus representation through a co-association matrix, that captures the frequency with which sample pairs are clustered together across different methods. (The final model is saved into a .h5 file for testing)

# Clustering using Fingerprints

Using the 6500-bit fingerprints dataset, five clustering algorithms (K-Means, HDBSCAN, Spectral Clustering, Agglomerative Clustering, and GMM) are individually modelled and then integrated into a consensus representation through a co-association matrix, that captures the frequency with which sample pairs are clustered together across different methods. (The final model is saved into a .h5 file for testing)

Note: Based on the performance of clustering, the fingerprints based model was not considered for further analysis.

# Drug-target association prediction

To evaluate the predictive capacity of trained molecular representations, multi-layer perceptron (MLP) was used to design cluster-wise classification models to predict molecular targets for each compound, capturing their biological activity profiles. 10 MLP models for each cluster was developed to predict the drug-target association. All the 10 models are 'MLP_Classifiers' folder with the training set generated from cluster wise Chemberta embeddings from the drugs. 

# Performance evaluation

For evalating the performance of the clustering models, following parameters have been used -  silhouette score, Davies–Bouldin index, Calinski–Harabasz score, and Dunn index. For classification models sing MLP, evaluation is based on confidence scores, which represents the probability of prediction. 

# Optimization

For hyperparameter optimization, Optuna framework has been used within the scope of each models. The final models have been developed using the best parameters revealed after 20 trials using Optuna.

# Screening of natural products

A set of 4076 natural product have been screened using Chemberta embeddings first with the ensemble clustering model and then target association was made using the MLP models developed using the FDA dataset. However, reader may reproduce using their own convenient paths.

 
