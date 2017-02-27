### Git commands
- git log --oneline
- git diff --staged which tells diff with the staged version
- hit q to quit LESS view
- `git remote add <name> <github url>` - add a remote (i.e. github https url), name it (eg. "origin")
- `git remote -v` - to see remote repositories (for fetch and push)
- `git push -u` ; -u = upstream, tells it to default to "origin" and "master" for "git push" in future
- `git push <where> <what>` ; where = remote repo name, what = branch i.e. master
- `git branch <name>` create, `git branch -a` view / `git checkout -b <name>` create & checkout
- `git branch -d <name>` - delete local branch
- `git log --oneline --all` - shows all including branches
- `git long --oneline --all --decorate --graph` - shows all with branch information
- `git merge <my_branch>` - merge my_branch into current branch (master)
- `git commit --amend` - to change the commit message

### Git command to change the remote origin
- `git remote -v` first then do above command
- git remote set-url origin https://canadagoose.visualstudio.com/Internal%20Web%20Projects/_git/cg-internal-controls-survey`

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
