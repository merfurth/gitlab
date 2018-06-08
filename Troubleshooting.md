Troubleshooting your GitLab installation
When your GitLab instance does not work the way you expect it to work, it's nice to have a way to check what parts of your installation are not working properly. In this recipe, we will take a look at the self-diagnostic tools provided by GitLab.

How to do it…
Learn how to troubleshoot your GitLab server with the following steps:

Log in to your server using SSH.
The first case shows troubleshooting in the case of a GitLab source installation.

Go to your gitlab folder:
$ cd /home/git/gitlab
To autodiagnose your installation, run the following command:
$ sudo -u git -H bundle exec rake gitlab:check RAILS_ENV=production
When there is a problem with your GitLab installation, it will be outputted in red text, as shown in the following screenshot:
How to do it…
The solution for the problem is also given; just follow the explanation given by the problem you walk into. In this case, we have to run the following command:
$ sudo-u git -h bundle exec rake  gitlab:satellites:create RAILS_ENV=production
If everything is green, your installation is in great shape!
The next few steps concentrate on troubleshooting in the case of the Gitlab Omnibus installation.

Run the following command:
$ sudo gitlab-rake gitlab:check
When you have any problem with your GitLab installation, this will be outputted; also, the possible solution will be shown.
The solution that is given for this problem is the solution for the source installation. To fix this issue in the Omnibus installation, we need to alter the command a little. You have to replace the $ sudo-u git -h bundle exec rake part with $ sudo gitlab-rake. So, the command will look as follows:
$ sudo gitlab-rake gitlab:satellites:create RAILS_ENV=production
If everything is green, your installation is in top shape!
In case you need to view the logs, you can run the following command:
$ sudo gitlab-ctl tail
To exit the log flow, use Ctrl + C.
How it works…
When you think your GitLab installation might not be in a good shape or you think you've found a bug, it's always a good idea to run the self-diagnostics for GitLab. It will tell you whether you've configured GitLab correctly and whether everything is still up to date.

Here is a list of what will be checked:

Is your database config correct?
If your database is still running SQLite instead of PostgreSQL or MySQL, it will give you a warning.
Are all the user groups configured correctly?
Is the GitLab config present and up to date?
Are the logs writable?
Is the tmp directory writable?
Is the init script present and up to date?
Are all the projects namespaced? This is important if you've upgraded from an old version.
Are all the satellites present?
Is your Redis up to date?
Is the correct Ruby version being used?
Is the correct Git version being used?
This is the first place you should start when walking into problems. If this does not give you the correct answers, you can open an issue on the GitLab repository (https://gitlab.com/gitlab-org/gitlab-ce). Make sure you post the output of this check as well, as you will most likely be asked to post it anyway.
