# Insurance-Data-analysis
A project which was done to learn R and other related theoretical statistical regression 

## Abstract
In this document I have explored the “InsuranceCost” dataset for the target variable of annual insurance cost (Charge) related to other given parameter variables. Initial exploratory analysis showed the relations between each variable related to the predictor variable and therefore further analysis were done to identify the quantifiable associations between variables using Analysis of variance model. Based on the correlation outputs of predictor variables important variables and interaction terms were selects. Using the outcomes of those analysis a model was built which can explain the Insurance cost with about 85% R squared value.

## Introduction
During these times of pandemic, obtaining an insurance has become an important decision for many people who weren’t interested in such option before. But due to various concerns involving the factors insurance companies consider before giving the insurance, people hesitated to obtain an insurance. But since having an insurance seemingly becoming an interesting option, in this study I am hoping to analyze one important aspect in this insurance selection, the cost. Usually, to determine the payment which the people required to pay to the insurance company, insurance agents use various parameters such as person’s current health, habits, income, family background etc. In this study I am hoping to understand the relationship between such parameters and Insurance cost. Also, I will be consider fitting a mathematical model to the obtained dataset which can be used to predict the possible payment cost which a person may required to pay for the insurance company.

## Methodology
To carry out the above tasks, following statistical techniques were used. 
First, for all the random variables exploratory analysis was done, scatter plots were graphed to visually identify the existing relationships with the target variable “Insurance Cost”. 
Then to get the numerical verification of variable significance full factorial Analysis of Variance (ANOVA) has been done for all the variables related to the aforementioned predictor variable.
Then based on above result a preliminary Linear Regression model has been fitted to get the base line model and to identify the base performance. Afterwards using the “Leaps” R library I have selected the best subset of random variables that provides highest adjusted R squared value and fitted a new linear model.
Finally in the analysis and conclusion section all the results obtained were discussed and summarized.

## Explanatory Analysis
--Note all the experiments were done on a training set with 80% of data from original data set.
During the initial exploration of the dataset, we can see that there are 6 variables including the target variable “Charge”.
 
