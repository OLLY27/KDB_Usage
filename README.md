# Using KDB on Client Site 
## Introduction
Continuing from your month 1 training, let's bridge the gap to real-world client projects. You've already learned about how KDB Tables are stored on disk, including partitioned and splayed storage methods. In established projects, data is often structured similarly, such as in an AWS data lake. Understanding how to connect, query, and maintain data in these data lakes is a crucial skill for client engagements.

___________________________________________________
## qConsole 
The Q Console is an interactive environment for working with kdb+ and the Q programming language. It provides a command-line interface where users can enter Q expressions, execute queries, and interactively explore data.

Good link for what a console is for background - https://www.linuxbabe.com/command-line/linux-terminal

### How to Set up and Use 
You can install q directly on your personal computer or you can set up a free EC2 AWS Instance. This exposure to AWS can be beneficial to the project as well and would recommend exposure to AWS too: https://fdplc.sharepoint.com/sites/FirstDerivativeCloudEngineering/SitePages/Cloud-Service-Providers.aspx

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

![image](https://github.com/OLLY27/KDB_Usage/assets/127981767/6a5f0f33-aba6-4980-9bfc-4cf59a978063)

#### Useful Links 
 - Set up a free EC2 Instance -  https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html
 - Installing q - https://code.kx.com/q/learn/install/

### Working Examples
Load up your console using the alias you have created and above and try querying the below table and typing some of the system commands to get confartable with the q Console - https://code.kx.com/q/basics/syscmds/

``` sh
trades:([] date:asc 1000?.z.d-til 5; time:1000?24:00; sym:1000?`appl`fb`amzn`goog; side:1000?`Buy`Sell; price:99+1000?2f; size: 1000?1000)
quotes:([] date:asc 10000?.z.d- til 5; time:10000?24:00; sym:10000?`appl`fb`amzn`goog; bid:100-10000?1f; offer:100-1*10000?1f)

select date,tiem,sym,buy from trades where date=.z.d-2

select last price by sym from trades
```
![image](https://github.com/OLLY27/KDB_Usage/assets/127981767/0fc31f93-6d90-46d9-915d-8d5593615197)

Debugging in Q involves identifying and resolving issues in your code, such as syntax errors, logical errors, or unexpected behavior. One common approach to debugging in Q is to use the .z.s system function along with the .z system variables to inspect and monitor code execution.

By inspecting the debug output, you can identify any issues or unexpected behavior in your code and make necessary adjustments to fix them. This approach can be applied to more complex functions and scripts in Q to facilitate effective debugging and troubleshooting.

``` sh
calculateAverageTradeSize:{
    avgTradeSize:select avg size by sym from trades;
    joinedTable:quotes lj avgTradeSize;
    joinedTable
}

combinedTable: calculateAverageTradeSize[trades;quotes]

/same again but lets make an error and debug it

calculateAverageTradeSize:{
    'dbg;
    avgTradeSize:select avG size by sym from trades;
    joinedTable:quotes lj avgTradeSize;
    joinedTable
}
/go through line by line to observe the output and find the error
```

### Conclusion

**Benefits:**
1. **Interactive Environment**: Enables quick query execution and immediate feedback.
2. **Fast Prototyping**: Facilitates rapid development and testing of algorithms.
3. **Efficient Data Exploration**: Provides tools for easy data inspection and manipulation.
4. **Debugging and Troubleshooting**: Supports debugging and issue resolution within the console.
5. **Real-time Monitoring**: Allows continuous monitoring and analysis of live data streams.
6. **Customization and Extension**: Offers flexibility for customization and integration with external tools.
7. **Education and Training**: Provides a practical learning environment for students and practitioners.

**Detriments Compared to UI Platforms:**
1. **Limited Visualization**: Lack of graphical interface may limit complex data visualization capabilities.
2. **Steep Learning Curve**: Requires familiarity with command-line interfaces and Q language syntax.
3. **Complex Queries**: Performing complex queries may be more challenging compared to GUI-based tools.
4. **Less Intuitive**: May not be as intuitive for users accustomed to graphical user interfaces (GUIs).
5. **Limited Collaboration**: Collaboration features are often limited compared to UI platforms with built-in collaboration tools.
6. **Resource Intensive**: Console-based environments may require more manual intervention for resource management and optimization.

___________________________________________________
## qStudio    
qStudio is an integrated development environment (IDE) tailored for working with Kx Systems' kdb+ database and the Q programming language. It provides a comprehensive suite of tools and features to facilitate efficient development, analysis, and deployment of Q code and data solutions. With its intuitive interface and powerful capabilities, qStudio empowers developers, data scientists, and analysts to streamline their workflow and maximize productivity when working with kdb+ and Q.

### How to Set up and Use 

**How to Install qStudio:**

To install qStudio, follow these steps:
1. Visit the official qStudio website or download the installer from [the Kx Systems website](https://www.timestored.com/qstudio/).
2. Run the installer executable file.
3. Follow the on-screen instructions to complete the installation process.
4. Once the installation is complete, launch qStudio from the desktop shortcut or start menu icon.

Using qStudio is straightforward and intuitive. Here's a brief guide on how to use qStudio effectively:

1. **Launching qStudio:**
   - After installation, launch qStudio by double-clicking the desktop shortcut or selecting it from the start menu.

2. **Creating or Opening a Project:**
   - Upon launching qStudio, you'll be presented with options to create a new project or open an existing one.
   - If you're starting a new project, select "New Project" and provide a name and location for your project files.
   - If you have an existing project, select "Open Project" and navigate to the project directory.

3. **Writing Q Code:**
   - qStudio provides a code editor where you can write Q code.
   - Create a new Q script file by selecting "File" > "New" > "Q Script" or open an existing script file.
   - Write your Q code in the editor. qStudio offers syntax highlighting, code completion, and error checking to help you write code more efficiently.

4. **Executing Q Code:**
   - To execute Q code, you can use the interactive console provided by qStudio.
   - Select the code snippet you want to execute in the editor and press Ctrl + Enter (or use the designated shortcut).
   - Alternatively, type directly into the console and press Enter to execute Q code interactively.

5. **Debugging Q Code:**
   - qStudio includes debugging tools to help you identify and resolve issues in your Q code.
   - Set breakpoints in your code by clicking in the left margin of the editor.
   - Run your code in debug mode by selecting "Debug" > "Start Debugging".
   - Use the debugging toolbar to step through code, inspect variables, and evaluate expressions.

6. **Connecting to kdb+ Databases:**
   - qStudio allows you to connect to kdb+ databases for querying and retrieving data.
   - Select "Database" > "Connect to Database" and provide the connection details for your kdb+ instance.
   - Once connected, you can execute queries directly from qStudio and work with the results.

7. **Data Visualization:**
   - qStudio includes built-in data visualization tools for creating charts, plots, and graphs from Q data.
   - Select "View" > "Data Visualization" to open the visualization pane.
   - Drag and drop variables from the data pane onto the visualization canvas to create visualizations.

8. **Saving and Sharing Projects:**
   - Save your project files regularly by selecting "File" > "Save" or using the Ctrl + S shortcut.
   - Share your projects with colleagues by packaging them into a zip file and sharing the zip file or hosting it on a version control system like Git.

By following these steps and also this link https://www.timestored.com/qstudio/help/, you can effectively use qStudio to develop, analyze, and deploy Q code and data solutions.

### Working Examples

``` sh
([] dt:2013.01.01+til 21; cosineWave:cos a; sineWave:sin a:0.6*til 21)
```
![image](https://github.com/OLLY27/KDB_Usage/assets/127981767/ba3adc24-9dc8-470b-b574-0de8797bb114)

### Conclusion

**Benefits:**
1. Comprehensive IDE tailored for kdb+ and Q development.
2. Intuitive interface with syntax highlighting, code completion, and error checking.
3. Interactive console for executing Q code and exploring data.
4. Built-in debugging tools for identifying and resolving issues in code.
5. Seamless integration with kdb+ databases for querying and retrieving data.
6. Data visualization capabilities for analyzing and visualizing Q data.
7. Version control integration with Git for managing code changes and collaboration.

**Detriments:**
1. Learning curve for users new to kdb+ and Q programming.
2. Limited customization options compared to some other IDEs.
3. Resource-intensive for large-scale data processing tasks.

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
## KX Community 

Be sure to sign up to the KX Community too (like StackOverflow) for tips and pages - https://learninghub.kx.com/
