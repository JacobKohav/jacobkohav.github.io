---
title: "Testing Programming Language Identification"
date: 2025-12-29T03:12:58
draft: false
github_link: "https://github.com/JacobKohav"
author: "Kohav, Jacob"
tags:
  - programming-language-identification
  - linguist
  - library/pandas
  - library/numpy
  - file-format/json
description: ""
toc: true
---

In the previous blog post, I introduced the background, motivation, objectives, challenges, and goals of this experiment in identifying programming languages in code files. 

## Introduction
In this post, will go through the benchmarking, testing, and analysis methods that I’m employing in more detail.

## Benchmarking procedure
First we’ll go through the benchmarking protocol that we’ve been utilizing on the CodeCommons project. 

As I’d gone over in the previous post, the project has been heavily making use of the [Linguist dataset](https://github.com/github-linguist/linguist/tree/main/samples) from [GitHub](https://github.com/github-linguist/linguist/tree/main) for prototyping and testing prior to full execution on the Software Heritage (SWH) archive.

With this dataset, we run the 
- selected utility across
- each of the 3039 dataset files

one by one, recording the results. 

We receive the results in a parseable `.json` format.

### Accuracy benchmarking
We receive the results of accuracy benchmarking in `benchmark-<utility_name>-output.json` and they look somewhat like this:

```json
{
  "results": [
    {
      "filename": "/samples/Prolog/dleak-report",
      "output": "{\"/samples/Prolog/dleak-report\":{\"lines\":11,\"sloc\":8,\"type\":\"Text\",\"mime_type\":\"text/plain\",\"language\":\"Prolog\",\"large\":false,\"generated\":false,\"vendored\":false}}\n"
    },
    {
      "filename": "/samples/Prolog/plunit_test_example.plt",
      "output": "{\"/samples/Prolog/plunit_test_example.plt\":{\"lines\":11,\"sloc\":7,\"type\":\"Text\",\"mime_type\":\"application/vnd.hp-HPGL\",\"language\":\"Prolog\",\"large\":false,\"generated\":false,\"vendored\":false}}\n"
    },
    {
      "filename": "/samples/Prolog/logic-problem.pro",
      "output": "{\"/samples/Prolog/logic-problem.pro\":{\"lines\":68,\"sloc\":60,\"type\":\"Text\",\"mime_type\":\"text/plain\",\"language\":\"Prolog\",\"large\":false,\"generated\":false,\"vendored\":false}}\n"
    }
  ]
}
```

In each entry, we first have the filename, followed by the "output,” including numerous elements of metadata, among which is the identified programming language.

### Speed benchmarking
Similarly, we have the speed-related metrics a `benchmark-<utility_name>-hyperfine.json` file.

```json
{
  "results": [
    {
      "command": "github-linguist --json '/samples/Prolog/dleak-report' > /results/tmp_file",
      "mean": 0.39646997458,
      "stddev": null,
      "median": 0.39646997458,
      "user": 0.36022556,
      "system": 0.03594272,
      "min": 0.39646997458,
      "max": 0.39646997458,
      "times": [
        0.39646997458
      ],
      "exit_codes": [
        0
      ],
      "parameters": {
        "filename": "/samples/Prolog/dleak-report"
      }
    },
    {
      "command": "github-linguist --json '/samples/Prolog/plunit_test_example.plt' > /results/tmp_file",
      "mean": 0.40772620558,
      "stddev": null,
      "median": 0.40772620558,
      "user": 0.36764456,
      "system": 0.03987772,
      "min": 0.40772620558,
      "max": 0.40772620558,
      "times": [
        0.40772620558
      ],
      "exit_codes": [
        0
      ],
      "parameters": {
        "filename": "/samples/Prolog/plunit_test_example.plt"
      }
    },
    {
      "command": "github-linguist --json '/samples/Prolog/logic-problem.pro' > /results/tmp_file",
      "mean": 0.40617827458,
      "stddev": null,
      "median": 0.40617827458,
      "user": 0.38222656,
      "system": 0.023823719999999996,
      "min": 0.40617827458,
      "max": 0.40617827458,
      "times": [
        0.40617827458
      ],
      "exit_codes": [
        0
      ],
      "parameters": {
        "filename": "/samples/Prolog/logic-problem.pro"
      }
    }
  ]
}
```

With numerous speed-related metrics, namely the time that it required to analyze the file in question.

## Analysis
With these benchmark results of accuracy and speed, we are able to analyze the results. Using Pandas data frames and NumPy, we produce numerous analyses in the realm of accuracy and speed.

### Accuracy analyses
Amongst several analyses, we produce the
- Success count per language
- Success rate per language
- List of discrepancy files 
- Final accuracy statistics

Finally, we produce a graphs, visually representing the general accuracy of the utility.

![Accuracy plot for Linguist utility run on Linguist 3039 sample files](https://raw.githubusercontent.com/JacobKohav/llm-programming-language-detection/refs/heads/main/analysis/01_utils/hw-unspecified/individual/analysis_linguist_2025-07JUL-16_07h39m52s--UTC/accuracy_with_database_syntax_comparator/accuracy_with_database_syntax_comparator-plot.png)

### Speed analyses
In this analysis, we produce the
- execution time per file
- execution time per programming language

Likewise, we produce a graph, visually representing general speed of the utility.

![Accuracy plot for Linguist utility run on Linguist 3039 sample files](https://raw.githubusercontent.com/JacobKohav/llm-programming-language-detection/refs/heads/main/analysis/01_utils/hw-unspecified/individual/analysis_linguist_2025-07JUL-16_07h39m52s--UTC/tool_execution_time_per_file/tool_execution_time_per_file-plot.png)

A full example directory of a full analysis can be found [here](https://github.com/JacobKohav/llm-programming-language-detection/tree/main/analysis/01_utils/hw-unspecified/individual/analysis_linguist_2025-07JUL-16_07h39m52s--UTC).

## Conclusion
Having discussed the result of the programming language identification benchmarking and the analysis format, we'll discuss initial results of programming, language, identification, benchmarking in the next post.