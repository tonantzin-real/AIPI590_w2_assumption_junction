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
| Logistic regression | Binary outcome, independence of observations, multicollinearity, linearity of the logit, sufficient sample size | The target was correctly coded as a binary variable. Each row represents an individual customer, so observations were treated as independent. VIF analysis showed high multicollinearity for some features, especially MonthlyCharges and InternetService variables. Empirical logit plots showed that MonthlyCharges did not fully satisfy the linearity-of-the-logit assumption. The model had 81.3 events per variable. | Some coefficients should be interpreted carefully because of multicollinearity and the violation of the linearity-of-the-logit assumption. The model may not capture nonlinear effects well. |
| GAM | Nonlinearity, model fit, smooth-term interpretation | The GAM achieved ROC-AUC = 0.8476 and accuracy = 0.8027, suggesting strong discriminative power for churn risk; smooth terms allow nonlinear relationships to be modeled while remaining interpretable | GAMs are more complex than linear coefficients and require careful tuning of smoothness parameters; results still need additional out-of-sample validation |

## Model Comparison

| Model | Performance Evidence | Interpretability Strength | Interpretability Weakness |
|---|---|---|---|
| Linear regression | Test R² = 0.9125, RMSE = 672.46, MAE = 539.08 for TotalCharges prediction | Coefficients are easy to interpret and allow direct understanding of variable influence | Assumes linear relationships, shows heteroscedasticity, and is not the correct model for the binary churn outcome itself |
| Logistic regression | With `class_weight="balanced"`: Accuracy = 0.726; Recall = 0.799; F1 = 0.608; ROC-AUC = 0.835 (recall rose sharply from 0.567 in the unweighted model, while precision fell from 0.648 to 0.491) | Coefficients turn directly into odds ratios, so we can explain each feature's effect on churn in plain terms (e.g., a one-year contract cuts the odds of churn roughly in half) | A few features (MonthlyCharges, InternetService) are highly correlated with each other, so their individual coefficients are unstable and shouldn't be trusted on their own. Balancing the classes also trades away precision for recall, so the model now flags more customers as at risk of churning, including more false alarms |
| GAM | ROC-AUC = 0.8476; Accuracy = 0.8027 | Smooth functions capture nonlinear relationships while remaining more interpretable than a black-box model | More complex than a single coefficient table; interpretation is less direct than linear or logistic regression |

## Recommendation
Recommended model: Logistic regression

Why this model: Logistic regression performs almost as well as the GAM (Accuracy 0.803 vs. 0.8027, ROC-AUC 0.836 vs. 0.8476), but its coefficients are much easier to explain to someone outside the data science team. Turning a coefficient into an odds ratio lets us say something simple like "customers on month-to-month contracts have much higher odds of churning than customers on two-year contracts," which is exactly the kind of explanation a business team would want. Linear regression isn't a good fit here at all, since churn is a yes/no outcome and not something to predict as a continuous number.

What the company can responsibly conclude: Contract type, tenure, and payment method are strongly and reliably linked to churn. Customers who have been with the company longer are much less likely to churn, and customers on month-to-month contracts or paying by electronic check are more likely to churn. These relationships had low p-values and reasonably tight confidence intervals, so the company can act on them, for example by encouraging month-to-month customers to move to longer contracts.

What the company should not conclude yet: The company shouldn't read too much into the exact effect of MonthlyCharges or InternetService type on their own. These features were highly correlated with each other (shown in the VIF table), so their individual coefficients had very wide confidence intervals and even flipped direction in a way that didn't make intuitive sense. We only trust the general pattern (fiber-optic and higher-cost customers churn more), not the precise size of the effect.

One next analysis we would run: We would look more closely at MonthlyCharges specifically, since our empirical logit plot showed it doesn't have a straight-line relationship with churn like logistic regression assumes. Trying a GAM just for that one feature, or binning MonthlyCharges into groups, would probably give a more honest picture of how price relates to churn.


## Conclusion
This project highlights that model interpretability must be considered together with model assumptions and predictive performance. Linear regression is useful for understanding continuous outcomes, but it does not fit the churn classification problem as naturally as a classifier. 
