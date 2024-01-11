t-SMILES: A Scalable Fragment-based Molecular Representation Framework for De Novo Molecule Generation
======================================================================================================

When using advanced NLP methodologies to solve chemical problems, two
fundamental questions arise: 1) What are 'chemical words'? and 2) How can they
be encoded as 'chemical sentences’?

This study introduces a scalable, fragment-based, multiscale molecular
representation algorithm called t-SMILES (tree-based SMILES) to address the
second question. It describes molecules using SMILES-type strings obtained by
performing a breadth-first search on a full binary tree formed from a fragmented
molecular graph.

Systematic evaluations using JTVAE, BRICS, MMPA, and Scaffold show that:

1.  It can build a multi-code system for molecular description, in which each
    decomposition algorithm creates a kind of language, and all these languages
    can complement each other and contribute to a whole mixed chemical space.
    Under this framework, classical SMILES can be unified as a special case of
    t-SMILES to achieve better balanced performance using hybrid decomposition
    algorithms.

2.  It exhibits impressive performance on low-resource datasets JNK3 and
    AID1706, whether the model is original, data augmented, or pre-training
    fine-tuned;

3.  It significantly outperforms classical SMILES, DeepSMILES, SELFIES and
    baseline models in goal-directed tasks.

4.  It outperforms previous fragment-based models being competitive with
    classical SMILES and graph-based methods on Zinc, QM9, and ChEMBL.

To support the t-SMILES algorithm, we introduce a new character, '&', to act as
a tree node when the node is not a real fragment in FBT. Additionally, we
introduce another new character, '\^', to separate two adjacent substructure
segments in t-SMILES string, similar to the blank space in English sentences
that separates two words.

Three coding algorithms are presented in this study:

1.  TSSA: t-SMILES with shared atom.

2.  TSDY: t-SMILES with dummy atom but without ID.

3.  TSID: t-SMILES with ID and dummy atom.

For example, the three t-SMILES codes of Celecoxib are:

1.  TSID\_M:

    **[1\*]C&[1\*]C1=CC=C([2\*])C=C1&[2\*]C1=CC([3\*])=NN1[5\*]&[3\*]C([4\*])(F)F&[4\*]F\^[5\*]C1=CC=C([6\*])C=C1&&[6\*]S(N)(=O)=O&&&**

2.  TSDY\_M (replace [n\*] with \*):

    **\*C&\*C1=CC=C(\*)C=C1&\*C1=CC(\*)=NN1\*&\*C(\*)(F)F&\*F\^\*C1=CC=C(\*)C=C1&&\*S(N)(=O)=O&&&**

3.  TSSA\_M:

    **CC&C1=CC=CC=C1&CC&C1=C[NH]N=C1&CN&C1=CC=CC=C1\^CC\^CS&C&N[SH](=O)=O&CF&&&&FCF&&**

![](media/27e1e223138ebc4eec1aaa668ec07ad5.tiff)

![](media/f337effc42bf3fefb6a7e32a6a989fab.tiff)

![](media/1915cecce9d17ade54fa6572b2e03607.png)

![](media/8e0ee188e740fb80cee8334d8f5616c4.png)

Here we provide the source code of our method.

Dependencies
============

We recommend Anaconda to manage the version of Python and installed packages.

Please make sure the following packages are installed:

1.  Python**(version \>= 3.7)**

2.  [PyTorch](https://pytorch.org/)** (version == 1.7)**

>   \$ conda install pytorch torchvision cudatoolkit=x.x -c pytorch

>   Note: it depends on the GPU device and CUDA tookit

>   (x.x is the version of CUDA)

1.  [RDKit](https://www.rdkit.org/)** (version \>= 2020.03)**

>   \$ conda install -c rdkit rdkit

1.  Networkx**(version \>= 2.4)**

>   \$ pip install networkx

1.  [Numpy](https://numpy.org/)** (version \>= 1.19)**

>   \$ conda install numpy

1.  [Pandas](https://pandas.pydata.org/)** (version \>= 1.2.2)**

>   \$ conda install pandas

1.  [Matplotlib](https://matplotlib.org/)** (version \>= 2.0)**

>   \$ conda install matplotlib

Usage
=====

For designing the novel drug molecules with t-SMILES, you should do the
following steps sequentially by running scripts:

1.  **DataSet/Graph/CNJTMol.py**

>   preprocess()

>   It contained a preprocess function to generate t-SMILES from data set.

1.  **DataSet/Tokenlizer.py**

>   preprocess(delimiter=',', invalid\_token = '&', save\_split = False)

>   It defines a tokenizer tool which could be used to generate vocabulary of
>   t-SMILES and SMILES.

1.  **DataSet/Graph/CNJMolAssembler.py**

>   rebuild\_file()

>   It reconstructs molecules form t-SMILES to generate classical SMILES.

In this study, MolGPT, RNN, VAE, and AAE generative models are used for
evaluation.

Acknowledgement
===============

We thank the following Git repositories that gave me a lot of inspirations:

1.  GPT2: <https://github.com/samwisegamjeee/pytorch-transformers>

2.  MolGPT: https://github.com/devalab/molgpt

3.  MGM：https://github.com/nyu-dl/dl4chem-mgm

4.  JTVAE：[https](https://github.com/wengong-jin/icml18-jtnn)://github.com/wengon-jin/icml18-jtnn

5.  hgraph2graph: https://github.com/wengong-jin/hgraph2graph

6.  FragDGM: https://github.com/marcopodda/fragment-based-dgm

7.  Guacamol：<https://github.com/BenevolentAI/guacamol_baselines>

8.  MOSES: https://github.com/molecularsets/moses
