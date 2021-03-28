# HatefulTwitter
This readme contains a description of the Keras model in Jupytor notebook. 
## Preprocessing
Preprocessing is done in the following steps:
### 1. Removing RT, Mentions and URL
RT and mentions did not add any context to the tweets. As URL was mosly in the twitter shortened form, it also added no context. Hence they are all removed.

### 2. Removing punctuations and stopwords, followed by stemming
These processes were done after each tweets were tokenised. The tweets were then reconstructed after the process.

#### 2.1. Removing punctuations
Punctuations are removed to better focus on the words of the tweets.

#### 2.2. Removing stop words
Stop words are common words that are used in everyday context, hence their usage have little relavence to the categorisation of the tweets. However, certain stop words are retained, like gendered pronouns (to weed out sexist tweets) and negative stop words (in case they negate certain words the tweet contain)

### 2.3. Stemming
Stemming aims to regularise words into their base form. This would decrease the number of words in the model's dictionary, which would decrease overfitting and biaseness.

### 3. Tokenising
The reassembled tweets were then tokenised by Kera's tokeniser. This was done instead of the NLTK tokenising used previously because it allowed easy counting of the frequency of the words.

### 4. Creation of word index and sequensing
Words that appeard at least twice were then added into a word index. The word index was than used to sequence the tweet, converting it into a form that was ready to be handled by Keras. The word index is also saved into a separate file so that it can be used in future applications of the model.

### 5. Processing of labels
The labels were first factorised and converted into a matrix representing each label ready for input into Keras.

## Model settings
This section describes the settings used in the structure and fitting of the Keras model. 

### 1. Structure settings
The model consists of 3 layers with decreasing number of nodes (from 512 to 3). The number of nodes in the easlier sections can be optimised using the number and nature of the inputs, but the last layer has to have 3 nodes because that is the number of categories available. The activation (relu, sigmoid and softmax) describes how the data is transformed by the node. Softmax is required at the last node as it is a categorising model. 

The dropout between layers describes the amount of randomness intruduced into the model to prevent over fitting.

Lastly, the loss of the model is set to 'categorical_crossentropy' as it is a categorical model. The metrics of optimisaiton is set to accuracy to better to choose settings that optimsise accuracy.

### 2. Fittings settings
The training data is first split into 32 parts for testing in each epoch. This model was fitted for 5 epochs. 

## Result analysis and improvements
While the training accuracy was very high at 96%, the testing accuracy was much lower at 76%. This tells us that the model was heavily overfitted.

Here are some ways which the models can be optimised:

### 1. Stop word selection
While negative stop words are not removed, their original counterparts continue to be removed. 

### 2. Word index criteria
There remain words that appear very infrequently in the word index. A better way to optimise this would be to study the distribution of the word frequency to cut out less frequently used words.

### 3. Structure of the Keras model
The Keras model is highly flexible, and accordingly there are many ways it could be better optimised. Low hanging fruits include increasing the number of layers, changing the number of nodes and the activation settings.

(I also need to read more about this. Haha)