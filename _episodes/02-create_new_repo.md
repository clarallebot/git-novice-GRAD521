---
title: Create a Repository
teaching: 10
exercises: 0
questions:
- "What is a repository?"
- "How do we create a repository?"
objectives:
- "Create a new Git repository in GitHub."
- "Edit a file in GitHub"
keypoints:
- 
---


Our project for this lesson will be to create a repository to write our Data Management Plan. 

We can start repositories in many different ways. We could create a local repository in our computer, create a new repository in GitHub, or copy somebody's elses repository. Let's create our new repository from scratch. 

Sign in to https://www.github.com If you don't have an account, create one. 

Now click on the "+" icon, on the upper right, and select New repository. 

![newbutton](../fig/new_newbutton.png)

Choose a Public repository. Name the repository following this file naming convention: 

~~~
GRAD521_DMPSurname_YYYY 
~~~
{: .language-bash}

where Surname is your surname. And YYYY is the year you are taking this class (e.g. 2020).

Make sure that you tick the option Initialize this repository with a README.

It will take a minute or two to be ready.

![importform](../fig/new_initializerepo.png)


Explore the GitHub space. The first thing you will see is that there is one file in the repository: a README.md This is a markdown file. Markdown is a language to write formatted text that is very intuitive, and that is quite useful to work in GitHub, so we will use it a little bit for this lesson. The content of the README.md file is what you see under the list of files. At this point the automatic readme has only the name of the repo. 

Let's edit the README file. We will add some information about what the repository will be. Click on the pencil icon on the top right of the page. 

![editreadme](../fig/edit_readme_1.png)

~~~
Data Management Plan for the research project Biogeochemical model of the Columbia River Estuary.

Context of the project:


~~~
{: .language-bash}

Under Context of the project add the description of your research project that you wrote for the assignment DMP Part 1. Remember that this document is public, do not include any information that cannot be shared publicly.

![editreadme2](../fig/edit_readme_2.png)

To save the changes go to the very bottom of the page. You have the option of including a short description and an optional extended description. It is very important to always add a short description, and this short description should be meaningful, because this will be the metadata that will help you keep a good control of the different versions of your files. Avoid vague messages like "update file".

![commitchanges](../fig/import_commit_changes.png)

Let's explore the repository a little more. You will see a tab named "main". This is where you see the branches that you have in the repository. In this case there is only one branch that, by default, is named "main". When you work with other repositories you may encounter other default branch names. For example, "master" used to be the default repository name, and still used by many. This term evokes the racist practice of human slavery and the [software development community](https://github.com/github/renaming) has moved to adopt more inclusive language. 

If you want to change the name of the branch you can do so by clicking on the little triangle next to the branch name and click on "view all branches".

![viewallbranches](../fig/view_all_branches.png)

Find the pencil button next to the branch name and click it. 

![penciltoeditbranchname](../fig/pencil_to_edit_branch_name.png)

Type the new name, and click on "Rename branch". Common possibilities for your new branch are "development" or "trunk". You can chose any name you want. 

![renamebranch](../fig/rename_branch.png)

We will not go over details about how to use branches in GitHub during this lesson. 

Let's explore the version control of capabilities a bit more. Edit the readme again.  

![editreadmefile](../fig/edit_readme_1.png)

Add a line to the file. Add a commit message and Commit changes. 

A "commit" is a different version of the content in the repository. Version control software saves a lot of information about your code every time you commit: 
* Date
* Author
* Description
* Unique identifier for the commit
Let's find this information in GitHub. Navigate to your main project page again. You can do that by clicking on the name of your project, the blue link at the top of the page. Now find the "commits" button. It is on the pale blue bar, next to the clock symbol. 

![commitsbutton](../fig/commits_button.png)

When you click on it you will find a list of the different commits that were done on the files of the repository. Each of the commits shows clearly who commited each change, when, and the commit message that was entered. Each commit also has a collection of letters and numbers that is a unique identifyer. We will not talk about going back to previous versions in this lesson, but it is a capability of Git. 

![listofcommits](../fig/list_of_commits.png)

Clicking on the commit also shows us a visualization of the changes that were made on this particular commit. In red, with a preceeding minus "-" you will see the lines that have been deleted. In green, with a preceeding plus "+" you will see the lines that have been added. In white you will see the lines that have not changed. 

![commitchanges](../fig/commit_changes.png)



