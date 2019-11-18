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

