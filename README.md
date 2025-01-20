# Good practices in research software development
The key objective of this lesson is to grow researchers' software skills necessary to apply good practices
that enable open and reproducible research. 
The lesson focuses on building modular, reusable, maintainable, sustainable, reproducible, testable, and robust software. 
This will allow you to more easily organize, maintain and share your code. 

The main themes that are addressed are generically applicable, but please note that a lot of the exercises and demonstrations are in Python.

This lesson is heavily inspired by and based on the awesome [CodeRefinery training materials](https://coderefinery.org/lessons/).
It originated from teaching many workshops using bits and pieces from the CodeRefinery materials 
that went through many cycles of improvement, but became a complicated set of pointers to other materials, making it hard to teach by new instructors. 
At some point there was a need for One Holy Source of Lesson Material to teach a 1-day Good practices in research software development workshop.

## How does this lesson relate to Intermediate research software development?
This lesson is more an introduction to good practices in research software development for researchers that are relatively unexperienced in programming.
If you find the topics that are covered in this lesson too basic, you could consider the [Intermediate Research Software Development](https://carpentries-incubator.github.io/python-intermediate-development/) lesson.
That lesson has a similar focus, but also teaches more intermediate topics like software architecture, advanced coding best practices, 
Integrated Software Development environments and is targeted to slightly more advanced research software engineers. 

## Teaching this lesson?
Do you want to teach Good practices in research software development? This material is open-source and freely available. 
Are you planning on using our material in your teaching? 
We would love to help you prepare to teach the lesson and receive feedback on how it could be further improved, based on your experience in the workshop.

You can notify us that you plan to teach this lesson by creating an issue in this repository. 

Also, it would be great if you can update [this overview of all workshops taught with this lesson material](workshops.md). 
This helps us show the impact of developing open-source lessons to our funders.

## Target Audience
It is assumed that participants already write code for their research, but no expertise is required.
Basic Git and GitHub knowledge is required. The lesson is typically taught as day 2 in a 2-day workshop, 
after a first day in which [Collaborative version control with Git and GitHub](https://carpentries-incubator.github.io/collaborative-git-and-github-lesson/) is taught.
Some experience in navigating file trees and editing files in a terminal session, as well as basic knowledge of Python programming is recommended.

## Lesson development sprints
We regularly host lesson development sprints, in which we work together at the lesson.
Send an email to o.lyashevska@esciencecenter.nl if you want to get involved.

## Contributing

We welcome all contributions to improve the lesson! Maintainers will do their best to help you
if you have any questions, concerns, or experience any difficulties along the way.

We'd like to ask you to familiarize yourself with our [Contribution Guide](CONTRIBUTING.md) and
have a look at the [more detailed guidelines][lesson-example] on proper formatting, ways to
render the lesson locally, and even how to write new episodes.

Please see the current list of
[issues](https://github.com/esciencecenter-digital-skills/good-practices-lesson/issues)
for ideas for contributing to this repository.

For making your contribution, we use the GitHub flow, which is nicely explained in the
chapter [Contributing to a Project](http://git-scm.com/book/en/v2/GitHub-Contributing-to-a-Project)
in Pro Git by Scott Chacon.
Look for the tag ![good_first_issue](https://img.shields.io/badge/-good%20first%20issue-gold.svg).
This indicates that the maintainers will welcome a pull request fixing this issue.

## Setup the Lesson Website locally

To build this lesson locally, you should follow the [setup instructions for the
workbench](https://carpentries.github.io/sandpaper-docs/#overview). In short,
make sure you have R, Git, and Pandoc installed, open R and use the following
commands to install/update the packages needed for the infrastructure:

```r
# register the repositories for The Carpentries and CRAN
options(repos = c(
  carpentries = "https://carpentries.r-universe.dev/",
  CRAN = "https://cran.rstudio.com/"
))

# Install the template packages to your R library
install.packages(c("sandpaper", "varnish", "pegboard", "tinkr"))
```

## Rendering the website locally

See the [Carpentries Workbench usage instructions](https://carpentries.github.io/workbench/#usage) on how to render the website locally.

