# Part-of-Speech Tagging
Part of Speech Tagging Use several techniques, including table lookups, n-grams, and hidden Markov models, to tag parts of speech in sentences, and compare their performance.

This project demonstrates text processing techniques that allow you to build a part of speech tagging model. You will work with a simplelookup table, and progressively add more complexity to improve the model using probabilistic graphical models. Ultimately you’ll be using a Python package to build and train a tagger with a hidden Markov model, and you will be able to compare the performances of all these models in a dataset of sentences.

## Hidden Markov Model

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

### HMM network : Model Topology 
![HMM](_post-hmm.png)

Basic HMM tagger produces the expected accuracy using the universal tagset as follows: 
- >97% accuracy on the training sentences
- >95.5% accuracy the test sentences

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
----------
### Reference
- [Pomegranate](http://pomegranate.readthedocs.io/)
- [Hidden Markov Model](https://pomegranate.readthedocs.io/en/latest/HiddenMarkovModel.html#initialization)
- [Missing Values](https://pomegranate.readthedocs.io/en/latest/nan.html)
- [NLTK](https://www.nltk.org/)
- [Tagged Corpora](http://www.nltk.org/book/ch05.html)
- [Univrsal Part-of-Speech Tagset](https://arxiv.org/pdf/1104.2086.pdf)
- [Statistical Part-of-Speech Tagger](http://www.coli.uni-saarland.de/~thorsten/publications/Brants-ANLP00.pdf)
- [Penn Treebank Part-of-Speech Tagset](https://www.ling.upenn.edu/courses/Fall_2003/ling001/penn_treebank_pos.html)
- [Graphviz](http://www.graphviz.org/)
