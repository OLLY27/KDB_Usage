# Using KDB on Client Site 
## Introduction
This information is a continuation on from your motnh 1 training. It will aim to bridge the gap from your initial traininging, to whta you may experience on client site. In your training, you will have covered how KDB Tables are stored on disk (partitioned/splayed etc.). In an establised project, the data you would be working with will liely be stored like this. An example of which could be a data lake on AWS. Knowing the different methods and trying to connect to the data lake to query and maintain data is an important skill to have ahead of client site. We will aim to look at the different platforms you can use for connecting to the datalakein more detail below.

___________________________________________________
## qConsole    
Description anbd explanation

### How to Set up and Use 
You can install q directly on your personal computer or you can set up a free EC2 AWS Instance. This exposure to AWS can be beneficial to the project as well and would recommend exposure to AWS too: https://fdplc.sharepoint.com/sites/FirstDerivativeCloudEngineering/SitePages/Cloud-Service-Providers.aspx

 - Set up a free EC2 Instance -  https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html
 - Installing q - https://code.kx.com/q/learn/install/

Text 
Screenshots

### Working Examples

``` sh

```
Relevant screenshots and explanantions

### Conclusion
Brief summary and list benefits whilstr referring to limiations 

___________________________________________________
## qStudio    
Description anbd explanation

### How to Set up and Use 

Relevant Links - timestored https://www.timestored.com/qstudio/
Text 
Screenshots

### Working Examples

``` sh

```
Relevant screenshots and explanantions

### Conclusion
Brief summary and list benefits whilstr referring to limiations 

___________________________________________________
## qRemote   
Description anbd explanation

### How to Set up and Use 

Relevant Links
Text 
Screenshots

### Working Examples

``` sh

```
Relevant screenshots and explanantions

### Conclusion
Brief summary and list benefits whilstr referring to limiations 

___________________________________________________
## qPad  
Description anbd explanation

### How to Set up and Use 

Relevant Links
Text 
Screenshots

### Working Examples

``` sh

```
Relevant screenshots and explanantions

### Conclusion
Brief summary and list benefits whilstr referring to limiations 

___________________________________________________
## Jupyter Notebooks  
A verstaile approach which has been used alot in your month one training and good to always revisit - https://fdplc.sharepoint.com/sites/LearningDevelopment/SitePages/Week-1---Getting-Started.aspx

### How to Set up and Use 

How to access and set up from your browse

How it works and how to oepn connections etc

We can use KX Academy, a greatr resource for practicing with notebooks here - https://learninghub.kx.com/academy/

Relevant Links
Text 
Screenshots

### Working Examples

``` sh

```
Relevant screenshots and explanantions

### Conclusion
Brief summary and list benefits whilstr referring to limiations 

___________________________________________________
## Exercises

You can try and oepn each of the above methods and run the following once connected. Have a look at the results of each and see how they compare in the outputs and how we can change the output to our desired look.

``` sh
trades:([] date:asc 1000?.z.d-til 5; time:1000?24:00; sym:1000?`appl`fb`amzn`goog; side:1000?`Buy`Sell; price:99+1000?2f; size: 1000?1000)
quotes:([] date:asc 10000?.z.d- til 5; time:10000?24:00; sym:10000?`appl`fb`amzn`goog; bid:100-10000?1f; offer:100-1*10000?1f)

select date,tiem,sym,buy from trades where date=.z.d-2
```

You can make your own queries and try and query the above date set

___________________________________________________
## KX Community 

Be sure to sign up to the KX Community too (like StackOverflow) for tips and pages - https://learninghub.kx.com/
