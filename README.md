# K8cproject


# Overview:
This project is to containerise an application using Docker, deploy it to kubernetes cluster and access it through Nginx.

# Task 

## 1. Created a new project director in my workspace folder on my local system 

                mkdir Doc-k8project

 ![A new directory created](./img/1.%20A%20new%20directory%20created.png)

 ## Created a html file( index.html) and a css file ( style.css)

                touch index.html
                touch styles.css 


 ![created html file and a css file](./img/2.%20created%20an%20index%20file%20and%20css%20file%20in%20the%20new%20directory.png)

 ## 2.  Initialize a git repository in the project directory

                  git init 
  ![initialized a git repository](./img/3.%20git%20init,%20git%20add%20and%20commit.png)                

 ##   3. Git add and commit initial code to the repository 
 

                     git add . 

                   git commit -M "first commit"
![git add and commit](./img/3.%20git%20init,%20git%20add%20and%20commit.png)

##  4. Dokerize the application, 
A docker file specifiying Nginx as the base image 

               touch Dockerfile 
![Created a docker file with nginx as the base image](./img/4.%20Dockerfile%20created.png)

Contents defined, From the base image, setting the working directory, coping the local html and css file to the Nginx default public directory 

![content of the dockerfile](./img/5.%20content%20of%20dockerfile.png)


            Docker build -t nginx-projectapp . 

![building the dockerfile](./img/9.%20docker%20build.png)



I generated a simple index.tml file and a style.css file using  ChatGpt for a simple web application for this project. 

![content of the index.html file](./img/6.%20edit%20both%20files.png)

![content of the index.html file](./img/7.%20a%20simple%20index%20html%20file.png)


![content of the styles.css file](./img/8%20.%20a%20simple%20styles.css%20file.png)

edit each file and saved the content in the files and saved. 


                vim index.html
                vim styles.css

## 5. Logged in to docker hub( i have docker desktop installed on my system)

                    Docker login 

i had my docker destop already installed and running 

![Docker login](./img/9.%20docker%20login%20succeeded.png)

## Pushing docker image to Docker hub, firstly i had to tag my image
* The image to tag is **nginx-projectapp** 

    
            docker tag nginx-projectapp timipahozori/nginx-projectapp:1.0 

![Tagging your image](./img/12.%20docker%20tag.png)


                Docker push timipahozori/nginx-projectapp:1.0


![Docker push after the tag](./img/13.%20docker%20push.png)        

## 6. Setting up KIND( Kubernetes in docker) installation and creating the kind cluster

  I installed Kind on my windows system, i downloaded the .exe and ran the installer and installed kubectl earlier in the project class. 

To confirm  the installation 

                    kind --version

![Kind installation and confirmation](./img/14.%20Kind%20already%20install,%20after%20down%20load.png)


                   kind create cluster 

![kind cluster ](./img/15.%20kind%20cluster%20created.png)

                    kubectl get nodes

![kind cluster info](./img/16.%20kind%20cluster%20info(%20kubectl%20already%20installed).png)


## 7. Deploy Kuburnetes 
Created a new directory for the yaml files

![Created an directory ](./img/17.%20create%20new%20directory%20fof%20yaml%20files.png)

                vim my-nginx-deployment.yaml
Created a the deployment yaml file, defined the name of deployment, replicas and containers.
Port opening : 80 

![Content of deployment](./img/18.%20content%20of%20deployment%20yaml%20file.png)


              kubectl apply -f my-nginx-service.yaml

![applying of deployment yaml file](./img/21.%20created%20deployment%20and%20service%20yaml.png)    


## 8. Create  a service (ClusterIP)

 Created a service yaml file 

                vim my-nginx-service.yaml 

![creating service yaml](./img/19.%20create%20service%20yaml%20file.png)



![Editing service yaml file ](./img/20.%20content%20of%20service%20yaml%20file.png) 


Service yaml file 

![apply service yaml file](./img/21.%20created%20deployment%20and%20service%20yaml.png)


           kubectl apply -f my-nginx-service.yaml
    
## Confirm Deployment and Service 

                kubectl get deployments 
                kubectl get services

![Confirming](./img/22.%20confirm%20deployment%20and%20service.png)


## Port foward to the service to access to access the application locally 

                kubectl port-forward service/my-nginx-service 8080:80

![Port foward](./img/23.%20port%20forwarding.png)


## Opened my browser to visit the specified port to  view the simple frontend application 


![Accessing](./img/24.%20port%20forwarding%20done%20and%20accessing%20via%20local%20host%20and%20port.png)



