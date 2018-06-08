Creating a backup
It's important that you have your source code secured so that when your laptop breaks down—or even worse, the office got destroyed—the most valuable part of your company (besides the employees, of course) is still intact. You've already taken an important step into the right direction; you set up a Git server so that your source code has multiple places to live. However, what if that server breaks down?

This is where backups come into play! GitLab Omnibus makes it really easy to create backups. With just a simple command, everything in your system gets backed up: the repositories as well as the databases. It's all packed in a tar ball, so you can store it elsewhere, for example, Amazon S3 or just another server somewhere else.

In this recipe, we not only created a backup, but also created a schema to automatically back up the creation using crontabs. This way, you can rest assured that all of your code gets backed up every night.

How to do it…
In the following steps, we will set up the backups for GitLab:

First, log in to your server using SSH.
The first few steps concentrate on the GitLab source installation.

Go to your gitlab folder:
cd /home/git/gitlab
Run the backup command:
bundle exec rake gitlab:backup:create RAILS_ENV=production
The backup will now run. This might take a while depending on the number of repositories and the size of each repository.

The backups will be stored in the /home/git/gitlab/tmp/backups directory.

Having to create a backup by hand everyday is no fun, so let's automate the creation of backups using a cronjob file.

Run the following command to open the cronjob file:
$ sudo -u git crontab -e
Add the following content to the end of the file:
0 2 * * * cd /home/git/gitlab && PATH=/usr/local/bin:/usr/bin:/bin bundle exec rake
  gitlab:backup:create RAILS_ENV=production
Save the file, and the backups will be created everyday at 2 A.M.
The next few steps talk about the GitLab Omnibus installation.

To create the backup, run the following command:
$ sudo gitlab-rake gitlab:backup:create
A backup is now created in the $ /var/opt/gitlab/backups directory.

Let's verify that our backup is actually there:
$ ls /var/opt/gitlab/backups/
You should see at least one filename, such as 1404647816_gitlab_backup.tar. The number in the filename is a timestamp, so this might differ in your case.

Now we know how to create the backup. Let's automate this via a cronjob file.

Run the following command as the root user:
$ crontab -e
Add the following code to the end of the file to have the backup run every day at 2 A.M.:
0 2 * * * /opt/gitlab/bin/gitlab-rake gitlab:backup:create
After you save the file, a backup will be created every day at 2 A.M. This is great, but there is a tiny catch; if you have the backups run for too long, it will take up all of your disk space. Let's fix this!

Open this file location: /etc/gitlab/gitlab.rb.
Let's have the backups only last for a week. After that, they will be destroyed. 7 days is 604,800 seconds. Add the following code to the bottom of the file:
gitlab_rails['backup_keep_time'] = 604800
To have the changes take effect, we have to tell GitLab to reconfigure itself. Run the following command:
$ sudo gitlab-ctl reconfigure
