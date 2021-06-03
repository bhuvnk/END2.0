## Building Sentiment Classifier using LSTM

### Data Overview 

StanfordSentimentAnalysis Dataset is considered to build the LSTM Model 

Used `pytreebank` to convert downloaded data into train, test and validation sets

with around 70 | 10 | 20 split

### Data Augmentation

Performed data augmentation with these techniques:

**Back Translation**

Used google translate api to convert around 2000 samples into a random language and convert it back to english.

The slow nature of this application was dreadful.

**Radom swap**

We take a sentence and swap words within it `n` times. with each iteration working on previously swapped sentence. Below code explains how slow this process can be.

```python
def random_swap(sentence, n=5): 
    length = range(len(sentence)) 
    for _ in range(n):
        idx1, idx2 = random.sample(length, 2)
        sentence[idx1], sentence[idx2] = sentence[idx2], sentence[idx1] 
    return sentence
```

**Random Deletion**

We randomly delete words from a sentence. Feels quite similar to cut-out used in CNNs.

Given a probability parameter p, it will go through the sentence and decide whether to delete a word or not based on that random probability. 

```python
def random_deletion(words, p=0.5): 
    if len(words) == 1: # return if single word
        return words
    remaining = list(filter(lambda x: random.uniform(0,1) > p,words)) 
    if len(remaining) == 0: # if not left, sample a random word
        return [random.choice(words)] 
    else:
        return remaining
```
These augmentations were applied on the training data and and 50% sample was taken from the data.

### Data Preparation

**Built a vocabulary** on sentences and lables and for reviews using pretrained emmbeddings
*Convert into iterators for training*

### Model Architecture 

1. Input : emmbeddings layer with 256 hidden dimention
2. 2 stacked-LSTMs with 256 hidden features with a drop out function
3. output : fully connected : 5

Model summary and parameters 

```
classifier(
  (embedding): Embedding(18686, 256)
  (encoder): LSTM(256, 256, num_layers=2, batch_first=True, dropout=0.5)
  (fc): Linear(in_features=256, out_features=5, bias=True)
)
The model has 5,837,573 trainable parameters
```

### Training Parameters

| Embedding DIM  |  256  |

| HIDDEN DIM     |  256  |

| NUM LAYERS     |   2   |

| DROUP OUT      |  0.5  |

| BATCH SIZE     |  128   |

| LR             | 2.e-4 |

### Training logs

**Model is trained for 30 epochs**

```
	 epoch : 24 |	Train Loss: 1.027 | Train Acc: 88.48%
	 Val. Loss: 1.584 |  Val. Acc: 30.52% 

	 epoch : 25 |	Train Loss: 1.026 | Train Acc: 88.58%
	 Val. Loss: 1.563 |  Val. Acc: 33.04% 

	 epoch : 26 |	Train Loss: 1.022 | Train Acc: 89.00%
	 Val. Loss: 1.566 |  Val. Acc: 33.04% 

	 epoch : 27 |	Train Loss: 1.015 | Train Acc: 89.59%
	 Val. Loss: 1.591 |  Val. Acc: 30.11% 

	 epoch : 28 |	Train Loss: 1.013 | Train Acc: 89.64%
	 Val. Loss: 1.592 |  Val. Acc: 29.27% 

	 epoch : 29 |	Train Loss: 1.010 | Train Acc: 89.94%
	 Val. Loss: 1.594 |  Val. Acc: 29.56% 
```

**Model Evaluation Test data** 

```
Test Loss: 1.546 | Test Acc: 33.14%
```

**A couple of predictions**

```
Input: Effective but too - tepid biopic, 
 	 label : 3 	 predicted : 1 

Input: If you sometimes like to go to the movies to have fun , Wasabi is a good place to start ., 
 	 label : 4 	 predicted : 2 

Input: Emerges as something rare , an issue movie that 's so honest and keenly observed that it does n't feel like one ., 
 	 label : 5 	 predicted : 1 

Input: The film provides some great insight into the neurotic mindset of all comics -- even those who have reached the absolute top of the game ., 
 	 label : 3 	 predicted : 0 

Input: Offers that rare combination of entertainment and education ., 
 	 label : 5 	 predicted : 0 

Input: Perhaps no picture ever made has more literally showed that the road to hell is paved with good intentions ., 
 	 label : 4 	 predicted : 1 

Input: Steers turns in a snappy screenplay that curls at the edges ; it 's so clever you want to hate it ., 
 	 label : 4 	 predicted : 0 

Input: But he somehow pulls it off ., 
 	 label : 4 	 predicted : 1 

Input: Take Care of My Cat offers a refreshingly different slice of Asian cinema ., 
 	 label : 4 	 predicted : 0 

Input: This is a film well worth seeing , talking and singing heads and all ., 
 	 label : 5 	 predicted : 1 
```


## TODO
Improve it before the assignment gets graded.
