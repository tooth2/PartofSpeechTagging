# Part-of-Speech Tagging
Part of Speech Tagging Use several techniques, including table lookups, n-grams, and hidden Markov models, to tag parts of speech in sentences, and compare their performance.

This project demonstrates text processing techniques that allow you to build a part of speech tagging model. You will work with a simplelookup table, and progressively add more complexity to improve the model using probabilistic graphical models. Ultimately you’ll be using a Python package to build and train a tagger with a hidden Markov model, and you will be able to compare the performances of all these models in a dataset of sentences.

## Implementation Approach

- Review the provided interface to load and access the text corpus
- Build a Most Frequent Class tagger to use as a baseline
- Build an Hidden Markov Model(HMM) Part-of-Speech(PoS) tagger and compare to the MFC baseline
- Use HMM to build a part of speech tagging model
- Train HMM with the Viterbi and the Baum-Welch algorithms

**HMM Tagger**
- pair_counts() function
    - Emission count: The emission counts dictionary has 12 keys, one for each of the tags in the universal tagset, for example, "time" is the most common word tagged as a NOUN
- MFC tagger: MFC Tagger produces the expected accuracy using the universal tagset as follows: 
    - >95.5% accuracy on the training sentences
    - 93% accuracy the test sentences
- Calculating Tag Counts
    - unigram_counts()
    - bigram_counts()
    - start_counts()
    - end_counts()

### Dataset
- Data
    - There are 57340 sentences in the corpus.
    - There are 45872 sentences in the training set.
    - There are 11468 sentences in the testing set.
    - There are a total of 1161192 samples of 56057 unique words in the corpus.
    - There are 928458 samples of 50536 unique words in the training set.
    - There are 232734 samples of 25112 unique words in the testing set.
    - There are 5521 words in the test set that are missing in the training set.
- Dataset-only Attributes:
    - training_set: reference to a Subset object containing the samples for training
    - testing_set: reference to a Subset object containing the samples for testing
- Dataset & Subset Attributes:
    - sentences: a dictionary with an entry {sentence_key: Sentence()} for each sentence in the corpus
    - keys: an immutable ordered (not sorted) collection of the sentence_keys for the corpus
    - vocab: an immutable collection of the unique words in the corpus
    - tagset: an immutable collection of the unique tags in the corpus
    - X: returns an array of words grouped by sentences ((w11, w12, w13, ...), (w21, w22, w23, ...), ...)
    - Y: returns an array of tags grouped by sentences ((t11, t12, t13, ...), (t21, t22, t23, ...), ...)
    - N: returns the number of distinct samples (individual words or tags) in the dataset

### HMM network : Model Topology 
![HMM](_post-hmm.png)

Basic HMM tagger produces the expected accuracy using the universal tagset as follows: 
- >97% accuracy on the training sentences : training accuracy basic hmm model: 97.54%
- >95.5% accuracy the test sentences : testing accuracy basic hmm model: 95.95%

## Helper 
### Model2PNG: Convert a Pomegranate model into a PNG image
The conversion pipeline extracts the underlying NetworkX graph object, converts it to a PyDot graph, then writes the PNG data to a bytes array, which can be saved as a file to disk or imported with matplotlib for display.
   > Model -> NetworkX.Graph -> PyDot.Graph -> bytes -> PNG

```Parameters
- model : Pomegranate.Model
        The model object to convert. The model must have an attribute .graph
        referencing a NetworkX.Graph instance.
- filename : string (optional)
        The PNG file will be saved to disk with this filename if one is provided.
        By default, the image file will NOT be created if a file with this name already exists unless overwrite=True.        
- overwrite : bool (optional)
        overwrite=True allows the new PNG to overwrite the specified file if it already exists
- show_ends : bool (optional)
        show_ends=True will generate the PNG including the two end states from the Pomegranate 
        model (which are not usually an explicit part of the graph)
```

### Show Model: Display a Pomegranate model as an image using matplotlib
```Parameters
    - model : Pomegranate.Model
        The model object to convert. The model must have an attribute .graph referencing a NetworkX.Graph instance.
    - figsize : tuple(int, int) (optional)
        A tuple specifying the dimensions of a matplotlib Figure that will display the converted graph
    - **kwargs : dict
        The kwargs dict is passed to the model2png program
```  

### Next Step
- Trying other corpus: nltk.corpus.brown or nltk.corpus.treebank datasets
- Using pseudocounts or interpolated smoothing to handle missing data
- Retraining the hidden markov model using Baum-Welch re-estimation (available via the .fit() method in Pomegranate)
- Laplace Smoothing (pseudocounts):  Laplace smoothing is a technique where you add a small, non-zero value to all observed counts to offset for unobserved values.
- [Additive Smoothing](https://en.wikipedia.org/wiki/Additive_smoothing)
- Backoff Smoothing:  Another smoothing technique is to interpolate between n-grams for missing data. This method is more effective than Laplace smoothing at combatting the data sparsity problem. 
- Extending to Trigrams HMM taggers have achieved better than 96% accuracy on this dataset with the full Penn treebank tagset, incorporating trigram probabilities in your frequency tables, and re-implementing the Viterbi algorithm to consider three consecutive states instead of two.
----------
### Reference
- [Universal Tagset](http://www.petrovi.de/data/universal.pdf)
- [Pomegranate Hidden Markov Model](https://pomegranate.readthedocs.io/en/latest/HiddenMarkovModel.html#initialization)
- [Missing Values](https://pomegranate.readthedocs.io/en/latest/nan.html)
- [NLTK](https://www.nltk.org/)
- [Tagged Corpora](http://www.nltk.org/book/ch05.html)
- [Univrsal Part-of-Speech Tagset](https://arxiv.org/pdf/1104.2086.pdf)
- [Statistical Part-of-Speech Tagger](http://www.coli.uni-saarland.de/~thorsten/publications/Brants-ANLP00.pdf)
- [Penn Treebank Part-of-Speech Tagset](https://www.ling.upenn.edu/courses/Fall_2003/ling001/penn_treebank_pos.html)
- [Graphviz](http://www.graphviz.org/)
- [IBM Watson Discovery](https://www.ibm.com/watson/services/discovery/)
- [IBM Watson Assistant](https://www.ibm.com/watson/ai-assistant/)
