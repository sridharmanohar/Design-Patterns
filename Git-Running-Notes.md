## To install git(in linux):
1. sudo apt install git

## To clone a repository:
1. Use this command to clone(download) a repository.
2. git clone <repo url>
3. As soon as you do this, there will be a folder created in your system with the name of the remote repo.
4. Now, this folder is automatically mapped to the remote repo (need not run any additional commands to do so).
5. You can make changes to the files localy and run git diff to see the differences b/w the local files and the remote ones.
6. TEST.

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

## To see the difference b/w local and remote repos:
1. git diff
2. This will show all differences whether it is deleteions/additions/modifications.
3. Then take a call as to what to do with the changes.

## To push locally deleted files to also be deleted in remote:
1. git diff - this will list all the files deleted (for that matter all differences b/w local and remote).
2. git rm <file_name> - this will index the file to be deleted in the remote repo.
3. git commit -m "comment"
4. git push origin master

## To push locally modified files to also be modified in remote:
1. git diff - this will list all the files modified (for that matter all differences b/w local and remote).
2. git add <file_name> - this will index the file to be modified in the remote repo.
3. git commit -m "comment"
4. git push origin master
