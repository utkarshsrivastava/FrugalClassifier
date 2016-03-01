from NaiveBayes import  Pool
import os

DClasses = ["1",  "2",  "3",  "4",  "5",  "6"]

base = "../learn/"
p = Pool()
for i in DClasses:
    p.learn(base + i, i)



base = "../test/"
for i in DClasses:
    dir = os.listdir(base + i)
    for file in dir:
        res = p.Probability(base + i + "/" + file)
        print(i + ": " + file + ": " + str(res))
