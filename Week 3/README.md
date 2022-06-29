`Week 3` Reproducible Research
================

-   👨🏻‍💻 Author: Anderson H Uyekita
-   📚 Specialization: <a
    href="https://www.coursera.org/specializations/data-science-foundations-r"
    target="_blank" rel="noopener">Data Science: Foundations using R
    Specialization</a>
-   📖 Course:
    <a href="https://www.coursera.org/learn/reproducible-research"
    target="_blank" rel="noopener">Reproducible Research</a>
    -   🧑‍🏫 Instructor: Roger D Peng
-   📆 Week 3
    -   🚦 Start: Tuesday, 28 June 2022
    -   🏁 Finish: Wednesday, 29 June 2022

------------------------------------------------------------------------

#### Assignments & Deliverables

-   This week there is no 📝 Quiz

------------------------------------------------------------------------

#### Slides

-   Lesson 1: Communicating Results <a href="" id="lesson-1"></a>
    -   [Specifying Levels of
        Details](./slides/3_1_levels-of-detail.pdf)
-   Lesson 2: RPubs <a href="" id="lesson-2"></a>
-   Lesson 3: Reproducible Research Checklist
    <a href="" id="lesson-3"></a>
    -   [What to Do and What Not to Do](./slides/3_3_checklist.pdf)
-   Lesson 4: Evidence-based Data Analysis <a href="" id="lesson-4"></a>
    -   [Evidence based data
        analysis](./slides/3_4_evidence-based-data-analysis.pdf)

------------------------------------------------------------------------

#### Description

> This week covers what one could call a basic check list for ensuring
> that a data analysis is reproducible. While it’s not absolutely
> sufficient to follow the check list, it provides a necessary minimum
> standard that would be applicable to almost any area of analysis.

------------------------------------------------------------------------

## Class Notes

### [<kbd>Lesson 1</kbd>](#lesson-1) Communicating Results

**tl;tr**

-   People are busy, especially managers and leaders
-   Results of data analyses are sometimes presented in oral form, but
    often the first cut is presented via email
-   It is often useful to breakdown the results of an analysis into
    different levels of granularity / detail

### [<kbd>Lesson 2</kbd>](#lesson-2) RPubs

-   <https://rpubs.com>

### [<kbd>Lesson 3</kbd>](#lesson-3) Reproducible Research Checklist

**Summary**

-   Are we doing good science?
-   Was any part of this analysis done by hand?
    -   If so, are those parts precisely document?
    -   Does the documentation match reality?
-   Have we taught a computer to do as much as possible (i.e. coded)?
    -   `download.file()`
-   Are we using a version control system?
    -   `Github`
-   Have we documented our software environment?
    -   `sessinInfo()`
    -   `set.seed()`
-   Have we saved any output that we cannot reconstruct from original
    data + code?
-   How far back in the analysis pipeline can we go before our results
    are no longer (automatically) reproducible?

### [<kbd>Lesson 4</kbd>](#lesson-4) Evidence-based Data Analysis

**Replication**

-   Focuses on **the validity of the scientific claim**
-   “Is this claim true?”
-   The ultimate standard for strengthening scientific evidence
-   **New investigators, data, analytical methods, laboratories,
    instruments, etc.**
-   Particularly important in studies that can impact broad policy or
    regulatory decisions

**Reproducibility**

-   Focuses on **the validity of the data analysis**
-   “Can we trust this analysis?”
-   Arguably a minimum standard for any scientific study
-   New investigators, same data, same methods
-   Important when replication is impossible

**Summary**

-   Reproducible research is important, but does not necessarily solve
    the critical question of whether a data analysis is trustworthy
-   Reproducible research focuses on the most “downstream” aspect of
    research dissemination
-   Evidence-based data analysis would provide standardized, best
    practices for given scientific areas and questions
-   Gives reviewers an important tool without dramatically increasing
    the burden on them
-   More effort should be put into improving the quality of “upstream”
    aspects of scientific research
