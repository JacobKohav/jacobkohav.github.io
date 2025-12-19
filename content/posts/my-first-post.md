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

# Motivation

## Method

![Accuracy plot for StarCoder analysis](https://raw.githubusercontent.com/JacobKohav/llm-programming-language-detection/refs/heads/main/02_selected_all/hardware-specified/hw_4xTesla_V100-SXM2-32GB/analysis_starcoder2_2025-08AUG-01_10h02m39s--UTC_all-StarCoder-mid/accuracy_with_database_syntax_comparator/accuracy_with_database_syntax_comparator-plot.png)