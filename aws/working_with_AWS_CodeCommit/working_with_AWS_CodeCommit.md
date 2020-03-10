
# https://www.qwiklabs.com/catalog

# Working with AWS CodeCommit
## Overview
* **AWS Codecommit**:-
  - is highly scalable, managed source control that hosts private Git repositories.
  - it stores your data in Amazon S3 & Amazon DynamoDB giving your repositories **high scalability, availability, & durability**.
  - simply, create a repository to store your code.
  - no hardware to provision & scale or software to install, configure, and operate.
## Objective of this lab:
* practice with AWS CodeCommit, part of AWS Developer Tools.
* create a code repository in AWS CodeCommit.
* create a local repository on a Linux instance in EC2
* after you create local repo, you will make some change to it.
* then you will synchronize (commit) your changes to the **AWS CodeCommit repository**.

## Task 1: Create an AWS CodeCommit Repository
* 3. In the AWS Management Console, on the Services menu, click Codecommit.
* 4. Click the **Create repository**
* 5. On the **Create repository page, configure**:
  - **Repository name**: My-Repo
  - **Description**: `My first repository`
  - Click `Create`
* An empty repository called `My-Repo` will be created in AWS CodeCommit. Connection details will be displayed

## Task 2: Connect to your EC2 Instance
* An EC2 has been created for you as part of the lab. In this task, you will connect to this instance.
### Mac and linux Users
* To the left of the instructions you are currently reading, click **Download PEM**.
* Save the file to the directory of your choice.
* Cope this command to a text editor.
```python
chmod 400 KEYPAIR.pem
ssh -i KEYPAIR.pem ec2-user@EC2PublicIP
```
* Replace the KEYPAIR.pem with the path to the PEM file you download.
* Replace EC2PublicIP with the value of EC2PublicIP shown to the lefte of these instructions
* Paste the updated command into the Terminal window and run it.
* Type `yes` when prompted to allow a first connect to this remote SSH server.
* NB. Because you are using a key pair for authentication, you will not be prompted for a password.

## Task 3: Create a Local Repository using Git
* This provide an example of how you would use AWS CodeCommit to synchronize to any local code repository that you might create in your normal production developmet environment.

* 21. Install the git client
```python
sudo yum install -y git
```
* 22. Run these commands to use the Git credential helper with the AWS credential profile, and enable the Git credential helper to send the path to repositories:
```python
git config --global credential.helper '!aws codecommit credential-helper $@'
git config --global credential.UseHttpPath true
```
* You will now need to obtain the HTTPS URL of your AWS CodeCommit repository.
* 23. In the **AWS CodeCommit Mangement Console**, click `Clone URL` then click `Clone HTTPS`
* This copies your repository URL to your clipboard. The URL look similary to : `https://git-codecommit.us-east-1.amazonaws.com/v1/repos/My-Repo`
* 24. Paste the clone URL into your text editor.
* 25. In your remote SSH session, copy and paste: ` git clone URL`
* 26. Replace URL with your CodeCommit clone URL that you copied to your text editor.
* 27. Run the command by pressing **ENTER**
  - you should seee the following messages:
    - warning: You appear to have cloned an empty repository
    - Congratulations!

## Task 4: Making a Code Change and First Commit to the Repo
- you will now create your first commit in your local repo. To do this, you will create two example files in your local repo. You will use git to stage the change to your local repo and then commit the change to your local repo.

* 28 .Copy and paste these commands to create two files in your local repo.
```python
cd ~/My-Repo
echo "The domestic cat (Felis catus or Felis silvestris catus) is a small, usually furry, domesticated, and carnivorous mammal." >cat.txt
echo "The domestic dog (Canis lupus familiaris) is a canid that is known as man's best friend." >dog.txt
```

* 29. List the directory to see the files were created.
```python
ls
```

* 30. Run this command to stage the change in your local repo
```python
git add cat.txt dog.txt
```

* 31. View the status of your repo.

```python
git status
```
  - you will see that the two files are ready to be commited to the repository.
* 32. Run this command to commit the change in your local repo
```python
git commit -m "Added cat.txt and dog.txt"
```

* 33. view details about the commit you have just made.
```python
git log
```

* **Now that you have an initial commit in ypur local repo, you can push the commit from your local repo to your AWS codeCommit repository.**
