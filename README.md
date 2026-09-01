# Team Name: Assumption Junction

## Contributors
- Ammy Lin: Linear Regression
- Farnoosh Memari: Logistic Regression
- Tonantzin Real Rojas: Generalized Additive Model (GAM)

## Dataset
This project uses the Telco Customer Churn dataset, which contains information about customers in a telecommunications company, including demographics, account information, services used, tenure, monthly charges, and total charges. The goal is to predict whether a customer is likely to churn, meaning that they discontinue their service.

We compare three interpretable modeling approaches—linear regression, logistic regression, and a generalized additive model (GAM)—to evaluate both predictive performance and interpretability. A major focus of the project is to check whether the assumptions behind each model are reasonably satisfied for meaningful business interpretation.

## Assumption Checks

| Model | Key Assumptions Checked | Evidence | Concern |
|---|---|---|---|
| Linear regression | Linearity, independence, homoscedasticity, normality, multicollinearity, influential outliers | Durbin-Watson statistic was approximately 1.9932, suggesting little evidence of autocorrelation; the residual plot showed no strong systematic pattern; fanning shape indicated heteroscedasticity (p < 0.001); Q-Q plot showed heavy tails and non-normal residuals; VIFs were moderate and Cook's distance suggested no extreme outliers | The model does not fully satisfy the usual linear regression assumptions. In particular, residual variance is not constant, and the residuals are not close to normal. This makes the model less reliable for formal statistical inference and not appropriate for actual churn classification |
| Logistic regression | Pending team analysis | Pending final team results | Pending final team results |
| GAM | Nonlinearity, model fit, smooth-term interpretation | The GAM achieved ROC-AUC = 0.8476 and accuracy = 0.8027, suggesting strong discriminative power for churn risk; smooth terms allow nonlinear relationships to be modeled while remaining interpretable | GAMs are more complex than linear coefficients and require careful tuning of smoothness parameters; results still need additional out-of-sample validation |

## Model Comparison

| Model | Performance Evidence | Interpretability Strength | Interpretability Weakness |
|---|---|---|---|
| Linear regression | Test R² = 0.9125, RMSE = 672.46, MAE = 539.08 for TotalCharges prediction | Coefficients are easy to interpret and allow direct understanding of variable influence | Assumes linear relationships, shows heteroscedasticity, and is not the correct model for the binary churn outcome itself |
| Logistic regression | Pending final model summary | Usually interpretable through coefficients and odds ratios | Pending final model summary |
| GAM | ROC-AUC = 0.8476; Accuracy = 0.8027 | Smooth functions capture nonlinear relationships while remaining more interpretable than a black-box model | More complex than a single coefficient table; interpretation is less direct than linear or logistic regression |

## Recommendation
Recommended model: 

Why this model:


What the company can responsibly conclude:

What the company should not conclude yet:


One next analysis we would run:


## Conclusion
This project highlights that model interpretability must be considered together with model assumptions and predictive performance. Linear regression is useful for understanding continuous outcomes, but it does not fit the churn classification problem as naturally as a classifier. 
