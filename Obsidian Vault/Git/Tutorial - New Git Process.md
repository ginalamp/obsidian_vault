# Tutorial - New Git Process

[Learn Git with Bitbucket Cloud Full Tutorial](https://www.atlassian.com/git/tutorials/learn-git-with-bitbucket-cloud)

# Create & Add your SSH key
In order to use bitbucket from your computer you need to add your computer's SSH key to bitbucket.
[Eureka Stack Overflow: How to set up an SSH Key on BitBucket?](https://stackoverflow.com/c/shoprite-eureka/questions/158)
* I suggest labeling your ssh key clearly such as:
	*  `<yourName>-<yourComputerType>-<year>-<month>`

# Create repo
## Select the blue "Create" button and choose "Repository"
![[Pasted image 20220621142922.png]]

## Create > Repository
### Workspace
*  `shopritelabs`: this is for company purposes
*  `your_name`: this is for your own private purposes

### Project
* if workspace == `shopritelabs`
	* choose appropriate available project from list
* if workspace == `your_name`
	* choose a project you've already created, or you can opt to Create a new project

### Access level
* `private`
	* Typically choose private.
	* can be viewed only by those invited / granted access.
* `public`
	* open source
	* can be viewed by anyone

### Include a README
* `"Yes, with a tutorial (for beginners)"`
	* if you want to know how to use the README, otherwise you can create your own later
* Your README is where you document what your repo is about. You'd include things like what the overview is of what your code is trying to achieve, how to run the code from scratch, how to get the needed input files, etc.

### Default branch
* `main` 

### Include .gitignore
* `Yes`
	* This will exclude files based on the programming language you select in  `Advanced settings/Language`
* A .gitignore is there to ensure you only commit the necessary files to your repo. You'd typically want to exclude byte files (such as python `.pycache`) and data files (rather have your input files on S3 and include a link to this bucket in your README)
	* Learn more [here](https://www.atlassian.com/git/tutorials/saving-changes/gitignore)

### Advanced settings
* **Description**
	* A short description of the purpose of your repository
* **Forking**
	* `Allow only private forks`
* **Language**
	* Search for the primary programming langauge you'll be using

## Example 
### Input
![[Pasted image 20220708101028.png]]

### Output
Your README (generated if you selected the tutorial option) should also have some instructions on how to edit a file, create a file, and clone a repository.
![[Pasted image 20220708105303.png]]
# Clone repo
[Eureka Stack Overflow: How to clone an existing git repository from a remote server such as BitBucket?](https://stackoverflow.com/c/shoprite-eureka/questions/157)




# Create Branch
```shell
git checkout -b <branch_name>
```

# How to "push" your changes to IT heaven
The following cases show how you can add your local changes to the cloud.

## First time pushing
This can also be the first time you push to a new branch
```shell
git status
git add <file_name>
git commit -m "<message>"
git push --set-upstream origin <repo_name>
```
Note that I skip the "pull" part here, since this is under the assumption that you just created your new branch and it is thus the most up to date version.

## General case
```shell
git status
git add <file_name>
git commit -m "<message>"
git pull
git push
```

# How to "see" your commits
```shell
git log
```
## Information
* Commit ID
* Commit message
* Who commited
* When commited

# Pull Request


# Command meanings
`add`
* allows you to select which files (new or modified) you wish to add to a particular commit

`commit`
* words

`pull`
* words

`push`
* words

`log`
* words

`status`
* words

`reset`
* words


