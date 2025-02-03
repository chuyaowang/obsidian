# The Gauss-Markov Theorem

The Gauss-Markov theorem, also known as the Gauss-Markov assumptions or the Gauss-Markov conditions, is a fundamental concept in the field of statistics and econometrics. It provides conditions under which the Ordinary Least Squares (OLS) method is the Best Linear Unbiased Estimator (BLUE) of the parameters in a [Linear Regression](2.%20UDL%20Supervised%20Learning.md#Linear%20Regression) model. In simpler terms, it establishes the conditions under which OLS estimates are unbiased, have the minimum variance among all linear estimators, and are normally distributed.

The Gauss-Markov theorem assumes the following conditions for a linear regression model:

1. Linearity: The relationship between the dependent variable (Y) and the independent variables (X1, X2, ..., Xk) is linear.

2. Independence of errors: The errors (residuals) of the model (ε) are independent of each other. This means that the error in predicting one observation is not related to the error in predicting any other observation.

3. Homoscedasticity: The variance of the errors is constant across all levels of the independent variables. In other words, the spread of the errors should remain roughly the same for all values of the independent variables.

4. No perfect multicollinearity: There should be no exact linear relationship among the independent variables. This means that you cannot express one independent variable as a perfect linear combination of the others.

5. Zero conditional mean: The expected value (mean) of the error term is zero given any values of the independent variables. This condition is also known as the strict exogeneity condition.

Mathematically, the Gauss-Markov theorem states that if these conditions are met, then the OLS estimators of the coefficients in a linear regression model are:

- Unbiased: The expected value of the OLS estimators equals the true population parameters.

- Efficient: Among all linear unbiased estimators, OLS has the minimum variance, making it the most precise estimator.

- Normally Distributed: The OLS estimators are approximately normally distributed, especially for large sample sizes, due to the Central Limit Theorem.

Example:
Suppose you want to predict a student's final exam score (Y) based on their study hours (X1) and the number of practice tests they took (X2). You collect data from 100 students and run a linear regression:

Y = β0 + β1X1 + β2X2 + ε

Here, β0, β1, and β2 are the population parameters you want to estimate using OLS. The Gauss-Markov theorem applies if the following assumptions are met:

1. Linearity: The relationship between study hours, practice tests, and exam score is linear.

2. Independence of errors: The errors (ε) are independent, meaning the error in predicting one student's score is not influenced by the error in predicting another student's score.

3. Homoscedasticity: The spread of errors remains constant for all levels of study hours and practice tests.

4. No perfect multicollinearity: Study hours and practice tests are not perfectly correlated.

5. Zero conditional mean: The expected value of the error term is zero given any values of study hours and practice tests.

If all these conditions are met, then the OLS estimates of β0, β1, and β2 will be unbiased, efficient, and approximately normally distributed, making them the best linear unbiased estimators of the population parameters in this regression model.