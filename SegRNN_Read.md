##How to train a model

To train a model using segmental RNNs, you need to specify the following things:

```
--train, no argument, you are in the training mode
--train_file, --dev_file, --test_file, the train/dev/test file paths
--model_file_prefix, the model file prefix, the model will be saved as model_file_prefix.params, 
                     model_file_prefix.dict, model_file_prefix.tdict in the model_file_prefix directory.
--upe, (optional), you can specify the pre-trained word embeding you want to use 
                  (simply don't use this if you don't want to use pre-trained embeddings)
```
(see more explainations of different parameters in https://github.com/clab/cnn/blob/master/examples/segrnn-sup.cc#L1019)

e.g.

```
examples/segrnn-sup --train --evaluate_test \
                    --train_file /usr1/home/lingpenk/data_scripts/data/icwb2-data/processed/train \
                    --dev_file /usr1/home/lingpenk/data_scripts/data/icwb2-data/processed/dev \
                    --test_file /usr1/home/lingpenk/data_scripts/data/icwb2-data/processed/test \
                    --upe /usr1/home/lingpenk/data_scripts/data/embeding/vec-cwin.txt \
                    --model_file_prefix model > stdout_log 2> stderr_log
```

The input file format (for train/dev/test) will be, one sentence per line:

```
European Union rejects German call to boycott British lamb . ||| ORG:2 O:1 MISC:1 O:1 O:1 O:1 MISC:1 O:1 O:1
```

Basically, this means, "European Union" is ORG of length 2, "German" is MISC of length 1, "British" is MISC with length one.
In the paper (http://arxiv.org/abs/1511.06018), length is $z$ and label (e.g. ORG) is $y$.

<b>Note</b> that you can use any tagging scheme you want, BIOES could be the choice.
