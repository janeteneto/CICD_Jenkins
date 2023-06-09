# CICD Jenkins

## What is Jenkins?
- Open-source automation server that helps automate parts of the software development process, including building, testing, and deploying software.
- Built on Java and can run on various operating systems, including Windows, macOS, and Linux.
- Provides a web-based graphical user interface (GUI) that allows users to configure and manage automation jobs, as well as a command-line interface (CLI) for more advanced usage.
- Can integrate with various tools and technologies, including version control systems like Git, build tools like Apache Maven, testing frameworks like JUnit, and containerization tools like Docker. It can also integrate with cloud platforms like Amazon Web Services (AWS) and Microsoft Azure.

## What are the Jenkinks stages?
- A way to divide a pipeline into logical units of work or phases.
- Provides a visual representation of the pipeline, showing the progress of the pipeline and highlighting any errors or failures in the pipeline.
- Can be defined in the pipeline script or through the Jenkins GUI.
- Each stage can have one or more steps, which represent the actual work being done.


## Difference between Continuous Delivery (CI) and Continuous Development (CDE)

![image](https://user-images.githubusercontent.com/129942042/235732809-ec7f1df1-a949-4063-a712-4a6f6e2b9b40.png)

- **Continuous Delivery** is a software development practice that involves automatically building, testing, and preparing code changes for release.
- **Continuous Deployment**, on the other hand, is a practice where code changes are automatically deployed to production as soon as they pass the automated testing phase.
- The main difference between CD and CDE is that **CD** involves a manual approval process before releasing code changes to production, while **CDE** automates the entire release process, including deploying the changes to production. CD allows for more control over when and how code changes are released, while CDE can result in faster and more frequent releases but with a higher risk of issues.

# Connect Jenkins with Gihub repo

![2023-05-02](https://user-images.githubusercontent.com/129942042/235733268-faf79e11-5768-4338-b954-7a1cc5bc30fb.png)

1. Open a terminal and `cd` into the `.ssh` folder

2.  Create a new key par with the following command:
````
sss-keygen -t rsa -b 4096 -C janeteneto26@gmail.com
````
- This creates a public key and a private key

3. Give it a convenient name. I named it `janete-jenkins-key`

- Have a repository with the app folder on GitHub ready. I forked someone else's repo.

4. Grab the public key from the terminal by running the command `cat janete-jenkins-key.pub` and add it to the repo, on the `deploy keys` section.

- Now, on the Jenkins page:

5. Create a new job and name it conveniently (this will be an agent node)

- On the job's settings:

6. Tick `discard old builds` and set the max # to 3 or any number you think is appropriate.

7. Tick `Github project` and paste the HTTPS link of your repo

8. On the Office 365 section, tick `Restrict where this project can be run` and type `sparta-ubuntu-node` (or don't if you don't have this option)

9. On the Source Code Management section select `Git` 

10. Paste your SSH link of your repo

11. On credentials select `jenkins` and press add key

12. Change kind to `SSH private key`

13. Type your key's name in the username field

14. Tick `private key` and press add

15. Copy and paste your private key in the field

16. Leave branch name blank and press add

17. On the Build Environment section tick `Provide node & npm`

18. Select the pre-created `Sparta-Node-JS`

19. On the Build section select `execute shell` and add the following code:
````
cd app
npm install
npm test
````

20. Save the job and check its status to see if it worked.

## Webhook Configuration

1. Create a webhook for jenkins (end point) on Github on the app repo:

![2023-05-03](https://user-images.githubusercontent.com/129942042/235941170-e3b6b2cb-22b0-406b-a88c-8260e8151ea8.png)

2. On the terminal, create a `dev` branch. Remember you need to `cd` into your app repo first and then use the command:
````
git checkout -b dev
````

3. Make change to the app's README file, add, and commit them

4. Run `git push -u origin dev` to push the changes

5. Run `git merge dev` to 

5. Create job called janete-ci-merge

5. Run `git push -u origin dev`

9. push the code to github which should trigger the job
10. if the tests passed, they should merge the code to main branch
11. create 3rd job to push code to production
12. create ec2 instance
13. create sg rule to allow jenkins ip

create new key for 3rd job
(same process) 
put copy command in the execute shell (scp)
also add the other shell code
add npm start

ssh into ec2 using pem file
scp the code
cd app
npm install
npm 

we need only one key pair for the dev branch



