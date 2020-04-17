---
title: "Linux Find String in All Files From Current Directory"
date: "2018-12-24 16:11"
categories: linux grep
---

The Linux `grep` command can be used to search string in files or pipeline output.
For example, I offen search string in a command output, `command arg | grep <pattern>`.

And, it's also possible to find in a file, `grep -i "string" <file1> <file2>`.

But how to find in all files in current directory? Or even do a recursive find.
* Uses `*` to find in all files
* Uses `r` to do recursive find

E.g. `grep -rni "string" *`. It will find in all files in current directory and its sub directories.

More information can run `grep --help` to get.
