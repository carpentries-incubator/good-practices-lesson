---
title: Document your research software
teaching: 25
exercises: 30
---

::::::::::::::::::::::::::::::::::::::: objectives

- Know what makes a good documentation
- Know how to document your project and get credit for your work 
- Learn what docstrings are and how to use them
- Learn what tools can be used for generating documentation
- Implement MkDocs to generate comprehensive project documentation


::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- What different types of documentation are there?
- How to help others to use your project?
- What are docstrings and what information should go into docstrings?
- What different tools exist for generating documentation?


::::::::::::::::::::::::::::::::::::::::::::::::::

:::instructor
Use [these slides](https://esciencecenter-digital-skills.github.io/digital-skills-slides/modules/good-practices-lesson/documentation-slides) as
a guidance.

The main purpose of this lesson is to make sure participants understand that DOCUMENTATION IS IMPORTANT. The goal is more to trigger participants then to teach them all the different ways one could document a project. It is good to communicate this (and that this will give more time for the other parts of the workshop).

:::

## Why we teach this lesson

Specific motivations:

- Code documentation should be part of your source code so that it remains easily accessible and maintainable for all users.
- Good documentation allows others to install and make use of your code independently and increase the impact of your project.
- Documentation can facilitate collaborations by helping us onboard new project members quickly and more easily.
- By writing documention you think about the design of your code.



## What makes a good documentation?

::: challenge
### Exercise: Think of good and bad examples 
Write down your thoughts in the collaborative documents.
Respond with emojis :+1: :scream_cat: to your colleagues' answers.
- Think of projects of which you like the documentation. What do you like about them?
- Think of projects for which you don’t like the documentation. What don’t you like about them? Are you missing anything?

**NB: You can choose a mature library with lots of users for this exercise, but try to also think of less mature projects you had to collaborate on, or papers you had to reproduce.**

:::: solution
- It is important to document code
- Think about the people reading your documentation (your audience)
- Depending on the purpose and state of the project documentation needs to meet different criteria. 
- For most scientific projects, in-code documentation and a well thought out README file is enough.
- Documentation should be tracked with corresponding code
::::
:::

## Types of documentation
There are different types of documentation:

- README and CITATION files
- in-code documentation (Docstrings)
- Tutorials


## Writing good README files
The README file is the first thing a user/collaborator sees. It should include:

- A descriptive project title
- Motivation (why the project exists)
- How to setup
- Copy-pastable quick start code example
- Link or instructions for contributing
- Badges
- Citation 


::: challenge
### Exercise README: Draft or improve a README for one of your recent projects (in breakout rooms)

Try to draft a brief README or review a README which you have written for one of your projects.

You can work individually, but you could also discuss whether anything can be improved on your neighbour's README file(s).

Think about the user (which can be a future you) of your project, what does this user need to know to use or contribute to the project? And how do you make your project attractive to use or contribute to?

(Optional): Try the https://hemingwayapp.com/ to analyse your README file and make your writing bold and clear.
:::

### Badges
TODO: What they are, suggest zenodo, pytest, code coverage, documentation, licence.
Link to shields.io

### Citation
- It is very easy to correctly cite a paper: all the necessary information (metadata) can be found on the title page or the article website. Software and datasets have no title page, the relevant information is often less obvious.
- To get credit for your work, you should provide citation information for your software. 
- One way to do this is by including a [CITATION.cff](https://citation-file-format.github.io/) file (Citation File Format) in the root of your repository. This plain text file, written in YAML format, contains all the necessary citation details in a structured manner. 
- Platforms like GitHub, Zenodo, and Zotero reuse the citation metadata you provide. GitHub, for example, automatically renders file on the repository landing page and provide BibTeX snippet which users can simply copy! 

#### Minimal example

```yaml
authors:
  - family-names: Doe
    given-names: John
cff-version: 1.2.0
message: "If you use this software, please cite it using the metadata from this file."
title: "My research software"
```
We can also include other important information of software such as version, release date, DOI, license, keywords.

#### How to create a CITATION.cff file?

You can use [cffinit](https://citation-file-format.github.io/cff-initializer-javascript/) tool to create citation file. 

:::challenge
### Exercise: Create a CITATION.cff using cffinit
1. Follow [these](https://book.the-turing-way.org/communication/citable/citable-cffinit) steps to create a CITATION file with cffinit.
1. Give this file CITATION.cff name and add it to the root folder of your repository.
1. What has happened?.

:::

## In-code documentation 

Documentation strings:
- Makes code more understandable
- Explains decisions we made

### When not to use in-code documentation:
- When the code is self-explanatory
- To replace good variable/function names
- To replace version control
- To keep old (zombie) code around

### Readable code vs commented code
```python
# convert from degrees celsius to fahrenheit
def convert(d):
    return d * 5 / 9 + 32
```

vs

```python
def celsius_to_fahrenheit(degrees):
    return degrees * 5 / 9 + 32
```


:::::::::::::::::::::::::::::::::::::::  challenge

## Writing good comments - In-code-1: Comments

Let's take a look at two example comments (comments in Python start with `#`):

**Comment A**

```python
  # now we check if temperature is below -50
  if temperature < -50:
      print("ERROR: temperature is too low")
```

**Comment B**

```python
  # we regard temperatures below -50 degrees as measurement errors
  if temperature < -50:
      print("ERROR: temperature is too low")
```

**Which of these comments is more useful? Can you explain why?**

:::::::::::::::  solution

## Solution

+ **Comment A** describes **what** happens in this piece of code. This can be
    useful for somebody who has never seen Python or a program, but for somebody
    who has, it can feel like a redundant commentary.
+ **Comment B** is probably more useful as it describes **why** this piece of code
    is there, i.e. its **purpose**.

:::::::::::::::::::::::::


::::::::::::::::::::::::::::::::::::::::::::::::::

### What are "docstrings" and how can they be useful?

Here is function `fahrenheit_to_celsius` which converts temperature in
Fahrenheit to Celsius.

The first set of examples uses **regular comments**:

```python
# This function converts a temperature in Fahrenheit to Celsius.
def fahrenheit_to_celsius(temp_f: float) -> float:
    temp_c = (temp_f - 32.0) * (5.0/9.0)
    return temp_c
```

The second set uses **docstrings or similar concepts**. Please compare the two
(above and below):

```py
def fahrenheit_to_celsius(temp_f: float) -> float:
    """
    Converts a temperature in Fahrenheit to Celsius.

    Parameters
    ----------
    temp_f : float
        The temperature in Fahrenheit.

    Returns
    -------
    float
        The temperature in Celsius.
    """

    temp_c = (temp_f - 32.0) * (5.0/9.0)
    return temp_c
```

Docstrings are more powerful than comments:

- Docstrings are automatically extracted when calling the help function.
- Tools can generate documentation pages automatically from docstrings known as API documentation.

It is common to write docstrings for functions, classes, and modules.

TODO: Introduce how to write docstrings and show an example of API documentation.
Good docstrings describe:
- What the function does
- What goes in (including the type of the input variables)
- What goes out (including the return type)


**Naming is documentation**:
Giving explicit, descriptive names to your code segments (functions, classes,
variables) already provides very useful and important documentation. In
practice you will find that for simple functions it is unnecessary to add a
docstring when the function name and variable names already give enough
information.

TODO: Add docstring exercise. 
Idea add docstrings to convertion function and improve naming.


## Tools for generating and deploying documentation
You can use the following tools to generate user or API documentation.

### Generating documentation 

MkDocs and Sphinx:
- creates nicely-formatted HTML pages out of .md or .rst files
- programming language independent

### Deploying documentation using Github pages

- set up inside your GitHub repository
- automatically deploys your Sphinx-generated documentation

TODO: add lesson materials and exercise for generating documentation with MkDocs
TODO: add lesson materials and optional exercise for generating documentation with Sphinx


::: instructor
You can show the example documentation deployed on GitHub pages here: https://esciencecenter-digital-skills.github.io/good-practices-documentation-example/

Then, you can show that this content comes from simple markdown files, like: https://github.com/esciencecenter-digital-skills/good-practices-documentation-example/blob/main/doc/another-feature.md?plain=1

In addition, you can explain that with a few settings you can automatically generate documentation from docstrings. You can give https://nanopub.readthedocs.io/en/latest/reference/client.html as an example.

:::


:::::::::::::::::::::::::::::::::::::::: keypoints

- Depending on the purpose and state of the project documentation needs to meet different criteria.
- Good README files provide a good landing place for anyone that is new to your project
- Comments should describe the why for your code not the what.
- Writing docstrings can be a good way to write documentation while you type
  code since it also makes it possible
  to query that information from outside the code or to auto-generate
  documentation pages.
::::::::::::::::::::::::::::::::::::::::::::::::::
