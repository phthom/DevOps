

---
# Microclimate and Jenkins Lab
---


![microclimate](images/mcmicroclimate.png)
This lab is compatible with ICP version 3.1

---


In this tutorial, you create, install, deploy and run a **cloud-native microservice application** on an IBM® Cloud Private platform on Kubernetes.

Microclimate will guide you thru the creation of complete project including all the directories, the manifest files, the monitoring option that you need for a perfect application.

[Link to Microclimate documentation here](https://microclimate-dev2ops.github.io/)

---




# Task 1: Access the console and check Helm


From a machine that is hosting your environment, open a web browser and go to one of the following URLs to access the IBM Cloud Private management console:
  - Open a browser
  - go to https://ipaddress:8443
  - Where ipaddress is the ip address of the ICP cluster given by the instructor with the password.

![Login to ICP console](./images/login2icp.png)



# Task 2: Check Microclimate

Application workloads can be deployed to run on an IBM Cloud Private cluster. The deployment of an application workload must be made available as a Helm package. Such packages must either be made available for deployment on a Helm repository, or loaded into an IBM Cloud Private internal Helm repository. 

Microclimate has been installed for you on a specific IBM Cloud Private cluster instance. To check that Microclimate and Jenkins are running, go to the ICP console, then **open the hamburger menu on the top left part of the page, then click on Workloads and Helm Releases **



![image-20190308141646744](images/image-20190308141646744-2051006.png)



Then on the search field type **microclimate** (this will search all helm releases containing microclimate string)

![image-20190308141818349](images/image-20190308141818349-2051098.png)

Microclimate should be already deployed and the light should be green. The latest version is 1.11.0.

Click on the blue link (i.e **microclimate**) :

![image-20190308142252004](images/image-20190308142252004-2051372.png)

Browse the page to the bottom to look at the **Deployment section** :

![image-20190308151545678](images/image-20190308151545678-2054545.png)

Check that you have all 1 in all columns for the 4 deployments. 

Then go to the **bottom** of that page :

![image-20190308151710072](images/image-20190308151710072-2054630.png)



Copy the URL : https://microclimate.ipaddress.nip.io

Finally get access to the **Microclimate portal** with the following link in your browser:

`https://microclimate.<ipaddress>.nip.io`
(replace <ipaddress> with your icp ip address)

Accept the license agreement:

![Accept the license](./images/mcaccept.png)

You should click on **No, not this time** and  **Done** and then you are on the main menu:
![Main](./images/mcaccess.png)

This concludes the Microclimate login. 

> Note: this installation can also be done thru the ICP Catalog.


# Task 3: Install a simple application

You’re now ready to deploy your Kubernetes application to the IBM Cloud Private environment.  In this case, the deploy command will :


Click on **New project** button:

![project](./images/mcproject.png)

Choose Node.JS (because we want to create a Node.js application) and type the name: **nodeone** and click **Next**

![image-20190308152249201](images/image-20190308152249201-2054969.png)

On the next menu, don't choose any service (but you can notice that we can bind a service to your new application), then click on **Create**

![image-20190308152416608](images/image-20190308152416608-2055056.png)

Be patient (it could take a **few minutes**). Your application should appear and the building process could still be running: 

![image-20190308152538052](images/image-20190308152538052-2055138.png)



After a few minutes, the application should be running (check the green light):

![image-20190308152803014](images/image-20190308152803014-2055283.png)

To access the application, click on the **Open App** button on the left pane:

![image-20190308152831529](images/image-20190308152831529-2055311.png)

The application should appear (this is a very simple page):

![image-20190308152908524](images/image-20190308152908524-2055348.png)

Navigate on the left pane to the **Edit** button:

![image-20190308153005837](images/image-20190308153005837-2055405.png)



At this point, the editor can be used to edit the Node.JS application.

![image-20190308153615235](images/image-20190308153615235-2055775.png)

Expand **nodeone** and you can see all predefined files (like Dockerfile, Jenkinsfile, manifest files) and you can look around the code and files necessary for your application. 

![image-20190308153925679](images/image-20190308153925679-2055965.png)

Expand **nodeone>public>index.html**

![index](./images/mcindex.png)

Go to the end of the index.html file and modify the **congratulation** line by adding your name :

![congratulation](./images/mcmodify.png)

Save (**File>Save**) and then re-build the application (because Auto Build is on, building will start automatically after saving) .

Wait until the green light(Running) to see the modification your simple application:

![build](./images/mcpht.png)

From the main menu of the application, click on **Monitor** to see some metrics:

![build](./images/mcmon.png)



From here, Click on Projects at the top of the page:

![image-20190308154744243](images/image-20190308154744243-2056464.png)



# Task 4: Import and deploy an application

To import a new application from Github, click on the **Project** button. Then choose **Import project**:

![build](./images/mcimport.png)

On the Import page, type `https://github.com/microclimate-demo/node` as the Git location :

![image-20190308154844264](images/image-20190308154844264-2056524.png)

Enter a name : `nodetwo` and click **Finish import and validate**

![image-20190308154938734](images/image-20190308154938734-2056578.png)

The validation will detect automatically detect the type of project and then click on **Finish Validation**:

![image-20190308155104877](images/image-20190308155104877-2056664.png)



Wait until the application is running (it could take 1 minute) : 

![build](./images/mcbuild2.png)

Click on **Open App** icon to go to the application:

![build](./images/mcapp2.png)


# Task 5: Use a pipeline

Microclimate has been linked with Jenkins and so you don't have to install a separated Jenkins instance in IBM Cloud Private. 

Goto the **pipeline** icon and **create a pipeline**:

![image-20190308155730684](images/image-20190308155730684-2057050.png)

Type a pipeline name **pipe2** and a repository to get the application (optional)

![image-20190308155928017](images/image-20190308155928017-2057168.png)  



 Click on **Create pipeline**:

![image-20190308160044319](images/image-20190308160044319-2057244.png)

![image-20190308160140683](images/image-20190308160140683-2057300.png)

Click on **Open Pipeline** to get access to Jenkins  (enter your credentials at some point):

![image-20190308160247361](images/image-20190308160247361-2057367.png)



Wait until the progression ends:

![build](./images/mcstage.png)



![image-20190308163403858](images/image-20190308163403858-2059243.png)



# Congratulations

You have successfully created and installed a microservice application with Microclimate.



![icp000](images/icp000.png)