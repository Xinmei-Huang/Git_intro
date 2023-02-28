# Git_intro
Basic command for git/github

reference: https://www.youtube.com/watch?v=RGOj5yH7evk 

------------------------------------------------------------------------------
## 1. SSH setup 
For pulling a private repo from Github to Git or pushing from git to Github, an SSH key needs to be set up first.

### 1.1 Create SSH key
***ssh-keygen -t rsa -b 4096 -C "ricc....lll@gmail.com"*** : imput the email of Github

"*Generating public/private rsa key pair.*"    
"*Enter file in which to save the key (C:\Users\Riccy Huang/.ssh/id_rsa): public_key*" : a name for the SSH key to replace "id_rsa"--!!!! when changing the name, the key will be saved in the working directory rather than "C:\Users\Riccy Huang/.ssh"   
Here, changing the name is not recommended. Keep the input empty.

"*Enter passphrase (empty for no passphrase):*" : r***y    
"*Enter same passphrase again:*"

### 1.2 Check SSH key

(a) On Git：

***ls | grep id_rsa***

"*grep id_rsa*"   
"*-a----         1/21/2023  10:59 AM           3434 id_rsa*": private key (no sharing!)   
"*-a----         1/21/2023  10:59 AM            748 id_rsa.pub*" : public key

***cat id_rsa.pub*** : print the SSH key

Or On Git BasH:

***ls -al ~/.ssh***    
***cat ~/.ssh/id_rsa.pub***

(b) On Github: 

Go to "SSH and GPG keys" -- "New SSH key" -- paste the key1.pub and press "Add SSH key"

(c) Add SSH key to the ssh-agent

STEP 1: Make sure SSH-agent can be opened

In Windows PowerShell (run as admin!!!!!):

***Get-Service | ?{$_.Name -like '*ssh-agent*'} | select -Property Name, StartType, Status *** : Check the current status of ssh-agent   
***Set-Service -Name ssh-agent -StartupType Manual*** : Enable the Service if it is disabled   
***Start-Service ssh-agent*** : Start the Service

(Implement step in Git: Add your key as before: ssh-add <path to the key>)

STEP 2: In Git/Git Bash

(In Git: ***ssh-add ~/.ssh/id_rsa*** : input password: !!! Giving error due to space in the path)

In Git Bash:

***$ ls ~/.ssh***   
"*id_rsa  id_rsa.pub  known_hosts*"

***$ eval "$(ssh-agent -s)"   
"*Agent pid 1031*"

***$ ssh-add ~/.ssh/id_rsa***   
"*Enter passphrase for /c/Users/Riccy Huang/.ssh/id_rsa:*"   
"*Identity added: /c/Users/Riccy Huang/.ssh/id_rsa (riccyhxmlll@gmail.com)*"

-------------------------------------------------------------------------------------------

## 2. Pull and Push

### 2.1 Git command intro
- clone: bring a repo that is hosted somewhere else like Github into a folder on your local machine
- add: track your files and changes in Git
- commit: save your files in Git
- push: upload Git commits to a remote repo, like Github
- pull: download changes from remote repo to your local machine


### 2.2 Basic command

(a) Pull from Github first
  
***git clone ...(SSH)*** ： For a private repo, need access token--“https://username:access_token@github.com/username/repo_name.git”

After make some changes, input   
***git status*** : check the status for recent file

 If creating a new file, remember to track it:   
***git add .*** : stage all files listed in "git status"
***git add abc.html*** : stage a speific file

***git commit -m "Add abc.html"*** : -m for the message, which is the title of the commit
***git commit -am "add new line"*** : -am for "add" + "message"

***git push origin master*** : "origin" : for the location of the repo, "master" is the branch that is pushed to.


(b) Creating files locally and pull

Create a new subfolder "demo2", and move inside the new folder   
***cd ../demo2

Add a new file "README.md" in the folder "demo2"   
***git init*** 
"* Initialized empty Git repository in User/../../demo2/.git*"

***git status*** : will show the untracked README.md file   
***git add .***
***git commit -m "new README.md"***

Then go to Github and create a new folder with the same name "demo2".

***git remote add origin git@github.com:xinmei-huang/demo2.git***
***git remote -v***
***git push origin push*** : Or ***git push -u origin push***, "-u" means upstream, next time the location is set to be "origin" directly without typing it. 


-------------------------------------------------------

## 3. Branch

### 3.1 Basic command

***git branch***   
“*.master*" : with a star sign ahead of the current branch, press q to quit
  
***git checkout -b new-branch*** : -b creating a new branch, and go to this new branch
  
***git checkout master*** : change to "master" branch, "master" can be changed to any other "branch".
  
Add a new README.md file in the new-branch, and save it   
***git add README.me***   
***git commit -m "updated readme"***

***git checkout master*** : no changes at all, only changes in new-branch
  
***git diff master*** : compare the difference between the recent branch with "master" branch.

!!(a) Merge on Github
  
***git push origin new-branch***   
Can directly compare and merge branch on the Github interface. "Create a pull request" (pr), and comments for a specific line of code can also be added by pressing the blue button; and then "Merge pull request".

***git checkout master***   
***git pull***

After merging, delete the new-branch on Git   
***git branch -d new-branch*** 

Or

!!(b) Merge on Git locally
  
***git merge master*** : merge changes from master to recent branch -- regularly keep up with changes from the master branch on Github.

### 3.2 Fix merge conflicts
Adjust direcly in the code script in Git (conflicts are noted in the script). 


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
  
Copy other people's Repo to our personal Github Repo

create pull request: comparing personal changes with the orginal version & Merge



-------------------------------------------------------
## 6. Syntax
1. Mermaid flowchart: https://mermaid.js.org/syntax/flowchart.html 




