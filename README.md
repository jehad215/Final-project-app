## CI/CD Pipeline To Deploy a backend app

### Second part of project: CI/CD

### Create credintials in Jenkins:
 - Dockerhub credintials
 - Credintials for the new service account 
![](./images/jenkins%20credentials.png)

### CI pipeline:
#### 1. Pull code from GitHub
![](./images/pipeline.png)

#### 2. Create Dockerfile
- to dockerize the app
```bash
$ docker build -t jehad21/app .
$ docker push jehad21/app
```
#### 3. Trigger CD pipeline to run
 - On jenkins
![](./images/web.png)

 - On GitHub 
![](./images/webhook.png)

###  Least but not least
![](./images/piprun.png)
![](./images/pipeline-build.png)

###  And Voila! Application is successfully deployed
![](./images/app.png)

### Finally: Destroy all resources
```bash
$ terraform destroy
```
