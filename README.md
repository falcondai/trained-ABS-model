# trained-ABS-model
a trained attention-based summarization neural network model based on the published
[paper](http://arxiv.org/abs/1509.00685v2)
and [code](https://github.com/facebook/NAMAS)

## usage

Consider to use [`nvidia-docker`](https://github.com/NVIDIA/nvidia-docker) with
the image `falcondai/abs` (built from `Dockerfile` in the repo) which contains all the dependencies needed: `docker pull falcondai/abs`

To evaluate the trained model,

0. download the trained model file from [Google drive](https://drive.google.com/open?id=0Bx73xeahAckPN0gyMXVMRC1aMlU)
1. clone my [fork](https://github.com/falcondai/NAMAS) of the NAMAS repo (which contains minor changes over the original):
```bash
git clone github.com/falcondai/NAMAS
```
2. put the downloaded model file to the project root (next to `test_model.sh`)
3. run the `test_model.sh` script (which generates 10-word-long summaries):
```bash
./test_model.sh paper-example.article.txt abs-model.th 10
```

## how this model was trained

This model is trained using my [fork](https://github.com/falcondai/NAMAS) of
the original repo and here are some notable differences.

- used the unannotated 5th edition gigaword dataset (https://catalog.ldc.upenn.edu/LDC2011T07).
  The original repo used the annotated version (https://catalog.ldc.upenn.edu/LDC2012T21)
  but didn't use the extra annotation aside from its tokenization.
- I used NLTK ``word_tokenize`` to tokenize the text (which may result in
  different tokenization from the annotated gigaword).
- I dropped article-title pairs that contains non-ASCII characters because it
  will cause errors in the tokenizer and it is known that gigaword contains
  some articles in non-English (Spanish). it would be better to remove these
  using the official list though.

I got similar validation perplexity (**27.74**) as the number quoted in the
paper (27.1) and here are some sample predictions (compare with ABS+ predictions
presented in the paper):

- detained iranian-american academic released from jail after posting bail 	
- eu ministers gather for unprecedented conference on economic cooperation
- death toll from school in haiti rises to #
- australian fm congratulates new zealand as 'man of respected
- two south africans upset at hong kong rugby coach
- christian conservatives in the last two us presidential elections
- un nuclear watchdog warns iran of possible new sanctions
- thousands of kashmiris rally in support for cancer treatment
- two us soldiers killed in iraq s restive province
- davydenko retires from # nd round at sydney international
- russia 's gazprom set up joint venture in northwest

## extra notes

I trained the model with the default hyperparameters but some of the
default hyperparameters, as pointed out in [this issue](https://github.com/facebook/NAMAS/issues/8), do not match the ones
presented in the paper.

## reference

Rush, Alexander M., Sumit Chopra, and Jason Weston. "A neural attention model for abstractive sentence summarization." arXiv preprint [arXiv:1509.00685](http://arxiv.org/abs/1509.00685v2) (2015).

## author

Falcon Dai (dai@ttic.edu)
