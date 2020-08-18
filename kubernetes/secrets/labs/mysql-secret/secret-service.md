#### Objective

In this lab, you will learn how to how deploy a MySQL server using Cloudplex integrated Docker-Hub which will be used to pull pre-build MySQL image and use Cloudplex secret service to store Kubernetes Secret.

#### Cloud Provider

CloudPlex platform gives you the freedom of choosing you any cloud provider among these four (AWS, AZURE, GCP and DO). Please select any of them to proceed.

#### Cloud Profile Credentials

You have to provide your selected cloud credentials in order to further continue this lab. There are fields under each cloud provider tab, fill them out.

Click on the **next** button on the top right corner.

#### Add Secret Service

CloudPlex platform provides a secret management service that provides the ability to store sensitive data such as passwords, tokens, and certificates in Cloudplex. Any data entered in this service is stored in a secure vault with at-rest encryption. This eventually becomes a [Kubernetes Secret](https://kubernetes.io/docs/concepts/configuration/secret) in a deployed application.

To configure the service, Drag-n-drop **Secret service** from pallet to the canvas.

![secret-service](images/secret-service-drag.gif)

Click on the service to open the configuration panel on the right side.

The platform will populate the default values of service (Service Id, Service Name, Namespace)

Update Service Id and Service Name to ***mysql-secret***

![secret-service-info](images/mysqlsecret.png)

By default, the type of secret is Opaque, you can choose different types according to your use case.

![secret-service-type-opaque](images/secret-type.png)

Click on Add secret string and type ***MYSQL_ROOT_PASSWORD*** in key and the Password in the value field. For this lab, type (the password as shown) ***5dzo2MsriVJNYTTtud8gOyDc3A*** in the value field.

![secret-key-password](images/secret-password.png)

```yaml
key : MYSQL_ROOT_PASSWORD
value : 5dzo2MsriVJNYTTtud8gOyDc3A
```

Click on save button to save service

![button-save](images/save-button.png)


#### Configure the MySQL Container

Drag-n-drop the ***Docker Hub*** service from pallet to the canvas.

![docker-hub-service](images/docker-hub-service.gif)

Drag the arrow from ***Secret*** service to ***Container*** service.

![dockerhub-secret-link](images/link-docker-secret.gif)

Click on the service to open the configuration panel on the right side.

![docker-hub-service-configuration](images/service-configuration.png)

Type MySQL in the search bar and click on the search button.

![mysql-search](images/mysql-search.png)

Select MySQL service.

![mysql-service](images/mysql-service.png)

CloudPlex automatically pulls all the tags and metadata of the image and populates default values of service (Service Id, Service Name, Namespace, Type)


##### Add new Environment Variables 

Click on the **Environment variables section** to add a new [environment variable](https://kubernetes.io/docs/tasks/inject-data-application/define-environment-variable-container/#define-an-environment-variable-for-a-container).

Cloudplex provides two types of variables ([Static](https://docs.cloudplex.io/#/pages/user-guide/components/k8s-resources/container/container), [Dynamic](https://docs.cloudplex.io/#/pages/user-guide/components/k8s-resources/container/container)). We are going to use Dynamic variable in this lab to use the ***Secret*** key in our container

![dynamic-parameters](images/dynamic-parameters.gif)

Select mysql-secret from the service drop-down and type MYSQL_ROOT_PASSWORD in the key field.

![dynamic-variables-key](images/dynamic-variables.png)

Expand ***Service Attributes*** and Secrets Data and select ***MYSQL_ROOT_PASSWORD***. Cloudplex automatically generates dynamic  parameters for you.

![dynamic-variables-key-select](images/dynamic-variables-key-select.png)

Click on the save button to save the parameters.

![save-button-2](images/save-button-2.png)

A new environment variable with the key ***MYSQL_ROOT_PASSWORD*** will be added in the list of Environment Variables.

![saved-environment-variable](images/saved-environment-variable.png)

Click on the back button on top of the configurations.

![back-button](images/back-button.png)


##### Add new Port

[Ports](https://kubernetes.io/docs/concepts/services-networking/connect-applications-service/#the-kubernetes-model-for-connecting-containers) are required to access your applications. Click on the **Port section** to add a new port

![Add-Ports-01](images/add-ports-01.png)

Cloudplex automatically discovers ports from Docker images and populates them in the ports section of the service.

![Add-Ports-02](images/add-ports-02.png)

Click on the save button to save the service.

![service-save](images/save-button-3.png)


#### Save Application

Click on the **Save** button at the top right corner, On saving the application you will be taken to the status page.

![save-app](images/save-app.png)



#### Deploy MySQL on the Cluster

Click on the Start button to start deploying the application on the cluster you have created.

![app-start-button](images/app-start.png)

In the log window, you can see the logs of your infrastructure, Kubernetes Cluster and Application which you have deployed.

![app-deployment-logs](images/app-deployment-logs.png)

**!! Deployment will take around 15 minutes!!** 

You can see the status of the application you just deployed by clicking on the app tab and click on Table view to see the realtime status of the services.

![app-status](images/app-status.png)


#### Cleanup

To avoid unnecessary costs, don’t forget to terminate your application when you are done.
Click on the terminate button to delete all your resources from Cloud.

![app-cleanup-01](images/termination.png)