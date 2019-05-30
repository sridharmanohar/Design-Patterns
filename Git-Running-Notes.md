## To install git(in linux):
1. sudo apt install git

## To clone a repository:
1. Use this command to clone(download) a repository.
2. git clone <repo url>
3. As soon as you do this, there will be a folder created in your system with the name of the remote repo.
4. Now, this folder is automatically mapped to the remote repo (need not run any additional commands to do so).
5. You can make changes to the files localy and run git diff to see the differences b/w the local files and the remote ones.

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

## svn and git:
1. git is a distributed version control system (dvcs) which is basically based on the concept that complete code base of a project along w/ it's full version history (not just latest snapshot) would be copied onto every developer's machine.
2. This mainly gives the advantage of working offline and also allows us to not rely on a single backup.
3. But because of the concept of full checkout (including the history), the initial checkout is slower and problematic for projects w/ huge history.
4. And this a problem particularly in enterprise codebases where the code base spans across multiple repos., checking-out all and storing everything on local machine is an head-ache.
5. DVCS like git also lacks pessimistic locking mechanisms where only one user is allowed to checkout a file and every other user who tries to checkout the same file will only get a read-only copy.
6. In DVCS, since each developer has a full copy of the repo., s/he can share their changes with other people to get some feedback before sharing these changes w/ everybody.
7. DVCS can also have a central project repo. for e.g. github.
8. Github is a hosting service and software code management too implementing git. But, github, in general, is a centralized repo. following git model, meaning, users of github can get a full-copy of the entire project (along w/ its history) thereby allowing users to work offline and also allowing users to have a full-copy of the entire project w/o having to depend on the github copy.
9. Projects on a dvcs, with a long history, as long as 50000 changesets or more will take a huge amount of time and diskspace to download.
10. svn (Apache Subversion), on the other hand, is a centralized version control system (cvcs), which basically means, there is always a single central copy on a server and all commits are made to this copy.
11. svn provides locking mechanism - both optimistic and pessimistic locking.
12. Since, in case of a cvcs like svn, there is only one true repo (which is the server), it is almost impractical to work offline - can't perform tasks like commit, viewing history etc.
13. a cvcs like svn is probably a better choice when it comes for managing enterprise level projects whereas a dvcs like a git is a better choice for managing foss (free-and-open-source) projects.
14. coz in an enterprise project, downloading full source code spanning across multiple repos to a local machine may not be a practical and secure option whereas in a foss project, especially w/ contributors all across the world, a distributed model with an ability for each developer to download the full copy of the project (along w/ its history) and work offline is a more powerful and practical approach.



