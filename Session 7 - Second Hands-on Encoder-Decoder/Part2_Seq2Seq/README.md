# 1. CMU Question Answer Dataset

http://www.cs.cmu.edu/~ark/QA-data/

## Data Preprocessing

* we have 3 `\t` files that contains useful data
```
File: /content/Question_Answer_Dataset_v1.2/S08/question_answer_pairs.txt; Shape: (1715, 6)
File: /content/Question_Answer_Dataset_v1.2/S09/question_answer_pairs.txt; Shape: (825, 6)
File: /content/Question_Answer_Dataset_v1.2/S10/question_answer_pairs.txt; Shape: (1458, 6)
```

**After merging these three files**

* Columns - `'ArticleTitle', 'Question', 'Answer', 'DifficultyFromQuestioner',
       'DifficultyFromAnswerer', 'ArticleFile'`
* Shape of final clean data : `(3998, 6)`

* Tokenized sample: 

`{'src': ['james', 'watt', 'was', 'born', 'where', '?'], 'trg': ['greenock', ',', 'a', 'seaport', 'on', 'the', 'firth', 'of', 'clyde']}`

## Train Valid Test Split [70:15:15]
* Number of training examples: `2395`
* Number of validation examples: `514`
* Number of testing examples: `513`

## Vocab
* Unique tokens in source (question) vocabulary: `1979`
* Unique tokens in target (answer) vocabulary: `1280`

# 2. Quora Question-Question Dataset

https://quoradata.quora.com/First-Quora-Dataset-Release-Question-Pairs

For seq2seq we take the samples where `is_duplicate` is `1`

## Data Preprocessing
* Columns : `['id', 'qid1', 'qid2', 'question1', 'question2', 'is_duplicate']`
* Shape of Trainable data : `(149263, 6)`
* Example After Tokenizatino: 

`'src': ['what', "'s", 'a', 'good', 'workout', 'program', 'and', 'a', 'diet', 'for', 'a', '14', 'year', 'old', 'male', '?'], 

'trg': ['what', "'s", 'a', 'great', 'workout', 'program', 'and', 'diet', 'for', 'a', '14', 'year', 'old', 'male', '?']}`

## Train Valid Test Split

* Number of training examples: `104484`
* Number of validation examples: `22390`
* Number of testing examples: `22389`

## Vocab
* Unique tokens in source (question1) vocabulary: 14522
* Unique tokens in target (question1) vocabulary: 14469

# Bonus Stuff
# 3. Quora Question-Question Dataset

https://nlp.cs.washington.edu/ambigqa/ : Light Version (1.1M QA)


## Data Preprocessing
* Data is in JSON format; Created a lazy function to parse `singelAnswer` and `multipleQAs` and then merge them to create full dataset.
* Example After Tokenization: 

`{'src': ['who', 'won', 'the', 'gold', 'medal', 'in', 'the', 'mixed', 'doubles', 'in', 'badminton', 'in', 'commonwealth', 'games', '2018', '?'],

'trg': ['chris', 'adcock', 'and', 'gabrielle', 'adcock']}`

## Train Valid Test Split

* Number of training examples: `15395`
* Number of validation examples: `3849`
* Number of testing examples: `4377`

## Vocab
* Unique tokens in source (question) vocabulary: `7164`
* Unique tokens in target (answer) vocabulary: `4430`
