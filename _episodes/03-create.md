---
title: Creating a Repository
teaching: 10
exercises: 0
questions:
- "Where does Git store information?"
objectives:
- "Create a local Git repository."
keypoints:
- "`git init` initializes a repository."
- "Git stores all of its repository data in the `.git` directory."
---

Once Git is configured,
we can start using it.

We will continue with the story where you are investigating if it
is possible to send a planetary lander to Mars. Luckily, our collaborator has
already started a repository for us to share!

First, let's clone the repository our collaborator has made from our `Desktop`
and then move into it:

~~~
$ cd ~/Desktop
$ git clone https://github.com/illinois-cse/git-local-sp19.git 
$ cd git-local-sp19
~~~

We want to take notes on the planet Mars, so let's make a folder in this
repository for our work: 

~~~
$ mkdir planets
$ cd planets
~~~
{: .language-bash}

Then we tell Git to make `planets` a [repository]({{ page.root }}/reference#repository)—a place where
Git can store versions of our files:


Alternatively, we could start a new repository from the command line without
using the clone command. That would look like this:

~~~
$ cd ~/Desktop
$ mkdir planets
$ cd planets
$ git init
~~~
{: .language-bash}

It is important to note that `git init` will create a repository that
includes subdirectories and their files---there is no need to create
separate repositories nested within the `planets` repository, whether
subdirectories are present from the beginning or added later. Also, note
that the creation of the `planets` directory and its initialization as a
repository are completely separate processes.

If we use `ls` to show the directory's contents,
it appears that nothing has changed:

~~~
$ ls
~~~
{: .language-bash}

But if we add the `-a` flag to show everything,
we can see that Git has created a hidden directory within `planets` called `.git`. In our 
cloned repository, the .git folder is located at `/git-local-sp19/.git`:

~~~
$ ls -a
~~~
{: .language-bash}

~~~
.	..	.git
~~~
{: .output}

Git uses this special sub-directory to store all the information about the project, 
including all files and sub-directories located within the project's directory.
If we ever delete the `.git` sub-directory,
we will lose the project's history.

We can check that everything is set up correctly
by asking Git to tell us the status of our project:

~~~
$ git status
~~~
{: .language-bash}
~~~
# On branch master
#
# Initial commit
#
nothing to commit (create/copy files and use "git add" to track)
~~~
{: .output}

If you are using a different version of `git`, the exact
wording of the output might be slightly different.

> ## Places to Create Git Repositories
>
> Along with tracking information about planets (the project we have already created), 
> Your associate, Tobey, would also like to track information about moons.
> Despite your concerns, Tobey creates a `moons` project inside your `planets` 
> project with the following sequence of commands:
>
> ~~~
> $ cd ~/Desktop          # return to Desktop directory
> $ cd git-local-sp19     # go into git-local-sp19 directory, which is already a Git repository
> $ ls -a                 # ensure the .git sub-directory is still present in the planets directory
> $ mkdir moons           # make a sub-directory git-local-sp19/moons
> $ cd moons              # go into moons sub-directory
> $ git init              # make the moons sub-directory a Git repository
> $ ls -a                 # ensure the .git sub-directory is present indicating we have created a new Git repository
> ~~~
> {: .language-bash}
>
> Is the `git init` command, run inside the `moons` sub-directory, required for 
> tracking files stored in the `moons` sub-directory?
> 
> > ## Solution
> >
> > No. Tobey does not need to make the `moons` sub-directory a Git repository 
> > because the `git-local-sp19` repository will track all files, sub-directories, and 
> > sub-directory files under the `git-local-sp19` directory.  Thus, in order to track 
> > all information about moons, your collaborator only needed to add the `moons` sub-directory
> > to the `git-local-sp19` directory.
> > 
> > Additionally, Git repositories can interfere with each other if they are "nested":
> > the outer repository will try to version-control
> > the inner repository. Therefore, it's best to create each new Git
> > repository in a separate directory. To be sure that there is no conflicting
> > repository in the directory, check the output of `git status`. If it looks
> > like the following, you are good to go to create a new repository as shown
> > above:
> >
> > ~~~
> > $ git status
> > ~~~
> > {: .language-bash}
> > ~~~
> > fatal: Not a git repository (or any of the parent directories): .git
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}
> ## Correcting `git init` Mistakes
> Another scientist in the group, Harley, explains to Tobey how a nested repository 
> is redundant and may cause confusion
> down the road. Tobey would like to remove the nested repository. How can Tobey undo 
> their last `git init` in the `moons` sub-directory?
>
> > ## Solution -- USE WITH CAUTION!
> >
> > To recover from this little mistake, Tobey can just remove the `.git`
> > folder in the moons subdirectory by running the following command from inside the `planets` directory:
> >
> > ~~~
> > $ rm -rf moons/.git
> > ~~~
> > {: .language-bash}
> >
> > But be careful! Running this command in the wrong directory, will remove
> > the entire Git history of a project you might want to keep. Therefore, always check your current directory using the
> > command `pwd`.
> {: .solution}
{: .challenge}
