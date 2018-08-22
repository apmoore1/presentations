# Visulising meaning: Modeling communication through simulations. -- Keynote

The main point of the talk is mixing gesture, vision and natural language processing. The example they gave is where somebody was telling a virtual avatar to move blocks around the virtual environment where the controls were speech and gestures.

# a
Event type task: Trying to predict some sort of semantic event descriptions that are within a text. There are 11 event types which break down into 8 needs and 3 issues.

This is easy in English which is a high resource language.

They have low resource and high resource data that is unlablled and labeled data in the high resource language, they also assume a bilingual dictionary between the two languages.

1. They get keywords in English and use a dictionary to translate them. They then expand the keywords by using TF.IDF scores.
2. They also make use of an adversial CNN model.

They find the keyword model to perform better than the adversial model. So they want to know how to combine these models.

They use the keyword model to create distantly supervised data for the Adversial model.

They find that bootstraping to make the largest difference Adding data in the domain/language you are testing in is that most important.

### Problems they have
They have the problem that the development set is not representative of the test set and therefore affects the model.

### My own thoughts
It is interesting how they use the more basic model to improve the Neural Network model showing that the they think that the Neural Network can learn more efficiently as in it has a lot of capacity
