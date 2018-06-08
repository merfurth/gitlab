Restoring a backup
If your server breaks down, it is nice to have a backup. However, it's a pain when it's a full day's work to restore that backup; it's just a waste of time.

Luckily, GitLab makes it super easy to restore the backup. Retrieve the backup from your external Amazon S3 storage or just your external hard drive, copy the file to your server, and run the backup restore command. It won't get any easier!

Getting ready
Make sure you have a recent backup of your GitLab instance. After you restore the backup, all the data created between the backup creation and the restoration of your backup will be lost.

How to do it…
Let's restore a backup using the following steps:

Start with a login to your server using SSH.
The next few steps concentrate on the GitLab source installation.

Go to your gitlab folder:
$ cd /home/git/gitlab
Go to the backup folder of GitLab:
$ cd /home/git/gitlab/tmp/backups
Look at the filename of the most recent file and note the number that the filename starts with.
Go back to your GitLab folder:
$ cd /home/git/gitlab
Now, run the following command and replace the 1234567 part with the number you took from the latest backup filename:
$ bundle exec rake gitlab:backup:restore RAILS_ENV=production BACKUP=1234567
The next few steps concentrate on the GitLab Omnibus installation.

Make sure your backup file is located at /var/opt/gitlab/backups:
$ cp 1407564013_gitlab_backup.tar /var/opt/gitlab/backups/
Before we can restore the backup, we need to stop our instance. First, stop GitLab itself:
$ sudo gitlab-ctl stop unicorn
Next, stop the background worker:
$ sudo gitlab-ctl stop sidekiq
Now, we will restore our backup. You need to provide the timestamp of the backup you want to restore. The timestamp is the long number before the filename. Warning: this will overwrite all the data in your database! The following command depicts this:
$ sudo gitlab-rake gitlab:backup:restore BACKUP=TIMESTAMP_OF_BACKUP
Restoring the actual backup might take a little while depending on the size of your database.
Restart your GitLab server again:
$ sudo gitlab-ctl start
