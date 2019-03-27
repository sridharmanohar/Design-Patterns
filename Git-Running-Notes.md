
## To create a git rep (in the local file system):
1. Go to your project folder or make a separate copy of your project folder in a dedicated directory (just for git code).
2. git init (this is asking git to monitor your project folder).
3. git remote add origin <git_url>
4. Now, to complete the configuration, you have to add atleast one file into repo. Use the following command:
5. git add <file/dir_name>
6. now commit that added file/dir: git commit -a -m "first commit"
7. now push it: git push origin master
8. That's it, you have made your first commit.
9. At any point, you can always run, git status, to check the status of what files are to be commited/staging etc.
