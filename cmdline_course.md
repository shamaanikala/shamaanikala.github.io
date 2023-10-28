---
layout: default
---

# Command-Line Course

## Introduction

[_Command-Line Tools for Linguists_](https://studies.helsinki.fi/kurssit/toteutus/hy-opt-cur-2324-261401a1-c550-4436-91b9-7edf4a1a3b57) is a 5 credit intermediate level course unit of Bachelor's Programme in Languages in University of Helsinki.
([More details.](https://studies.helsinki.fi/courses/course-unit/otm-92ee484e-456b-409f-a397-d9d2b6e40a2f/KIK-LG221))

Main foucs of the course is UNIX (or Linux) command line, several different command line tools, their basic usage and also a bit how to use the tools in language technology related problems.

---

_I used bash shell mainly within Ubuntu Linux 22.04 LTS in Windows Subsystem Linux 2 (WSL2)._

## Table of Contents

<!-- prettier-ignore -->
* Do not remove this line (it will not be displayed)
{:toc}

## Week 1: Introduction to Command Line Environments

The first week focused on setting up bash and basic command-line usage.

This week also introduced the text editor `nano`.

### Introduction Lecture

The first week had the only on-site lecture of the course.
The lecture included the following command-line snippet:

<!-- Koodiesimerkki -->

#### Example 1.1: Creating a frequency list of words in a text file

Suppose there is a text file `file.txt` in the working directory:

```bash
cat file.txt | tr -s '\r\n' '\n' \
  | grep "." \
  | sort \
  | uniq -c \
  | sort -nr \
  | head -10

```

where the `\` (backslash) can be used to split the commands to multiple lines.

---

_I have used command line for years already so first week was easy._
_Still the UNIX tool `tr` was something I don't recall ever using or seeing before._

_I have been using Vim as my command-line editor so I decided to use it instead of Nano._
_I actually need to find the keyboard shortcut to quit Nano_ 😹.

## Week 2: Navigating a UNIX System

Second week had more basic usage such as using and navigating the file system.  
Week 2 looked into following concepts and related tools:

- Process management
- File permissions
- Remote server usage with `ssh`
- Remote server file operations with `scp`

<!-- Koodiesimerkki -->

#### Example 2.1 Connecting remote server with `ssh`

```bash
ssh username@remote.host
```

#### Example 2.2 Uploading `file.txt` to a remote server with `scp`

Copying `file.txt` from current working directory to a remote server folder `remote_dir` inside users `/home`-directory with `scp`

```bash
scp  file.txt username@remote.host:~/remote_dir
```

---

_The interview video with the creator of `ssh` tool was interesting._

_Creating links with `ln` was something that I hadn't done that much, so it was nice to learn more about it._

_Using `ssh` config was new to me._

## Week 3: Basic Corpus Processing

Week 3 focused on text file and standard input and output operations with the command-line tools.

`grep` tools was introduced and its extended regular expression syntax (`-E` in Linux bash) was used for analyzing text files.

### Unix and Windows line endings

Unix and Windows text files have different kinds of line endings.

**Windows**:
`\r\n`

**Unix**:
`\n`

To change the used line-endings one can use bash programs `dos2unix` and `unix2dox`.

#### Example 3.1 Changing Windows text file to Unix format

```bash
dos2unix file.txt
```

#### Example 3.2 Using `ap-get` to install `dos2unix`

If the `dos2unix` program is not installed, it can be installed with `apt`.

Updating the package information before installation.

```bash
sudo apt-get update
sudo apt-get install dos2unix
```

---

_I was already familiar with the different encodings and line ending difference between Windows and UNIX systems._
_But I had never encountered such a concise treatment of how to handle these problems with bash before._

_It was fun to learn more about_ `grep`_!_

## Week 4: Advanced Corpus Processing

<!-- Koodiesimerkki -->

---

_This was the one of the most time consuming weeks._
_For some reason I also got many of the exercises wrong eventhough I checked and rechecked my answers and regular expressions many times before submitting the Moodle Quiz._
_I wonder if the there were some differences between my Project Gutenberg text files and the ones used with the model solutions._

## Week 5: Scripting and Configuration Files

<!-- Koodiesimerkki -->

## Week 6: Installing and Running Programs

### Python Virtual Environments

![xkcd comic about the complicated nature of Python environment](https://imgs.xkcd.com/comics/python_environment.png)  
[Original comic](https://xkcd.com/1987/)

<!-- Koodiesimerkki -->

## Week 7: Version Control

<!-- Koodiesimerkki -->

## Final Assignment: Building Webpages using GitHub Pages

### How to add Table of Contents

https://stackoverflow.com/questions/9602936/how-to-create-a-table-of-contents-to-jekyll-blog-post

<!-- prettier-ignore -->
```markdown
* Do not remove this line (it will not be displayed)
{:toc}

```

if using Prettier jotakinjotakin
https://prettier.io/docs/en/ignore.html#markdown

```markdown
<!-- prettier-ignore -->
* Do not remove this line (it will not be displayed)
{:toc}
```

## MISC

The course did take into account the differences between linux and mac environments.

## Conclusion

Mihail Cxcdsfssss defines flow...
This course did manage hit that spot..
I could deepen my understanding of regex, bash and sed, grep...

## Appendix A: Commands

The table lists selection of the commands used during the course with a short description.

| `bash` command    | description                                                      |
| ----------------- | ---------------------------------------------------------------- |
| `ls`              | Lists files                                                      |
| `tr`              | Translates or deletes characters                                 |
| `ln`              | Create links within the file system                              |
| `chmod`           | Edit the file permissions                                        |
| `touch`           | "Touch" a file. Create an empty file if it doesn't exist yet.    |
| `mkdir`           | Create new folder/directory                                      |
| `cp`              | Copy file                                                        |
| `ssh`             | _Secure SHell_, connect to a remote server                       |
| `scp`             | _Secure Copy_, Exchange files with the remote server             |
| `cat`             | Catenate files. Or output one file to the terminal               |
| `rm`              | Remove file                                                      |
| `which <command>` | Outputs the location of `<command>` stored in the `$PATH`        |
| `kill`            | Kill a process                                                   |
| `ps aux`          | List processes                                                   |
| `grep`            | Filter standard output or files with regular expressions.        |
| `sort`            | Sort standard output                                             |
| `wget`            | Download files                                                   |
| `nano`            | Simple command line text editor                                  |
| `vim`             | Powerful command line text editor                                |
| `less`            | Display text file                                                |
| `dos2unix`        | Change Windows line-endings to Unix line-endings                 |
| `unix2dos`        | Change Unix line-endings to Windows line-endings                 |
| `iconv`           | Conver text file character encondings                            |
| `uniq`            | "_report or omit repeated lines_" - `whatis uniq`                |
| `whatis`          | "_display one-line manuaal page descriptions_" - `whatis whatis` |
