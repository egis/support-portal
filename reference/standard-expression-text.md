# Standard Expressions

Expressions allow for values to be substituted at runtime. As an example of how expression values are substituted, if you are given a document with the following index values:

```javascript
createdDate = 2009-03-15  
filename = Test.doc  
title = sample title  
docid = 123  
index1 = value1
index2 = hello123 world
index3 = 500
index4 = 100.15

```

If the basic syntax is `${lookup?defaultValue:format}` then this is how you would read the expression results using the values in the table in Document properties / indexes on page :

| Standard Expression        | Output
| ------------- |-------------
| ${createdDate:yyyy}   | 2009 
| ${createdDate:yyyy-MM-dd}   | 2009-13-15 
| ${createdDate:yyyyMM} | 200903 
| ${filename} - ${title} ($docid})   | Test.doc - sample (123) 


> Note that due to the `?` and `:` being used to format values they cannot be used in code e.g. 

e.g. ```'${index1 == 'val' ? 'yes' : 'no }``` will not work, use ```${ if (index1 == 'val') then 'yes' else 'no' }```


### Custom Scripts

Custom Groovy code can also be used e.g. to

| Script       |	Description	| Output
| ------------- |------------- | -----------
|`filename.toLowerCase()`||test.doc
|`filename.toUpperCase()`||TEST.doc
|`index1.replaceAll(' ', '_')`||hello123_world
|`index1.find('\d+')`||123
|`index1.find('^\d+')`||hello world
|`filename[0..3]`| return the first 3 chars of a filename|*tes*
|`index1.length() == 6` | | *true*
|`Double.valueOf('7.55') * 1.14).round(2)`||*8.61*
|`index3.asInt() < 10000`  |Most properties and all custom index values are in String format. In order to use arithmetic in filters etc, you need to first convert them to a Number type|*true*
|`index3 < 10000`  ||*false*




## Method Reference 

[String](http://docs.groovy-lang.org/docs/latest/html/groovy-jdk/java/lang/String.html)  
[Date](http://docs.groovy-lang.org/docs/latest/html/groovy-jdk/java/util/Date.html) and [SimpleDateFormat](http://download.oracle.com/javase/7/docs/api/java/text/SimpleDateFormat.html)  
[Number](http://docs.groovy-lang.org/docs/latest/html/groovy-jdk/java/lang/Number.html)  

See [Groovy JDK](http://docs.groovy-lang.org/docs/latest/html/groovy-jdk)

See [Document Properties](document-properties-text.md) for a full list of fields available.


