Importing an existing repository
It's quite simple to import your repositories from somewhere else. All you need to do is create a new project and select the repository to be imported. In this recipe, we will take a look at how this is done. For this recipe, we will import the repository hosted on GitHub at https://github.com/gitlabhq/gitlab-shell.

How to do it…
In the following steps, we will import a repository:

Log in to your GitLab instance.
Click on New project.
How to do it…
Enter the project name as GitLab Shell.
Click on Import existing repository?.
How to do it…
Enter the URL for the repository we want to import:
https://github.com/gitlabhq/gitlab-shell

Now, click on Create Project.
Importing the existing repository might take a while depending on the size of the repository.
After the importing is done, you will be redirected to the project page.
Let's check whether it's actually an imported repository. Click on the Network menu item. If everything is fine, you should see the graph in the following screenshot:
How to do it…
How it works…
There is really nothing magical about importing a repository. All GitLab does is clone the URL you give it to its own satellite. After this is done, the satellite will be linked to your project, and you're done!

What if your repository is private and not publicly accessible? You can import it by adding the user credentials in the URL. Don't worry; this information is not stored anywhere!

So, if we have the same repository as the one we used earlier but it has credentials, it will look like what is shown in https://username:password@github.com/gitlabhq/gitlab-shell.
