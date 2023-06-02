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
Clustering coefficient.

All measures were found different across groups, both between HC and PD, and between PSQI < 5 and > 5. 
In particular, PD were found to have a lower density, degree and clustering coefficient, while showing higher centrality, and path length.
The statistical significance of node degree strenght and clustering coefficient were tested and were significant (p < 0.05).
Similarly, the PSQI > 5 group showed the same pattern of the PD group, but on a lower degree. 
The statistical significance of node degree strenght and clustering coefficient were tested and significant (p < 0.05).
Modularity optimization was calculated with the Louvain algorithm. It measures the strength of the division of nodes into separate communities compared to what would be expected by chance

<img width="607" alt="MOD_HC" src="https://github.com/Sebarz98/Graph-TDA/assets/70062910/356e87d0-1023-49b7-bf96-7d0c6d86f1ba">

#### Modularity of HC

<img width="602" alt="Screenshot 2023-06-02 at 16 48 58" src="https://github.com/Sebarz98/Graph-TDA/assets/70062910/744e201c-2a9c-4c79-8892-5025dda5a8d5">

#### Modularity of PD

### TDA
Basic topological measures were computed for each group. 
Persistent homology examines the evolution of topological features, such as connected components, loops, voids, or higher-dimensional structures, across different scales or thresholds. It allows for the detection and quantification of topological characteristics that persist across multiple scales, revealing the intrinsic structure of the data.

<img width="600" alt="Screenshot 2023-06-02 at 17 46 28" src="https://github.com/Sebarz98/Graph-TDA/assets/70062910/bcd147a3-cc32-4bbc-8ba9-07b2f2416bf7">

#### Persistence Diagram HC

<img width="613" alt="Screenshot 2023-06-02 at 17 46 47" src="https://github.com/Sebarz98/Graph-TDA/assets/70062910/2703ee5e-ce29-4544-bd96-9108f041ce14">

#### Persistence Diagram PD

<img width="548" alt="Screenshot 2023-06-02 at 17 46 57" src="https://github.com/Sebarz98/Graph-TDA/assets/70062910/a09d2391-bf46-435a-8b1e-a7420a65065a">

#### Persistence Density HC

<img width="568" alt="Screenshot 2023-06-02 at 17 47 06" src="https://github.com/Sebarz98/Graph-TDA/assets/70062910/e2049456-7877-44b9-aadd-2beb25fe03ec">

#### Persistence Density PD

Betti numbers are persistent homology algorithms that analyze the topology of the simplicial complexes across the filtration process. Betti numbers are computed by counting the number of topological features that persist at different scales. Specifically, Betti numbers count the number of connected components (Betti-0), loops (Betti-1), voids (Betti-2) and so on.
The PD group had a lower Betti-1 than the others. 

<img width="676" alt="Screenshot 2023-06-02 at 16 49 23" src="https://github.com/Sebarz98/Graph-TDA/assets/70062910/8b9b313f-3e78-4f19-9e00-08945c6aaa5a">


#### PD k-cliques 3(triangles, where k-clique is a subset of k vertices in an undirected graph in which all vertices are connected to each other)
<img width="578" alt="3K_HC" src="https://github.com/Sebarz98/Graph-TDA/assets/70062910/bdd45d88-9ece-4d23-a5d1-f40c5276e370">


#### HC k-cliques 3

<img width="714" alt="Screenshot 2023-06-02 at 16 55 09" src="https://github.com/Sebarz98/Graph-TDA/assets/70062910/357ad8b5-8240-4802-aa84-ae6d24a53d5b">


#### PD Nodal Curvature

<img width="610" alt="CURV_HC" src="https://github.com/Sebarz98/Graph-TDA/assets/70062910/3fceee38-12d3-4f21-8913-b8b6aee7c22a">

#### HC Nodal Curvature
