# How to Setup Zeppelin in Debain


### Zeppelin
Zeppelin is a web-based notebook that enables data-driven,
interactive data analytics and collaborative documents with SQL, Scala and more.

## Let's Start

To work with zeppelin, we need to install some prerequisties 
 - Oracle JDK 	1.7 or 1.8 (set JAVA_HOME)
 -  OS        -  Mac OSX/Ubuntu 14.X /                CentOS 6.X /  Windows 7 Pro

## Installing Java and setting path for jdk
As I mentioned above zeppelin needs java to work properly. For that we need to download jdk 1.7 or 1.8. And also need to set the path variable for java. So we can restart java services from any directories.
So download jdk from the following link:
https://www.oracle.com/technetwork/java/javaee/downloads/java-ee-sdk-6u3-jdk-7u1-downloads-523391.html

And extract the jdk where you want to store. Better thing is extract it in Home folder in ubuntu and C drive in Windows
## Setting the path variable for Java
For this simply copy the jdk directory. Then open bashsrc file using terminal. And just paste at the end of that file.
we need to open editor. 
Just type the below things:
```
sudo gedit .bashsrc
``` 
And at the end of the file write this:
```
export $JAVA_HOME=/home/<username>/<jdk directory name>
```
for example
```
export export JAVA_HOME=/home/user/jdk1.8.0_191
```

### Installing Apache Zeppelin from binary package.

Download zeppelin binary file
http://zeppelin.apache.org/download.html

Just download all interpreter package: unpack it in a directory of your choice and you're ready to go.

But before starting the appache Zeppelin we have to do 2 things:

- Setting the javapath in .sh file

 Like how we set the java path variable for jdk, we also need tospecify the java path name for Zeppelin too,
 For that open the "conf" directory then rename the file "zeppelin-env.sh.template" as "zeppelin-env.sh" and open it.
 And type the $JAVA_HOME at there.
ie, 
```
export $JAVA_HOME=/home/<username>/<jdk directory's name>
```
For example :  
```
        export JAVA_HOME=/home/user/jdk1.8.0_191
```
  

-  Changing the port number (Optional)
 This is optional, because zeppelin will work even if we skip this step.
 But most of the appache applications are work under the same portnumber, ie,port number 8080, So if more than one appache applications are working, it will be a problem. So better thing changing the portnumber from 8080 to other number:
 General convention is changing it into 8082.(I changed portnumber into 8082)
 
 For that go the "conf" directory. From that directory change 

Starting Apache Zeppelin
Starting Apache Zeppelin from the Command Line

just go to the bin and run the zeppelin-daemon.sh. (If you are using a windows enviornment just run the zeppelin.cmd ,ie,command file )

for that go the folder where the zepplin folder is extracted, 
for example:
```
cd zeppelin-0.8.0-bin-all
``` 


On all unix like platforms:
```
bin/zeppelin-daemon.sh start
```
If you are on Windows:
```
bin\zeppelin.cmd
```
Now the zeppelin is started. So open a browser and just type 
```
 localhost:8082
```
Next you need to start the corresponding interpreters for getting the services.
****************************************

 
*********************************************
### MySql Integration with Zeppelin

How to connect zeppelin with mysql.
Zeppelin can able to connect with many technologies. We use to call those technologies as intrepreters. There is some default intrepreters are already there in Zeppelin. ie, Zeppelin can able to connect those technologies default. But if you want to add some other intrepreter which is not in zeppelin, then it is also possible to create our own intrepreter.
So let's see how to connect this with Mysql. By default zeppelin doesn't have that intrepreter.
To create a new intrepreter.Click on the create button on the top lef corner.
 ![](https://zeppelin.apache.org/docs/0.8.0/assets/themes/zeppelin/img/docs-img/click_create_button.png)
 Fill Interpreter name field with whatever you want to use as the alias (e.g. mysql, mysql2, hive, redshift, and etc..). Please note that this alias will be used as %interpreter_name to call the interpreter in the paragraph. Here we are
 using 'mysql' as the intrepreter name. Then select 'jdbc' as an Interpreter group. 

![](https://zeppelin.apache.org/docs/0.8.0/assets/themes/zeppelin/img/docs-img/select_name_and_group.png|width=100)

 The default driver of JDBC interpreter is set as PostgreSQL. It means Zeppelin includes PostgreSQL driver jar in itself. But If you want to connect other database like Mysql, you need to edit the property values. You can also use Credential for JDBC authentication. If default.user and default.password properties are deleted for database connection in the interpreter setting page, the JDBC interpreter will get the account information from Credential.
The below example is for Mysql connection. So let's try these values.
![](https://zeppelin.apache.org/docs/0.8.0/assets/themes/zeppelin/img/docs-img/edit_properties.png)


The last step is Dependency Setting. 
Since Zeppelin only includes PostgreSQL driver jar by default, you need to add each driver's maven coordinates or JDBC driver's jar file path for the other databases.
![](https://zeppelin.apache.org/docs/0.8.0/assets/themes/zeppelin/img/docs-img/edit_dependencies.png)

## How to test
### Run the paragraph with JDBC interpreter

To test whether your databases and Zeppelin are successfully connected or not, type %jdbc_interpreter_name(e.g. %mysql) at the top of the paragraph and run show databases.
```
%jdbc_interpreter_name
show databases
```
If the paragraph is `FINISHED` without any errors, a new paragraph will be automatically added after the previous one with `%jdbc_interpreter_name`. So you don't need to type this prefix in every paragraphs' header.
For example:
![](https://zeppelin.apache.org/docs/0.8.0/assets/themes/zeppelin/img/docs-img/run_paragraph_with_jdbc.png)




