# how to get a dataset lookup

## Train a RNN, then loop over with a text corpus to generate lookup table
model = Sequential()
model.add(LSTM(128, return_sequences=True, input_shape=(maxlen, len(words))))
model.add(Dropout(0.2))
model.add(LSTM(128, return_sequences=False))
model.add(Dropout(0.2))
model.add(Dense(len(words)))
model.add(Activation('softmax'))

model.compile(loss='categorical_crossentropy', optimizer=RMSprop(lr=0.002))
model.fit(X, y, batch_size=32, nb_epoch=10)

Model will be MBs or GBs in size and npm package would need to run inference lokally... Also need to package with tensorflow dependency. Too heavy

## Use word2vec to learn embeddings
use existing emoji lookup to find emoji per word. If word does not have assoicated emoji, use word2vec to find semantically similar words and try again
training my own word2vec is probably too hard due to data

## Use n-gram
Take learnings from creating search engine and apply it here

Tokenization: Split dataset sentences into words. Distinguish between emojis and words
n-grams: 
- unigram: each emoji becomes a unigram
- bigram: use each emoji as pointer and add 1 previous word
- n-gram: use each emoji as pointer and add N previous words


text that treat emojis as extra wordform is more valuable
text that include emojis gain "sense" and is part communication

emojis are usually treated as monosemous units. But, they are rather context-sensitive.
Fire emoji can mean physical attractiveness, heat, fire, congratulations etc...
A WordNet semantic structure can apply to emoji