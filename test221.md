
# DAY 2 - GIT/GITHUB : BRANCHES TRAINING - 27/06/2023

## Introduction

The diagram below [^1] illustrates the logic behind branching in GitHub/Git. The simple sequence **main** $\rightarrow$ **development** $\rightarrow$ **feature** summarises our particular example. The feature branch constitutes the actual work space.
![](slide54.png)
## Preliminaries
- On the GITHUB website, look for the + sign to create a new repository, and do it (it just contains a README file).
- SSH-clone to my local Linux system the newly created repository.
- On my local Linux computer, edit README and change one line.
- Check status (`$ git status` shows one modified file).
- Stage and Commit.
- Push to Origin (`$ git push`, since we have not used any branch commands as yet; by default, only the main branch is present on the repository).

## Ready to  do some work with branches
- Start locally a new branch (the famous development branch) off main.
- Start locally a new feature branch off development (feature/hello_world).
- I am now inside the feature branch and ready to create a file:
  
    > Create and edit a simple fortran file under the name `hello.f90`.
    > 
    > Create a relevant makefile (`Makefile`).

 ```bash
program Hello
  print *, "Hello, World!"
end program Hello
 ```
 
 ```bash
all:
        gfortran hello.f90
 ```
- Compile-link the fortran file `hello.f90` using the makefile (`make`).
- Run the executable `hello.exe`.
- After a successful run, look at the status (`$ git status`).

    > We see three untracked files, ie `hello.f90`, `hello.exe`, `Makefile`

- Create (or copy from another GitHub directory) a `.gitignore` file that ignores executables
- stage/commit just the `.gitignore` file (I am in the feature branch)
- Check status
- Out of the blue, I decide that my `.gitignore` file would be useful on my development branch (not now; it will be done when merging)
- Before that, I am pushing my new development branch onto Origin
  
    > Switch to development
    >
    > Look at all the existing files in this directory (ls -al): There is no .gitignore file (still only README)
    > 
    > Now push development onto Origin (`$ git push origin development`)
    
- Switch back to the feature branch
- Look at the status: There are two untracked files, ie `Makefile` and `hellow_world.f90`:
 ```bash
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git status
On branch feature/hellow_work
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        Makefile
        hw.f90

nothing added to commit but untracked files present (use "git add" to track)
 ```
- Stage/commit both `Makefile` and `hellow_world.f90`:
 ```bash
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git add Makefile hw.f90
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git commit -m 'Stage-Commit Makefile and hw.f90'
[feature/hellow_work 0a3071e] Stage-Commit Makefile and hw.f90
 2 files changed, 5 insertions(+)
 create mode 100644 Makefile
 create mode 100644 hw.f90
 ```
- Push to origin the feature branch (`git push origin feature/hellow_world`):
 ```bash
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git status
On branch feature/hellow_work
nothing to commit, working tree clean
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git push origin feature/hellow_work
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 463 bytes | 463.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:mperezjigato/branchexercisepart1.git
   e7a4fcf..0a3071e  feature/hellow_work -> feature/hellow_work
 ```
- Go to the GitHub website and set up a Pull-Request **feature** $\rightarrow$ **development** (once the Pull-Request has successfully been completed the feature branch is deleted on the website!).
- Back on the local Linux system, compare my current feature branch with my local development branch (on the website, development contains already all the files -including .gitignore-; however, locally, the development branch only contains README).
 ```bash
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git diff development
diff --git a/.gitignore b/.gitignore
new file mode 100644
index 0000000..a18d948
--- /dev/null
+++ b/.gitignore
@@ -0,0 +1,8 @@
+# editor backup files
+*~
+*.swp
+*.bak
+
+# executables
+a.out
+*.exe
diff --git a/Makefile b/Makefile
new file mode 100644
index 0000000..5f5179b
--- /dev/null
+++ b/Makefile
@@ -0,0 +1,2 @@
+all:
+       gfortran hw.f90
diff --git a/hw.f90 b/hw.f90
new file mode 100644
index 0000000..4072ab0
--- /dev/null
+++ b/hw.f90
@@ -0,0 +1,3 @@
+program Hello
+  print *, "Hello, World!"
+end program Hello
 ```
- Switch to the development branch (`$ git switch -`)
- Pull the remote development branch towards the local Linux machine (`$ git pull origin development`)

## Continue working with branches

- On the local Linux system, create -off the development branch- a new feature branch (feature/bye_world) and, then push it to origin:  

    > $ git switch -C feature/bye_world
    >
    > $ git push origin feature/bye_world

