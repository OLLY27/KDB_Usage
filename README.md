# Using KDB on Client Site 
## Introduction
Continuing from your month 1 training, let's bridge the gap to real-world client projects. You've already learned about how KDB Tables are stored on disk, including partitioned and splayed storage methods. In established projects, data is often structured similarly, such as in an AWS data lake. Understanding how to connect, query, and maintain data in these data lakes is a crucial skill for client engagements.

___________________________________________________
## qConsole 
The Q Console is an interactive environment for working with kdb+ and the Q programming language. It provides a command-line interface where users can enter Q expressions, execute queries, and interactively explore data.

Good link for what a console is for background - https://www.linuxbabe.com/command-line/linux-terminal

### How to Set up and Use 
You can install q directly on your personal computer or you can set up a free EC2 AWS Instance. This exposure to AWS can be beneficial to the project as well and would recommend exposure to AWS too: https://fdplc.sharepoint.com/sites/FirstDerivativeCloudEngineering/SitePages/Cloud-Service-Providers.aspx

 - Set up a free EC2 Instance -  https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html
 - Installing q - https://code.kx.com/q/learn/install/

 - Setting up a free AWS instance and installing Q on it involves a few steps. Here's a general guide to get you started:

1. **Create an AWS Account**:
   - If you don't have an AWS account, you'll need to sign up for one. Go to the AWS website (https://aws.amazon.com/) and follow the instructions to create an account. You'll need to provide your contact information and payment details, although signing up for a free tier account won't require any immediate payment.

2. **Launch an EC2 Instance**:
   - Once you're logged into your AWS Management Console, navigate to the EC2 dashboard.
   - Click on "Launch Instance" to start the instance creation process.
   - Choose an Amazon Machine Image (AMI) for your instance. You can use a standard Amazon Linux AMI or any other compatible Linux distribution.
   - Select an instance type. For testing purposes, you can choose a t2.micro instance, which is eligible for the AWS Free Tier.
   - Configure the instance details, including network settings, storage, and security groups. You can use default settings for most of these options.
   - Review your instance configuration and click "Launch".

3. **Set up SSH Access**:
   - After launching your instance, you'll need to set up SSH access to connect to it remotely.
   - Download the SSH key pair provided by AWS during instance creation.
   - Change the permissions of the private key file to make it readable only by the owner: `chmod 400 your-key.pem`.
   - Connect to your instance using SSH: `ssh -i your-key.pem ec2-user@your-instance-public-ip`.

4. **Install Q**:
   - Once connected to your instance via SSH, you can install Q.
   - Download the Q software package from the Kx Systems website or any other trusted source. You may need to register for a free trial or obtain a community edition license.
   - Transfer the Q package to your EC2 instance using SCP or any other file transfer method.
   - Install the Q package on your EC2 instance following the provided installation instructions. This typically involves extracting the package and running an installation script.
   - Verify the installation by running Q from the command line: `q`.

5. **Optional: Configure Q Environment**:
   - Depending on your specific use case, you may need to configure additional settings for your Q environment, such as setting environment variables or configuring network settings.

Once you've completed these steps, you should have a running AWS EC2 instance with Q installed and ready to use. Remember to monitor your AWS usage to ensure that you stay within the limits of the AWS Free Tier to avoid unexpected charges.

Text 
Screenshots

### Working Examples
Load up your console using the alias you have created and above and try querying the below table and typing some of the system commands to get confartable with the q Console - https://code.kx.com/q/basics/syscmds/

``` sh
trades:([] date:asc 1000?.z.d-til 5; time:1000?24:00; sym:1000?`appl`fb`amzn`goog; side:1000?`Buy`Sell; price:99+1000?2f; size: 1000?1000)
quotes:([] date:asc 10000?.z.d- til 5; time:10000?24:00; sym:10000?`appl`fb`amzn`goog; bid:100-10000?1f; offer:100-1*10000?1f)

select date,tiem,sym,buy from trades where date=.z.d-2
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
