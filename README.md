# `pke` - python keyphrase extraction

`pke` is an **open source** python-based **keyphrase extraction** toolkit. It
provides an end-to-end keyphrase extraction pipeline in which each component can
be easily modified or extended to develop new models. `pke` also allows for 
easy benchmarking of state-of-the-art keyphrase extraction models, and 
ships with supervised models trained on the
[SemEval-2010 dataset](http://aclweb.org/anthology/S10-1004).

[![Build Status](https://travis-ci.org/boudinfl/pke.svg?branch=master)](https://travis-ci.org/boudinfl/pke)

## Table of Contents

* [Installation](#installation)
* [Minimal example](#minimal-example)
* [Getting started](#getting-started)
* [Implemented models](#implemented-models)
* [Citing pke](#citing-pke)

## Installation

To pip install `pke` from github:

```bash
pip install git+https://github.com/boudinfl/pke.git
```

`pke` also requires external resources that can be obtained using:

```bash
python -m nltk.downloader stopwords
python -m nltk.downloader universal_tagset
python -m spacy download en # download the english model
```

As of April 2019, `pke` only supports Python 3.6+.

## Minimal example

`pke` provides a standardized API for extracting keyphrases from a document.
Start by typing the 5 lines below. For using another model, simply replace
`pke.unsupervised.TopicRank` with another model ([list of implemented models](#implemented-models)).

```python
import pke

# initialize keyphrase extraction model, here TopicRank
extractor = pke.unsupervised.TopicRank()

# load the content of the document, here document is expected to be in raw
# format (i.e. a simple text file) and preprocessing is carried out using spacy
extractor.load_document(input='/path/to/input.txt', language='en')

# keyphrase candidate selection, in the case of TopicRank: sequences of nouns
# and adjectives (i.e. `(Noun|Adj)*`)
extractor.candidate_selection()

# candidate weighting, in the case of TopicRank: using a random walk algorithm
extractor.candidate_weighting()

# N-best selection, keyphrases contains the 10 highest scored candidates as
# (keyphrase, score) tuples
keyphrases = extractor.get_n_best(n=10)
```

A detailed example is provided in the [`examples/`](examples/) directory.

## Getting started

Tutorials and code documentation are available at
[https://boudinfl.github.io/pke/](https://boudinfl.github.io/pke/).

## Implemented models

`pke` currently implements the following keyphrase extraction models:

* Unsupervised models
  * Statistical models
    * TfIdf [[documentation](https://boudinfl.github.io/pke/build/html/unsupervised.html#tfidf)]
    * KPMiner [[documentation](https://boudinfl.github.io/pke/build/html/unsupervised.html#kpminer), [article by (El-Beltagy and Rafea, 2010)](http://www.aclweb.org/anthology/S10-1041.pdf)]
    * YAKE [[documentation](https://boudinfl.github.io/pke/build/html/unsupervised.html#yake), [article by (Campos et al., 2020)](https://doi.org/10.1016/j.ins.2019.09.013)]
  * Graph-based models
    * TextRank [[documentation](https://boudinfl.github.io/pke/build/html/unsupervised.html#textrank), [article by (Mihalcea and Tarau, 2004)](http://www.aclweb.org/anthology/W04-3252.pdf)]
    * SingleRank  [[documentation](https://boudinfl.github.io/pke/build/html/unsupervised.html#singlerank), [article by (Wan and Xiao, 2008)](http://www.aclweb.org/anthology/C08-1122.pdf)]
    * TopicRank [[documentation](https://boudinfl.github.io/pke/build/html/unsupervised.html#topicrank), [article by (Bougouin et al., 2013)](http://aclweb.org/anthology/I13-1062.pdf)]
    * TopicalPageRank [[documentation](https://boudinfl.github.io/pke/build/html/unsupervised.html#topicalpagerank), [article by (Sterckx et al., 2015)](http://users.intec.ugent.be/cdvelder/papers/2015/sterckx2015wwwb.pdf)]
    * PositionRank [[documentation](https://boudinfl.github.io/pke/build/html/unsupervised.html#positionrank), [article by (Florescu and Caragea, 2017)](http://www.aclweb.org/anthology/P17-1102.pdf)]
    * MultipartiteRank [[documentation](https://boudinfl.github.io/pke/build/html/unsupervised.html#multipartiterank), [article by (Boudin, 2018)](https://arxiv.org/abs/1803.08721)]
* Supervised models
  * Feature-based models
    * Kea [[documentation](https://boudinfl.github.io/pke/build/html/supervised.html#kea), [article by (Witten et al., 2005)](https://www.cs.waikato.ac.nz/ml/publications/2005/chap_Witten-et-al_Windows.pdf)]
    * WINGNUS [[documentation](https://boudinfl.github.io/pke/build/html/supervised.html#wingnus), [article by (Nguyen and Luong, 2010)](http://www.aclweb.org/anthology/S10-1035.pdf)]

## Citing pke

If you use `pke`, please cite the following paper:

```
@InProceedings{boudin:2016:COLINGDEMO,
  author    = {Boudin, Florian},
  title     = {pke: an open source python-based keyphrase extraction toolkit},
  booktitle = {Proceedings of COLING 2016, the 26th International Conference on Computational Linguistics: System Demonstrations},
  month     = {December},
  year      = {2016},
  address   = {Osaka, Japan},
  pages     = {69--73},
  url       = {http://aclweb.org/anthology/C16-2015}
}
```

## Evaluate
### TopicRank

#### Inspec
N=5
P=0.2628
R=0.1337540716612378
F1=0.1772800863464652

N=10
P=0.21764825759119624
R=0.21742671009771988
F1=0.2175374274366025

N=15
P=0.1916809605488851
R=0.2730048859934853
F1=0.225226738327175

#### SemEval2017
N=5
P=0.31724137931034485
R=0.09168718489858131
F1=0.14225941422594143

N=10
P=0.2578616352201258
R=0.1490209872200727
F1=0.18888393520582553

N=15
P=0.223837999456374
R=0.19310587407667956
F1=0.20733933404670485

#### DUC2001
N=5
P=0.23192182410423454
R=0.14349052801289802
F1=0.17729083665338646

N=10
P=0.1788750817527796
R=0.22047561467150342
F1=0.1975085755551544

N=15
P=0.14689141856392293
R=0.2704554615074567
F1=0.19038161441339194

### SingleRank
#### Inspec
N=5
P=0.2928
R=0.1490228013029316
F1=0.19751753912574205

N=10
P=0.2614116227629198
R=0.26465798045602607
F1=0.26302478502781995

N=15
P=0.23255813953488372
R=0.34405537459283386
F1=0.2775268905493062

#### SemEval2017
N=5
P=0.30304259634888436
R=0.08758353851565248
F1=0.13589230489357831

N=10
P=0.2949290060851927
R=0.17047719545081486
F1=0.2160636005646779

N=15
P=0.2721981591770439
R=0.2357837964591394
F1=0.2526858076270654

#### DUC2001
N=5
P=0.19804560260586318
R=0.12253123740427246
F1=0.15139442231075698

N=10
P=0.17443756113465927
R=0.21563885530028215
F1=0.19286229271809663

N=15
P=0.1579637317019882
R=0.2914147521160822
F1=0.2048739019552281