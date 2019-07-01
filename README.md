# MongoDB University
## M220J: MongoDB for Java Developers

This project is part of M220 course from MongoDB University

### Source: [https://university.mongodb.com/courses/M220J/about](https://university.mongodb.com/courses/M220J/about)

In order to run properly, the  _MFlix software_  project has some installation requirements and environmental dependencies.

These requirements and dependencies are defined in this lesson, and they can also be found in the  README.rst  file from the  mflix-java  handout. This lesson is to make sure you don't skip them!

If you haven't downloaded the  mflix-java  handout, please download it now.

After following this README, you should be able to successfully run the MFlix application.

# Table of Contents

1.  Project Structure
2.  Database Layer
3.  Local Environment Dependencies
4.  Java Project (MFlix) Installation
5.  MongoDB Installation
6.  MongoDB Atlas Cluster
7.  Importing Data
8.  Running the Application
9.  Running the Unit Tests

# Project Structure

MFlix is composed of two main components:

-   _Frontend_: All the UI functionality is already implemented for you, which includes the built-in React application that you do not need to worry about.
-   _Backend_:  _Java Spring Boot_  project that provides the necessary service to the application. The code is managed by a Maven project definition file that you will have to load into your Java IDE.

Most of what you will implement is located in the  src/main/java/mflix/api/daos  directory, which contains all database interfacing methods.

The unit tests in  src/test/java/mflix/api/daos  will test these database access methods directly, without going through the API.

The UI will run these methods as part of the integration tests, and therefore they are required for the full application to be running.

The API layer is fully implemented, as is the UI. By default the application will run on port 5000, but if you need it to run on a port other than 5000, you can edit the  index.html  file in the  build  directory to modify the value of  **window.host**. You can find  index.html  in the  src/main/resources/build  directory.

We're using  _Spring Boot_  for the API. Maven will download this library for you. More on that below.

# Database Layer

We will be using  _MongoDB Atlas_, MongoDB's official Database as a Service (DBaaS), so you will not need to manage the database component yourself. However, you will still need to install MongoDB locally to access the command line tools that interact with Atlas, to load data into MongoDB and potentially do some exploration of your database with the shell.

The following set of steps are here to get you setup for this course.

# Local Environment Dependencies

There are two main system dependencies in this course:

1.  Java 1.8

