### This fork modifies the preprocessed output to JSON format to allow using non-Tensorflow libraries to work with the CNN/DailyMail summarization dataset
**Note**: requires Python 3

*This fork is primarily developed in order to work with [this repository](https://github.com/ChenRocks/fast_abs_rl) which uses pytorch*

-- 

## 1. Download data
Download and unzip the `stories` directories from [here](http://cs.nyu.edu/~kcho/DMQA/) for both CNN and Daily Mail. 

**Warning:** These files contain a few (114, in a dataset of over 300,000) examples for which the article text is missing - see for example `cnn/stories/72aba2f58178f2d19d3fae89d5f3e9a4686bc4bb.story`. The [PyTorch code](https://github.com/ChenRocks/fast_abs_rl) works fine with it unless in an extreme case such that all data sampled in a batch is empty.

## 2. Download Stanford CoreNLP
We will need Stanford CoreNLP to tokenize the data. Download it [here](https://stanfordnlp.github.io/CoreNLP/) and unzip it. Then add the following command to your bash_profile:
```
export CLASSPATH=/path/to/stanford-corenlp-full-2016-10-31/stanford-corenlp-3.7.0.jar
```
replacing `/path/to/` with the path to where you saved the `stanford-corenlp-full-2016-10-31` directory. You can check if it's working by running
```
echo "Please tokenize this text." | java edu.stanford.nlp.process.PTBTokenizer
```
You should see something like:
```
Please
tokenize
this
text
.
PTBTokenizer tokenized 5 tokens at 68.97 tokens per second.
```
## 3. Process into JSON files (packed into tarballs) and vocab_cnt files (python pickle)
Run
```
python make_datafiles.py /path/to/cnn/stories /path/to/dailymail/stories
```
replacing `/path/to/cnn/stories` with the path to where you saved the `cnn/stories` directory that you downloaded; similarly for `dailymail/stories`.

This script will do several things:
* The directories `cnn_stories_tokenized` and `dm_stories_tokenized` will be created and filled with tokenized versions of `cnn/stories` and `dailymail/stories`. This may take some time. ***Note**: you may see several `Untokenizable:` warnings from Stanford Tokenizer. These seem to be related to Unicode characters in the data; so far it seems OK to ignore them.*
* For each of the url lists `all_train.txt`, `all_val.txt` and `all_test.txt`, the corresponding tokenized stories are read from file, lowercased and written to tarball files `train.tar`, `val.tar` and `test.tar`. These will be placed in the newly-created `finished_files` directory. This may take some time.
* Additionally, a `vocab_cnt.pkl` file is created from the training data. This is also placed in `finished_files`. This is a python Counter of all words, which could be useful for determining the vocabulary by word appearance count.
