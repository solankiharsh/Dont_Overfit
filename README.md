# Dont_Overfit
Avoid overfitting with a tiny sliver for training data  

Inspired by the Kaggle Don’t Overfit Challenge: Tiny Training Trial. 

The challenge; build the best performing model you can with a &lt;5% training vs >95% test split with TF-IDF encodings on an Amazon multi-classification problem. 

With so many data hungry algorithms out there that take days or more to compute, we thought it’d be refreshing to go the other way and experiment with what can be done with extremely small and noisy datasets! Iterate and experiment with training times on the order of seconds. 

Our split is:  Train: 1244 points  

Approach overview  

•Build Ensemble that includes multiple model categories: Logistic Regression, Random Forests, XGBoost, Adaboost, and Neural Networks.  
•Split the training dataset into K stratified folds. For each fold and model category, train a separate model using Grid Search.  
•Combine all models into ensemble using Averaging.  

I experimented with:  

1.Which model categories to include in the ensemble 
2.How many stratified folds to use: 1, 5, 10, 20, 40 
3.How to build the ensemble: Averaging vs. Max voting 
4.Oversampling techniques such as SMOTE and ADASYN: including models trained with SMOTE data in the ensemble worked for the Public leaderboad, but not for Private 5.Feature standardization: did not seem to improve anything.  

Lessons Learned  

1. Ensembling is the way to go, of course. 
2. Increasing the number of stratified folds improved performance. 
3. Improvements in training data accuracy (on validation set) did not necessarrily translate to better accuracies in the Public dataset. A prime example for this was the LR method that did not perform as well in the training validation accuracy compared to other methods such as NN. 
However, LR was an integral part of the overall Ensemble; whenever we removed it, the Public dataset accuracy ended up much worse. 
4. Ensembling using Averaging always worked better than Max voting. We kind of `overfitted' to the Public Leaderboard, i.e., our best performing model in Public was not the best in Private. 
5. Adding models trained with oversampled data, using either SMOTE or ADASYN, decreased accuracy in Private dataset. 
6. Gini impurity appeared to work better than Entropy for tree-based models.
