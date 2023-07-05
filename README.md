# OkCupid-Profiles-LDA-Topic-Modeling
This project aims to implement Latent Dirichlet Allocation in conjunction with keyword extraction to improve topic modeling and selection
The dataset used in the project is available on Kaggle: https://www.kaggle.com/datasets/andrewmvd/okcupid-profiles

# Background
OkCupid is an online dating and friendship application, owned and operated by the Match Group. It boasts a unique matching algorithm and impressive user statistics. However, it appears that the algorithm is only aimed at adding users to a dating pool and matching them through multiple-choice questions with different weights assigned to the options. At the same time, user-generated profile content (free-form essays) is largely disregarded and does not contribute to the matching accuracy. 

As a linguist and scientist, I would argue that textual data produced by an individual can offer significant insights into their personality and, therefore, contribute to the improvement of the existing matching algorithm. This project is aimed at determining whether it is indeed the case. Moreover, as previous profile grouping projects (see code for details) displayed mixed results in ML algorithm application, it might be reasonable to assume that an alternative approach is needed.

# Methods
1. Raw text data were collected from an OkCupid dataset available on Kaggle. The texts were subset and grouped by user.
2. Null values were eliminated and resulting strings were preprocessed (punctuation and stopword removal, lowercasing, stemming).
3. To offset the large quantity of the data (59946 rows), I selected a number of random samples without replacement (3000, approximately 5% of the data). No random state was assigned during selection to see the impact sample variation has on model coherence.
4. Unlike purposefully created text data, e.g. news items or academic articles, these profile essays do not have a uniform aim or rather, the aim is to represent the user in terms of being desirable. This can involve a wide range of linguistic, and sometimes paralinguistic means that hinder classification. Therefore,  to further streamline the data analysis, I selected only relevant keywords with YAKE and used them for corpus creation.
5. In previously mentioned projects, vectorization and K-Means clustering were applied together to try and group OkC profiles for improved user recommendations. However, this method was not a complete success in either of the cases, despite the implementation of dimensionality-reducing practices such as PCA and t-SNE. In this project, the given methods showed equally poor results even on keyword data, with no optimal tradeoff between the K-value and inertia for the dataset. Due to this, Latent Dirichlet Alloction technique was chosen for topic modeling and clustering as an algorithm that may produce better results.
6. To compare the keyword-oriented approach and the general text-oriented one, I first implemented Latent Dirichlet Allocation to stemmed essays. This produced a coherence score of 0.34 (approximately) for over 100 topics, which is not a satisfactory result and is likely due to the diversity of the given texts that cannot be improved by preprocessing.
7. Interestingly enough, when used on keywords, LDA showed nearly double the coherence with fewer topics (0.6 and higher for under 90 topics) and clear topic divergence. With the number of topics going over 100, the model was able to reach an 0.8 coherence score, which is a good result for a large dataset.

# LDA applied to preprocessed essay texts
![image](https://github.com/OlgaIudina1992/OkCupid-Profiles-LDA-Topic-Modeling/assets/110724838/b84910c1-f850-48e5-b459-08812fada0c7)
# LDA applied to preprocessed keywords
![image](https://github.com/OlgaIudina1992/OkCupid-Profiles-LDA-Topic-Modeling/assets/110724838/5b1b1f6e-8b8a-4680-b58b-a4b83f1022d2)

# Conclusions
Despite Latent Dirichlet Allocation being a "soft" clustering algorithm, which gauges topic distribution across data rather than group distribution according to a topic, its value in determining text similarity is very high. The quality of the allocation can be further improved by selecting user-relevant keywords and stemming them for uniformity. 

# Further applications
As far as the application is concerned, the outcome of this LDA analysis can be used as a foundational step to create diversified topic-based dating pools to which users are added after keyword selection. When the profiles are grouped on topic similarity, the existing question-based algorithm can be applied to further increase matching precision with weighted answer options. This should ensure that both linguistic and mathematical aspects are taken into consideration in the matching process and user-generated data are not disregarded.
