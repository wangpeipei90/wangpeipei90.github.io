* [Why Aren't Regular Expressions a Lingua Franca?](#regexlinguafranca) FSE'19
* [Understanding real-world concurrency bugs in Go](#concurrencybugstudygo) ASPLOS'19
* [Analyzing and Supporting Adaptation of Online Code Examples](#onlinecodeadaptation) ICSE'19
* [Replication Can Improve Prior Results: A GitHub Study of Pull Request Acceptance](#pr_acceptance) ICPC'19
* [Software engineering for machine learning: a case study](#seForml) ICSE SEIP'19
* [Simple fast algorithms for the edit distance between trees and related problems](#TreeDistance) SIAM J. Comput. 1989
* [Findings from GitHub: Methods, Datasets and Limitations](#GithubStudy) MSR 2016

<a name="seForml"></a>
Title: Software engineering for machine learning: a case study

The research paper from ICSE this paper talking about challenges in SE for ML.

This paper is a study on observing software teams in Microsoft as they develop AI-based applications. 
From my perspective, this paper put forward three challenges in SE for AI applications: 1) data management and versioning; 2) model customization and reusability; 3) AI-based application debugging. The root cause I think for these challenges is the non-linear ML workflows (hidden feedback loops).  Thus, models are entangled (no clean boundaries) and errors are propagated nonmonotonically.

Another statement this paper claim is the three different roles in AI-based application development: domain expert; modeler; platform builder.  The experience levels of AI development meet different challenges. For example, education and training are important to those with low experience levels but are less important to medium or high levels.

<a name="pr_acceptance"></a>
# Replication Can Improve Prior Results: A GitHub Study of Pull Request Acceptance
Title: Replication Can Improve Prior Results: A GitHub Study of Pull Request Acceptance ICPC'19

Jack Chen's paper on ICPC 19. Although the paper talks mainly about replicating qualitative research results with crowdsourcing, I checked the study because it is related to pull request acceptance. 

My goal of this paper is the factors influencing GitHub Pull Request acceptance, which I may use to study my sampled unmerged PRs. The reason for my 64 rejected sampled PRs can be divided into 1) disapproval of the question 2) disapproval of the solution 3) suggestion of alternate solutions. Maybe the number of discussion and code reviews and the role of the submitter and other participants can also shed lights on similar PRs being rejected or accepted.

<a name="regexlinguafranca"></a>
# Why Aren't Regular Expressions a Lingua Franca?
Title: Why Aren't Regular Expressions a Lingua Franca? An Empirical Study on the Re-use and Portability of Regular Expressions 

Lingua Franca means "common language" or "universal language". 

This is a paper on reusing regular expression across different program languages. It starts with a survey of 158 developers. The survey shows that most developers copy paste regular expressions and 47% of them do it without considering the programming language. 
Thus it constructs a regex corpus with over 5 million regexes to evaluate its re-use and measure the semantic and performance portability problems. 

The conclusion is what I have expected. But there are some details different from what we usually do. 
1) definition of re-use----------not based on the string/behavioral similarity, but identical regexes which are at least 15 characters long
2) differences among languages with the same regex notation at 3 levels-----is/is not a feature, different features, subtly different behaviors. (See Table 4, and 3 types of witnesses in Table 3)
-------we may use them as the classification for bugs across languages.
3) The performance differences across languages are caused by regex engine implementation: Thompson's algorithm (grep), Spencer's algorithm Medium and Spencer's algorithm Slow. 

<a name="TreeDistance"></a>
# Simple fast algorithms for the edit distance between trees and related problems
Title: Simple fast algorithms for the edit distance between trees and related problems

A research paper which shed light on comparing similarities of regular expression syntax trees. (Accidentally I found this topic from a poster on the 2nd floor of EBII) 

This paper describes how one tree is changed to be the same as the other and a fast parallel algorithm to calculate it. Most importantly, it defines edit operations in order to calculate the tree edit distances. From a certain point, these edit operations provide us some backgrounds on mutating regexes. 

