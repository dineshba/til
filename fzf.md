#### How I am using fzf for every 5 min of my programming life

#### Installation for new users
```bash
brew install fzf
$(brew --prefix)/opt/fzf/install # useful key bindings and fuzzy completion
```
> Note: Its better to use key bindings and fuzzy completion

#### Default options that I use
```bash
export FZF_DEFAULT_OPTS=--height 40% --reverse --border
```

####  My usages

##### To Search in command history:
CTRL + R

##### To Change directory:
```bash
cd + (CTRL + T)
or
cd ** + TAB
```

##### To find and open files in vim(or any editor):
```bash
vim $(fzf)
vim ** + TAB
vim $(fzf --preview 'cat {}')
```
> You can even search and open multiple files using tab

##### To kill a process:
```bash
kill -9 + TAB
```

##### To ssh into a machine:
```bash
ssh ** + TAB
```

##### To get the glimse of a file
```bash
fzf --preview 'cat {}'
```

#### Extensibility
Fzf's usage is **limitless**. We can use it wherever **we want to search and select one(or many) from a list**

##### Case 1:
```
How will you jump to different directory?
- cd /path/to/your/project/path/to/your/service
```
##### Fzf way:
```
alias goproject="cd $(find path/to/your/project -type d -maxdepth 2 | fzf)"
goproject
```
You can have multiple alias for multiple projects or directories


##### Case 2:
```
How will you switch git branch? (select one branch from many)
    - git branch -a
    - copy the branch name
    - git checkout $new_branch_name
    or
    - git checkout + TAB (auto completion feature)

    Both the above approches are not O(1) :-P. How can we optimize?
```
##### Fzf way:
```
alias gcx="git checkout \$(git branch -a | sed 's/remotes\/origin\///' | grep -v '\*|HEAD' | sort |uniq | fzf --select-1)"
gcx
```

##### Case 3:
```How will you tmux workspaces? We are using tmuxp tool to do that.
- tmuxp load workspace_name
or
- tmuxp load ~/.tmuxp/workspace_name.yaml

First involes rembembering all workspace_names (Space Complexity != O(1)) and type correct and fastly (Time Complexity != O(1)). Second involes lot of TABs or searching from commit history (Time Complexity != O(1))

```

##### Fzf way:
```bash
alias ktx='tmuxp load $(ls ~/.tmuxp/*.yaml | grep ".*/.tmuxp/" -r "" | grep "\.yaml" -r "" | fzf) --yes'
```


##### Other tools which use fzf effectively
- kubectx
- kubens
- lazy-connect
- may be your tool

> replace `grep` with `rg` for better experience