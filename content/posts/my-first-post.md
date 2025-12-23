---
title: "Identifying Programming Languages"
date: 2025-12-03T22:53:58+05:30
draft: false
github_link: "https://github.com/JacobKohav"
author: "Kohav, Jacob"
tags:
  - programming-language-identification
  # - "#test"
description: ""
toc: true
---
This is the beginning of a series of blog posts focusing on programming language identification in code files.

## Introduction
This past summer, as part of work for the 
- [CodeCommons (CC)](https://codecommons.org/) and 
- [Software Heritage (SWH)](https://www.softwareheritage.org/) projects, 

I set out to run a series of tests benchmarking currently existing utilities specializing in identifying programming languages in code files. In a series of blog posts, I will share my methods, results, and findings. 

## Background
First, some background on the two projects involved.
- **Software Heritage** (SWH) is an effort to develop software to support open-source initiative that collects and preserves software in source code form
- **CodeCommons** (CC) is an effort to add historical data, metadata, and contextual links to Software Heritage (SWH)

Within the DiverSE team division of the CodeCommons project, one of the objectives, among several, has been to identify and categorize the syntax of code files hosted in the SWH archive.

## Motivation and Objectives

### Broader motivation
- What are all programming languages utilized in programming industry?
- Is the SWH archive representative of all the (major) programming languages in existence?
- Is there a correlation between programming language popularity (TIOBE) and SWH's language frequency (COBOL model)?
### Technological objective
determine the programming language of a code source file
### Organizational objective
determine the pl of every source file int eh SWH archive; integrate the metadata into SWH's data COBOL model
## Challenges
### Accuracy
- Conventional misidentification: C++ vs. Java
- Language descendants and sub-families: C++ vs. C
- Version/dialect differentiation:
	- Fortran vs. Fortran77
	- RMarkdown vs. Markdown
### Resource-usage
for the purposes of this blog post, as well as the subsequent ones in this series, resource-usage limitations are not in scope.

## Method(s)
Now I will describe CC's current approach to programming language identification, including the 
- dataset,
- programming languages identification techniques encountered, and
- utilities currently explored.
### Dataset
At the time when I'd joined the CC, the team had been using [the dataset](https://github.com/github-linguist/linguist/tree/main/samples) of the [Linguist](https://github.com/github-linguist/linguist/tree/main) programming language identification tool. This has been out of convenience of having a dataset readily curated for testing programming language identification.

Likewise, while the ultimate goal of the team is to classify data in the SWH archive, work on this specific objective began in the third part of 2025 and continues to be in progress, namely managing the protocol for traversing the SWH graph and the immense size of the data repository.

Here are some details on the Linguist dataset which the team has been using thus far, and with which I've continued experiments:
- 3039 programming files, and
- 680 syntaxes (i.e. programming languages) present.

While the Linguist samples dataset has been a mainstay of our testing, it will certainly be valuable to evaluate this dataset in and of itself.
### Programming language identification technique types
Let's discuss some of the existing programming language identification techniques types encountered on CC
### Classification approaches
- Heuristics and Statistical classification 
- Machine Learning
- LLM
### Data delimitation/processing techniques
- Filename/extension
- File header: Shebang, vim/emacs modlines
- Core file content analysis

Some tools also use a combination of the approaches above to classify the file's programmings language(s) in a sequential manner. Such an approach avoid more computationally expensive techniques (ex. processing core file contents) when a simpler approach (i.e. the filename/extension) suffices.

## Testing method