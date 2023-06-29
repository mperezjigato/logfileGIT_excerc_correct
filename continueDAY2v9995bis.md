
# DAY 2 - GIT/GITHUB : BRANCHES TRAINING - 27/06/2023

## Introduction

The diagram below [^1] illustrates the logic behind branching in GitHub/Git. In this particular example the sequence we followed is **main** $\rightarrow$ **development** $\rightarrow$ **feature**. The latter  constitutes the actual working space.
![](slide54.png)
## Part 1: Preliminaries
- *Create a new repository on the GITHUB website (it just contains a "README" file)*
- *SSH clone to my local computer*
- *On my local computer, edit README file and change one line*
- *Check status ("git status" will show one modified file)*
- *Stage and Commit (git commit -a)*
- *Push to Origin*

## Part 2: Ready to  do some work with branches
- *Start locally a new branch (famous "development" branch) off main*
- *Start locally a new feature branch off development ("feature/hello_world")*
- *I am now inside the feature/hellow_world branch and ready to create a file*
  
    > Create and edit a simple fortran file under the name "hello.f90"
    > 
    > Create a relevant makefile

- *Compile-link the fortran file hello.f90 using the makefile ("make")*
- *Run the executable "hello.exe"*
- *Everything seems to have gone fine, now check the status (git status)*

    > We see three untracked files, ie hello.f90, hello.exe, makefile (and README.md)

- *Create (or copy from another GitHub directory) a .gitignore file that ignores executables*
- *Focus on Staging/committing just the .gitignore file (I am in the feature branch)*
- *Check status*
- *Out of the blue I decide that my .gitignore file is permanently required on my development branch (not now; it will be done when merging)*
- *Before that, I am pushing my new development branch onto Origin*
  
    > Switch to development
    >
    > Look at all the existing files in this directory (ls -al): There is no .gitignore file
    > 
    > Now push "development" onto Origin (git push origin development)
    
- *Switch back to the "feature/hello_world" branch*
- *Look at the status: There are two untracked files, ie `Makefile` and `hellow_world.f90`:*
 ```bash
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git status
On branch feature/hellow_work
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        Makefile
        hw.f90

nothing added to commit but untracked files present (use "git add" to track)
 ```
- *Focus on stage/commit both `Makefile` and `hellow_world.f90`:*
 ```bash
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git add Makefile hw.f90
mperez2023@DESKTOP-UGTH925:~/GitHub/tmpnew1/branchexercisepart1$ git commit -m 'Stage-Commit Makefile and hw.f90'
[feature/hellow_work 0a3071e] Stage-Commit Makefile and hw.f90
 2 files changed, 5 insertions(+)
 create mode 100644 Makefile
 create mode 100644 hw.f90
 ```
- *Push to origin the feature/hellow_world branch (git push origin feature/hellow_world):*
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
- *Go to the GitHub website and set up a Pull-Request **feature** $\rihtarrow$ **development** (once the pull-request has successfully completed the feature branch is deleted on the website!)*
- *Back on the local Linux system, compare my current feature branch with my local development branch (on the website, development contains already all the files -including .gitignore-; however, locally, the development branch only contains README)
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
- *Switch to the development brach (git switch development)*
- *Pull the remote development branch towards the local Linux machine (git pull origin development)* 
- *On the local Linux system, create -off the development branch- a new feature branch (feature/bye_world) and, then push it to origin:*  

    > $ git switch -C feature/bye_world
    >
    > $ git push origin feature/bye_world

## Part 3: Continue with branches
