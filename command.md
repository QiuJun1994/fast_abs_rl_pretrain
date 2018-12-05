# DataSet : Newsroom
# command for momo passport at cruise machine

### 1.test stanford core nlp tools
export CLASSPATH=/home/zmh/qiujun_lib/stanford-corenlp-full-2018-10-05/stanford-corenlp-3.9.2.jar
echo "Please tokenize this text." | java edu.stanford.nlp.process.PTBTokenizer

### 2.run the code to pretrain data



# DataSet : CNN/Daily
# command for momo passport at cruise machine
### 1.1 Download data
You can follow the README.md
### 1.2 test stanford core nlp tools
export CLASSPATH=/home/zmh/qiujun_lib/stanford-corenlp-full-2018-10-05/stanford-corenlp-3.9.2.jar
echo "Please tokenize this text." | java edu.stanford.nlp.process.PTBTokenizer
### 1.3 run the code to pretrain data
python make_datafiles_cnndaily.py /home/zmh/qiujun_data/cnn-dailymail/cnn/stories /home/zmh/qiujun_data/cnn-dailymail/dailymail/stories
### 1.4 decompress train.tar/val.tar/test.tar in /home/zmh/qiujun_fast_abs_rl_pretrain/finished_files
tar xmf train.tar
tar xmf val.tar
tar xmf test.tar
