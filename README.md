# Source Code Embeddings with Word2Vec

**Python2Vec · CS 421 Project 2 · Spring 2023**

This project trains Word2Vec on open-source code to explore which tokens appear in similar contexts. The main notebook uses Python source code to find neighbors for keywords such as `for` and `if`, measure cosine similarity between `math` and `numpy`, and rank pairs of common identifiers by their embedding similarity. A milestone notebook extends the experiment to Java.

## How it works

1. Collect Python source files recursively from `libraries/` and concatenate them into `py_files.txt`.
2. Skip lines beginning with `#` after trimming whitespace. Lowercase the remaining lines, split on whitespace, and strip punctuation from token edges. Each line provides one sequence of tokens for training.
3. Train a Gensim Word2Vec model with a context window of 5 and a minimum token count of 1.
4. Parse individual Python lines with `ast` to count identifiers on lines that parse on their own. Write the 50 most frequent identifiers to `most_common.txt` and compare pairs that appear in the embedding vocabulary.

The saved Python run processed **4.6 million lines** and **11.1 million tokens**. In that run, `math` and `numpy` had a cosine similarity of **0.51**. The embeddings capture co-occurrence under the notebook’s tokenization, so similarity scores describe how tokens are used in the training corpus.

## Run the Python experiment

From the project root, install the notebook dependencies and start Jupyter:

```bash
python -m pip install jupyterlab gensim numpy pandas plotly
python -m jupyter lab
```

Open [3-Word2Vec.ipynb](3-Word2Vec.ipynb) and run the cells in order. You can skip the notebook’s install cells after installing the packages above.

- **Use an existing corpus.** If `py_files.txt` is present and contains the source text, skip the two cells that scan `libraries/` and write the corpus. If you cloned a Git LFS checkout and received a pointer file, run `git lfs pull` first.
- **Build the corpus.** Place local copies of Python repositories under `libraries/` and run the corpus-building cells before training. The original project used repositories including Django, Flask, NumPy, and pandas.

The training cell loads the tokenized corpus into memory. Use a smaller set of source repositories for a quick run.

## Notebooks

| Notebook | Experiment |
| --- | --- |
| [3-Word2Vec.ipynb](3-Word2Vec.ipynb) | Python source-code embeddings, keyword neighbors, and identifier-pair similarity. |
| [Milestone 3 demo.ipynb](Milestone%203%20demo.ipynb) | Builds a Java corpus from `my_repos/` and trains Word2Vec on it. With local repositories, start at the cell that scans for Java files. The final identifier-analysis cells use the Python corpus. |
| [2-Word2Vec-GOT.ipynb](2-Word2Vec-GOT.ipynb) | Word2Vec exploration on *A Song of Ice and Fire* text in `data/`, with PCA visualization. |
| [1-Simple-N-Gram-Wikipedia-autocomplete.ipynb](1-Simple-N-Gram-Wikipedia-autocomplete.ipynb) | N-gram autocomplete using text from Wikipedia’s “Deep learning” article. |
| [2-Simple-N-Gram-Trump-generate.ipynb](2-Simple-N-Gram-Trump-generate.ipynb) | N-gram text generation using a tweet dataset. |
