# Learn command line

Please follow and complete the free online [Bash Scripting Tutorial](https://ryanstutorials.net/bash-scripting-tutorial/) or [Codecademy's Learn the Command Line](https://www.codecademy.com/learn/learn-the-command-line). These are helpful tutorials. You should be able to go through these in a couple of hours.

**Note:** Bash is not installed on a PC. Rather, PC users must install Cygwin. Once Cygwin has been installed, the command line interface witll _emulate_ bash. You can find all information regarding Cygwin [here](https://www.cygwin.com/).

---

### Q1.  Cheat Sheet of Commands  

Here's a list of items with which you should be familiar:  
* show current working directory path
* creating a directory
* deleting a directory
* creating a file using `touch` command
* deleting a file
* renaming a file
* listing hidden files
* copying a file from one directory to another

Make a cheat sheet for yourself: a list of at least **ten** commands and what they do.  (Use the 8 items above and add a couple of your own.)  

* $ pwd :: show current working directory path
* $ mkdir xxx :: creating a directory
* $ rm -r xxx :: deleting a directory
* $ touch xxx :: creating a file using `touch` command
* $ rm xxx :: deleting a file
* $ mv xxx_oldname xxx_newname :: renaming a file
* $ ls -a :: listing hidden files
* $ cp xxx_file xxx_directory/ :: copying a file from one directory to another
* $ cp * :: selects all files in a directory
* $ grep xxx_search xxx_file :: global regular expression print searches files for lines that match a pattern and returns the results
---

### Q2.  List Files in Unix   

What do the following commands do:  
`ls`  
`ls -a`  
`ls -l`  
`ls -lh`  
`ls -lah`  
`ls -t`  
`ls -Glp`  

* $ ls :: lists all files and directories in the working directory
* $ ls -a :: lists all contents in the working directory, including hidden files and directories
* $ ls -l :: lists all contents of a directory in long format
* $ ls -lh :: list long format with readable file size
* $ ls -lah :: list long format with hidden files with readable file size
* $ ls -t :: orders files and directories by the time they were last modified
* $ ls -Glp :: in a long listing but doesn't print group names with directory indicator
---

### Q3.  More List Files in Unix  

Explore these other [ls options](http://www.techonthenet.com/unix/basic/ls.php) and pick 5 of your favorites:

* $ ls -u :: displays files by the file access time
* $ ls -R :: displays subdirectories as well
* $ ls -r :: displays files in reverse order
* $ ls -q :: displays all nonprinting characters as ?
* $ ls -c :: displays files by file timestamp

---

### Q4.  Xargs   

What does `xargs` do? Give an example of how to use it.

xargs is a command that allows you to apply a given command to a series of things in ordered fashion (similar to loop logic). In the ls context, xargs can be useful to apply something to a group of files, such as deleting every file that contains a certain word, or renaming a group of files to something in one command line.

$ seq 5 | xargs -n 1 echo "Hello" :: loops in "Hello" so that for each number in seq 5 "Hello" is stated plus the number 



 

