# FastText Embeddings Booster
Improving FastText Embeddings for out-of-vocabulary (OOV) words

In FastText paper entitled "Enriching Word Vectors with Subword Information", a word is represented by the sum of the vector representations of its n-grams. As well as vector representation the constituent n-grams, the vector representation of the whole word is also taken into the sum.

In this setting, a problem arises is that for OOV words, we do not have the vector representation of the whole word. Therefore, the vector representation of the OOV words is constructed using the sum on their constituent n-grams.

To tackle this problem, we hypothesize that an auto-encoder can be trained to reconstruct the missing value from the OOV embeddings which is the vector representation of the whole word.

For training the auto-encoder, first, we construct FastText embeddings of the in-vocabulary words without incorporating the whole word vector representations. This data is then given to the encoder as the noisy data. On the other side, the original FastText embeddings for the corresponding words incorporating the whole word vector representations is given to the decoder output as the gold standard.

Adam optimizer is used to train the network. The loss function that is utilized here is MSELoss.

After the network is trained, the constructed FastText vector representations of OOV words are given to the network as the noisy data and post-enriched embeddings are extracted from the network.
