# ITEM2VEC NEURAL ITEM EMBEDDING FOR COLLABORATIVE FILTERING [1]

## Keywords
word2vec, collaborative filtering, recommender systems, item recommendations

## Inovations
1. In order to overcome the imbalance between rare and frequent words the following subsampling procedure is proposed [2]: Given the input word sequence, we discard each word w with a probability<img src='images/1.jpg'>where f (w) is the frequency of the word w and ρ is a prescribedthreshold. This procedure was reported to accelerate the learning process and to improve the representation of rare words significantly.

## Evaluations
Comparing the performance of item2vec with item2item SVD on clustering.

## References
[1] [Barkan, O. and Koenigstein, N., 2016, September. Item2vec: neural item embedding for collaborative filtering. In Machine Learning for Signal Processing (MLSP), 2016 IEEE 26th International Workshop on (pp. 1-6). IEEE.](https://arxiv.org/pdf/1603.04259.pdf)
[2] [Mikolov, T., Sutskever, I., Chen, K., Corrado, G.S. and Dean, J., 2013. Distributed representations of words and phrases and their compositionality. In Advances in neural information processing systems (pp. 3111-3119).](http://papers.nips.cc/paper/5021-distributed-representations-of-words-and-phrases-and-their-compositionality.pdf)