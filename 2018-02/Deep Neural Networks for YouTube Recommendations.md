# Deep Neural Networks for YouTube Recommendations

## Keywords
Recommender system, deep learning, Youtube

## Architecture
<img src="images/1.jpeg">

## Candidate generation network
<img src="images/2.jpeg">
<img src="images/3.jpeg">
Inspired by continuous bag of words language models [14], we learn high dimensional embeddings for each video in a fixed vocabulary and feed these embeddings into a feedforward neural network. A user’s watch history is represented by a variable-length sequence of sparse video IDs which is mapped to a dense vector representation via the embeddings. The network requires fixed-sized dense inputs and simply averaging the embeddings performed best among sev- eral strategies (sum, component-wise max, etc.). Impor- tantly, the embeddings are learned jointly with all other model parameters through normal gradient descent backpropagation updates. Features are concatenated into a wide first layer, followed by several layers of fully connected Rectified Linear Units (ReLU) [6]. Figure 3 shows the general network architecture with additional non-video watch features described below.

### DNN over MF
A key advantage of using deep neural networks as a gener- alization of matrix factorization is that arbitrary continuous and categorical features can be easily added to the model.

### Example age feature
we feed the age of the training example as a feature during training. At serving time, this feature is set to zero (or slightly negative) to reflect that the model is making predictions at the very end of the training window.

### Label and Content Selection
1. <strong>Training examples are generated from all YouTube watches (even those embedded on other sites) rather than just watches on the recommendations we produce.</strong> Otherwise, it would be very difficult for new content to surface and the recom- mender would be overly biased towards exploitation.
2. Another key insight that improved live metrics was to <strong>generate a fixed number of training examples per user, effectively weighting our users equally in the loss function.</strong> This prevented a small cohort of highly active users from dominating the loss.
3. user has just issued a search query for “tay- lor swift”. Since our problem is posed as predicting the next watched video, a classifier given this information will predict that the most likely videos to be watched are those which appear on the corresponding search results page for “taylor swift”. Unsurpisingly, reproducing the user’s last search page as homepage recommendations performs very poorly. <strong>By discarding sequence information and representing search queries with an unordered bag of tokens</strong>, the classifier is no longer directly aware of the origin of the label.
4. Natural consumption patterns of videos typically lead to very asymmetric co-watch probabilities. Episodic series are usually watched sequentially and users often discover artists in a genre beginning with the most broadly popular before focusing on smaller niches. <strong>We therefore found much better performance predicting the user’s next watch, rather than predicting a randomly held-out watch (Figure 5).</strong> Many collaborative filtering systems implicitly choose the labels and context by holding out a random item and predicting it from other items in the user’s history (5a). This leaks future information and ignores any asymmetric consumption patterns. In contrast, we “rollback” a user’s history by choosing a ran- dom watch and only input actions the user took before the held-out label watch (5b).
<img src="images/4.jpeg">

## Experiments with Features and Depth
Adding features and depth significantly improves precision on holdout data as shown in Figure 6. In these experiments, a vocabulary of 1M videos and 1M search tokens were embedded with 256 floats each in a maximum bag size of 50 recent watches and 50 recent searches. The softmax layer outputs a multinomial distribution over the same 1M video classes with a dimension of 256 (which can be thought of as a separate output video embedding). These models were trained until convergence over all YouTube users, corresponding to several epochs over the data. Network structure followed a common “tower” pattern in which the bottom of the network is widest and each successive hidden layer halves the number of units (similar to Figure 3). The depth zero network is effectively a linear factorization scheme which
performed very similarly to the predecessor system. Width and depth were added until the incremental benefit diminished and convergence became difficult:<img src="images/5.jpeg">
