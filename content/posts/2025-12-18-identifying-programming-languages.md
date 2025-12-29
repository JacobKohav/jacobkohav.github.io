---
title: "Identifying Programming Languages"
date: 2025-12-18T22:53:58-07:00
lastmod: 2025-12-23T18:27:58-07:00
draft: false
github_link: "https://github.com/JacobKohav"
author: "Kohav, Jacob"
tags:
  - programming-language-identification
description: ""
toc: true
---
This is the beginning of a series of blog posts focusing on programming language identification in code files.

## Introduction
This past summer, as part of work for the 
- [CodeCommons (CC)](https://codecommons.org/) and 
- [Software Heritage (SWH)](https://www.softwareheritage.org/) projects, 

I set out to run a series of tests benchmarking currently existing utilities that specialize in identifying programming languages (PL) in code files. In a series of blog posts, I will share my methods, results, and findings. 

## Background
First, some background on the two projects involved.
- **Software Heritage** (SWH) is an effort to develop software to support open-source initiative that collects and preserves software in source code form [1]
- **CodeCommons** (CC) is an effort to add historical data, metadata, and contextual links to Software Heritage (SWH) [2]

Within the DiverSE team division of the CodeCommons project, one of the objectives, among several, has been to identify and categorize the syntax of code files hosted in the SWH archive.

## Motivation and Objectives

### Broader motivation
- What are all PLs utilized in programming industry?
- Is the SWH archive representative of all the (major) PLs in existence?
- Is there a correlation between PL popularity (TIOBE) and SWH's language frequency (COBOL model)? [3]
### Technological objective
- Determine the PLs of a code source file [3]
### Organizational objective
- Determine the PL of every source file in the SWH archive; integrate the metadata into SWH's data COBOL model [3]
## Challenges
### Accuracy
- Conventional misidentification: C++ vs. Java
- Language descendants and sub-families: C++ vs. C
- Version/dialect differentiation:
	- Fortran vs. Fortran77
	- RMarkdown vs. Markdown [3][4][5]
### Resource-usage
for the purposes of this blog post, as well as the subsequent ones in this series, resource-usage limitations are not in scope.

## Method(s)
Now I will describe CC's current approach to PL identification, including the 
- dataset,
- PL identification techniques encountered, and
- utilities currently explored.
### Dataset
At the time when I'd joined the CC, the team had been using [the dataset](https://github.com/github-linguist/linguist/tree/main/samples) of the [Linguist](https://github.com/github-linguist/linguist/tree/main) PL identification tool. This has been out of convenience of having a dataset readily curated for testing PL identification [4]

Likewise, while the ultimate goal of the team is to classify data in the SWH archive, work on this specific objective began in the third part of 2025 and continues to be in progress, namely managing the protocol for traversing the SWH graph and the immense size of the data repository.

Here are some details on the Linguist dataset which the team has been using thus far, and with which I've continued experiments:
- 3039 programming files, and
- 680 syntaxes (i.e. PL) present [4][5][6]

While the Linguist samples dataset has been a mainstay of our testing, it will certainly be valuable to evaluate this dataset in and of itself.
### Programming language identification technique types
Let's discuss some of the existing PL identification techniques types encountered on CC
### Classification approaches
- Heuristics and Statistical classification 
- Machine Learning
- LLM
### Data delimitation/processing techniques
- Filename/extension
- File header: Shebang, vim/emacs modlines
- Core file content analysis

Some tools also use a combination of the approaches above to classify the file's programmings language(s) in a sequential manner. Such an approach avoids more computationally expensive techniques (ex. processing core file contents) when a simpler approach (i.e. the filename/extension) suffices [4][5].

## Testing method
As can be expected, the testing method which we employ on CC is straightforward

1. Select the utility being tested
2. Provide each file from the file samples to the utility for classification
3. Receive the classification result and record it
4. Run an analysis of the utility classificaiton results juxtaposed against the ground truth to produce an accuracy to score.

Throughout updates, I will describe the testing procedure in more detail.

## Conclusion
With this basis set, we'll launch our exploration of PL identification in this series of posts.

## References
> [1] Software Heritage. [Online]. Available: https://www.softwareheritage.org/
>
> [2] Code·Commons. [Online]. Available: https://codecommons.org/
> 
> [3] Software Heritage, “Programming Language Identification (PLI) for Software Heritage,” in *Technical Committee Slides*, 18 Jul. 2025. [Online]. Available: https://gitlab.softwareheritage.org/teams/codecommons/cc-public-resources/-/blob/main/specifications/Programming%20Language%20Identification/slides_technical_committee_2025-05.pdf. Version: Git commit 869b6b39.
>
> [4] CodeCommons contributors. "2025-09-23 Syntax Identification on SWH," CodeCommons GitLab repository, commit 227ccecb, 2025. [Online] Available: https://gitlab.softwareheritage.org/teams/codecommons (access restricted).
>
> [5] Code Commons, “Syntax Identification for CodeCommons WP3.1,” in *2025 CodeCommons Annual Review Slides*, 29 Sep. 2025. [Online]. Available: https://gitlab.softwareheritage.org/teams/codecommons/cc-public-resources/-/blob/main/communication/2025-09-22_CC_Annual_Review/slides/Track1_Language-detection.pdf. Version: Git commit 25f5129c.
>
> [6] GitHub, Inc., “Linguist sample files dataset,” GitHub Linguist repository, commit a7e40d3, 2025. [Online]. Available: https://github.com/github-linguist/linguist/tree/main/samples.

