# Part 1: Install Nexus on AWS EC2 Instance:
- I installed Nexus on AWS EC2 instance, set up a nexus server, gave it ownership over the nexus application, started the application and then configured Nexus.
<img width="1102" height="761" alt="image" src="https://github.com/user-attachments/assets/76410283-8ff3-4cb5-8afc-778d809aa0d8" />
- Use the ff links for steps on how to do this:
[Link1](https://medium.com/@wealthiscertain/setting-up-nexus-and-sonarqube-servers-on-aws-ec2-450555695711)
[Link2](https://dev.to/himanshusinghtomar/setting-up-nexus-repository-on-aws-ec2-with-terraform-and-publishing-a-custom-gradle-plugin-p1)

# Part 2: Create npm hosted repository
I first cloned a repo that I had forked containing all the code I needed:

```
git clone https://gitlab.com/munodennis/node-app.git
```
- I will create a new repository with a new blob store:

- To create my new blob store I will navigate to System Status > Repository > Blob Stores > Create Blob Store:
<img width="828" height="343" alt="image" src="https://github.com/user-attachments/assets/82c84d7c-783e-407b-aa18-a2961eb9ea94" />
- I will then setup the page as follows and then create my blob store:
<img width="800" height="719" alt="image" src="https://github.com/user-attachments/assets/12a2cfb1-fe57-4372-8cf0-3b724ede695b" />
- I will then create my repo by navigating to System Status > Repository > Repositories > Create repository:
<img width="815" height="416" alt="image" src="https://github.com/user-attachments/assets/ce04b3f3-ce47-4566-8237-9461cb530201" />
- I will select npm hosted:
<img width="813" height="202" alt="image" src="https://github.com/user-attachments/assets/1be88549-0a3c-4b2f-a1f3-0cca5b33ccbf" />
- I will setup my settings for my repository as follows:
  <img width="773" height="580" alt="image" src="https://github.com/user-attachments/assets/0fde2a8a-9827-4091-8e65-0be5af841ff6" />
<img width="776" height="435" alt="image" src="https://github.com/user-attachments/assets/c5e142b7-774c-4191-a24a-a5e4d3fc3ce2" />
- I will then create my repo

# Part 3: Create user for team 1
- I will navigate to System Status > Security > Roles:
<img width="796" height="687" alt="image" src="https://github.com/user-attachments/assets/d82aacf3-7c60-40db-bc9e-78e51816106c" />
<img width="745" height="724" alt="image" src="https://github.com/user-attachments/assets/b4b75dd6-4f65-4572-9514-7fd867a3c236" />
<img width="731" height="118" alt="image" src="https://github.com/user-attachments/assets/a334b828-9c13-4108-ab7c-647f964eecd0" />
- I will then navigate to System Status > Security > Users > Create local user and setup my settings as follows:
<img width="773" height="678" alt="image" src="https://github.com/user-attachments/assets/7a67b7ae-431c-4f57-aa19-2f498c287629" />

# Part 4: Build and publish npm tar
- Ensure that in Settings > Security > Realms , NPM Bearer Token Realm is set to active:
<img width="770" height="690" alt="image" src="https://github.com/user-attachments/assets/476304fd-cadb-4e8b-bd07-cb833f77daac" />
- In the directory of the node app I will run the command:
```
npm login --registry=http://54.145.29.176:8081/repository/npm-hosted-repo/
npm publish --registry={npm-repo-url-in-nexus}
```
<img width="556" height="155" alt="image" src="https://github.com/user-attachments/assets/9ec3ca52-c314-48a6-b0f1-0569128e1b8e" />
<img width="995" height="387" alt="image" src="https://github.com/user-attachments/assets/8e4b936c-3f33-47fd-9abb-32350d80c0b8" />
- When we navigate to the repo, voila!
<img width="391" height="166" alt="image" src="https://github.com/user-attachments/assets/172372fb-02da-4a95-8c5d-a42bba0d0bb7" />

# Part 5: Download from Nexus and start application
- I will SSH into my server running my Nexus server:
- To query the Nexus REST API to get the download info for our NodeJS artifact I will use the command below to get info about our repositories with respect to a certain user:
```
curl -u <nexus-user>:<nexus-user-password> -X GET 'http://<nexus-server-ip>:8081/service/rest/v1/repositories'
```
<img width="598" height="147" alt="image" src="https://github.com/user-attachments/assets/4637bd89-b28f-4266-9e0a-827344ba38a8" />

- Now to get info about contents of a particular repo, I will use the curl command to query my repo below:
```
curl -u <nexus-user>:<nexus-user-password> -X GET 'http://<nexus-server-ip>:8081/service/rest/v1/components?repository=<name-of-repo'
```
<img width="1057" height="625" alt="image" src="https://github.com/user-attachments/assets/a44ef88d-de83-435e-9446-fb545cd1e2fb" />
- I will download the artifact using the downloadURl by the command:
```
wget http://54.145.29.176:8081/repository/npm-hosted-repo/nodejs-app/-/nodejs-app-1.0.0.tgz://54.145.29.176:8081/repository/npm-hosted-repo/nodejs-app/-/nodejs-app-1.0.0.tgz
```




  


























 



