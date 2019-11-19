# Semantic Search on CDTN

## Introduction

Currently the semantic search algorithm is based on the [USE-QA](https://ai.googleblog.com/2019/07/multilingual-universal-sentence-encoder.html) a google algorithm based on semantic similarity for semantic retrieval [[paper]](https://arxiv.org/abs/1907.04307) [[tf-hub]](https://tfhub.dev/google/universal-sentence-encoder-multilingual-qa/2).

The objective is to suggest a list of documents from a user query, based on semantic distance as computed with cosine-similarity.


### indexing:

The indexing is based on this [script](https://github.com/SocialGouv/code-du-travail-numerique/blob/master/packages/code-du-travail-nlp/scripts/dump.py)
- the possible answers `response_encoder` `text` are the titles of documents. 
- the `context` placeholder is fed with the document text.

The Preprocessing is identical for indexing and querying (remove stop words - lowercase - strip accents).

### Querying

The querying is performed with [this endpoint](https://github.com/SocialGouv/code-du-travail-numerique/blob/master/packages/code-du-travail-nlp/api/search.py)



### Model Selection & Evaluation:

The selection of this model has been made based on evaluation set made of [experts scores of query - documents pairs](https://datafiller.num.social.gouv.fr/)

we generate learning to rank [(letor)](https://github.com/ArmandGiraud/letor_scores) scores based on the slug list returned by:
1) the semantic algorithm
2) the semantic + the BM25 deduplicated

we use a harmonic average of NDCG and MRR.

Many model types have been evaluated:
- [StarSpace](https://github.com/facebookresearch/StarSpace)
- [StarSpace custom]() (repo not available yet)
- USE standard


#### Sentence embedding average/composition:

- fasttext (finetuned or not)
- [flair Emeddings](https://github.com/zalandoresearch/flair/blob/master/resources/docs/TUTORIAL_5_DOCUMENT_EMBEDDINGS.md) finetuned or not
- [Bert Multilingual](https://github.com/hanxiao/bert-as-service) - finetuned or not
- [Flair RNN](https://github.com/zalandoresearch/flair/blob/31cc245f45b38dbbc4ddfc0214a2761a45b2b3a9/flair/models/similarity_learning_model.py) (fine-tuned on semantic similarity)
- seq to seq projection (as in)[search from code] (https://github.blog/2018-09-18-towards-natural-language-semantic-code-search/)


