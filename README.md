## Credit_line_Extension_prediction

### Business Case: LoanTap Logistic Regression

#### Problem Statement:

LoanTap is an online platform committed to delivering customized loan products to millennials. They innovate in an otherwise dull loan segment, to deliver instant, flexible loans on consumer friendly terms to salaried professionals and businessmen.

The data science team at LoanTap is building an underwriting layer to determine the creditworthiness of MSMEs as well as individuals.

LoanTap deploys formal credit to salaried individuals and businesses 4 main financial instruments:

1. Personal Loan
2. EMI Free Loan
3. Personal Overdraft
4. Advance Salary Loan

This case study will focus on the underwriting process behind Personal Loan only

Given a set of attributes for an Individual, determine if a credit line should be extended to them. If so, what should the repayment terms be in business recommendations?

#### Solution: EDA | ML model building

LoanTap is an online platform committed to delivering customized loan products to millennials. They innovate in an otherwise dull loan segment, to deliver instant, flexible loans on consumer friendly terms to salaried professionals and businessmen. The data science team at LoanTap is building an underwriting layer to determine the creditworthiness of MSMEs as well as individuals. This case study will focus on the underwriting process behind Personal Loan only.

As per the business problem, the company wants to know if a credit line should be extended to individuals. If so, what should the repayment terms?

It was a simple data frame which had almost sufficient features corresponding to each individual in each row which can act as predictors in classifying the target variable which is loan status in this case. Missing values were found in few of the features. They were treated with mode imputation. Outlier treatment was also done using IQR method. 

With the given data, I was able to draft certain observations which can help LoanTap in their growth as a company. I also created a Logistic regression model which can classify whether an individual will fully pay the loan or be charged off based on a set of attributes. 

1. I started with the basic EDA. The data set which was given to us had the values with data types as integer, object or float. Loan status is the target variable. The independent features reflected some of the important attributes of individuals which can help predict the target variable.
2. Firstly, EDA was done on all the continuous features. Every distribution was right skewed. Most of our loan amounts are as low as 5000 to 10000. We need to start attracting more individuals and provide more incentives or offers if they opt for higher loan amounts. Higher the loan amounts, higher is the revenue. In addition to this, we have to start attracting people with higher salaries. Higher the salary, higher is the loan amount they request. Also, higher the annual income, higher is the chances of avoiding unpaid loans. Interest rates seem to be higher for loans which were charged off. To avoid unpaid loans, we can decrease our interest rates and keep it between 10 to 15 with 15 as the maximum. 
3. For EDA on categorical variables, I could see that enormous number of loans were given for the purpose of debt consolidation. I would consider this as a threat as individuals are taking more loans to repay their existing loans. I would recommend to consider other factors very seriously before giving out loans for this purpose. Also, more loans are given to employees with only 10+ years of experience. I actually found no relation between loan status and years of experience. Hence, we can also start providing loans to employees with little experience too. 
4. I also found a drastic decrease in the loans issued after 2015. The total count decreased from 90000 to 30000. We need to advertise more about our loan products. For the next few months, we can roll out new offers and incentives to attract more people to take loans. 
5. I also did multivariate analysis using heat map on spearman correlation coefficients. I dropped few predictors which had high correlation coefficient with among each other. 
After EDA, I started with preparing my data set for modelling. Split was performed. I used ridge Logistic regression to classify my target variable. 1 - Fully paid, 0 - Charged off. Precision was my important metric as I wanted to decrease my false positives. Would not want to increase line of credit for non creditworthy individuals.
6. I trained my model on training set and tuned it on validation set using its precision score. Once tuned, I tested the model on test data set, where the score came out to be very good which is 0.9(approx.). 
7. Since, we had so many features in training data set, I checked feature importance and dropped many features which were absolutely unnecessary. In the end with just 5 features, I got a precision score of 0.89 and recall score of 0.70 on test data set. 
ROC curve was plotted. AUC was found to be 0.69. which is better than the random model(0.5 AUC), but not the best obviously. Also, there was a huge class imbalance in test data set. Due to this AUC-ROC doesn't work.
8. PRC works even if there is an unbalance. AUC was found to be 0.87 across all the thresholds which was very good. 
From the confusion matrix, I could see that type2 error is very high as compared to type 1 error. We might lose good customers, but we will not be at# a loss by giving loans to non credit worthy customers.
9. In my case, I have defined 1 as fully paid and 0 as charged off. Hence, type1 error (False postive) is Model has falsely predicted that an individual will fully pay the loan amount and type2 error (False negative) is Model has falsely predicted that an individual will be charged off. If I want to generate more revenue or not lose out on an opportunity to finance more individuals and earn interest on it, I will decrease my false negatives using Recall score. I will tune my model until I get the best recall score.
10. To avoid NPA's in the future,  we can tune our model on precision score such that there lesser false positives.

To whoever reads this, I hope my insights and recommendations from this case study were meaningful.

Thank you,

Krishna