- Create a bye.f90 file by copying and modifying the above hello.f90 file. Modify the above Makefile accordingly (keeping the same filename). Compile, link and run:
 ```bash
program Bye
  print *, "Bye, World!"
end program Bye
 ```

 ```bash
all:
        gfortran bye.f90 
 ```
 
 ```bash
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ ./bye.exe
Bye, World!
 ```
- Stage/Commit the new/both files:
```bash
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ ls
Makefile  README.md  bye.exe  bye.f90  hw.exe  hw.f90
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git status
On branch feature/bye_world
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   Makefile

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        bye.f90

no changes added to commit (use "git add" and/or "git commit -a")
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git add bye.f90
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git commit -a -m 'Changes in Makefile and new bye.f90'
[feature/bye_world 0f07059] Changes in Makefile and new bye.f90
 2 files changed, 4 insertions(+), 1 deletion(-)
 create mode 100644 bye.f90
```
```bash
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git push origin feature/bye_world
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 489 bytes | 163.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:mperezjigato/branchexercisepart1.git
   198f5e9..0f07059  feature/bye_world -> feature/bye_world
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git status
On branch feature/bye_world
nothing to commit, working tree clean
```
- Once I check my GitHub website (three branches!) a merging procedure different from the above (the feature/hello_world branch was merged to the development branch on the website!-) is applied: The merging **feature** $\leftarrow$ **development** is now carried out locally on the Linux system!. First switch to the development branch:

   > $ git switch development
   >
   > $ git merge feature/bye_world
  
 ```bash
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git switch development
Switched to branch 'development'
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git merge feature/bye_world
Updating 198f5e9..0f07059
Fast-forward
 Makefile | 2 +-
 bye.f90  | 3 +++
 2 files changed, 4 insertions(+), 1 deletion(-)
 create mode 100644 bye.f90
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git branch
* development
  feature/bye_world
  feature/hellow_work
  main
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git branch -r
  origin/HEAD -> origin/main
  origin/development
  origin/feature/bye_world
  origin/feature/hellow_work
  origin/main
 ```
 where the last two entries list the existing branches both locally and remotely.
- You can remove locally on the Linux system my feature/hellow_world branch;   
  afterwards, remove the feature/bye_world branch ($ git branch -d feature/something)
 ```bash
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git branch -d feature/hellow_work
Deleted branch feature/hellow_work (was 0a3071e).
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git branch -d feature/bye_world
Deleted branch feature/bye_world (was 0f07059).
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git branch
* development
  main
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ ls
Makefile  README.md  bye.exe  bye.f90  hw.exe  hw.f90 
 ```
 Just two branches are left locally on the Linux system: main and development.
- Get rid now of the remote bye_world feature branch ($ git branch -r -d feature/bye_world):
 ```bash
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git branch -r -d origin/feature/bye_world
Deleted remote-tracking branch origin/feature/bye_world (was 0f07059).
 ```
- Probably the most important steps before we close down this document:

    > Push to Origin the local development branch.
    >  ```bash
    >               $ git push origin development
    >  ```
    >
    > On the GitHub website, set up a Pull-Request **development** $\rightarrow$ **main** and carry out the merge (NEVER delete a development branch!).
    >
    > Locally on the Linux system, switch to the main branch and pull it:
    >  ```bash
    >               $ git switch main
    >  ```
    >
    >  ```bash
    >               $ git pull
    >  ```
    >
    > On the local Linux system, *switch back to the development branch and leave it there!*
    >  ```bash
    >               $ git switch development
    >  ```bash
    >
    
 with the outcome:
  ```bash
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git push origin development
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:mperezjigato/branchexercisepart1.git
   198f5e9..0f07059  development -> development
  ```   
  ```bash
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git switch main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git pull
remote: Enumerating objects: 1, done.
remote: Counting objects: 100% (1/1), done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (1/1), 625 bytes | 625.00 KiB/s, done.
From github.com:mperezjigato/branchexercisepart1
   9f9ef59..153efd0  main              -> origin/main
 * [new branch]      feature/bye_world -> origin/feature/bye_world
Updating 9f9ef59..153efd0
Fast-forward
 .gitignore | 8 ++++++++
 Makefile   | 2 ++
 bye.f90    | 3 +++
 hw.f90     | 3 +++
 4 files changed, 16 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 Makefile
 create mode 100644 bye.f90
 create mode 100644 hw.f90
  ```
  ```bash
 mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git branch
  development
* main
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git switch development
Switched to branch 'development'
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git branch                                                    
* development
  main
  ```
 Incidentally, it should be noted that my remote branch deletion does not seem to work!


[^1]: github.com/gjbex/Version-control-with-git