Besides the edit distance between ordered labeled trees might be a better idea than just comparing the extracted regex vectors of 34 features. Tree edit distances are harder to calculate than string edit distances, but there are several implementations of this algorithm in the GitHub now. So next time we can just use it when we need similarity measures of the regex 

<a name="ConcurrencyBugStudyGo"></a>
# Understanding real-world concurrency bugs in Go
Title: Understanding real-world concurrency bugs in Go

Authors: Tengfei Tu, Xiaoyu Liu, Linhai Song, and Yiying Zhang

The paper is a bug study on the specific bug (concurrency bug) in all Go projects. Go language is built for concurrency. It is interesting that this paper tries to verify if Go helps concurrency or not.

Gains from the paper:
1) Bug collection: handpick popular GitHub projects; collected commits by keywords, random sampling and manually identifying concurrency bugs---similar to ours
2) Bug taxonomy. It uses two orthogonal dimensions: causes/behaviors; in each behavior, the causes are again divided. -------It looks unbelievable to me that the classification is so neat and have no overlaps. 
3) Study bug fixes: add/change/remove + move + miscellaneous; It evaluates the correlation between fix strategies and the divided causes--------the bug fix only calculate the concurrency primitives, I guess
4) The authors also reproduce the bugs and evaluate how capable existing concurrency tools to detect these bugs--------will probably do something similar after bug taxonomy is finished
5) The bug lifetime calculation starts from when the bug is introduced to when the patch is committed. In other words, use "git blame" 
6) Tables are clean, especially when displaying two comparative categories. Figure 4 good to learn as well. 
7) The correlation uses a different formula, it is none of Pearson, Spearman, Kendal, use method P(AB)/P(A)P(B)---not sure why it chose this formula

<a name="OnlineCodeAdaptation"></a>
# Analyzing and Supporting Adaptation of Online Code Examples
Title: Analyzing and Supporting Adaptation of Online Code Examples 

Authors: Tianyi Zhang, Di Yang, Crista Lopes, Miryung Kim

Thoughts: The main contribution of this paper is the taxonomy of adaption types from StackOverflow examples to GitHub code snippets. 

Gains:
1) The process of making the taxonomy is very clear (qualitative analysis): a) first 90 examples and found convergent types, and then stop at 200; b) random sampling; c) joint work---two authors do the initial labeling and the other two joined later for refining taxonomy
2) Automated categorization: a) rules are inferred; b) validation manually
3) The figure types are better than boxplots (Figure 2).
Questions:
1) is "API misuse" same as "API usage violations"?
2) Is it a good way to show distribution statistics and then describe only mean and median in text, especially Figure 1?
3) Should we use "median" or "mean"  when trying to describe a tendency or correlation? Figure 2 uses "median" 

<a name="GithubStudy"></a>
# Findings from GitHub: Methods, Datasets and Limitations
Title: Findings from GitHub: Methods, Datasets and Limitations

Authors: Valerio Cosentino, Izquierdo Javier Luis Canovas, Jordi Cabot

A research paper (short) studying the latest research on mining GitHub repositories, one of the papers I found while searching for how PRs are studied.

Thoughts:

This paper is a study of GitHub studies, focusing on research papers published from 2010 to 2015 and then reporting statistics of 1) empirical methods employed 2) dataset used and 3) limitations

One of the interesting points is on the sampling techniques employed. Around 2/3 of sampled papers use non-probability sampling (or handpicking). And this is one major factor impacting generalization of results.  
Another point is that most papers chose GHTorrent mirroring GitHub data and only around 13% of selected papers use GitHub search API. As this paper said in the discussion, there is actually a trade-off between limited fresh uncurated data and the curated but outdated data.  Most of the papers use less than 100 projects in their studies, some even less than 50.  So I guess 50 projects would be a proper number in our study.
This paper also mentions the lack of longitudinal studies in the studied papers, a study concerns the same observation over a long period of time. This is true and will be a new point of view if we can somehow apply it.
