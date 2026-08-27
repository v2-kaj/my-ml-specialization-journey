Anomaly Detection 

Applications:
1. Fraud detection
2. Manufacturing
3. Monitoring computers in data centers


Anomaly detection which unsupervised learning vs Supervised learning

Anomaly detection when you have very few labeled data eg 0-20. This small set can be used for cross-validation or testing during evaluation or parameter tuning.
If you have a large set of labeled examples, then supervised learning eg logistic regression.

If there are different "types" of anomalies or if future anomalies may be very different from examples seen in the past then anomaly detection. eg financial fraud (unique anomalies in the future). In supervised learning the assumption is future examples will be similar to past examples eg spam email. or weather forcasting, specific disease detection.


Feature Selection for anomaly detection.
It turns out the choice of features you feed into the anomaly detection algorithm is very important. because there no labeled examples. as such choosing the most appropriate features is key. 

Tips.
Choose a feature that is gaussian or make it more gaussian eg taking a log of feature x. or log(x2 + c) or taking square root or the power of c=1/3.

Error Analysis for anomaly detection.

Say for both non-anomalous and anomalous test example x you may see that p(x)>episilon then adding a new feature on training may help to flag the anomalous example.

For instance in computers monitoring you may train an anomaly detection model on features like:
x1 = RAM of the computer
x2 = number of disk accesses/sec
x3 = CPU load
x4 = network traffic

you may create a new feature

x5  = CPU load / network traffic or x6 = (CPU load)^2 / network traffic

Play around with feature engineering to get p(x) to be lower than episilon for the anomalous example x so that the trained model on the engineered features get to correctly flag x as anomalous.

