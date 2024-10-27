# graphmind
Static Traffic Prediction for BT using Graph Machine Learning

### Graphmind: Graph Machine Learning for Static Traffic Prediction on Optical Networks
Graphmind predicts private static traffic (106-node UK network), outperforms existing models (4 times), learns from 30% of a single traffic matrix, provides feature explainability, and addresses sparsity and asymmetry for the first time. 

### Dataset - Multivariate data and BT Topology 
- BT's Private Core Network (UK): 106 nodes, 180 edges.
- Static Traffic Matrix (2020, pre-pandemic): 650 node pairs representing asymmetric demand between node pairs.
  - Internet Peering Points and Data Centers:
  - IXPs: 4 IXPs in 8 cities.
  - Data Centers: 345 centers across 71 locations.
  - Both IXPs and data centers are spatially aggregated to BT’s 106-node network.
- Population Data: Aggregated from the Office for National Statistics (UK, 2023) 
  — ~60 million across 188 locations, aggregated to BT’s 106 nodes.
- Demand Topology: Derived from the private traffic matrix. 106 nodes, 325 edges.
- Graph Metrics: Computed for both demand and physical topologies.
- Edge Embeddings:
  - Computed for each edge in the demand topology using node embeddings from the physical topology (Node2Vec).
  - Computed for each edge in the demand topology using node embeddings from the demand topology (Node2Vec).

### Suite of 3 Models that handle sparsity, asymmetry and outliers.
We build a suite of models to predict pairwise demand for BT. 
- _Graphmind-lr_: Predicts total normalized demand between node pairs using linear regression.
- _Graphmind-mlr_: Models asymmetric traffic patterns with multi-output linear regression for inflow and outflow separately.
- _Graphmind-cl_: Classifies high-demand links using logistic regression.
![image](https://github.com/user-attachments/assets/33fc1309-8c8c-43e2-a486-b364c5c2ffab)

### Results: Graphmind outperforms existing static traffic matrix generators
Our model captures the variability of demand using only 30% of the data. 
![image](https://github.com/user-attachments/assets/9d07503e-3775-4404-98f1-bffc3de49a92)

| Models         | Dataset                  | Test MSE | Test RMSE | Test MAE |
|----------------|--------------------------|----------|-----------|----------|
| Gravity (2000) [1]    | Generated for 100% dataset | 0.09250  | 0.30413   | 0.25372  |
| DC-IXP (2020) [2]     | Generated for 100% dataset | 0.09417  | 0.30688   | 0.25489  |
| **Graphmind-lr**      | Predicted on 70% dataset   | **0.02204**  | **0.14844** | **0.11355** |

**Graphmind outperforms existing static traffic matrix generator models by up to 4 times.**

### Please Note: 
- _Data about BT's infrastructure is unavailable due to privacy concerns._
- _Randomness can generate different results at each run; irrespective of the minor changes, the performance gains for our model compared to heuristics remain 4x._

### Requirements 
- Python 3.10.12
- pandas - 2.2.2
- networkx - 3.4.2
- numpy - 1.26.4
- matplotlib - 3.7.1
- seaborn - 0.13.2
- scipy - 1.13.1
- sklearn (scikit-learn) - 1.5.2
- node2vec - 0.5.0

### References
- [1] A. Dwivedi and R. E. Wagner, “Traffic Model for USA Long-distance Optical Network,” in Optical Fiber Communication Conference
(OFC), 2000.
- [2] S. K. Patri, A. Autenrieth, J.-P. Elbers, and C. M. Machuca, “Planning Optical Networks for Unexpected Traffic Growth,” in European
Conference on Optical Communication (ECOC), 2020.
- [3] A. Grover and J. Leskovec, “node2vec: Scalable Feature Learning for Networks,” in Knowledge Discovery and Data Mining(KDD), 2016.
- [4]  A. Ahuja, S. N. Herzberg, A. Rafel, P. Wright, A. Lord, and S. J. Savory, “Topology-Driven Edge Predictions with Graph Machine
Learning for Optical Network Growth,” in Optical Fiber Communication Conference (OFC), 2024.
- [5]  “Data Center Map,” accessed Oct. 2024. [Online]. Available: https://www.datacentermap.com/
- [6] Office for National Statistics (ONS), “Population estimates for the UK, England, Wales, Scotland, and Northern Ireland: mid-2022,”
Statistical Bulletin, released 26 March 2024. [Online]. Available: https://www.ons.gov.uk
