# Coding Notes
by [Brandon Booth](https://brandon-booth.com/index.php) - Fall 2020


## Table of Contents
- [Terminal](#Terminal)
- [Git Command Line](#git-command-line)
- [Python](#Python)
- [Django](#Django)
- [Heroku](#Heroku)
- [HTML and CSS](#HTML-and-CSS)

**Helpful links:**
- https://guides.github.com/features/mastering-markdown/#syntax
- https://github.com/RichardLitt/standard-readme/edit/master/README.md
- https://education.github.com/git-cheat-sheet-education.pdf
- https://guides.github.com/introduction/flow/
- https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging

> Note: TBD...

## Terminal
Show hidden files on Mac: ```Command+Shift+.```

To see environment variable enter the following into terminal:
```sh
printenv
```

Add .zshrc (or .bash) files using nano by entering the following into terminal:
```sh
nano .zshrc
```
Add envrionment variable:
```sh
export db_user="username"
```
Save changes:
Enter ```Control+X```, then ```Y``` to save, then ```Enter``` to keep the same file name.



Check version of git installed on mac:
```sh
git -–version
```

Add GitHub username and email to git on Mac:
```sh
git config --global user.email "brandon.booth@yahoo.com"
```
```sh
git config --global user.name "brandonbooth"
```

Navigate to location of folder or project:
```sh
cd projects
```

Initialize the git repository within the project folder:
```sh
git init
```

Use terminal to view the hidden git repository that was created (this will make files visible in finder):
```sh
defaults write com.apple.find AppleShowAllFiles YES
```

Check status of git folder:
```sh
git status
