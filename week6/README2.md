**XGBoost Algorithm**

This is by far one of the most commonly used implementations of decision tree ensembles.

Recall the bagged decision tree algorithm.

For b = 1 to B:
    use sampling with replacement to create a bootrap training set of size m
    train a decision tree on the bootstrap data set.

XGBoost works by sequentially adding trees that improve the current ensemble by fitting the loss gradients/residual errors.

XGBoost stands for Extreme Gradient Boosting. XGBoost is an optimized implementation of gradient-boosted decision trees (GBDTs), designed for efficiency, scalability, and strong predictive performance. It also has built-in regularization which reduces high variance (overffiting). While understanding the mathematics behind the XGBoost is important; implementing an industrial-strength version from scratch is usually unnecessary.

For classification

from xgboost import XGBClassifier

model = XGBClassifier()
model.fit(X_train, Y_train)
y_pred = model.predict(X_test)

For regression

from xgboost import XGBRegressor

model = XGBRegressor()
model.fit(X_train, Y_train)
y_pred = model.predict(X_test)

