# Spark-Examples
var data = sc.parallelize(Seq(("venu","TV", 3000), ("venu","mobile", 4000), ("kiran","mobile", 5000), ("satya","fan", 2000), ("kiran","bike", 5000),("venu","fan",3000)))

Now please find each customer how many items purchased? 
How much average money spend?

means venu 3 items, spend 10000 means avg 3333 spend average

val b = data.map(x =>(x._1,1)).reduceByKey(_+_).collect  // Each customer how many times purchased

val z = data.map(x=>( x._1,x._3)).mapValues(y => (y,1)).reduceByKey((a,b) => (a._1 + b._1,a._2+b._2)).
     | map{ x => 
     | val temp = x._2
     | val total = temp._1
     | val count = temp._2
     | (x._1,total,total/count)
     | }.collect   //How much average money spent and how many times purchased
