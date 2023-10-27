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

## Week 2: Navigating a UNIX System

Second week had more basic usage such as using and navigating the file system and connecting to a remote server.

<!-- Koodiesimerkki -->

#### Example 2.1 Connecting remote server with `ssh`

```bash
ssh username
```

---

_The interview video with the creator of `ssh` tool was interesting._

_Creating links with `ln` was something that I hadn't done that much, so it was nice to learn more about it._

## Week 3: Basic Corpus Processing

<!-- Koodiesimerkki -->

#### Unix and Windows line endings

## Week 4: Advanced Corpus Processing

<!-- Koodiesimerkki -->

## Week 5: Scripting and Configuration Files

<!-- Koodiesimerkki -->

## Week 6: Installing and Running Programs

### Python Virtual Environments

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

## Appendix A: Used Commands

| `bash` command | description                         |
| -------------- | ----------------------------------- |
| `ls`           | Lists files                         |
| `tr`           |                                     |
| `ln`           | Create links within the file system |
