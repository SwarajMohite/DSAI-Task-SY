#### Name - Swaraj Mohite

#### Branch - Computer Science and Engineering
---
#### Model Arch & core idea

* Problem: predict the chance of 6 types of toxicity for each comment
* One comment can have many labels, so it is a multi label problem
* Most comments are clean, so the data is very imbalanced
---
* Score used is mean ROC AUC over the 6 labels
  
* Preprocessing: filled empty comments with blank text
* Kept the text as it is, no stop word removal, no heavy cleaning to preserve the comments org
---  
* Turned text into numbers using TF-IDF
* Word features: single words and word pairs, 50000 features
* Character features: groups of 2 to 5 characters, 80000 features
* Joined both feature sets side by side into one big table

   ---
* Model: _Logistic Regression_ , one separate model for each of the 6 labels
* Each model gives a probability between 0 and 1 for its label
  
* Training: split data 80 percent train and 20 percent validation, same split every time
* Split was balanced on the toxic label so rare cases are in both parts
* Final model was trained again on all the training data to predict the test set
---  
* Baseline score was 0.976 on validation
* Leaderboard score was 0.9859
---
#### Differentiating ideas

* Added character features so the model can catch spelling tricks like idi0t and other
* Kept stop words like you and are, because they help find insults
* Used word pairs, so phrases like you are stupid are understood better

 ---
* Learned the word list from both train and test text so no test word is missed
* Tried class weights for imbalance, score went slightly down, so I did not use it
* as, ROC AUC only checks the ranking order so thought weights do not help much

   ---
* Tried averaging two models, no gain because both were almost the same
* Trained the 6 label models in parallel to save time
