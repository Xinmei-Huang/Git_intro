# Git_intro
Basic command for git/github

reference: https://www.youtube.com/watch?v=RGOj5yH7evk 

------------------------------------------------------------------------------
## 1. SSH setup 
For pulling a private repo from Github to Git or pushing from git to Github, an SSH key needs to be set up first.

### 1.1 Create SSH key
***ssh-keygen -t rsa -b 4096 -C "ricc....lll@gmail.com"*** : imput the email of Github

"*Generating public/private rsa key pair.*"

"*Enter file in which to save the key (C:\Users\Riccy Huang/.ssh/id_rsa): public_key*" : a name for the SSH key

"*Enter passphrase (empty for no passphrase):*" : r***y

"*Enter same passphrase again:*"

### 1.2 Check SSH key

(a) On Git：

***ls | grep public_key***

"*grep public_key*"

"*-a----         1/21/2023  10:59 AM           3434 public_key*": private key (no sharing!)

"*-a----         1/21/2023  10:59 AM            748 public_key.pub*" : public key

***cat public_key.pub*** : print the SSH key

(b) On Github: 

Go to "SSH and GPG keys" -- "New SSH key" -- paste the public_key.pub and press "Add SSH key"

(c) Add SSH key to the ssh-agent

STEP 1: Make sure SSH-agent can be opened

In Windows PowerShell (run as admin!!!!!):

***Get-Service | ?{$_.Name -like '*ssh-agent*'} | select -Property Name, StartType, Status *** : Check the current status of ssh-agent

***Set-Service -Name ssh-agent -StartupType Manual*** : Enable the Service if it is disabled

***Start-Service ssh-agent*** : Start the Service

(Implement step in Git: Add your key as before: ssh-add <path to the key>)

STEP 2: In Git

***ssh-add public_key*** : input password

"*Identity added: public_key (riccyhxmlll@gmail.com)*"


-------------------------------------------------------------------------------------------

## 2. Pull and Push

### 2.1 Git command intro
- clone: bring a repo that is hosted somewhere else like Github into a folder on your local machine
- add: track your files and changes in Git
- commit: save your files in Git
- push: upload Git commits to a remote repo, like Github
- pull: download changes from remote repo to your local machine


### 2.2 Basic command
***git commit -am "add new line"*** : -am for "add" + "message"

***git status*** : check the status for recent file


-------------------------------------------------------

## 3. Branch

### 3.1 Basic command

***git checkout master*** : change to "master" branch, "master" can be changed to any other "branch". 

***git diff master*** : compare the difference between the recent branch with "master" branch.

***git merge master*** : merge changes (recent branch) to "master" branch.


### 3.2 Fix merge conflicts
Adjust direcly in the code script. 



-------------------------------------------------------

## 4. Reset


***git add README.me***

***git reset*** / ***git reset README.md*** : the add file "README.md" no longer staged

Or

***git reset HEAD*** : reset last commit

***git reset HEAD~1*** : reset the commit one further ahead

Or

***git log*** : chech all commits with inverse chronological order with a specific serial number for each commit

***git reset 37sjfaweh...*** : input the specific serial number for the commit, changes after this commit will be unstaged

***git reset --hard 37sjfaweh...*** : changes after this commit will be completely deleted



-------------------------------------------------------

## 5. Fork
Copy other people's Repo

create pull request: comparing personal changes with the orginal version & Merge




