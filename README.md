# trained-ABS-model
a trained attention-based summarization neural network model based on the published
[paper](http://arxiv.org/abs/1509.00685v2)
and [code](https://github.com/facebook/NAMAS)

## usage

I used Github LFS (Large File Service) to store the large model binary:
it is pretty awesome!

So you need to install [Git LFS](https://git-lfs.github.com/) and then just
clone the repo.

To evaluate the model, clone the NAMAS repo (mine or the original) and run the `test_model.sh` script:
```bash
./test_model.sh paper-example.article.txt abs-model.th 10
```

Consult the original repo for more instructions.

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
default hyperparameters, as pointed in [this issue](https://github.com/facebook/NAMAS/issues/8), do not match the ones
presented in the paper.

## reference

Rush, Alexander M., Sumit Chopra, and Jason Weston. "A neural attention model for abstractive sentence summarization." arXiv preprint [arXiv:1509.00685](http://arxiv.org/abs/1509.00685v2) (2015).

## author

Falcon Dai (dai@ttic.edu)
