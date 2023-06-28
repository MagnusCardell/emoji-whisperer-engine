## Engine for the emoji whisperer npm package
Building a search engine for emojis

1. Index the corpus

term - token

term - emoji index. A sparse matrix with true/false if emoji appears with term
inverted index - dictionary of terms, and a list of their appearances (emojis)

Building index:
1. collect documents (sentences with emojis)
2. tokenize the documents
3. preprocess the tokens. lowercase, cleanup, english
4. Index documents with inverted index

Each emoji has unique ID
Maintain dictionary and postings
dictionary - emoji and pointer to document its from
postings - inverted index [emoji, frequency in doc, [docID1, docID2]]


Boolean query Happy AND Sad
Answer set rank emojis that has both happy and sad, otherwise, happy then sad, depending on frequency. 

Tokenization
- lowercase might be bad for emojis because we need to keep names apart from words (General Motors)
- stemming and lemmatization - Porter algorithm

Intersection algorithm for Happy and Sad is O(n+m) where n and m are number of occurrences 

Tolerant retrieval
Wildcard searches like re*val would need to use re AND val. for those searches, 
k-gram index woudl help
phonetic correction
lehvenstein distance


Index compression
Possibly 75% less storage
Allow use of caching frequently used terms and 
Rule of 30 - the 30 most common words account for 30% of the tokens in text. 
In the postings list, the term is the most space needed. Instead of using the emoji, use a pointer to the emoji


Scoring, term weighting, vector space model 

example
```
input = 'my flight was amazing'

Top scoring emoji for word 'flight': 😢
Top scoring emoji for word 'amazing': 😊
Top scoring emoji overall 🙏
```