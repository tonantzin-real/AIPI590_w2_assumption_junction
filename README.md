# AIPI590: Week 2 - Assumption Junction
## Assumption Junction: Interpretable Churn Modeling

### Contributors
- Ammy Lin: Linear Regression
- Farnoosh Memari: Logistic Regression
- Tonantzin Real Rojas: Generalized Additive Model (GAM)

## Dataset
This project uses the Telco Customer Churn dataset, which contains information about customers of a telecommunications company, including demographic characteristics, account information, services used, tenure, monthly charges, and total charges.

The goal of the analysis is to predict whether a customer is likely to churn, meaning that they discontinue their telecommunications service. We compare three interpretable modeling approaches—linear regression, logistic regression, and a generalized additive model (GAM)—to determine which model provides the best balance between predictive performance and interpretability.

A key focus of this project is not only model performance, but also whether the assumptions required for interpreting each model are reasonably satisfied.

## Linear Regression Assumptions

The linear regression analysis included several diagnostic checks.

- Independence:
The Durbin-Watson statistic was [insert value]. A value close to 2 suggests little evidence of autocorrelation. The residuals-versus-order plot showed [describe whether residuals appeared randomly scattered around zero].

- Homoscedasticity:
The Breusch-Pagan test produced an LM statistic of 1151.12 with a p-value of 5.62 × 10⁻²²³, and an F-statistic of 62.66 with a p-value of 2.67 × 10⁻²⁵⁷. Because the p-value is far below 0.05, we reject the null hypothesis of constant variance. This indicates that the homoscedasticity assumption is violated and that the residuals exhibit heteroscedasticity.

- Normality:
The residual histogram and Q-Q plot showed [describe result]. The Jarque-Bera test produced a p-value of [insert value], suggesting [approximately normal / non-normal] residuals.

- Multicollinearity:
Some Variance Inflation Factor (VIF) results were:

- `tenure`: 6.33
- `MonthlyCharges`: 3.36
- `TotalCharges`: 8.08

`MonthlyCharges` showed relatively low multicollinearity, while `tenure` and `TotalCharges` exceeded the commonly used VIF threshold of 5. However, none exceeded 10, suggesting moderate rather than severe multicollinearity.

## Model Comparison
Model	Performance Evidence	Interpretability Strength	Interpretability Weakness
- Linear Regression:	[R², RMSE, MAE, etc.]	Coefficients are straightforward to interpret and directly describe changes in predicted churn probability.	Assumes a linear relationship and produced evidence of heteroscedasticity; predicted probabilities can also fall outside the 0–1 range.
- Logistic Regression:	[Accuracy, ROC-AUC, precision/recall, etc.]	Coefficients and odds ratios provide a clear explanation of how features affect churn odds.	Assumes linearity in the log-odds and may not capture nonlinear relationships without additional feature engineering.
- GAM:	[Performance metrics]	Smooth functions allow nonlinear relationships to be visualized and interpreted while remaining more transparent than many black-box models.	Interpretation is more complex than individual linear coefficients, and results depend on the choice and estimation of smooth terms.

## Recommendation
Recommended Model: [Linear Regression / Logistic Regression / GAM]

## Why This Model
We recommend [model] because it provides the best balance between predictive performance and interpretability for the telecom company's churn prediction task.

Compared with the other models, [briefly explain performance and interpretability comparison].

The model also allows the company to understand how customer characteristics are associated with predicted churn, rather than providing predictions without an interpretable explanation.

## What the Company Can Responsibly Conclude

Based on our analysis, the company can conclude that:

[Finding 1 supported by your model]
[Finding 2 supported by your model]
[Finding 3 supported by your model]
The selected model provides [strong/moderate/etc.] predictive performance while remaining interpretable.
The model identifies statistical associations between customer characteristics and churn risk.
What the Company Should Not Conclude Yet

The company should not interpret the model's associations as proof of causation. For example, if customers with higher monthly charges have higher predicted churn, this does not establish that increasing monthly charges causes customers to churn.

The company should also be cautious about acting on predictions without considering the model's assumption violations. In particular, [insert relevant concern, such as heteroscedasticity or multicollinearity] should be addressed or accounted for before using model estimates for high-stakes decision-making.

## One Next Analysis We Would Run
Our next analysis would be [insert analysis].

For example, we could evaluate the recommended model using cross-validation and out-of-sample performance metrics, while also investigating whether robust standard errors or alternative modeling approaches improve the reliability of the model's statistical inference.

## Conclusion

This project demonstrates that model interpretability depends on more than simply choosing a model with understandable coefficients. Before using an interpretable churn model to make business decisions, the company should evaluate whether the assumptions underlying the model are reasonably satisfied.

Our comparison suggests that [recommended model] offers the strongest overall combination of predictive performance, interpretability, and appropriate modeling assumptions for this churn prediction task. However, the identified limitations and assumption concerns should be considered before deploying the model in practice.
