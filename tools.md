# Tools to help make your life easier (code and task management)

We will be using both GitHub and GitLab to keep track of code, tasks and documents. These sites allow users to create repositories for storing files. The repositories are under version control, which means that any revisions made to files can be easily monitored and, if necessary, rolled-back. Both sites also provide a number of tools for creating and tracking sets of tasks or publishing release versions of code.

We will be using each site for a different purpose:

* **GitHub** - GitHub is a widely used service which allows people to create publicly visible repositories.

  Anything stored here should be placed in a *public* repository under the [GitHub GLAMOD organisation](https://github.com/glamod).

  *This should be the preferred location for keeping project resources.*

* **GitLab** - GitLab does not restrict the use of private repositories. This makes it a useful alternative to GitHub for storing in-development code, internal documents or other sensitive information.

  Anything stored here should be placed in a *private* repository under the [GitLab GLAMOD organisation](https://gitlab.com/glamod).

## Geting started with GitHub

Create a GitHub account [here](https://github.com/join?source=header-home). 

Contact one of the owners of the GLAMOD organisation, such as Ag Stephens, to become a member.

You should now be able to clone any of the repositories and push changes once you have Git set up.

## Getting started with GitLab

Create a GitLab account [here](https://gitlab.com/users/sign_in#register-pane). 

Contact one of the owners of the GLAMOD organisation, such as Ag Stephens, to become a member.

Since the repositories on GitLab will be private, you will not immediately have the ability to clone them. Refer to the next section for instructions on cloning private repositories.

## Getting started with Git

### Learning Git
In order to make best use of GitHub and GitLab repositories you will need a basic understanding of the Git version control tool which both sites are designed around.

This tutorial demonstrates some basic usage of the tool: [try.github.io](https://try.github.io/)

The web interfaces for GitHub and GitLab also provide a number of basic Git functions such as the ability to modify individual files or perform a diff.

### Download Git
Git is available for Windows, Mac and Linux and can be downloaded from the [Git website](https://git-scm.com/downloads).

### Cloning public repositories
Once you have Git installed and understand the basics, you should be able to clone any public GLAMOD repository. For instance:
```
git clone https://github.com/glamod/glamod-help.git
```

### Cloning private repositories
In order to clone a private repository from GitLab, you will need to link an SSH key to your [GitLab profile](https://gitlab.com/profile/keys).

This process is similar to how you set up your JASMIN SSH key earlier but is explained in detail [here](https://gitlab.com/help/ssh/README).

If you have done this step correctly, you should be able to clone private repositories via SSH using the following syntax:
```
git clone git@gitlab.com:glamod/<repository_name>.git
```
