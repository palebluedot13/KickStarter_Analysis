# KickStarter_Analysis

## Model Description
________________________________________
### Exploratory Analysis
To thoroughly explore all the instances we were given, we combined the provided training and test datasets. To create our training dataset, we combined the train x and train y into one dataset and binded the rest of the x variables from the test x dataset file. We also created a new column called original_TR to be able to filter our original training data from the original test data. The original training set has an original_TR value of 1, and the test set has a value of 0. Train_success will include all data without big_hit or backers_count and filter out all instances with NAs in the success column. We found that some variables had NULL values, so in our data cleaning, we dealt with these NA’s. 
Our data exploration also showed us that some of the frequency of unique values in each categorical data column was relatively small, and our model would benefit from binning the less common values together in a new value called “Other.” Combining similar categories such as “journalism” and “photography” helps us with converting common values together into binned variables (factors). 
Lastly, we created a correlation matrix (Figure 1), variable importance plot (Figure 3), and feature selection plot (Figure 2). Based on the correlation matrix, we decided to remove num_words, sentence_counter, and afinn_neg because these showed high correlation with other variables, and based on the variable importance plot, genre proved to not be important in predicting success. 


![image](https://user-images.githubusercontent.com/81589704/171780050-f9b12d7e-2935-4343-90ed-764a24bb29af.png)

Figure 1. Correlation Matrix


                                                            
![image](https://user-images.githubusercontent.com/81589704/171780074-40273341-dfae-4ff5-8ae7-6b866902d905.png)

Figure 2. Feature Selection Plot


![image](https://user-images.githubusercontent.com/81589704/171780090-3b829abc-9a7b-49d4-8ad2-80818889b312.png)

 Figure 3. Variable Importance Plot
                                                             
                                                             
                                                             

### Additional Variables Used
The following variables are the variables that we used, but we didn’t perform any feature engineering. goal, numfaces_project, numfaces_creator, male_project, male_creator, female_project, female_creator, smiling_project, smiling_creator, minage_project, minage_creator, maxage_project, maxage_creator, accent_color, avg_wordlengths, avgsentencelength, avgsyls, grade_level, affinn_pos, ADV, NOUN, ADP, PRT, DET, NUM, CONJ, ADJ.

### Holdout Process & Modeling
We utilized two different kinds of holdout processes. When selecting our final model for predictions, we split our original training data set into 70% for training data and 30% for validation data. This split was used on every model to compare accuracies and choose the best-performing model, as seen in Table 2. We found that XGBoost had the highest accuracy based on our split of the training data set. 
	For our best model, XGBoost, we implemented cross-validation for hyperparameter tuning, specifically for the argument nrounds/number of iterations. This process included using the function xgb.cv with 5 folds which returns the best number of iteration (nrounds) for the XGBoost model based on the highest score (log of AUC). 
Table 3 shows the performance improvement from features created from the unstructured text columns (blurb, caption, reward description) and external dataset (Dow Jones Industrial Average data). 
 
![image](https://user-images.githubusercontent.com/81589704/171780219-e79bced6-eea7-4cb0-ad19-282dd7f92355.png)

Table 2. Model Performance Comparison

![image](https://user-images.githubusercontent.com/81589704/171780231-66c53a27-4dec-4ecd-8859-67c75917e28c.png)

Table 3. Performance Improvement Comparison
 
 
![image](https://user-images.githubusercontent.com/81589704/171780242-c46c5879-bc9b-41ee-b8e9-be4f2e5fdd15.png)

Figure 4. Nrounds Accuracy Plot


![image](https://user-images.githubusercontent.com/81589704/171780247-ca234cbb-806f-44d5-947a-8cd66fe492db.png)

Figure 5. Max Depth Accuracy Plot 





## Conclusion
________________________________________
### Takeaways
Our group did well on working together to brainstorm new features to include in our model and delegating the work to clean the data, create the new features, and build our predictive models. It was a challenge to coordinate tasks and conduct meetings on a regular basis as every member had a different schedule and availability. We were able to utilize each person's skill set to create a model with high accuracy. Some members were more versed in data cleaning, others more familiar with building the models or feature engineering. 
One key challenge of the project was applying new concepts from class to our project. Since some feature engineering techniques were less familiar to us, it took longer to comprehend, write and implement the code. Additionally, the data set was very large, so we had to figure out how to test our code efficiently and adjust to different datasets between debugging and training our final model. Even though we were prepared to implement more models (like KNN), its lack of feasibility/time consumption led us to discard them. 
	If we were to do this project again, we would thoroughly comment on our code as we wrote it. Over the span of around a month, this project ended up requiring hundreds of lines of code, and it was easy to get lost in what we wrote before or the thought process behind it. This also helps your teammates to understand any changes to the code or for troubleshooting errors. However, one key change we would implement is to delegate the tasks more heavily and have a dedicated lead which would give a much needed structure to our project team. If we had more time to work on the project, we would further tune our hyperparameters and experiment with more feature engineering utlizing unsupervised learning methods. We also would’ve incorporated more than one external data set, such as geographic data or other crowdfunding websites, for additional information and features. 
	We got many important insights from this project. Most were affirmations of knowledge we had in theory, and some were new to us. Early on, we affirmed that methods like one-hot encoding (in our case for XGBoost) and feature split-binning would be an important part of this project. It helped us rescale the data and allowed representation of categorical data in a more expressive way, which in turn increases accuracy. It would not only help us prepare the proper input dataset which is compatible with our algorithm requirements but also help improve the performance of our models. Selecting the right hypertuning parameters also helped with increasing the accuracy of our models by minimizing the objective function over a dataset. We found some unique things in our models, such as how the length of blurb and caption columns is really useful. We also found that the description length of the captions and count of rewards also impacted our accuracy in a significant manner.
For students starting this project next year, we would tell them to regularly meet with your team (in-person would be quicker) and delegate work with specificity and urgency. Having teammates is extremely beneficial when your code isn’t working or brainstorming how to create a specific feature. 
	Our main business takeaways are that imperfect predictive information is better than just historical information, working as a team can create a better model, and each Kickstarter campaign has many different features that can contribute to the success of a project. Every approach in predictive analytics has an expected error. Improvements to the model are never-ending since a predictive model with 100% accuracy is impossible. However, we were able to derive new information from existing data that has the potential to help all stakeholders on Kickstarter. More money can be crowdfunded, and time can be saved with this new information. We also learned the value of working as a team. Different backgrounds and experiences allowed multiple perspectives on the problem, specifically during feature engineering. We were able to improve our model by coming up with new features to create every time we submitted our predictions. Through our developed model, knowing which feature variables contribute to the success of a campaign will help future users tailor their campaigns and reach their fundraising goals. 


