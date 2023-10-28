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

#### Example 1.1: Creating a frequency list of words in a text file {#example-1.1}

The list is outputted to the standard output stream.
It can be written in a text file with `>` operator if needed.

Suppose there is a text file `file.txt` in the working directory:

```bash
cat file.txt | tr -s '\r\n' '\n' \
  | grep "." \
  | sort \
  | uniq -c \
  | sort -nr \

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

Fourth week focused on `sed` tool and piping commands with `|` operator.
Using `sed` tool included also even more work with regular expressions.

The exercises also included some basic statistical analysis of the text corpora.

<!-- Koodiesimerkki -->

#### Example 4.1 Using `sed` and `grep` together with piping

First select only the lines with "Example" using extended regex `-r`, only output these selected lines `-n` and then pipe the output to `grep` and count `-c` the lines with string "Example":

```bash
sed -rn '/\bExample/p' < cmdline_course.md | grep -c 'Example'
```

---

_This was the one of the most time consuming weeks._
_For some reason I also got many of the exercises wrong even though I checked and rechecked my answers and regular expressions many times before submitting the Moodle Quiz._
_I wonder if the there were some differences between my Project Gutenberg text files and the ones used with the model solutions._

## Week 5: Scripting and Configuration Files

Bash configuration with `.bashrc` and basic bash-scripting.

Shell prompt customization with `PS1`.

### Table of bash variables

Table based on the table found in [this bash-scripting tutorial](https://ryanstutorials.net/bash-scripting-tutorial/bash-variables.php).
The tutorial was used in the course and was well written.

These variables can be used in the bash command line and in scripts.

| Variable    | Description                                                |
| ----------- | ---------------------------------------------------------- |
| `$0`        | name of the script (or first command line argument given)  |
| `$1` - `$9` | command line arguments 1-9 given to the script             |
| `$#`        | number of total command line arguments given to the script |
| `$@`        | All arguments                                              |
| `$?`        | Exit code of the latest process                            |
| `$$`        | Process PID of the current script                          |
| `$RANDOM`   | Random number                                              |
| `$PWD`      | Current working directory or `pwd`.                        |
| `$OLDPWD`   | Previous working directory                                 |

#### Example 5.1 Bash-script to calculate frequency list similar to [Example 1.1](#example-1.1)

```bash
#!/bin/bash

# script: ferqlist.sh
#
# Read a text file from the stadard input and compute a
# frequency list of the words in the text. Print output
# to standard output.
#
# Abort the script if either file $1 or $2 is missing

if [ $# -ne 2 ]
then
  echo "ERROR: Two command line arguments required!"
  echo "$0 input_text_file output_freq_file"
  exit 1
fi

cat $1 |
dos2unix |
tr -s "[:space:]" "\n" |
tr -d "[:punct:]" |
sort |
uniq -c |
sort -nr > $2

```

