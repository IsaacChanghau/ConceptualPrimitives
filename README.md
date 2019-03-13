# Conceptual Primitives

Re-implementation of "[SenticNet 5: Discovering Conceptual Primitives for Sentiment Analysis by Means of Context Embeddings](
https://aaai.org/ocs/index.php/AAAI/AAAI18/paper/view/16839/15882)" in tensorflow for verb substitution and clustering.

## Overall Framework and Algorithm
**Framework**:
<p align="center">
  <img src="/assets/overall-framework.png">
</p>

**Algorithm** for context and target word (verb) embedding generation:
<p align="center">
  <img src="/assets/algorithm.png">
</p>


## Training
To train the conceptual primitives model, please run:
```bash
python3 main.py --gpu_idx 0 1 \  # number of GPUs used for training and their indices
    --mode train \  # training model or infer
    --resume_training false \  # if true, will resume previous trained parameters
    --neg_sample 10 \  # number of negative samples
    --word_dim 300 \  # input pre-trained / randomly initialized word embedding dimension
    --num_units 300 \  # number of units for rnn cell and hidden layer of feed-forward network
    --k 100 \  # number of units for output layer
    --use_ntn true \  # if use neural tensor network to fuse left and right contexts
    --tune_emb false \  # whether the input word embedding are tunable while training
    --lr 0.002 \  # learning rate
    --batch_size 1000 \  # batch size
    --epochs 30 \  # total training epochs
    --ckpt ckpt/ \  # checkpoint path to save model
    --model_name conceptual_primitives \  # model name
    --ukwac_path <raw ukwac dataset path> \  # raw ukwac dataset path
    --glove_path <pre-trained glove embedding path> \  # pre-trained glove word embedding path
    --save_path <processed data save path> \  # path for saving processed dataset
    --word_threshold 90 \  # word threshold, minimal occurrence of words to be kept
    --word_lowercase true  # whether lowercase the text
```

## Reference
- [SenticNet 5: Discovering Conceptual Primitives for Sentiment Analysis by Means of Context Embeddings](
https://aaai.org/ocs/index.php/AAAI/AAAI18/paper/view/16839/15882).
- [The WaCky Wide Web: A Collection of Very Large Linguistically Processed Web-Crawled Corpora](
http://wacky.sslmit.unibo.it/lib/exe/fetch.php?media=papers:wacky_2008.pdf).
- [ukWaC](http://wacky.sslmit.unibo.it/doku.php?id=corpora#english) dataset: a 2 billion word corpus constructed from 
the Web limiting the crawl to the .uk domain and using medium-frequency words from the [BNC](http://www.natcorp.ox.ac.uk/) as seeds. 
The corpus was POS-tagged and lemmatized with the [TreeTagger](http://www.ims.uni-stuttgart.de/projekte/corplex/TreeTagger/).
- [ukWaC TagSet](http://wacky.sslmit.unibo.it/lib/exe/fetch.php?media=tagsets:ukwac_tagset.txt): explanation of POS tag meaning used in UKWAC dataset.
- [jungokasai/skipgram](https://github.com/jungokasai/skipgram/blob/master/word2vec_model.py): refer the negative sampling and loss function design.
