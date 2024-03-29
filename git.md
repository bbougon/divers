# commandes

**Montrer les fichiers modifiés lors d'un commit**

```bash
git show --pretty="" --name-only [REVISION]
```

**Revert last commit**
```bash
git reset --soft HEAD~1
```

# .gitconfig

```ini

# This is Git's per-user configuration file.
[user]
# Please adapt and uncomment the following lines:
#	name = Bertrand Bougon
#	email = bertrand.bougon@gmail.com
[user]
	name = Bertrand Bougon
	email = bertrand.bougon@gmail.com

[alias]
	lg = log -p
    	lol = log --graph --decorate --pretty=oneline --abbrev-commit
    	lola = log --graph --decorate --pretty=oneline --abbrev-commit --all --date=local

[color]
	branch = auto
	diff = auto
	status = auto
[color "branch"]
	current = yellow reverse
	local = yellow
	remote = green
[color "diff"]
	meta = yellow bold
	frag = magenta bold
	old = red bold
	new = green bold
[color "status"]
	added = yellow
	changed = green
	untracked = cyan

```
