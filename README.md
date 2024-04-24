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
qRemote is a command-line interface (CLI) tool designed for remote interaction with kdb+ instances. Developed by Kx Systems, it allows users to execute Q code, query data, and interact with kdb+ databases remotely over a network connection. Key features include remote connection setup, Q code execution, basic debugging capabilities, lightweight and portable design, and seamless integration with existing workflows. qRemote provides a streamlined and efficient way to interact with kdb+ instances without the need for a graphical user interface (GUI) or extensive setup.

### How to Set up and Use 
To install qRemote, follow these steps:

1. **Download the qRemote Binary:**
   - Visit the official Kx Systems website or another trusted source to download the qRemote binary file - https://github.com/t-martin/qremote
   - Ensure that you download the appropriate binary for your operating system (e.g., Windows, Linux, macOS).

2. **Extract the qRemote Binary:**
   - Once the binary file is downloaded, extract it from the compressed archive (if applicable).
   - Place the extracted binary file in a location on your system where you can easily access it.

3. **Set Permissions (Linux/macOS):**
   - If you're using Linux or macOS, you may need to set execute permissions on the qRemote binary.
   - Open a terminal window and navigate to the directory containing the qRemote binary.
   - Run the following command to set execute permissions:
     ```
     chmod +x qRemote
     ```

4. **Optional: Add to PATH (Linux/macOS):**
   - To run qRemote from any location on your system, you can add the directory containing the qRemote binary to your system's PATH environment variable.
   - Add the following line to your shell configuration file (e.g., ~/.bashrc or ~/.bash_profile) to set the PATH:
     ```
     export PATH="/path/to/qRemote/directory:$PATH"
     ```
   - Replace "/path/to/qRemote/directory" with the actual path to the directory containing the qRemote binary.

5. **Verify Installation:**
   - To verify that qRemote is installed correctly, open a terminal or command prompt and navigate to the directory containing the qRemote binary.
   - Run the following command to display the qRemote version information:
     ```
     qRemote --version
     ```

6. **Start Using qRemote:**
   - Once qRemote is installed and verified, you can start using it to interact with kdb+ instances remotely.
   - Use the `qRemote` command followed by any additional arguments or options to connect to remote kdb+ instances, execute Q code, and query data.

By following these steps, you can install qRemote on your system and begin using it to remotely interact with kdb+ instances.

1. **Launching qRemote:**
   - Begin by launching qRemote by either double-clicking its icon or executing it from the command line.

2. **Connecting to a kdb+ Instance:**
   - Upon launching qRemote, you'll need to connect to a kdb+ instance.
   - Enter the hostname or IP address of the server running the kdb+ instance.
   - Specify the port number used for the kdb+ instance (usually 5000 for standard connections).
   - Provide any necessary authentication credentials, such as username and password.

3. **Writing and Executing Q Code:**
   - Once connected, you can start writing Q code directly into the qRemote interface.
   - Type your Q code into the input area at the bottom of the interface.
   - Press Enter to execute the code. The results will be displayed in the output area above.

4. **Debugging Q Code:**
   - qRemote provides basic debugging capabilities for Q code.
   - You can add print statements to your code to output debug information to the console.
   - Additionally, you can use error messages and other feedback from qRemote to identify and debug issues in your code.

5. **Data Visualization:**
   - qRemote is primarily a command-line interface and does not include built-in data visualization tools.
   - However, you can use qRemote in conjunction with other tools or libraries to visualize data generated by your Q code.

6. **Saving and Sharing Sessions:**
   - While qRemote does not support saving sessions or projects directly within the interface, you can save your Q code to a text file for later use.
   - You can also share your Q code and results with colleagues by copying and pasting code snippets or output from the qRemote interface.

7. **Disconnecting from the kdb+ Instance:**
   - Once you're finished working with the kdb+ instance, you can disconnect from it by closing the qRemote interface or using any built-in disconnect options provided by the interface.

By following these steps, you can effectively use qRemote to interact with kdb+ instances, execute Q code, and perform basic debugging and analysis tasks.

### Working Example
Start a qprocess on port 5001
```
$ q -p 5001
```
Define some data
```
q) t:([]a:1 2 3;b:2 3 4)
```
Now use qremote to connect to the remote process

Run qremote. It will prompt for server details

``` sh
$ ./qremote
host:localhost
port:5001
user:
password:

[qremote v1.1]
[qremote connecting to: :localhost:5001]
[qremote connected to:  :localhost:5001]
[\\ to exit. 'exit 0' will kill remote process]

q)a:100	
q)a
100
q)t
a b
---
1 2
2 3
3 4
```

We could achieve the same result using a config file.