Some differences between [Example 1.1](#example-1.1):

- `dos2unix` is used instead of `tr '\r\n' '\n'`.
- At the end the output is forwarded to a text file which name is given as second command line argument `$2`.

Also note the usage of special [POSIX regural expression character classes](https://en.wikibooks.org/wiki/Regular_Expressions/POSIX_Basic_Regular_Expressions#Character_classes) such as `[:space:]`!

#### Example 5.2 Command substitution syntax

I bash one can use commands inside commands with command substitution

1. Command inside _backticks_ `` ` ``
   > `` `<command>` ``
2. Command inside `$( )`
   > `$( <command> )`

```bash
echo /etc directory has `ls /etc | wc -l` targets.
```

```bash
echo /etc directory has $(ls /etc | wc -l) targets.
```

#### Example 5.3 Basic arithmetic operations within bash

With expression `$(( x € y))`, where `x` and `y` are numeric values and `€` is a arithmetic operator, one can calculate within bash.

Check if the number of lines in a text file `file.txt` is even (it outputs `0` if the answer is even):

```bash
echo $(( `wc -l < file.txt` % 2))
```

where `%` is the mod operator.

---

_Another time consuming week._
_Ability to write reliable and reusable bash-scripts is a really valuable skill in my opinion._
_The problem is that many times it is really time consuming and writing a similar Python script is much faster._
_Debugging and testing bash scripts isn't the most streamlined procedure or maybe I am unaware how to do it properly._
_Still this was maybe one of the most fun weeks as the bash scripting is quite fun._

_There were many new command-line variables that I didn't know, like `$OLDPWD` or using `cd -` to change directory to the `$OLDPWD`._

## Week 6: Installing and Running Programs

### Python Virtual Environments

![xkcd comic about the complicated nature of Python environment](https://imgs.xkcd.com/comics/python_environment.png)
[Original location](https://xkcd.com/1987/)

<!-- Koodiesimerkki -->

## Week 7: Version Control

<!-- Koodiesimerkki -->

## Final Assignment: Building Webpages using GitHub Pages

### CV

I decided to focus on this website more than to the CV.
I created a simple draft template of CV in [Overleaf](https://www.overleaf.com).
I generated some dummy text to the CV with [LaTeX lipsum-package](https://ctan.org/pkg/lipsum).

### How to add Table of Contents

https://stackoverflow.com/questions/9602936/how-to-create-a-table-of-contents-to-jekyll-blog-post

<!-- prettier-ignore -->
```markdown
* Do not remove this line (it will not be displayed)
{:toc}

````

if using Prettier jotakinjotakin
https://prettier.io/docs/en/ignore.html#markdown

```markdown
<!-- prettier-ignore -->
* Do not remove this line (it will not be displayed)
{:toc}
```

### Linking within the page

HTML has the ability to use hyperlinks within the website itself.
Many Markdown engines supports extended syntax (including Jekyll) which enables [creating and linking to heading ids](https://www.markdownguide.org/extended-syntax/#heading-ids).

```markdown
##### Heading {#own-heading-id}

<!-- linking to the heading -->

[Click this to see the Heading](#own-heading-id)
```

_Visualising the above example:_

---

> ##### Heading {#own-heading-id}
>
> <!-- linking to the heading -->
>
> [Click this to see the Heading](#own-heading-id)

---

_End of visualising the example._

## MISC

The course did take into account the differences between linux and mac environments.

## Conclusion

Mihail Cxcdsfssss defines flow...
This course did manage hit that spot..
I could deepen my understanding of regex, bash and sed, grep...

## Appendix A: Commands

The table lists selection of the commands used during the course with a short description.

| `bash` command    | description                                                                                                     |
| ----------------- | --------------------------------------------------------------------------------------------------------------- |
| `ls`              | Lists files                                                                                                     |
| `tr`              | Translates or deletes characters                                                                                |
| `ln`              | Create links within the file system                                                                             |
| `chmod`           | Edit the file permissions                                                                                       |
| `touch`           | "Touch" a file. Create an empty file if it doesn't exist yet.                                                   |
| `mkdir`           | Create new folder/directory                                                                                     |
| `cp`              | Copy file                                                                                                       |
| `ssh`             | _Secure SHell_, connect to a remote server                                                                      |
| `scp`             | _Secure Copy_, Exchange files with the remote server                                                            |
| `cat`             | Catenate files. Or output one file to the terminal                                                              |
| `rm`              | Remove file                                                                                                     |
| `which <command>` | Outputs the location of `<command>` stored in the `$PATH`                                                       |
| `kill`            | Kill a process                                                                                                  |
| `ps aux`          | List processes                                                                                                  |
| `grep`            | Filter standard output or files with regular expressions.                                                       |
| `sort`            | Sort standard output                                                                                            |
| `wget`            | Download files                                                                                                  |
| `nano`            | Simple command line text editor                                                                                 |
| `vim`             | Powerful command line text editor                                                                               |
| `less`            | Display text file                                                                                               |
| `dos2unix`        | Change Windows line-endings to Unix line-endings                                                                |
| `unix2dos`        | Change Unix line-endings to Windows line-endings                                                                |
| `iconv`           | Conver text file character encondings                                                                           |
| `uniq`            | "_report or omit repeated lines_" - `whatis uniq`                                                               |
| `whatis`          | "_display one-line manuaal page descriptions_" - `whatis whatis`                                                |
| `wc`              | "_print newline, word, and byte counts for each file_" - `whatis wc`. <br /> Or calculate word and line counts. |
| `sed`             | "_stream editor for filtering and transforming text_" - `whatis sed`                                            |
| `paste`           | "_merge lines of files_" - `whatis paste`                                                                       |
| `echo`            | "_display a line of text_" - `whatis echo`                                                                      |
| `export`          | "Export"/"Define" environmental variable                                                                        |
| `pwd`             | Current working directory                                                                                       |
| `cd`              | Change directory                                                                                                |
