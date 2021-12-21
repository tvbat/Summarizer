
## General description of the system

1. **Preprocessing.** At the preprocessing stage, all images, tables, sentences with formulas, information about authors and bibliographic references are deleted from the source text. The author's abstracts are cut and saved separately so that we could evaluate the system afterwards, by means of comparing the result with the original abstract.

2. **Building topic models, extracting keywords and multi-word expressions.** _A topic_ is a set of words that describe a subject area. _A topic model_ is a set of topics. Topics are not known in advance, they are discovered during the work of the probabilistic algorithm.
_A unigram topic model_ is a model in which topics are described with one-word terms. However, sometimes we use expressions instead of single words. _A multi-word expression (MWE)_ is an established combination of several words. For example, _‘система линейных уравнений’ (‘linear equation system’), ‘обработка изображений’ (‘image processing’), ‘машинное обучение’ (‘machine learning’)_, etc. _An extended topic model_ is a model in which topics are described not only with one-word terms, but also with multi-word terms.
The algorithm of building extended topic models is described below.
   - Lemmatization.
   - Building a morphological dictionary using Mystem [Yandex, 2004, https://yandex.ru/dev/mystem/].
   - Extraction of n-grams of words. To extract MWEs from the texts, the Rapid Automatic Keyword Extraction algorithm (RAKE) [Rose S. et al., 2010] is used. 
   - Grammatical agreement. Since the MWEs consist of word stems and not of words in the grammatical agreement, we need to perform a backward operation of transforming those stems into consistent phrases.
   - Building unigram topic models using Additive Regularization for Topic Modeling (ARTM) [Vorontsov K.V. et al., 2015, https://github.com/bigartm/bigartm].
   - Building extended topic models.
   - Building a dictionary with weights using TF-IDF [Leskovec J. et al., 2014] for ranking topics.
   - Distribution of topics and key terms by document.

3. **Rhetorical analysis and text transformation.** The Rhetorical structure theory is one of the most widely used theories of text organization [W. Mann, C. Thompson, 1988]. According to it, initially, a text is divided into non-overlapping fragments, namely, elementary discursive units (EDUs). Two types of EDUs can be defined. One of them, _a nucleus_, is considered to be the most important part of an utterance, while the latter one, called _a satellite_, explains the nucleus and is considered to be secondary. In the proposed approach, rhetorical analysis is used to form a quasi-abstract. _A quasi-abstract_ is a list of the most significant sentences of a text. This stage can be described as follows. First, we find nuclear EDUs in the text. Further, statements containing these EDUs should be transformed so that an abridged text, intermediate between the original text and the final summary, is obtained. Discursive markers are used to define EDU boundaries, while actions are used to transform the text.
_Markers (discourse markers)_ are words or phrases that do not have any real lexical meaning; they have an important function to form the structure of a text. They are used to connect EDUs, organize and manage the authors’ intentions. During the research, we created a linguistic knowledge base that consists of 121 markers for the Russian language and stores information about 8 possible actions for them. Here are some of them.  
    - **_remove_keep:_** This action removes the forthcoming clause and keeps the clause with the given marker.
    - **_keep_remove:_** This action keeps the preceding clause and removes the clause with the given marker.

4. **Evaluation of sentence weights.** The weight of each sentence of the quasi-abstract is calculated depending on whether it contains key terms, markers, and some special lexicon that are often found in scientific and technical texts and stored in a linguistic knowledge base.

5. **Sentence selection.** From the obtained set of sentences (see item 3), only those whose weight exceeds a predetermined threshold value (see item 4) are selected for the summary.

6. **Smoothing** makes the resulting abstract more coherent and readable. Smoothing replaces some words with ones that are more suitable, or removes them whatsoever.

## Acknowledgement

The study was funded by RFBR according to the research project N 19-07-01134.


## How to Cite

If you extend or use this work, please cite the [paper](https://www.researchgate.net/profile/Tatiana-Batura/publication/341369997_METHOD_FOR_AUTOMATIC_TEXT_SUMMARIZATION_BASED_ON_RHETORICAL_ANALYSIS_AND_TOPIC_MODELING/links/5ebcd2f7299bf1c09abbd54d/METHOD-FOR-AUTOMATIC-TEXT-SUMMARIZATION-BASED-ON-RHETORICAL-ANALYSIS-AND-TOPIC-MODELING.pdf) where it was introduced:
```
@article{batura2020method,
  title={A method for automatic text summarization based on rhetorical analysis and topic models},
  author={Batura, Tatiana and Bakiyeva, Aigerim and Charintseva, Maria},
  journal={International Journal of Computing},
  volume={19},
  number={1},
  pages={118--127},
  year={2020}
}
```
