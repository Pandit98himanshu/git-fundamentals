# Git Fundamentals
Notes of git commands from O'REILLY Media's [Git and GitHub LiveLessons By Peter Bell](https://learning.oreilly.com/videos/git-and-github/9780133992748/).


1. Get current username : ```git config --global user.name```
2. Change / Set username : ```git config --global user.name "New username"```

3. Get current user emailId : ```git config --global user.email```
4. Change / Set user  emailId : ```git config --global user.email abc@xyz.com```

5. ```cat ~/.gitconfig``` == ```git config --global --list```

6. Applies color : ```git config --global color.ui true```

7. Aliases for git commands: when you write ```git alias.<aliasing-keyword> "<alias-command>"``` it will run whole command
<details><summary>Click to see examples</summary>
<p>

  - ```git config --global alias.s "status -s"```
  - ```git config --global alias.lg "log --oneline --all --graph --decorate"```

</p>
</details>

8. Starts your project with *(Best practice)* : ```git status```
9. Initialize a git repo : ```git init <repo-name>``` or ```git init```
10. Adding files into staging area : ```git add <file-name1, file-name2...>```

11. Staging area is like shopping cart *(Order will not be placed until you hit ORDER NOW button)*. Files will not be saved into history until you commit.

12. Commiting file : ```git commit -m "<message>"```

13. ```root-commit``` = the very first commit, it appers only once in git repo

14. ```SHA1 Hash``` is used to uniquely identify each commit, therefore, each commit ID is suficiently long.

15. Uploading repo to Github : ```git remote add origin <repo-url>```

16. Pushing local repo to Github : ```git push -u origin <remote-branch-name>```

17. Deleting file : ```git rm <file-name>``` – This auto stages but doesn't commit

18. Rename file : ```git mv <ocurrent-name> <new-name>``` – This auto stages but doesn't commit

19. If you rename a file (not via git) then git understands that you've deleted previous file and added a new file. While staging, it runs through the renamed file(s) and see if similarity index of previous file and renamed file is more than 0.5 then it recognises it as renamed and associate all commit history of previous file with renamed file otherwise if it is less than 0.5 then it deletes previous file and NEW commit history starts from renamed file.
> **Don't make big changes to your file contents in the same commit, as you are renaming it.**

20. Ignore file :  create a file `.gitingnore`<br>
What to write? eg :- ```*.log``` – This means ignore all .log files in current directory and all of it's subdirectories.

21. Exclude certain file(s) : ```git config --global core.excludefile .gitignore```<br>
> **Don't exclude _.gitingnore_ file, because, if you're ignoring some kind of files then you must not allow other collaborators to commit those files into your repo. For example, `.DS_Store`, `.iml`**

22. Git ignore precedence : global `.gitignore` >> project `.gitignore` >> subdirectories `.gitignore`

23. Include some ignored file, write ```!<file-name>``` after ignoring files

eg:– 
**sequence matters**
```
.gitignore:		
				|	  DON'T WRITE 
	1. *.log 		|		1. !index.log 		(It will first not ignore index.log 
	2. !index.log 		|		2. *.log 		file then it will ignore all .log files)
```

24. Add and commit files in same command : ```git commit -am <message>``` – This works on only modified (not untracked) files

25. Show current branches : ```git branch```

26. Create a new branch each time you are adding a new feature *(Best practice)*.

27. Create a new branch : ```git branch <branch-name>```
	
28. Switch to another branch : ```git checkout <branch-name>```

29. Create a new branch and switch to it : ```git checkout -b <branch-name>```

30. Merge a branch into another branch : ```git merge <branch-name>``` – you should be on the branch in which you want to merge another branch

31. Delete a branch : ```git branch -d <branch-name>```

32. 2 types of merging:<br>
- **Recursive merge** happens when 2 diff branches have atleast 1 commit in each branch and you want to merge both branches.<br>
- **Fast-Forward merge** happens when 2 branches share same commit history. If you merge them you'll lose track of commit history in new created branch.

33. No fast-forward merge (no-ff) : ```git merge --no-ff <branch-name>``` – This will do recursive merge and keep history of another created branch.

34. See diff in UNSTAGED files : ```git diff```

35. See diff in STAGED files : ```git diff --staged```

36. See diff b/w working directory and the last commit : ```git diff HEAD```

37. Rebase branch : ```git rebase <to-branch>``` – you should be on the branch which you are rebasing

38. See content of object file : ```git cat-file -p <few-words-of-object-file-in-.git-folder>```

39. Add alias to remote server : ```git remote add origin <remote-server-link>```

40. Pushing everything in current branch (commit history, files etc.) to remote server : ```git push -u origin master```

41. Pull changes on remote server repo and merges with local git repo : ```git pull```

42. Fetch changes on remote sever repo : ```git fetch```

43. Pull = Fetch + Merge

44. Change to remote server branch : ```git checkout origin/master```

45. Fetch + Rebase = ```git pull --rebase```

46. Copy in local : ```git clone <repo-url>```

47. Add version tag : 
	- Regular tag : ```git tag v1.0.0```
	- Annotated tag : ```git tag -a v1.0.0 -m "<message>"```
	- Signed tag : *adds security*

48. Push relase tags into Github : ```git push --tags```

49. Undo things : ```git revert <few-words-of-the-commit-HASH-you-want-to-undo>```

50. Change latest commit message : ```git commit --amend```

51. Throw away commits : ```git reset --<type> HEAD~<number-of-commits-from-HEAD>```
					or, ```git reset --<type> <commit-hash>```
`<type>` : 
	- `soft` : put those files in staging area, so that we can again commit it
	- `hard` : delete all those files
	- `mixed` (default) : clear staging area but leave those files as untracked

52. Open time machine in git : ```git reflog```

53. Redo the commit : ```git cherry-pick <commit-hash>```

54. Undo things the way you want : ```git rebase -i HEAD~<number-of-commits-from-HEAD>```

55. Delete Remote Branch : ```git push <remote_name> :<branch_name>```<br>
eg :– `git push origin :serverfix`
