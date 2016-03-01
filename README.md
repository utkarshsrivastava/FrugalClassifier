# Frugal-Classifier
One major hurdle faced while Machine Learning is the accumulation and efficient utilization of test and training data .
It is often, a very expensive, time consuming and combursome process.
And even after a great deal of effort has been put into collecting this data, a uniformaly accurate classifier can not be guaranteed. The Classifier implemented here, severely reduces the above mentioned burden by performing classification "on the fly" and using a feedback system to check the nature of training data to improve it's own accuracy ! The classifer works on the principle of multi-level classification and "best of three" principle to sort observations into one or more classes. It regularly identifies classes with a low accuracy of classification ( below a pre-defined threshold) and feeds them more training data to improve their accuracy . It needs training data that is or can be sorted accordng to the actual observations 

If a given class "c" has a probability "p" of being correctly classified , and even after certain amount of training "A",  p is less than a pre-defined threshold value "T", it is placed in the "unstable bag" and the classifer keeps demanding regular training/test data to improve the accuracy for this perticular class. However, as soon as the accuracy( which is the reciprocal of the error component) for "c" reaches above the threshold T, it is dumped into a separate bag called the "stable bag".
Once a class is in the safe/stable bag, it is given less emphasis compared to the "un-safe" classes. safe classes are only occasionally and randomly provided test and training data (frequency of these checks can be tuned with the vatiable i_S) . 
The Un-safe classes, however, are regularly scrutinized and given much more "training and test data" to improve their accuracy. We continue to perform these steps until all the classes have reached an accuracy > T.
The classifer can also be set of change the Threshold value "T" for each class.

For instance, Let us consider a simple "hand written numeral classifier". The job of this classifier is to identifiy hand-written numerals based on the inspection of some images , each of which have a number written on them along with the digit they represent (eg 7: http://www.urbanthreads.com/productImages/regularSize/UTH4670.jpg )
Common sense dictates that the classifier is likely to quickly learn numbers such as 8 , 2, 0 and 3. However, it would likely confuse 1 with 7 and 4 with 9. The frugal-classifier will realize that it is wrongly classifying 1 and 7 and would demand more training data for 1 and 7, or 4 and 9. It will try to make a second level classifier that may even use a different learning methodology to classify these numbers. It will continue this for each class it doesnt recognize correctly. Thus, if level 1 of the classifer recognizes the number to be either 1 or 7, it passes this observation to level 2 classifier. 
else if, it recognizes the digit to be 4 or 9, it passes the observation to level 3 classifier.
.
.
.
until all classes are properly classfied
```
//Psuedocode:
level=0;
frugal_classify.register(frugal_classify,level);
//frugal classify is the main classifier that keeps appending improvements based on what it learns. 
//Initially, the classifier registers itself with a level 0, 
//each level represents a new addition/improvement.
HashMap map_clsfr2methdlgy(classifer,List<methdlgy_lredy_used>);
errordetails err_det_obj{
image_reference;
count_of_incorrect_observations;
}
HashMap errorMap(predictedclass+actualclass,err_det_obj);
// predictedclass+actualclass both are part of the key.
double [] p_class;
int count_obs=0;
String[] unstablebag;
do while ((∀pi∈ p_class) pi>T) 
{
  while(count_obs<A)
  {
    digit=getnextdata(dataset,unstablebag);
    predicted_result=frugal_classify(digit);
    if (predicted_result!=actual_result)
    {
    errorMap.put(<predictedclass,actualclass>,<image_reference,count_of_incorrect_observations+1>);
    }
  }
  count_obs=0;
   for each class c∈{c0,c1,c2..c9}
   {
      if (function(errorMap.get(c))<T)
        {
        unstablebag.add(c);
        if(c.getPriority()<MAX_PRIORITY)
          {
            c.setPriority(c.getPriority()+1);  
          }
        /* //Future impementation
        if(c.getPriority()==MAX_PRIORITY)
          for each distinct classification method m∈M-{map_clsfr2methdlgy.get(c)}
          {
          temp=make_new_temp_classifier(m);
          map_clsfr2methdlgy.put(c,m);
          if (test_classifier(temp,c,errorMap)>T)
            {
            level++;
            frugal_classify.register(temp,level);
            }
          }
          */
        
        }
        
    }
  }
```
