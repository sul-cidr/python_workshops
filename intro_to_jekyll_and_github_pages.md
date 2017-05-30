# Building Websites with Jekyll and Github Pages

Center for Interdisciplinary Digital Research

- Scott Bailey - scottbailey[at]stanford.edu
- Javier de la Rosa - versae[at]stanford.edu
- Ashley Jester - ajester[at]stanford.edu

## Goals

By the end of this workshop, we hope that through building a sample website and deploying it to Github Pages, you will understand why you would use Jekyll vs a content management system like Wordpress, how websites are built with Jekyll, and how to deploy a Jekyll website to Github for free hosting.

## Quick Quiz
- Some sort of multiple choice question through a webform that will let me get instant feedback on level of familiarity with code (especially HTML/CSS)

## Setup

For the requirements and setup process, see [https://github.com/sul-cidr/python_workshops/blob/master/setup_jekyll_githubpages.md](https://github.com/sul-cidr/python_workshops/blob/master/setup_jekyll_githubpages.md).


## What are Jekyll and Github Pages?
- What is Jekyll?
  - Static site generator built with Ruby; uses the Liquid template language.  
  - Static site generators vs dynamic websites (CMSs like Wordpress and other web applications)
- What is Git?
  - Version control
  - Shell vs GUI
- Github
  - Repository for code projects that runs on the Git version control language.
  - Also useful for non-code things.
- Github Pages
  - Github will build and serve websites for free whose code lives on their system. It will serve regular HTML/CSS, but also by default will build Jekyll sites.
  - User/Organization vs Project Pages

## First step: create a repository on Github for your project
- Sign in to Github in your browser
- Create a repository.
- Click "Set up in Desktop" to have Github automatically open Github Desktop, add the repo as a project, and clone it to your computer. You'll have a chance to choose where to copy the project to your local hard drive at this stage. I like to create a single folder or directory where I keep all of my projects that I use with git, simply called `projects`.

## Second step: on your local machine, create a Jekyll website in the folder for your repository
- Open your Bash shell and navigate to the local folder that matches your repository.
- Once inside that directory, in the shell, type `git checkout -b gh-pages`. This creates a new branch of your project that we'll use to hold the website code. By using a separate branch for the website, we can continue using the master branch to hold the code or files for the project itself.
- In the shell, run `jekyll new .`. This scaffolds a new website with the Jekyll framework.
- In Github Desktop, if you click on your project in the left sidebar, you should now see a list of files that have been changed. You can click on each file to see the new/changed content in each.
- In the left sidebar of Github Desktop, in the "Summary" field, type a short message that explains the change you're making. For an initial commit, I often just put in "Initial commit." You could be a bit clearer and write something like "Scaffolds Jekyll website." If you wanted to go into more detail you could write something further, or use bullet points, in the "Description" field. Do pay attention to which branch you're adding your work. Github Desktop will show which branch in the top middle of the application pane.
- Key concepts to explain: branches, adding files, commits


## Workflow
- Github desktop distinguishes between fetching and pulling

## Creating Posts and Pages

## Editing the appearance of your website


## Helpful links
https://pages.github.com/
https://help.github.com/articles/creating-a-github-pages-site-with-the-jekyll-theme-chooser/
https://jekyllrb.com/
https://shopify.github.io/liquid/
http://programminghistorian.org/lessons/building-static-sites-with-jekyll-github-pages