```
$ cat config/test.ini
[TEST.CONN.A]
host=localhost
port=5001
user=u
password=p

[TEST.CONN.B]
host=localhost
port=6001
user=u
password=p

$ qremote -config config/test.ini -connection TEST.CONN.A
[qremote v1.1]
[qremote connecting to: :localhost:5001]
[qremote connected to:  :localhost:5001]
[\\ to exit. 'exit 0' will kill remote process]
```
### Conclusion
**Benefits of qRemote:**

1. **Remote Interaction:** Enables users to interact with kdb+ instances remotely, facilitating flexibility and convenience in accessing and managing data.

2. **Command-Line Interface:** Provides a lightweight and efficient command-line interface, ideal for users comfortable with CLI workflows and automation tasks.

3. **Efficient Data Querying:** Allows for quick and efficient querying of data stored in kdb+ databases, enabling users to retrieve information in real-time.

4. **Basic Debugging:** Offers basic debugging capabilities for Q code, helping users identify and troubleshoot issues in their scripts.

5. **Portability:** qRemote's lightweight design makes it highly portable, allowing users to install and run it on a wide range of platforms and environments.

**Detriments of qRemote:**

1. **Limited Graphical Interface:** Lacks a graphical user interface (GUI), which may be less intuitive for users accustomed to GUI-based tools.

2. **Limited Debugging Features:** Provides only basic debugging capabilities, which may not be sufficient for complex debugging scenarios.

3. **Command-Line Learning Curve:** Requires users to be familiar with command-line interfaces (CLIs) and Q language syntax, which may have a learning curve for some users.

4. **Dependency on Network Connection:** Relies on network connectivity for remote interaction, which may introduce latency or connectivity issues depending on network conditions.

5. **Reduced Visualization Options:** Does not include built-in data visualization tools, limiting the ability to visualize data directly within the qRemote interface.

___________________________________________________
## qPad  
qPad provides a graphical interface for interacting with Q code and kdb+ databases. It includes features like syntax highlighting and code completion for efficient code writing, along with data visualization tools for analyzing data directly within the IDE. qPad facilitates interactive development and seamless integration with kdb+, enhancing productivity for developers, data scientists, and analysts.

### How to Set up and Use 

**Installing and Setting Up qPad:**

