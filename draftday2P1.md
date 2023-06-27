# DAY 2 - GIT/GITHUB : BRANCHES TRAINING - 27/06/2023
## Part 1: Preliminaries
- *Create a new repository on the GITHUB website (it just contains a README file)*
- *SSH clone to my local computer*
- *On my local computer, edit README file and change one line*
- *Check status ("git status" will show one modified file)*
- *Stage and Commit (git commit -a)*
- *Push to Origin*
## Part 2: Ready to  do some work with branches
- *Start locally a new branch (famous "development" branch) off main*
- *Start locally a new feature branch off development ("feature/hello_world")*
- *I am now inside the feature/hellow_world branch and ready to create a file*
   1. Create and edit a simple fortran file under the name "hello.f90"
   1. Create a relevant makefile
- *Compile-link the fortran file hello.f90 using the makefile ("make")*
- *Run the executable "hello.exe"*
- *Everything seems to have gone fine, now check the status (git status)*
   1. We see three untracked files, ie hello.f90, hello.exe, makefile (and README.md)
- *Create/copy a .gitignore file that ignores executables*
- *Focus on Staging/committing just the .gitignore file*
- *Check status*
- *Out of the blue I decide that my .gitignore file is permanently required on my development branch*
- *Before that, I am pushing my new development branch onto Origin*
   1. Switch to development
   1. Look at all the existing files in this directory: There is no .gitignore file
       ´´´
       $ls -al
       ´´´
   1. Now push "development" onto Origin (copy dev to the GITHUB website)
       ´´´
       $git push origin development
       ´´´
- *Switch back to the "feature/hello_world" branch*
- *Push "feature/hello_world" to Origin (copy this feature branch to website)*
