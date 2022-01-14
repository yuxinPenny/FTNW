# Decoding the stochastic profile of m6A over the entire transcriptome
## Abstract 
N6-methladenosine (m6A), an abundant eukaryotic mRNA modification, is a crucial epigenetic marker dynamically regulated by demethylase (Erasers), methyltransferase (Writers), and binding proteins (Readers). Hence, decoding the stochastic profile of m6A over transcriptome is invaluable to our understanding of its biological functions. The m6A site over 1624625 DRACH motifs on human exons were summarized from 40 experiments. Four machine learning algorithms, generalized linear model (GLM), multi-layer perceptron (MLP), extreme gradient boosting (XGBoost), and random forest (RF), were implemented to build Poisson regression models. Compared with classification models used in previous studies, our model provides a new framework to integrate multiple single-base RNA modification datasets. We demonstrated that the Poisson regressors can better predict the biological and technical variation between experiments than classifiers trained with same features. In addition, we for the first time utilized the protein binding information for prediction and achieved significantly better performance than models based on only sequence-derived and genome-derived features.

## Material and Methods
### Feature encoding scheme:chemical property
Three chemical properties, namely ring structure, functional groups and number of hydrogen bond, were used to classify adenine, cytosine, guanine and uracil. Based on the three properties, A, C, G and U can be marked as (1,1,1), (0,1,0), (1,0,0) and (0,0,1), respectively. For example, 5mer ‘GGACU’ will be encoded as a 5x3-dimensional vector: (1,0,0,1,0,0,1,1,1,0,1,0,0,0,1). 
### Sequence encoding scheme: nucleotide frequency
The nucleotide frequency within the sequence was calculated. The density of the ith nucleotide is defined as the frequency of this nucleotide before the i+1 position. Taking sequence ‘AAACU’ as an example, the accumulative frequencies of adenine at the first, second and third position is 1 (1/1), 1 (2/2) and 1 (3/3) while the frequencies of cytosine and uracil at the fourth and fifth position are 0.25 (1/4) and 0.2 (1/5), respectively. Thus, this 5mer will be encoded as a 5-dimensional vector (1,1,1,0.25,0.2). In this project, we utilized the sequence information of a 41bp region centered by the sample site. Using the above-mentioned encoding scheme, a 164-di

### Genomic features description
In this project, 35 genome-derived features were used in our model. Feature 1-13 are dummy variables that demonstrate whether a site is overlapped to a topological region within the transcript. Feature 14-16 describe their relative position to 5’UTR, 3’UTR and exon while feature 17-19 is the length of the corresponding 5’UTR, 3’UTR and exon region. Feature 20-22 measure the nucleotide distances to the splicing junction or nearest adenosine sites. Feature 23-26 are related to the conservation score of the sites. The rest features describe the secondary structure, genomic properties and attributes of the related genes or transcripts.

### machine learning platform: H2O
H2O is an in-memory, distributed and open-source machine learning platform that provides high-quality, high-speed ML model building on big data, together with model productionalization in an enterprise environment (Click et al., 2016). Here are three main reasons that explain why to choose H2O: Firstly, it includes four widely used machine learning algorithms--generalized linear modeling (GLM), Distributed Random Forest (DRF), Deep Learning (Neural Networks) and extreme gradient boosting (XGboost) we planned to use, comparing the results and performances come from the same platform are meaningful rigorous. Secondly, all the algorithms that we choose can specify the distribution family and link for loss function which gives the probabilistic approach to machine learning. Thirdly, the distributed computing, in-memory processing with fast serialization between nodes and clusters (Aiello et al., 2016) made H2O running much faster than the traditional package in R CRAN when solving ML problems, Algorithms for learning to handle our large and complex datasets it is more efficient. 
