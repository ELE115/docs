# How to setup Git for your computer

1. In IntelliJ IDEA workspace, find the `Terminal` panel (it is usually hidden at the bottom of your workspace).
1. Type the following into the terminal. Hit enter at the end of a line.

**Note:** If you are in `Welcome to IntelliJ IDEA` dialog, you should postpone this setup until you have created a project.

**Note:** Do **NOT** copy paste this. You may accidentally break things here.

**Note:** Use the same capitalization as you did on GitHub registration.
```
git config --global user.name <Your-GitHub-UserName>
git config --global user.email <Your-GitHub-Email>
```

**Note:** Omit the `<`/`>` surrounding.

# How to setup Git for a single project

1. **Make sure Git is setup for your computer first!** (See above for instructions)
1. In IntelliJ IDEA workspace, click menu: `VCS`/`Import into Version Control`/`Create Git Repository...`.
1. Make sure your project folder is selected. Click `OK`.

**EXTREMELY IMPORTANT NOTICE:
DO NOT SELECT `src` FOLDER. DO NOT SELECT ANY FOLDER OTHER THAN THE DEFAULT ONE AT ALL.
DO NOT CLICK ANYWHERE OTHER THAN THE `OK` BUTTON.
IF YOU PICK ANY FOLDER OTHER THAN THE ROOT FOLDER OF YOUR PROJECT,
YOUR PROJECT WILL BE IRREVERTABLY DESTROYED.**
[How to fix your destroyed project (if you are TA)](https://github.com/ELE115/labs/tree/master/docs/fix.md)

1. Click menu: `File`/`Settings...` (or `IntelliJ IDEA`/`Preferences...` if you are using **mac OS**).
1. Click `Version Control` (**NOT** unfolding it, just click).
1. Pick the only item in the list (it should currently be the path to your project).
1. Hit enter or click `Edit` (the small pen icon).
1. Make sure `Project` is selected.
1. Click `OK`.
1. Click `OK`.

Also, you need to do the following:

1. In IntelliJ IDEA workspace, click menu: `VCS`/`Git`/`Remotes...`.
1. Click `+`.
1. For the Name, just use `origin` by default. For the URL:
  * For Linux and mac OS users:
  When you accepted an assignment in GitHub Classroom, you were given a link to a private repo.
  At that page GitHub asked you to choose between `HTTPS` and `SSH`. Pick `SSH` and you will get a link looks like
  `git@github.com:ELE115/lab*****-netid.git`. That's what you need right here.
  * For Windows users:
  When you accepted an assignment in GitHub Classroom, you were given a link to a private repo.
  At that page GitHub asked you to choose between `HTTPS` and `SSH`. Pick `HTTPS` and you will get a link looks like
  `https://github.com/ELE115/lab*****-netid.git`. That's what you need right here.
1. Click `OK`.
1. Click `OK`.

**Note:** If there's already some contents in the repo, you may use the green `Clone or download` button to get the URL.

**Note:** The URL is **NOT** guranteed to work on Windows. If you have trouble doing Git Push, ask TA for help.

# How to create a commit

1. **Make sure Git is setup for your project first!** (See above for instructions)
1. [Auto-format](https://github.com/ELE115/docs/blob/master/faq.md#how-to-maintain-a-good-coding-style) your Java source files.
1. Click `VCS`/`Commit...`.
1. Choose what changes you want to include in the commit.
1. Add a meaningful commit message. The first line of your commit message shall be a summary.
**NEVER** use empty commit message or garbage commit message.
1. Uncheck **ALL** checkboxes in `Before Commit` section.
1. Click `Commit`.

> Well, but **what should I commit?**

Basically you have to *eventually* commit everything,
including all the files that are provided to you at the beginning (`build.gradle`, `settings.gradle`, ...),
and the files you created during the lab (`src/main/java/...`).

By *eventually* I mean, you don't have to commit everything all at once.
You can commit some files in your first commit,
other files in another commit.
But, before the code submittion deadline, you **must** have all files committed and pushed to GitHub.

# How to push your commit to GitHub

1. **Make sure Git is setup for your project first!** (See above for instructions)
Also make sure you have several commit(s) before you push.
1. Click `VCS`/`Git`/`Push...`.
1. Review the changes.
1. Click `Push`.

To **verify** everything is good, please visit the assignment repo on GitHub and directly browse your code.

If everything looks great there, you are all set!
