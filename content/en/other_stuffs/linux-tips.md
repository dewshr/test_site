---
title: "Linux Tips"
date: 2020-04-19T19:27:11-05:00
description: Some commonly used shell commands
draft: false
hideToc: false
enableToc: true
enableTocContent: false
tocPosition: inner
tocLevels: ["h2", "h3", "h4"]
tags:
- linux
- awk
- sed
- shell
series:
-
categories:
- linux
image: images/feature3/linux.png
---

<br/>

Find common lines between two files
`comm -12 >(sort file1) <(sort file2)`

Getting all the rows with 2 columns having same values
`awk '($4==$5)' input_file.txt > output_file.txt`

Filtering rows based on certain certain column value
`awk '($4 < 5)' input_file.txt > output_file.txt`

Getting mean value for specific column
`awk {total +=$4} END {print total/NR} input_file.txt`

Getting unique values based on multiple column comparison
`awk -F"\t" 'seen[$1,$2,$3,$4]++' input_file,txt > output_file.txt`

Removing first row without opening file
`sed '1d' input_file.txt > output_file.txt`

Changing the values of file
`sed 's/-/\t/g' input_file.txt > output_file.txt`

Sometimes there are carriage returns (\r, ^M) in file, which can mess up the file processing, you can remove it by
`sed 's/\r//g' input_file.txt > output_file.txt`


<br/>

