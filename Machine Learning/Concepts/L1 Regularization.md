# L1 Regression

Note that the [L2](L2%20Regularization.md) penalty shrinks coefficients towards zero but never to absolute zero; although model feature weights may become negligibly small, they never equal zero in ridge regression. Reducing a coefficient to zero effectively removes the paired predictor from the model. This is called feature selection, which is another means of correcting multicollinearity.[8](https://www.ibm.com/topics/ridge-regression#f8) Because ridge regression does not reduce regression coefficients to zero, it does not perform feature selection.[9](https://www.ibm.com/topics/ridge-regression#f9) This is often cited as a disadvantage of ridge regression. Moreover, another oft-cited disadvantage is ridge regression’s inability to separate predictor effects in the face of severe multicollinearity.[10](https://www.ibm.com/topics/ridge-regression#f10)

Lasso regression—also called L1 regularization—is one of several other regularization methods in linear regression. L1 regularization works by reducing coefficients to zero, essentially eliminating those independent variables from the model. Both lasso regression and ridge regression thus reduce model complexity, albeit by different means. Lasso regression reduces the number of independent variables affecting the output. Ridge regression reduces the weight each independent variable has on the output.

Elastic net is an additional form of regularization. Whereas ridge regression obtains its regularization parameter from the sum of squared errors and lasso obtains its own from the sum of the absolute value of errors, Elastic net incorporates both regularization parameters into the [RSS](Residual%20Sum%20of%20Squares.md) cost function.[11](https://www.ibm.com/topics/ridge-regression#f11)

Principal componenet regression (PCR) can also act as a regularizing procedure. While PCR can resolve multicollinearity, it does not do so by enforcing a penalty on the RSS function as in ridge and lasso regression. Rather PCR produces linear combinations of correlated predictors from which to create a new least squares model.