![image](https://user-images.githubusercontent.com/22634281/143720051-2f68e244-fcc8-41d9-9b2a-59167f450cd7.png)
 

When considering the above data, we can see that the gender, smoker and region variables acts as categorical variables. Interestingly children column has values which seemingly look like categorical. Below shows data distribution of Children column.
![image](https://user-images.githubusercontent.com/22634281/143720052-4facd1d9-fa09-4547-9510-476ff67c7303.png)

As we can see maximum value of children is 5 and mean value is close to 1. Therefore, in this analysis it is safe to use consider this as a categorical value rather than a numerical value due to its applicability.
For other variables descriptive details are as follows.
![image](https://user-images.githubusercontent.com/22634281/143720056-2f08a446-0da2-42fa-9070-cd74fbc23b7f.png)



(n = number of values excluding missing values, na = number of missing values. sd = Standard deviation, se_mean = Standard error mean, IQR = Inter Quartile Range)

Then for the all the numerical data, normality test (Shapiro-Wilk test) was done to check the normality assumption which is important for the inferencing related to Linear regression models.
 ![image](https://user-images.githubusercontent.com/22634281/143720059-06ad3429-b3f6-470b-8920-2b8188722248.png)


According to the above test we can see that all the numerical variables do obey the normality assumption with a very significant confidence level according to the p values.

![image](https://user-images.githubusercontent.com/22634281/143720071-dde6ae57-e69f-409f-94ca-78e2c281d1c7.png)
![image](https://user-images.githubusercontent.com/22634281/143720074-ed1b3c16-1dd9-4389-9a7c-5c2bab2dac2c.png)




According to the graphs BMI follows a near perfect normal distribution but age is bit deviating according to the Q-Q plot. But this can be understandable since insurance cannot be obtained by underage people and it is hard to get insurance to older people. Therefore, it is safe to assume the normality for age as well.
Below include the scatter plots representing relationships between target and predictor variables.

![image](https://user-images.githubusercontent.com/22634281/143720079-5ad94d33-071f-429b-96b3-5b566aaa69e6.png)
![image](https://user-images.githubusercontent.com/22634281/143720081-878d2162-61df-4cb1-92ee-667a0f8f55bf.png)






## Advanced Analysis
As the first step we will consider the ANOVA for all variables to identify the correlations between each variable as it is an important factor in modelling. The interactions between main effects suggests that all the predictors are significant compared to region and gender at 5% level.
(Charge=Age+BMI+Smoker+Region+Gender+Childrens)
![image](https://user-images.githubusercontent.com/22634281/143720084-e7117fe0-60b0-4861-85a0-96af2bd2e8dd.png)





When we consider the base model with only the main effects the model performance is as follows.
 ![image](https://user-images.githubusercontent.com/22634281/143720085-0ed81abb-865f-4a5c-95e1-ffaee17d8588.png)
![image](https://user-images.githubusercontent.com/22634281/143720086-30be04a1-0da3-4ba6-af11-bf41ef367819.png)

This base model was able to explain the 76% of training dataset variance according to the adjusted R squared values.
But with further analysis with Anova for full factorial suggested that following interactions were significant at 5% level as well.
Variable	DF	Sum Sq	Mean Sq	F Value	Pr(> F)	
Age	1	1.018e+10	1.018e+10	488.571	<2e-16	***
BMI	1	4.617e+09	4.617e+09	221.654	<2e-16	***
Smoker	1	8.806e+10	8.806e+10	4227.795	<2e-16	***
Region	3	2.417e+08	8.057e+07	3.868	0.009240	**
Childrens	5	4.620e+08	9.239e+07	4.436	0.000552	***
BMI:Smoker	1	1.246e+10	1.246e+10	598.395	<2e-16	***
BMI:Region	3	1.747e+08	5.825e+07	2.796	0.039403	*
BMI:Smoker:Region	3	1.721e+08	5.736e+07	2.754	0.041709	*
Age:Region:Childrens	14	6.268e+08	4.477e+07	2.149	0.008370	**
Smoker:Region:Childrens	9	4.184e+08	4.649e+07	2.232	0.018531	*
Age:BMI:Smoker:Childrens	3	1.731e+08	5.771e+07	2.771	0.040772	*

But with the usage of interaction terms along with the hierarchical principle we can obtain a model with outperform the basic model which can explain the variance of the training dataset up to 86%. (Did not used leaps library to perform subset analysis due to computation complexity)

![image](https://user-images.githubusercontent.com/22634281/143720089-f6222de5-3828-4d8f-84bf-f95fff9f028b.png)
![image](https://user-images.githubusercontent.com/22634281/143720092-1a0988f7-b303-48c9-b8d4-02bafb9824ba.png)



This may happen due to overfitting to training dataset which get confirmed by the comparison of residual mean squared error between base model (6480.319) and above model (6516.65).
Therefore, finetuning the model by removing few interaction terms (backward elimination) following model was obtained which provided much better results for the training set while eliminating the overfitting effect.
Final Model:
Charge = Age+BMI+Smoker+Region+Childrens+BMI*Smoker+BMI*Region+Smoker*Region+Age*Region + Intercept
![image](https://user-images.githubusercontent.com/22634281/143720097-6d245e6d-1ac0-4b9b-862e-47576bbf8886.png)
![image](https://user-images.githubusercontent.com/22634281/143720099-29613ff2-0635-4843-8c11-b062040a8e0c.png)

## Conclusion and Discussion

This model provides an adjusted R squared value which translate to 85% variance of the training data set while maintaining a considerably low residual mean squared error of 5359.454 compared to base model 6480.319.

In this analysis, based on the initial exploratory analysis and secondary analysis I identified the factors and interactions that could accurately model the Insurance Cost. Even though the main interactions showed that region was not significant at 5% level, factorial analysis showed the significance of it with the help of interactions between other variables which helped to build a significantly better model (by 10%) compared to the base model.
One of the main problems encountered during the advanced analysis phase was variable subset identification. But due to complexity when running leaps subset function it takes considerable amount of time. Also, one interesting observation was significance of predictor variable “Region” which was not significant in main effect analysis but became significant with the association of other variables.



## Refences
https://towardsdatascience.com/selecting-the-best-predictors-for-linear-regression-in-r-f385bf3d93e9

https://www.statology.org/linear-regression-assumptions/

https://www.r-bloggers.com/2013/08/exploratory-data-analysis-useful-r-functions-for-exploring-a-data-frame/

https://cran.r-project.org/web/packages/dlookr/vignettes/EDA.html

https://cran.r-project.org/web/packages/dlookr/vignettes/transformation.html

https://towardsdatascience.com/q-q-plots-explained-5aa8495426c0
