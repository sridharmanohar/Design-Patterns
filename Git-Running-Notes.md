## To install git(in linux):
1. sudo apt install git

## To clone a repository:
1. Use this command to clone(download) a repository.
2. git clone <repo url>

## To create a git repo (in the local file system):
1. Go to your project folder or make a separate copy of your project folder in a dedicated directory (just for git code).
2. git init (this is asking git to monitor your project folder).
3. git remote add origin <git_url>
4. Now, to complete the configuration, you have to add atleast one file into repo. Use the following command:
5. git add <file/dir_name>
6. The above step is called Indexing/Staging, where git creates an index file and maintains an entry in that file.
7. now commit that added file/dir: git commit -a -m "first commit"
8. The above commit step will commit the changes that are in the index file.
9. now push it: git push origin master
10. That's it, you have made your first commit.
11. At any point, you can always run, git status, to check the status of what files are to be commited/staging etc.
