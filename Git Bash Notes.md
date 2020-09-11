### Git commands
- git log --oneline
- git diff --staged which tells diff with the staged version
- hit q to quit LESS view
- `git remote add <name> <github url>` - add a remote (i.e. github https url), name it (eg. "origin")
- `git remote -v` - to see remote repositories (for fetch and push)
- `git remote set-url origin <git remote url>` - set remote
- `git remote remove origin` - removes the remote
- `git push -u` ; -u = upstream, tells it to default to "origin" and "master" for "git push" in future
- `git push <where> <what>` ; where = remote repo name, what = branch i.e. master
- `git branch <name>` create, `git branch -a` view / `git checkout -b <name>` create & checkout
- `git branch -d <name>` - delete local branch
- `git log --oneline --all` - shows all including branches
- `git long --oneline --all --decorate --graph` - shows all with branch information
- `git merge <some_branch>` - merge some_branch into currently working branch
- `git commit --amend` - to change the commit message
- `git revert <commit id>` - creates a patch to undo the commit
- `git merge --abort` - Undo a Merge

### Local merging in PHP storm
- You want to merge branch A to B
- checkout branch B
- VCS >> Git >> Branches >> select branch A >> merge
- you'll see a green message pop up left bottom saying `Merged A to B`

### Local merging in GitBash
- You want to merge branch bugfix to master
- git checkout master (Switches to your master branch)
- git merge bugfix (git merge --squash bugfix - squashes into 1 commit)
- git commit
ref: https://stackoverflow.com/questions/5308816/how-to-use-git-merge-squash


### Git command to change the remote origin
- `git remote -v` first then do above command
- git remote set-url origin https://canadagoose.visualstudio.com/Internal%20Web%20Projects/_git/cg-internal-controls-survey`

### Use remotes with ssh
[Use SSH key authentication - ADO](https://docs.microsoft.com/en-us/azure/devops/repos/git/use-ssh-keys-to-authenticate?view=vsts)  

1. generate an ssh key in your computer.  
  - Go to ssh in home directory `cd ~/.`  
	- Create if it doesn't exist  
	- Run `ssh-keygen -C "rferdinando@canadagoose.com"`  
	- enter a passphrase for best practice. you'll need this to run git commands at the end  
	- this will generate public/private rsa key pair - `id_rsa` & `id_rsa.pub` (public)  
2. copy this to your git account's *SSH public keys* section
  - you can find it in,
     - ADO; profile >> securiy >> SSH public keys
     - github; github page // settings // SSH Keys // Add key //  
  - go back to command prompt where you created keys, and copy the contents of the `id_rsa.pub` file.  
  - you can view it using `cat id_rsa.pub` and the highlight to copy  
  - Go to *SSH public keys* section and `Add` a new key  
     - give a title i.e. rferdinando  
     - then paste the key  
3. Go back to repository page and test from `git pull` to `git push`
  - make sure remote url is correctly set - if not, remove and add back in
  - for the remote url, use the ssh url instead of https
  - you'll be asked for the passphrase, which is the one you created earlier

## Easiest way to test mqsql connection in cmd (params - user, pass db)
c:\xampp\mysql\bin\mysql.exe -uictrls -pBXM5qLbpXueuzBZv ictrls

## Slack tips
- Tilda for `var x = 100`
- Triple tilda for ```code block```

- To update system varibles (path) using CMD `setx Path "%path%;c:\dir1\dir2"`

### Linux manual reading
`git commit [-a | --interactive | --patch] [-s] [-v] [-u<mode>] [--amend]
	   [--dry-run] [(-c | -C | --fixup | --squash) <commit>]
	   [-F <file> | -m <msg>] [--reset-author] [--allow-empty]
	   [--allow-empty-message] [--no-verify] [-e] [--author=<author>]
	   [--date=<date>] [--cleanup=<mode>] [--[no-]status]
	   [-i | -o] [-S[<keyid>]] [--] [<file>…​]`
- <> denotes mandatory, [] denotes optional and encapsulates a set
- | denotes mutually exclusive switches within a set
- `-` - short 1 letter only switches aka options, `--` - long switches aka options
- `[--cleanup=<mode>]` - entries for 'mode' will be in options section in manual
- `[-i | -o] [-S[<keyid>]] [--] [<file>…​]` - possibles: 0001, 0010, 0011 ... 1111

## Node related

- When an issue arrises with a node module, delete `node_modules` folder and do `npm i`
