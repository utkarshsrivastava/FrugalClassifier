# Frugal-Classifier
One major hurdle faced while Machine Learning is the accumulation and efficient utilization of test and training data .
It is often, a very expensive, time consuming and combursome process.
And even after a great deal of effort has been put into collecting this data, a uniformaly accurate classifier can not be guaranteed. The Classifier implemented here, severely reduces the above mentioned burden by performing classification "on the fly" and using a feedback system to check the nature of training data to improve it's own accuracy ! The classifer works on the principle of multi-level classification and "best of three" principle to sort observations into one or more classes. It regularly identifies classes , for which the accuracy of classification is below a pre-defined threshold and feeds them more training data to improve their accuracy .

If a given class "c" has a probability "p" of being correctly classified , and even after certain amount of training "A",  p is less than a pre-defined value "T", it is placed in the "unstable bag" and the classifer keeps demanding regular training/test data to improve the accuracy for this perticular class. However, as soon as the accuracy( which is the reciprocal of the error component) for "c" reaches above the threshold T, it is dumped into a separate bag called the "stable bag".
Once a class is in the safe/stable bag, it is given less emphasis compared to the "un-safe" classes. safe classes are only occasionally and randomly provided test and training data (frequency of these checks can be tuned with the vatiable i_S) . 
The frequency of these Un-safe classes, however, are regularly scrutinized and given much more "training and test data" to improve their accuracy. We continue to perform these steps until all the classes have reached an accuracy > T.
The classifer can also be set of change the Threshold value "T" for each class.

