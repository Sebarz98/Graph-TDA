# Graph-TDA
Graph Analysis and Topological Data Analysis of Parkinson's patients and Healthy Controls with PSQI &lt; 5 or > 5. HC were divided into good and bad sleepers according to the Pittsburgh Sleep Quality Index (PSQI).
The cutoff used was PSQI > 5 for bad sleep quality (https://www.med.upenn.edu/cbti/assets/user-content/documents/Pittsburgh%20Sleep%20Quality%20Index%20(PSQI).pdf).

## fMRI Preprocessing 

All the fmri preprocessing was done on brainlife.io (https://brainlife.io/about/) following their tutorial (https://brainlife.io/docs/tutorial/networkneuroscience-functional/) for the creation of the networks. The images were preprocessed as following: aligning T1 with FSL, generating freesurfer parc, mapping the hcp--1mm atlas, running fmriprep, and converting their outputs to connectivity matrices with https://github.com/faskowit/app-fmri-2-mat, whom uses 36p for nuisance regression. The resulting correlation matrices were downloaded as csv files.

## Analysis
The matrices were then import into Google Colab, where the last 14 rows and columns, corresponding to the subcortical structures resulting from the freesurfer parcellation, were dropped. 
After this step, the matrices were used as input for graph and topological data analysis, accordig to https://github.com/multinetlab-amsterdam/network_TDA_tutorial. 
### Graph Theory

Basic graph measures were calculated for HC and PD.

The measures calculated were: 
Density - 
Degree/Strength - the word degree is commonly used for binary graphs, whereas strength tends to be used for weighted networks - 
Centrality: Eigenvector, Betweenness, Closeness, Degree, Page Rank - 
Path length - 
Modularity - 
Assortativity - 
Clustering coefficient - 

All measures were found different across groups, both between HC and PD, and between PSQI < 5 and > 5. 
In particular, PD were found to have a lower density, degree and clustering coefficient, while showing higher centrality, and path length.
The statistical significance of node degree strenght and clustering coefficient were found to be statistically significant (p < 0.05).
Similarly, the PSQI > 5 group showed the same pattern of the PD group, but with on a lower degree. 
The statistical significance of node degree strenght and clustering coefficient were found to be statistically significant (p < 0.05).

<img width="607" alt="MOD_HC" src="https://github.com/Sebarz98/Graph-TDA/assets/70062910/930d294a-8540-4dd1-bd24-533be6231f69">
Modulariyt of HC
<img width="602" alt="Screenshot 2023-06-02 at 16 48 58" src="https://github.com/Sebarz98/Graph-TDA/assets/70062910/27869505-dc74-4742-b1c5-41e5c2f7d713">
Modularity of PD

### TDA
Basic topological measures were computed for each group. 
Persistent homology examines the evolution of topological features, such as connected components, loops, voids, or higher-dimensional structures, across different scales or thresholds. It allows for the detection and quantification of topological characteristics that persist across multiple scales, revealing the intrinsic structure of the data.

<img width="600" alt="Screenshot 2023-06-02 at 17 46 28" src="https://github.com/Sebarz98/Graph-TDA/assets/70062910/072fdb57-6c3e-420d-ae5e-d2f5d9433f0d">
Persistence Diagram HC
<img width="613" alt="Screenshot 2023-06-02 at 17 46 47" src="https://github.com/Sebarz98/Graph-TDA/assets/70062910/122c29bf-7fb4-4bc9-9973-add55ef640b2">
<img width="548" alt="Screenshot 2023-06-02 at 17 46 57" src="https://github.com/Sebarz98/Graph-TDA/assets/70062910/61eec6d0-e1e3-4b21-a70e-2341a14da350">
Persistence Diagram PD

![Uploading Screenshot 2023-06-02 at 17.46.57.png…]()
Persistence Density HC
<img width="568" alt="Screenshot 2023-06-02 at 17 47 06" src="https://github.com/Sebarz98/Graph-TDA/assets/70062910/93d59944-5e3a-4126-a7af-6178aeb803cf">
Persistence Density PD

Betti numbers are persistent homology algorithms that analyze the topology of the simplicial complexes across the filtration process. Betti numbers are computed by counting the number of topological features that persist at different scales. Specifically, Betti numbers count the number of connected components (Betti-0), loops (Betti-1), voids (Betti-2) and so on.

The PD group had a lower Betti-1 than the others. 
<img width="676" alt="Screenshot 2023-06-02 at 16 49 23" src="https://github.com/Sebarz98/Graph-TDA/assets/70062910/b3b32ca4-2652-411a-bb9d-caa7ba47938a">
PD k-cliques 3(triangles, where k-clique is a subset of k vertices in an undirected graph in which all vertices are connected to each other)
<img width="578" alt="3K_HC" src="https://github.com/Sebarz98/Graph-TDA/assets/70062910/5d7ff026-0ba7-4178-aa3d-e35af7a6439d">
HC k-cliques 3

<img width="714" alt="Screenshot 2023-06-02 at 16 55 09" src="https://github.com/Sebarz98/Graph-TDA/assets/70062910/1856e28d-4fa4-42a7-825d-a4f95f331c57">
PD Nodal Curvature
<img width="610" alt="CURV_HC" src="https://github.com/Sebarz98/Graph-TDA/assets/70062910/f9125c85-04d0-4f93-9027-b1a562f70628">
HC Nodal Curvature
