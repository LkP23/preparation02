Preparation 2 - Connecting RStudio and GitHub
================

All of your work for STA 418/518 will be stored in GitHub. This activity
will walk you through practicing some of the GitHub steps to get more
comfortable with this workflow.

**Estimated Time**

-   ☑️ Six Tasks: 45–60 minutes

## How to Set up Git

As I said in the syllabus, [Happy Git with R](http://happygitwithr.com/)
is by far the most complete resource for setting up Git and GitHub. If
you would like to set up R, RStudio, Git, and GitHub on your own
machine, I would recommend you use this text. Luckily for us, Git is
already installed on the RStudio Server (and of course R and RStudio are
available here too) so we will only need to worry about having our
RStudio sessions communicate with GitHub.

### ☑️ Task 1: Fork this repo

To begin, we need to make your own copy of this GitHub repo.

1.  Click on the ![fork icon](README-img/fork.png) **Fork** icon in the
    upper-right-hand corner of this repo.

After a few seconds, you should be taken to a new repo at
`<username>/preparation02`, where `<username>` is your GitHub username.

### ☑️ Task 2: Configure Git

1.  Login to the [RStudio Server](https://rstudio.gvsu.edu/) using your
    GVSU username and password,
2.  Verify that you are in an RStudio session (i.e., not the RStudio
    Workbench Sessions/Project screen).

There are a couple of ways to configure Git in RStudio. For STA 418/518,
we will use `{usethis}`.

Note that when you see something like `{name}`, I mean *the R package
called `name`*.

Specifically, we will use the `edit_git_config` function from
`{usethis}`. Sometimes I will shorten this to be
`usethis::edit_git_config` or *from the R package `usethis`, use the
function `edit_git_config`* (in short, `package::function`).

3.  In your **Console** pane (left-hand pane), type the following
    pressing Enter/Return after each line:

    ``` r
    library(usethis)
    edit_git_config()
    ```

A file should open in the pane above your **Console** that is called
`.gitconfig`. In this file, provide your email (can be any email, but it
would probably be helpful to use the same one you signed up for GitHub
to avoid confusion) and your preferred name. Remember that this
information will be publicly available. For example, my information
would look as follows:

    [user]
        name = "Bradford"
        email = "dykesb@gvsu.edu"

Your `.gitconfig` file might have additional lines within it, but you
can ignore these (simply leave them alone). Click on the ![save
icon](README-img/save-icon.png) icon and you can close this file. Now,
whenever you make commits in RStudio, it will remember that you are the
person making the commits!

### ☑️ Tasks 3: Connect RStudio and GitHub

Now that you have Git set up within RStudio, we can enable RStudio and
GitHub to communicate. To do this, we will need your GitHub username and
a Personal Access Token (PAT). Conveniently, `{usethis}` has a function
for this!

To create a PAT, type the following in your **Console** and press
Enter/Return:

``` r
create_github_token()
```

Note that you previously loaded `{usethis}` (using `library(usethis)`)
so you did not need to do this again. **Once you load a package in your
current RStudio session, you do not need to load it again.**

This will take you to a “New personal access token” page on GitHub.
Since I work on multiple machines (i.e., my personal laptop, my work
laptop, my personal desktop, and the RStudio Server), I like to name
each PAT. For example, in the **Note** text field, I called this token
“GVSU RStudio Server”.

Most of the other options you will accept the default selections.
However, you might want to change the **Expiration** date. A couple of
suggestions: have this PAT expire at the end of this semester (Dec. 18,
2021) or (*risky*) choose “No expiration”. After choosing a PAT
expiration, scroll down and click on **Generate Token**.

After clicking on **Generate Token**, you will be taken to a “Personal
access tokens” page that has a seemingly random string presented to you
beginning with `ghp_`. Keep this page open for a little bit (I will tell
you when it is safe to close it), as once you close this page, you will
never be able to view this PAT again! I highly recommend that you store
this code somewhere safe (e.g., a password manager tool). If you do lose
it, you will simply need to go through this process again.

Now we need to store this PAT in RStudio so that RStudio can connect to
your GitHub account. Back in your RStudio **Console**, type the
following and press Enter/Return after each line:

``` r
library(gitcreds)
gitcreds_set()
```

In your **Console** you will first be asked to
`? Enter password or token:` Paste your PAT here (NOT your GitHub
password) and press Enter/Return. You should see a message similar to:

    -> Adding new credentials...
    -> Removing credentials from cache...
    -> Done.

### ☑️ Tasks 4: Clone GitHub repo

Now that RStudio and GitHub are connected, we can clone this repo (i.e.,
copy the repo to our RStudio session)! What follows is our typical
workflow for this course.

1.  In RStudio, click on the ![RStudio Project
    icon](README-img/rproj-icon.png) icon (the icon below the Edit
    drop-down menu);
2.  Click on **Version Control** on the *New Project Wizard* pop-up;
3.  Click on **Git** and you should be on a “Clone Git Repository” page;
4.  Back to your `preparation02` GitHub repo, click on the gren **Code**
    button near the top of the page;
5.  Verify that **HTTPS** is underlined in red on the pop-down, then
    copy the URL provided;
6.  Back in RStudio, paste the URL in the “Repository URL” text field;
7.  The “Project directory name” text field should have automatically
    populated with `preparation02`. If yours did not, click into this
    box and press Ctrl/Cmd (usually this is a Mac issue);
8.  In the “Create project as subdirectory of” field, click on
    **Browse…**. Create a **New Folder** called “STA 418” of “STA 518”
    (depending on your course), then within this folder, create a **New
    Folder** called “Preparations”, think click **Choose**. Note that I
    am forcing you to use my file system management style.
9.  Click on **Create Project**.

Your screen should refresh and the **Files** pane should say that you
are currently in your `preparation02` folder that currently has three
files (`.gitignore`, `preparation02.Rproj`, and `README.md`) and a
folder (`README-img/`).

### ☑️ Tasks 5: Clone GitHub repo

Before we wrap-up, we will create a new file and see how to commit these
changes and view the commit history.

1.  In RStudio, click on the ![new file
    icon](README-img/new-file-icon.png) and select an R Script,
2.  Click on the ![save icon](README-img/save-icon.png) icon to save
    this file. Name it `preparation02-file.R` (notice the capital “R”
    for the file type).
3.  Type the following code within in your R script:

``` r
# Here are some simple calculations
2 + 2
(2 * 3)^2
```

4.  Run each line to verify that you get the results you would expect,
    then save your file,
5.  In the **Git** pane (upper-right pane), check the box next to all
    items listed and click on **Commit**,
6.  In the pop-up, provide a commit message of
    `Adding some calculations`, then click on **Commit**, and
7.  In this same pop-up, switch from **Changes** to **History**
    (upper-left corner)

Reflect on how this way of looking through your commit history compares
to GitHub. Feel free to add more to your R script, save, and commit.

### ☑️ Tasks 6: Wrapping Up

Go back to your `preparation02` GitHub repo and verify that your
`preparation02-file.R` file is here. **You can now close the PAT page
tab.**

In Blackboard, submit the link to your newly created
`<username>/preparation02` GitHub repo as a *clickable link* for
evidence of completing Preparation 2.

Then find the issue titled “Day 3 Agenda” that your I created in the
`community` repository. In this issue, post what was the muddiest thing
from the Preparation. If someone else already mentioned what you thought
was muddy, give them a “+ 1” 👍.

## Attribution

This activity is based on David Keyes’ tutorial at [R for the Rest of
Us](https://rfortherestofus.com/2021/02/how-to-use-git-github-with-r/)
and [Happy Git with R](http://happygitwithr.com/) by Jenny Bryan et al.
