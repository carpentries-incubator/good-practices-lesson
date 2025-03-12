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
- in-code documentation (comments and docstrings)
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

### Badges
Badges are a way to quickly show the status of a project: is it building, is it tested, what is the license?
You typically find them on top of the README file:

![Badges on top of a Readme file](fig/documentation-badges.png).

::: challenge
### Exercise README: 
#### Draft or improve a README for one of your recent projects (in breakout rooms)

Try to draft a brief README or review a README which you have written for one of your projects.
You can work individually, but you could also discuss whether anything can be improved on your neighbour's README file(s).
Think about the user (which can be a future you) of your project, what does this user need to know to use or contribute to the project? And how do you make your project attractive to use or contribute to?

#### Add a badge
Add a badge to your README file. This comes down to simply adding a link to an image on top of your README file.

You can pick from:

- [A simple static badge](https://shields.io/badges). You can decide what it says and what color it is.
- [The howfairis badge](https://app.howfairis.com). It indicates whether a project is in line with the 
[FAIR software recommendations.](https://fair-software.eu/)
- [A badge reporting test coverage](https://coveralls.io/) (we will discuss testing and continuous integration in upcoming episodes)
- [A badge linking to a publication in Zenodo](https://tutorials.inbo.be/tutorials/git_zenodo/)
- [A badge showing the license](https://gist.github.com/lukas-h/2a5d00690736b4c3a7ba)

#### (optional) Make your writing bold and clear
Try the https://hemingwayapp.com/ to analyse your README file and make your writing bold and clear.

:::



### Citation
It is easy to correctly cite a paper: all the necessary information (metadata) can be found on the title page or the article website. 

Software and datasets have no title page, the relevant information is often less obvious. To get credit for your work, you should provide citation information for your software. 

A good way to add citation information is by including a [CITATION.cff](https://citation-file-format.github.io/) file (Citation File Format) in the root of your repository. This plain text file, written in YAML format, contains all the necessary citation details in a structured manner. 

Platforms like GitHub, Zenodo, and Zotero reuse the citation metadata you provide. GitHub, for example, automatically renders the file on the repository landing page and provides a BibTeX snippet which users can simply copy! 

#### Minimal example for a CITATION.cff file

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

You can use the [cffinit](https://citation-file-format.github.io/cff-initializer-javascript/) tool to create a citation file. 

:::challenge
### Exercise: Create a CITATION.cff using cffinit
1. Follow [these steps to create a CITATION file with cffinit](https://book.the-turing-way.org/communication/citable/citable-cffinit).
1. Rename the created file to `CITATION.cff` and add it to the root folder of your repository.
1. Push your changes to `main` and check your repository in GitHub. What has happened?

:::

## In-code documentation 

In-code documentation makes code more understandable and explains decisions we made.

### When not to use:
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

## Exercise: Writing good in-code comments

Let's take a look at two example comments:

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

Comment B is the correct choice!

+ **Comment A** describes **what** happens in this piece of code. This can be
    useful for somebody who has never seen Python or a program, but for somebody
    who has, it can feel like a redundant commentary.
+ **Comment B** is probably more useful as it describes **why** this piece of code
    is there, i.e. its **purpose**.

:::::::::::::::::::::::::


::::::::::::::::::::::::::::::::::::::::::::::::::

### What are "docstrings" and how can they be useful?

Docstrings are a special kind of comment that are used to document functions, classes and modules. Here is function `fahrenheit_to_celsius` which converts temperature in
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

```python
def fahrenheit_to_celsius(temp_f: float) -> float:
    """
    Converts a temperature in Fahrenheit to Celsius.

    Args:
        temp_f: The temperature in Fahrenheit.

    Returns:
        The temperature in Celsius.
    """

    temp_c = (temp_f - 32.0) * (5.0/9.0)
    return temp_c
```

Unlike regular comments, docstrings are stored as an attribute (`__doc__`) of the object they document and can be extracted programmatically. 

Docstrings are more powerful than comments:

- Docstrings are automatically extracted when calling the `help` function.
- Tools (e.g. `mkdocs`, `sphinx`) can generate documentation pages automatically from docstrings known as API documentation.

A good docstring should describe:

- What the function does
- What goes in (including the type of the input variables)
- What goes out (including the return type)

There are different docstrings styles, such as Google style, numpy style and reStructered style, with Google style being the most common. 
See documentation [here](https://google.github.io/styleguide/pyguide.html#doc-function-args) for more information.

::::::::::::::::::::::::::::::::::::: challenge 
## Exercise: Identify a proper docstring

Which of the following options is the correct function with a proper docstring?

**Option A**

```python
def check_unit_validity(unit: str) -> bool:
    """
    Checks if a unit is valid.

    Args:
        unit: The unit to check. Must be "C", "F", or "K".

    Returns:
        True if the unit is valid, False otherwise.
    """
    if not unit in ["C", "F", "K"]:
        return False
    return True
```

**Option B**

```python
def check_unit_validity(unit):
    """
    Checks if a unit is valid.

    Args:
        unit (str): The unit to check. Must be "C", "F", or "K".

    Returns:
        bool: True if the unit is valid, False otherwise.
    """
    if not unit in ["C", "F", "K"]:
        return False
    return True
```

**Option C**

```python
def check_unit_validity(unit: str) -> bool:
    """
    Validates the unit.

    Parameters:
        unit (str): The unit to check.

    Returns:
        bool: True if the unit is valid, False otherwise.
    """
    if not unit in ["C", "F", "K"]:
        return False
    return True
```

:::::::::::::::::::::::: solution 

## Solution
Option A and B are both correct choices! 

- **Option A**: The docstring is detailed. It does not require types (str, bool) since they are already specified in the function signature.
- **Option B**: The docstring is detailed and includes descriptions of the arguments and return type since they are not specified in the function signature.
- **Option C**: The docstring is missing the specific valid units ("C", "F", "K") in the description of the unit parameter, making it less informative.

:::::::::::::::::::::::: 

::::::::::::::::::::::::::::::::::::: 


## Tools for generating and deploying documentation
You can use the following tools to generate user or API documentation.

### Tools for generating documentation 

MkDocs and Sphinx:

- create nicely-formatted HTML pages out of .md or .rST files
- programming language independent

#### MkDocs

::: challenge
### Exercise: Generate MkDocs documentation

Before we start generating documentation, make sure that you have installed mkdocs:

```bash
conda list mkdocs
```

Now, Lets create a new MkDocs project in the current project directory which contains the temperature conversion code: 

```bash
# In temperature-conversion
mkdocs new .    
```
```output
INFO    -  Writing config file: ./mkdocs.yml
INFO    -  Writing initial docs: ./docs/index.md
```

This command creates a new MkDocs project in the current directory with a `docs` folder containing an `index.md` file 
and a `mkdocs.yml` configuration file in the root of our project.

Now, let's fill in the `mkdocs.yml` configuration file for our project.

```yaml
site_name: Temperature Conversion Documentation
use_directory_urls: false
theme:
  name: "material"
font: false
nav:
  - Temperature Conversion Documentation: index.md

plugins:
  - mkdocstrings
```

Now that we have a basic structure for our docs, we can build them!

```bash
mkdocs build
```
Then we can view these locally with:

```bash
mkdocs serve
```

::: 

#### Sphinx
Like MkDocs, Sphinx is a documetatation generator which translates a set of plain text source files into various output formats. It natively supports reStructuredText (rST) and with some extensions also supports Markdown.

::: instructor

Please note that writing documentation using Sphinx is an optional part in this workshop. For some learners it is enough to know that Sphinx exists, but it is overkill for their current projects. Other learners really want to learn Sphinx and can benefit from it.  In practice, teaching Sphinx can be hard, since the ReStructuredText is quite error-prone when it comes to the right indentation, number of empty lines etcetera. It is up to you if and how you want to include this section when teaching this episode.

:::

:::::::::::::::::::::::::::::::::::::::  spoiler

##### Sphinx quickstart demo and optional exercises

Create a directory for the example documentation, step into it, and inside
generate the basic documentation template:

```console
$ mkdir doc-example
$ cd doc-example
$ sphinx-quickstart
```

The quickstart utility will ask you some questions. For this exercise, you can go
with the default answers except to specify a project name, author name, and project release:

```
> Separate source and build directories (y/n) [n]: <hit enter>
> Project name: <your project name>
> Author name(s): <your name>
> Project release []: 0.1
> Project language [en]: <hit enter>
```

A couple of files and directories are created:

| File/directory | Contents |
| -------------- | -------- |
| conf.py        | Documentation configuration file |
| index.rst      | Main file in Sphinx |
| _build/        | Directory where docs are built (you can decide the name) |
| _templates/    | Your own HTML templates |
| _static/       | Static files (images, styles, etc.) copied to output directory on build |
| Makefile       | Makefile to build documentation using make |
| make.bat       | Makefile to build documentation using make (Windows) |

`Makefile` and `make.bat` (for Windows) are build scripts that wrap the sphinx commands, but
we will be doing it explicitly.

Let's have a look at the `index.rst` file, which is the main file of your documentation:

```rst
.. myproject documentation master file, created by
   sphinx-quickstart on Sat Sep 23 17:35:26 2023.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to myproject's documentation!
=====================================

.. toctree::
   :maxdepth: 2
   :caption: Contents:


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
```

- We will not use the `Indices and tables` section now, so remove it and everything below.
- The top four lines, starting with `..`, are a comment.
- The next lines are the table of contents. We can add content below:

```rst
.. toctree::
   :maxdepth: 2
   :caption: Contents:

   some-feature.md
```
Note that `some-feature.md` needs to be indented to align with `:caption:`.

We now need to tell Sphinx to use markdown files. To do this, we open
`conf.py` and replace the line:
```python
extensions = []
```

with this line so that Sphinx can parse Markdown files:
```python
extensions = ['myst_parser']
```

Let's create the file `some-feature.md` (in Markdown format) which we have just listed in
`index.rst` (which uses reStructured Text format).

```md
# Some feature

## Subsection

Exciting documentation in here.
Let's make a list (empty surrounding lines required):

- item 1

  - nested item 1
  - nested item 2

- item 2
- item 3
```

We now build the site:

```console
$ ls -1

_static
_templates
conf.py
index.rst
make.bat
Makefile
some-feature.md

$ sphinx-build . _build

... lots of output ...
build succeeded.

The HTML pages are in _build.

$ ls -1 _build

_sources
_static
genindex.html
index.html
objects.inv
search.html
searchindex.js
some-feature.html
```

Now open the file `_build/index.html` in your browser.

- Linux users, type:
  ```console
  $ xdg-open _build/index.html
  ```
- macOS users, type:
  ```console
  $ open _build/index.htmlgit
  ```
- Windows users, type:
  ```console
  $ start _build/index.html
  ```
- If the above does not work:
  Enter `file:///home/user/doc-example/_build/index.html` in your browser (adapting the path to your case).

Hopefully you can now see a website. If so, then you are able to build Sphinx pages locally.
This is useful to check how things look before pushing changes to GitHub or elsewhere.

Note that you can change the styling by editing `conf.py` and changing the value `html_theme`
(for instance you can set it to `sphinx_rtd_theme` (if you have that Python package installed)
to have the Read the Docs look).



::: challenge

##### (Optional) exercise: Adding more Sphinx content

1. Add an entry below `some-feature.md` labeled `another-feature.md` (or a better name) to the `index.rst` file.
2. Create a file `another-feature.md` in the same directory as the `index.rst` file.
3. Add some content to `another-feature.md`, rebuild with `sphinx-build . _build`, and refresh the browser to look at the results.
4. Use the [MyST Typography](https://myst-parser.readthedocs.io/en/latest/syntax/typography.html) page as help.

Experiment with the following Markdown syntax:

- \*Emphasized text\* and \*\*bold text\*\*

- Headings:
```md
# Level 1

## Level 2

### Level 3

#### Level 4
```

- An image: `![alt text](image.png)`

- `[A link](https://www.example.org)`

- Numbered lists (numbers adjusted automatically):
```md
1. item 1
2. item 2
3. item 3
1. item 4
1. item 5
```

- Simple tables:
```md
| No.  |  Prime |
| ---- | ------ |
| 1    |  No    |
| 2    |  Yes   |
| 3    |  Yes   |
| 4    |  No    |
```

- Code blocks:
````markdown
The following is a Python code block:
```python
  def hello():
      print("Hello world")
```

And this is a C code block:
```c
#include <stdio.h>
int main()
{
    printf("Hello, World!");
    return 0;
}
```
````

- You could include an external file (here we assume a file called "example.py"
  exists; at the same time we highlight lines 2 and 3):
````markdown
```{literalinclude} example.py
:language: python
:emphasize-lines: 2-3
```
````

- We can also use Jupyter notebooks (*.ipynb) with Sphinx. It requires the
  [myst-nb](https://myst-nb.readthedocs.io/) extension to be installed.

:::

::: challenge

##### (Optional) exercise Adding Math equations


Math equations should work out of the box. In some older versions, you might need
to edit `conf.py` and add `sphinx.ext.mathjax`:
```python
extensions = ['myst_parser', 'sphinx.ext.mathjax']
```

Try this (result below):
````markdown
This creates an equation:
```{math}
a^2 + b^2 = c^2
```

This is an in-line equation, {math}`a^2 + b^2 = c^2`, embedded in text.
````

This creates an equation:
```{math}
a^2 + b^2 = c^2
```

This is an in-line equation, {math}`a^2 + b^2 = c^2`, embedded in text.
:::

::: challenge
##### (Optional) exercise: Adding API documentation

1. Write some docstrings in functions and/or class definitions of an `example` python module:
```python
def multiply(a: float, b: float) -> float:
    """
    Multiply two numbers.

    :param a: First number.
    :param b: Second number.
    :return: The product of a and b.
    """
    return a * b
```

2. In the file `conf.py` modify "extensions" and add 3 lines:
```python
extensions = ['myst_parser', "autodoc2"]

autodoc2_packages = [
    "multiply.py"
]
```

4. List `apidocs/index` in the toctree in `index.rst`.
```rst
.. toctree::
   :maxdepth: 2
   :caption: Contents:

   some-feature.md
   apidocs/index
```

5. Re-build the documentation and check the "API reference" section.

:::

:::::::::::::::::::::::::::::::::::::::  

### Deploying documentation using Github pages

- GitHub pages can be setup inside your GitHub repository
- It automatically deploys your Sphinx-generated documentation. Or in other words it creates a website for you that renders your documentation.

::: instructor
You can show the example documentation deployed on GitHub pages here: https://esciencecenter-digital-skills.github.io/good-practices-documentation-example/

Then, you can show that this content comes from simple markdown files, like: https://github.com/esciencecenter-digital-skills/good-practices-documentation-example/blob/main/doc/another-feature.md?plain=1

In addition, you can explain that with a few settings you can automatically generate documentation from docstrings. You can give https://nanopub.readthedocs.io/en/latest/reference/client.html as an example.

:::


:::::::::::::::::::::::::::::::::::::::: keypoints

- Depending on the purpose and state of the project documentation needs to meet different criteria.
- Good README files provide a good landing place for anyone that is new to your project.
- Comments should describe the why for your code not the what.
- Writing docstrings can be a good way to write documentation while you type
  code since it also makes it possible
  to query that information from outside the code or to auto-generate
  documentation pages.
- There are various tools for generating and deploying documentations which translate a set of plain text sources into various output formats.
::::::::::::::::::::::::::::::::::::::::::::::::::
