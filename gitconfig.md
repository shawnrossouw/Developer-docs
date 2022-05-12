#### Add these lines to the .gitconfig file in root directory. The editor = code line replaces vim with vscode for much better rebasing. 

```bash
[core]
	excludesfile = ~/.gitignore_global
  editor = code -n -w

[user]
	email = shawn@course.studio
	name = Shawn
	
[alias]
  # Show verbose output about tags, branches or remotes
  tags = tag -l
  branches = branch -a
  remotes = remote -v
  br = branch
  ci = commit
  co = checkout
  dump = cat-file -p
  lg = log --graph --abbrev-commit --decorate --date=relative --format=format:'%C(yellow)%h%C(reset) %C(dim)%ar %an %d%C(reset)%n%s%n'
  pr = pull-request
  prune-local = !git branch --merged | grep -v \"\\*\" | xargs -n 1 git branch -d
  prune-remote = remote prune origin
  s = status
  st = status
  type = cat-file -t
  pusho = "!git push -u origin $(git branch-name)"

[color]
  # Use colors in Git commands that are capable of colored output when outputting to the terminal
  ui = true
  ```
