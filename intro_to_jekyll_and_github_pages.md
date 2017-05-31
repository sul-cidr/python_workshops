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
  - Limitations: substantially restricted plugins and themes allowed.

## Create a repository on Github for your project

- Sign in to Github in your browser
- Create a repository.
- Click "Set up in Desktop" to have Github automatically open Github Desktop, add the repo as a project, and clone it to your computer. You'll have a chance to choose where to copy the project to your local hard drive at this stage. I like to create a single folder or directory where I keep all of my projects that I use with git, simply called `projects`.

## Create a Jekyll website in the folder for your repository on your local machine

- Open your Bash shell and navigate to the local folder that matches your repository.
- Once inside that directory, in the shell, type `git checkout -b gh-pages`. This creates a new branch of your project that we'll use to hold the website code. By using a separate branch for the website, we can continue using the master branch to hold the code or files for the project itself.
- In the shell, run `jekyll new .`. This scaffolds a new website with the Jekyll framework.

## Building the website locally

- In your shell, still within the repository on your local machine, run `bundle exec jekyll serve`. This will build the website and serve it from a local server on your machine. You can then open up the link it shows you in your browser to see the website. This is typically [http://localhost:4000/](http://localhost:4000/).
- Command break down:
  - `bundle exec`
  - `jekyll serve`
- You should see a straightforwardly themed website with a title/header, navigation, a list of posts (currently just one), and a footer with several pieces of information, including how to edit the content.

## Exploring the core components of Jekyll

- In order to explore what is in these new files, let's open the repository in a text editor.
- In your text editor you should be able to see a list of the files and folders that are in your repository. We'll go through them one by one now. I also always recommend reading the Jekyll [documentation](https://jekyllrb.com/docs/structure/) that explains each of these files or folders.

## Exploring the core components of Jekyll themes

- In the middle of 2016, Jekyll switched the way it handled themes and appearance related files. Instead of them being the core by default, they exist in Ruby gems as packaged themes, which can be overridden by code that you write in your own site.
- Let's take a look at the default theme, [Minima](https://github.com/jekyll/minima), and go over each of the folders/files there.
- Key concepts: themes, gems

## Creating and Editing your site's content

- Let's start by editing `_config.yml`. Within your text editor, open that file and edit several pieces of information, such as the title and description of the site. NOTE: for most changes, while `jekyll serve` is running, it will automatically rebuild the site. However, if you make a change to the config file, you will need to manually restart the process.
- Next, let's create a new post. We'll do this by duplicating the existing post in the `_posts/` directory, then editing the filename, the YAML front-matter, and content.
- Next, let's create a static page. Similarly to the post, we'll duplicate the existing `about.md` page, rename the file, edit the YAML front-matter, and then the content.
- Key concepts: YAML front-matter, posts, static pages

## Modifying your site's appearance

- Themes are now installed via Ruby gem rather than as part of the core Jekyll install. Let's take a look at the files and folders within the standard theme, [minima](https://github.com/jekyll/minima). After that, we'll learn how to override the theme you have installed in order to customize it.
- Tour through `_includes`, `_layouts`, `_sass`, `assets`
- As an example of overriding some of the theme, let's override part of the footer. In your local repository, create a new folder called `_includes`. Inside of that folder, create a file called `footer.html`. This is a **partial**, a reusable piece of code that we can include in the website.  
  - Within your new `footer.html`, just put in some text and then reload your page in the browser to see the change.
- Next, to look at how we'd actually just modify the theme, let's copy the raw html from the minima theme footer partial into our own footer partial file from [here](https://raw.githubusercontent.com/jekyll/minima/master/_includes/footer.html). If you reload in the browser, you'll see the footer from the theme. Back in your text editor, let's look through the code and remove line 5, which begins with an `h2` tag. This will remove header from the footer. Then, reload the page in the browser to see your change. NOTE: pay attention to the liquid language here and how it draws information out of the config file (`site.variable`).
- Switching entire themes:
  - Github Pages supports only a limited number of themes, which you can find [here](https://pages.github.com/themes/).
  - We want to be able to see what our website would look like locally before we switch our theme in our published site, so let's make sure we have those themes installed locally. In your editor, open `Gemfile`. Jekyll gives us some nice instructions in this file to get set up for Github Pages. Per it's instructions, comment out the line with the `jekyll`, and uncomment the line with `github-pages`. After you save, return to your shell and run `bundle`. If it gives you an error, try running `bundle update` to get the most recent gems. After this has run, you can look at `Gemfile.lock` and you should see `jekyll-themes-*` here. This means that the theme gems are installed and available now.
  - In our `_config.yml` file, find "theme", and change the value from "minima" to "jekyll-theme-midnight". Go back to your shell and run `bundle exec jekyll serve`. You'll notice that the site builds, but it gives you several build warnings about layouts being requested that don't exist. This is because the minima theme includes layouts called "post", "page", and "home", while the midnight theme only includes a "default" layout (check [here](https://github.com/pages-themes/midnight/tree/master/_layouts)). To fix this, let's go into each file we get a warning about and change the layout in the YAML front-matter to "default." After you do that, try to build/serve the site again and check it in your browser.
  - You'll notice another issue now: there is no navigation in the header to your static pages, such as "About". In the minima theme, there is a header partial in the `includes` folder that creates a nav link for each page ([see the code](https://github.com/jekyll/minima/blob/master/_includes/header.html#L22-L27)). The midnight theme doesn't have any partials, as you can see from the lack of `_includes` folder. It does hardcode its brief navigation group in the default layout file ([see the code](https://github.com/pages-themes/midnight/blob/master/_layouts/default.html#L21-L28)). There are a couple of potential ways to fix this. One would be to create a `_layouts` folder in your local repo, create a `default.html` file, copy the layout code from the midnight theme into your own default layout, and replace the nav code within that with the nav code from the minima theme, linked above. In general, you'll follow a similar pattern of overriding a theme partial or layout any time you're modifying the theme you've chosen.   

## Deploying your site to Github Pages

- In Github Desktop, if you click on your project in the left sidebar, you should now see a list of files that have been changed. You can click on each file to see the new/changed content in each.
- In the left sidebar of Github Desktop, in the "Summary" field, type a short message that explains the change you're making. For an initial commit, I often just put in "Initial commit." You could be a bit clearer and write something like "Scaffolds Jekyll website." If you wanted to go into more detail you could write something further, or use bullet points, in the "Description" field. Do pay attention to which branch you're adding your work. Github Desktop will show which branch in the top middle of the application pane.
- After you hit commit, make sure to hit the "Publish" button in the top right. This will push your code up to Github so that the remote repository has all the changes. If you go back to the repository on Github in your browser and switch to the gh-pages branch, you should now see your code.
- We now need to tell Github that we want to use the gh-pages branch as the source for Github Pages to build a website. In your browser, on the Github page for your repo, click "Settings". Scroll down to the section called "Github Pages". Usually, if a gh-pages branch exists, Github knows to set that as the source for Github Pages. If under "Source", it doesn't have gh-pages selected, go ahead and select it. In this same section, Github should tell you the URL for your site, which should be githubusername.github.io/reponame. If there are any problems building your site, Github will list the problems here and likely send you an email.
- Key concepts to explain: branches, adding files, commits

## Workflow

- Github desktop distinguishes between fetching and pulling


## Helpful links
- https://pages.github.com/
- https://jekyllrb.com/
- https://shopify.github.io/liquid/
- http://programminghistorian.org/lessons/building-static-sites-with-jekyll-github-pages