1. **Download qPad Installer:**
   - [Visit the official qPad website or a trusted source to download the qPad installer for your operating system (Windows, macOS, or Linux)](https://www.qinsightpad.com/download.html).

2. **Run the Installer:**
   - Double-click the downloaded installer file to begin the installation process.
   - Follow the on-screen instructions to complete the installation. Choose the installation directory and any additional settings as needed.

3. **Launch qPad:**
   - Once the installation is complete, launch qPad by double-clicking its icon or searching for it in your applications menu.

**Using qPad:**

1. **Create or Open a Project:**
   - Upon launching qPad, you can create a new project or open an existing one.
   - To create a new project, select "File" > "New Project" and provide a name and location for your project files.
   - To open an existing project, select "File" > "Open Project" and navigate to the directory containing your project files.

2. **Write Q Code:**
   - qPad provides a code editor where you can write Q code.
   - Create a new Q script file by selecting "File" > "New File" > "Q Script" or open an existing script file.
   - Write your Q code in the editor. qPad offers syntax highlighting and code completion to assist with code writing.

3. **Execute Q Code:**
   - To execute Q code, you can use the built-in console or run scripts directly.
   - Type or paste your Q code into the console or open your script file and select "Run" > "Run Script" to execute the code.

4. **Debugging Q Code:**
   - qPad includes debugging tools to help identify and resolve issues in your Q code.
   - Set breakpoints in your code by clicking in the left margin of the editor.
   - Run your code in debug mode by selecting "Debug" > "Start Debugging".

5. **Data Visualization:**
   - qPad integrates data visualization tools for creating charts, plots, and graphs from Q data.
   - Select "View" > "Data Visualization" to open the visualization pane.
   - Drag and drop variables from the data pane onto the visualization canvas to create visualizations.

6. **Save and Share Projects:**
   - Save your project files regularly by selecting "File" > "Save" or using the Ctrl + S shortcut.
   - Share your projects with colleagues by packaging them into a zip file or hosting them on a version control system like Git.

By following these steps, you can install, set up, and use qPad to write, execute, and analyze Q code for your kdb+ projects.

### Working Examples

``` sh
// Example Q code to calculate the average of a list of numbers
nums: 1 2 3 4 5;  // Define a list of numbers
avgNums: avg nums;  // Calculate the average of the numbers
avgNums;  // Output the average
```

### Conclusion
**Benefits of qPad:**

1. **Graphical Interface:** Provides a user-friendly graphical interface, making it accessible to users who prefer visual tools over command-line interfaces.

2. **Interactive Development:** Offers an interactive development environment (IDE) for writing, executing, and debugging Q code, enhancing productivity and efficiency.

3. **Code Editing Features:** Includes advanced code editing features such as syntax highlighting, code completion, and error checking, aiding in code writing and debugging.

4. **Data Visualization:** Integrates data visualization tools for creating charts, plots, and graphs from Q data, allowing users to analyze and visualize data within the IDE.

5. **Integration with kdb+:** Seamlessly integrates with kdb+ databases, enabling users to connect to remote instances, execute queries, and retrieve data directly within the IDE.

**Detriments of qPad:**

1. **Resource Intensive:** May require more system resources compared to lightweight command-line tools, potentially impacting performance on low-spec systems.

2. **Learning Curve:** Users may need to invest time in learning the IDE's interface and features, particularly if they are unfamiliar with graphical development environments.

3. **Dependency on GUI:** Relies on a graphical user interface (GUI), which may be less suitable for users who prefer command-line workflows or remote development scenarios.

4. **Complexity:** The richness of features and options in qPad may introduce complexity for users who require only basic Q code execution and querying capabilities.

5. **Platform Limitations:** Availability of qPad may be limited to specific operating systems, potentially excluding users on unsupported platforms from accessing its features.

___________________________________________________
## Jupyter Notebooks  
Jupyter Notebook is an open-source web application that enables users to create and share documents containing live code, visualizations, and narrative text, making it a versatile tool for interactive computing and data exploration. A verstaile approach which has been used alot in your month one training and good to always revisit - https://fdplc.sharepoint.com/sites/LearningDevelopment/SitePages/Week-1---Getting-Started.aspx

### How to Set up and Use 

To install Jupyter Notebooks, you can follow these steps:

1. **Install Python:**
   - Ensure you have Python installed on your system. You can download and install Python from the official Python website (https://www.python.org/).

2. **Install Jupyter using pip:**
   - Open a command-line interface (CLI) or terminal.
   - Run the following command to install Jupyter using pip, Python's package manager:
     ```
     pip install jupyterlab
     ```
   - Alternatively, you can install the classic Jupyter Notebook interface with:
     ```
     pip install notebook
     ```

3. **Launch Jupyter Notebook:**
   - After installation, you can launch Jupyter Notebook by typing the following command in your CLI or terminal:
     ```
     jupyter notebook
     ```
   - This command will start the Jupyter Notebook server and open a new tab in your web browser with the Jupyter Notebook interface.

4. **Start Using Jupyter Notebook:**
   - You can now create new notebooks, open existing ones, write code, execute cells, create visualizations, and more within the Jupyter Notebook interface.

KX Academy, available at [learninghub.kx.com/academy/](https://learninghub.kx.com/academy/), offers concise tutorials and structured courses for learning kdb+ and q, making it an ideal resource for users seeking to enhance their skills efficiently.

![image](https://github.com/OLLY27/KDB_Usage/assets/127981767/c28e9c14-c334-41a7-a7b4-1ab0ad135cc4)

### Working Examples

``` sh
// Create a list of numbers
nums: 1 2 3 4 5;

// Calculate the sum of the numbers
sum_nums: sum nums;

// Output the result
sum_nums
```

### Conclusion
**Benefits of Using Jupyter Notebook:**

1. **Interactive Environment:** Jupyter Notebook provides an interactive environment for writing code, running experiments, and visualizing data, enhancing productivity and collaboration.

2. **Support for Multiple Languages:** Supports multiple programming languages including Python, R, and Julia, allowing for versatile data analysis and experimentation.

3. **Rich Visualization:** Offers rich visualization capabilities with inline plotting, allowing users to create interactive charts, graphs, and visualizations directly within the notebook.

4. **Documentation and Explanation:** Enables users to combine code, narrative text, and visualizations in a single document, making it easier to document and share analyses and results.

5. **Integration with Data Science Tools:** Integrates seamlessly with popular data science libraries and tools such as pandas, NumPy, and scikit-learn, facilitating data manipulation, analysis, and machine learning tasks.

**Detriments of Using Jupyter Notebook:**

1. **Version Control Challenges:** Jupyter Notebook files are not always well-suited for version control systems like Git, leading to potential conflicts and difficulties in collaboration.

2. **Execution Order Dependency:** The order of code execution in Jupyter Notebooks can impact the results, making it important to run cells in the correct sequence to avoid errors and inconsistencies.

3. **Resource Intensive:** Jupyter Notebooks can be resource-intensive, particularly when working with large datasets or running computationally intensive tasks, potentially slowing down performance.

4. **Limited IDE Features:** While Jupyter Notebook provides basic code editing features, it lacks the advanced functionality and customization options of dedicated integrated development environments (IDEs).

5. **Dependency Management:** Managing dependencies and ensuring reproducibility can be challenging in Jupyter Notebooks, particularly when sharing or deploying analyses across different environments.

___________________________________________________
## KX Community 

Be sure to sign up to the KX Community too (like StackOverflow) for tips and pages - https://learninghub.kx.com/