> -   The java version this course is built against is Java 1.8. You can download the appropriate version for your operating system by clicking  [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

2.  Maven

> -   We use Maven to manage dependencies for the MFlix project. Click here to download  [Maven](https://maven.apache.org/download.cgi). You can find detailed installation instructions on the Apache  [website](https://maven.apache.org/install.html).

# Java Project (MFlix) Installation

The  mflix  project is supported by a  Maven  POM file that deals with all the dependencies required, as well as providing the  test  and  run  commands to control our project. This means that you can run all the tests and deploy the  mflix  backend from the command line with  Maven.

However, we recommend you use a Java IDE to follow along with the lessons and to accomplish the  **Tickets**  assigned to you in the course.

You can use any IDE that you like, as you do not need to have a specific product to complete the course. It would be better if your IDE supports  Maven POM  files, so it can set the dependencies correctly, otherwise you will need to download and install manually the different libraries and drivers used by the project.

That said, all the lectures and examples of this course have been produced using IntelliJ IDEA CE edition. You will find a lesson dedicated to setting up and exploring this IDE for the course.

Once you downloaded and unzipped the  mflix-java.zip  file, you will find the project folder. The project folder contains the application code, the  pom.xml  file that you would import into your IDE, and the dataset required that you will have to import to Atlas.

$ ls
mflix README.rst
$ cd mflix
$ ls
src pom.xml data

## MongoDB Installation

It is recommended to connect  _MFlix_  with  _MongoDB Atlas_, so you do not need to have a MongoDB server running on your host machine. The lectures and labs in this course will assume that you are using an  _Atlas_  cluster instead of a local instance.

That said, you are still required to have the MongoDB server installed, in order to be able to use two server tool dependencies:

-   mongorestore
    -   A utility for importing binary data into MongoDB.
-   mongo
    -   The shell for exploring data in MongoDB.

To download these command line tools, please visit the  [MongoDB download center](https://www.mongodb.com/download-center#enterprise)  and choose the appropriate platform.

# MongoDB Atlas Cluster

_MFlix_  uses  _MongoDB_  to persist all its data.

One of the easiest ways to get up and running with MongoDB is to use  _MongoDB Atlas_, a hosted and fully-managed database solution.

If you have taken other MongoDB University courses like M001 or M121, you may already have an account - feel free to reuse that cluster for this course.

Make sure to use a  **free tier cluster**  for the application and course.

_Note: Be advised that some of the UI aspects of Atlas may have changed since the redaction of this README, therefore some of the screenshots in this file may be different from the actual Atlas UI interface._

## Using an existing MongoDB Atlas Account:

If you already have a previous  _Atlas_  account created, perhaps because you've taken one of our other MongoDB university courses, you can repurpose it for M220J.

Log into your  _Atlas_  account and create a new project named  **M220**  by clicking on the  _Context_  dropdown menu:

![https://s3.amazonaws.com/university-courses/m220/cluster_create_project.png](https://s3.amazonaws.com/university-courses/m220/cluster_create_project.png)

After creating this new project, skip the next section and proceed to the  _Creating an M0 free tier cluster mflix_  section.

## Creating a new MongoDB Atlas Account:

If you do not have an existing  _Atlas_  account, go ahead and  [create an Atlas Account](https://cloud.mongodb.com/links/registerForAtlas)  by filling in the required fields:

![https://s3.amazonaws.com/university-courses/m220/atlas_registration.png](https://s3.amazonaws.com/university-courses/m220/atlas_registration.png)

## Creating an M0 free tier cluster  **mflix**:

_Note: You will need to do this step even if you are reusing an Atlas account._

1.  After creating a new project, you will be prompted to create the first cluster in that project:

> ![https://s3.amazonaws.com/university-courses/m220/cluster_create.png](https://s3.amazonaws.com/university-courses/m220/cluster_create.png)

2.  Choose AWS as the cloud provider, in a Region that has the label  **Free Tier Available**:

> ![https://s3.amazonaws.com/university-courses/m220/cluster_provider.png](https://s3.amazonaws.com/university-courses/m220/cluster_provider.png)

3.  Select  _Cluster Tier_  **M0**:

> ![https://s3.amazonaws.com/university-courses/m220/cluster_tier.png](https://s3.amazonaws.com/university-courses/m220/cluster_tier.png)

4. Set  _Cluster Name_  to  **mflix**  by scrolling to the appropriate section and clicking on the default name  _Cluster0_, and click  _Create Cluster_:

> ![https://s3.amazonaws.com/university-courses/m220/cluster_name.png](https://s3.amazonaws.com/university-courses/m220/cluster_name.png)

5.  Once you press  _Create Cluster_, you will be redirected to the account dashboard. In this dashboard, make sure that the project is named  **M220**. If not, go to the  _Settings_  menu item and change the project name from the default  _Project 0_  to  **M220**:

> ![https://s3.amazonaws.com/university-courses/m220/cluster_project.png](https://s3.amazonaws.com/university-courses/m220/cluster_project.png)

6.  Next, configure the security settings of this cluster, by enabling the  _IP Whitelist_  and  _MongoDB Users_:

> ![https://s3.amazonaws.com/university-courses/m220/cluster_ipwhitelisting.png](https://s3.amazonaws.com/university-courses/m220/cluster_ipwhitelisting.png)
> 
> Update your IP Whitelist so that your app can talk to the cluster. Click the "Security" tab from the "Clusters" page. Then click "IP Whitelist" followed by "Add IP Address". Finally, click "Allow Access from Anywhere" and click "Confirm".
> 
> _Note that in a production environment, you would control very tightly the list of IP addresses that can connect to your cluster._
> 
> ![https://s3.amazonaws.com/university-courses/m220/cluster_allowall.png](https://s3.amazonaws.com/university-courses/m220/cluster_allowall.png)

7.  Then create the MongoDB database user required for this course:

> -   username:  **m220student**
> -   password:  **m220password**
> 
> You can create new users through  _Security_  ->  _MongoDB Users_  ->  _Add New User_
> 
> Allow this user the privilege to  **Read and write to any database**:
> 
> ![https://s3.amazonaws.com/university-courses/m220/cluster_application_user.png](https://s3.amazonaws.com/university-courses/m220/cluster_application_user.png)

8.  When the user is created, and the cluster deployed, you have the option to  Load Sample Dataset. This will load the Atlas sample dataset, containing the MFlix database, into your cluster:
    
    ![https://s3.amazonaws.com/university-courses/m220/load_sample_dataset.png](https://s3.amazonaws.com/university-courses/m220/load_sample_dataset.png)
    
    **Note: The MFlix database in the Sample Dataset is called "sample_mflix".**
    
9.  Now you can test the setup by connecting via the  mongo  shell. You can find instructions to connect in the  _Connect_  section of the cluster dashboard:
    

> ![https://s3.amazonaws.com/university-courses/m220/cluster_connect_application.png](https://s3.amazonaws.com/university-courses/m220/cluster_connect_application.png)
> 
> Go to your cluster  _Overview_  ->  _Connect_  ->  _Connect Your Application_. Select the option corresponding to MongoDB version 3.6+ and copy the  mongo  connection URI.
> 
> The below example connects to  _Atlas_  as the user you created before, with username  **m220student**  and password  **m220password**. You can run this command from your command line:
> 
> mongo "mongodb+srv://m220student:m220password@<YOUR_CLUSTER_URI>"
> 
> By connecting to the server from your host machine, you have validated that the cluster is configured and reachable from your local workstation.

# Importing Data (Optional)

**Note: if you used Load Sample Dataset, you can skip this step.**

The  mongorestore  command necessary to import the data is located below. Copy the command and use the  _Atlas SRV_  string to import the data (including username and password credentials). If you have earlier versions of MongoDB installed on your machine, please make sure to use the 3.6 version for this project.

Replace the SRV string below with your own:

### navigate to mflix directory cd mflix-java/mflix
##### import data into Atlas mongorestore --drop --gzip --uri mongodb+srv://m220student:m220password@<YOUR_CLUSTER_URI> data

### import data into Atlas
##### mongorestore --drop --gzip --uri mongodb+srv://m220student:m220password@<YOUR_CLUSTER_URI> data

# Running the Application

In the  mflix/src/main/resources  directory you can find a file called  application.properties.

Open this file and enter your  _Atlas SRV_  connection string as directed in the comment. This is the information the driver will use to connect. Make sure  **not**  to wrap your  _Atlas SRV_  connection between quotes:

spring.mongodb.uri=mongodb+srv://m220student:m220password@<YOUR_CLUSTER_URI>

To run MFlix, run the following command:

cd mflix
mvn spring-boot:run

And then point your browser to  [http://localhost:5000/](http://localhost:5000/).

It is recommended you use an IDE for this course. Ensure you choose an IDE that supports importing a Maven project. We recommend IntelliJ  [Community](https://www.jetbrains.com/idea/download)  but you can use the product of your choice.

The first time running the application might take a little longer due to the initial setup process.

# Running the Unit Tests

To run the unit tests for this course, you will use  JUnit. Each course lab contains a module of unit tests that you can call individually with a command like the following:

cd mflix
mvn -Dtest=<TestClass> test

For example to run the ConnectionTest test your shell command will be:

cd mflix
mvn -Dtest=ConnectionTest test

Alternatively, if using an IDE, you should be able to run the Unit Tests individually by clicking on a green play button next to them. You will see this demonstrated in the course as we will be using IntelliJ.

Each ticket will contain the command to run that ticket's specific unit tests. When running the Unit Tests or the Application from the shell, make sure that you are in the same directory as the  pom.xml  file.
