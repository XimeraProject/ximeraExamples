Current Status: **Alpha**. 
This repo is still being built and rebuilt as we develop a solid testing bed for Ximera.

# Purpose/content
This repo contains tests for Ximera development, 
and thus also contains basic, advanced and border usecases for the Ximera commands, environments, etc. 

For a user friendly overview of Ximera  refer to the [Ximera User Manual](https://github.com/XimeraProject/ximeraManuals/releases).


The content of  this repo is published at:

 * [KU Leuven](https://set-p-dsb-zomercursus-latest.cloud-ext.icts.kuleuven.be/ximeraexamples/coreXimeraFeatures/environments/theoremEnvironments).
 * [OSU](https://ximera.osu.edu/ximeraexamples).
 * [UF](https://test.xronos.clas.ufl.edu/ximeraExamples) (Link still pending - dummy link entered)
Note you can always get the TeX-code by appending .tex to the URL of an activity.


## Vocabulary:
**This repo uses the following terminology**
1) ``elements`` refers to LaTeX commands, environments, macros, etc that are defined in a specific dtx file.
    e.g. the ``problem``, ``question``, ``exploration``, and ``exercise`` are all environments
    defined in the problem.dtx file. These would collectively be called ``elements of problem.dtx``.
2) ``touched`` refers to commands, environments, macros, etc that are: defined, redefined, or otherwise
    changed in a specific dtx file. For example, the command outcomes dtx file has a number of styling
    commands and hooks that are likely to be used in other dtx files for default styling. Wherever these
    commands/hooks are (re)defined in the dtx content other than the outcomes.dtx, we would say that
    the outcome commands are ``touched`` by that dtx file (e.g. in options due to class options).

## Quick Structure Outline

- `dtxTests` for tests-per-Ximera-dtx-source-file, with subfolders
    - `Deprecated` for content that is being removed in a future release, see README in folder
    - `Hardcoded` for content that is not testable, like macros. Included so we can easily verify all dtx files are accounted for.
    - `(DTXFileName)` subfolder for each `(DTXFileName).dtx`, with
        - ``(DTXFileName).tex file`` (e.g. problem.tex) which contains the most basic tests for the dtx file content.
        - ``(Additional Testing Feature).tex`` (e.g. ``nesting.tex`` or ``numbering.tex`` in the `problem` folder).
        - ``(dtxFileName)Test.tex`` is the xourse that tests (dtxFileName) dtx file.
- `compositeTests`  folder for tests of interactions between different dtx file contents, see README in folder.
    - `(composite Test)` folder named for composite testing case.
        - ``(composite Test)Xourse.tex`` (xourse for the composite test - may also load tests from dtxTests folder).
        - ``variousdtxTests.tex`` (test files for the composite test - should be named for the individual elements of test when possible e.g. ``refToProblemLabel.tex`` and/or ``refToTheoremLabel.tex``)        
- `savedArchive` contains old test files/content not in current use.
    - `Templates` contains templates for adding new files.

The repo also has following base Ximera folders and files:
- `.devcontainer` folder for devcontain er/Codespace setup, with
    - ``docker-compose.yml`` for the images of ximeraLatex and local server version.
- `.github` for Github Actions, 
- `.vscode` for VS Code settings
- `xmPictures` for included pictures
- `xmScripts` for the xmlatex build setup
    - `config.txt` for target url, name, port, etc. For development/testing.
- `global.css` for extra online CSS styling (in addition to the server base css).


### dtxTests Folder at a glance
The `dtxTests` folder contains a subfolder for every dtx file in the ximera package 
(some may be inside the Hardcoded or Deprecated subfolders)
Each subfolder contains a tex file with the same name as the dtx folder.
This is the basic test for all of the default uses of the elements, so
``problem.tex`` contains all the basic use cases that are tested for the problem environment.
and it should be located inside the "problem" subfolder of the dtxTest folder.

Any other tex files inside a subfolder of the dtxTests folder are tests for
additional use cases for elements being tested. Most commonly this would be tests
of things like optional arguments, nesting (environments, mathmode, etc), and/or different types of
input inside the tested element.

Finally, each subfolder should have a `xourse.tex` file that loads all the relevant test files for that dtx file.

### compositeTests Folder at a glance
The compositeTests folder contains files and xourses to verify how elements 
in different dtx files interact with each other. 
Each composite test set should be in a subfolder of the compositeTests folder, where that
subfolder has a name that reflects the nature of what the composite test is testing,
e.g. a composite test for how sagemath commands interacts with various environments could be named
something like ``sageInteraction`` or ``sageInEnvironments``. 
Files in a given composite subfolder should also be named to reflect the specific test, e.g.
for the sageInteraction example could have files like ``sageInProblemEnv`` and/or
``sageInTheoremEnv`` files that are testing those specific interactions. 

Also in each compositeTest subfolder, there should be a file named after the folder itself
appended with ``Xourse`` which is the xourse file for that composite test, e.g. for our
previous example there should be a file called ``sageInteractionXourse.tex``.

<!-- 
* **testGroupings Folder at a glance**
Finally, the testGroupings folder should contain a list of folders that represent ''types'' of 
content that may need to be verified or tested - e.g. ''environments'', ''answerables'' or ''authorship tools''. 
More folders may be added here as we determine elements that are commonly needed to test together/in tandem. 
Note that the intent here, is that the same test file may be referenced in multiple (many!) of these subfolders... 
since something like the ``\answer`` command is likely to show up under a lot of different categories of areas 
that might need testing (e.g. ''student interactions'', ''page credit generating elements'', and 
''javascript elements'' would all have the ``\answer`` command as a relevant test).

* **Important Note About Test Groupings**
To ensure all tests stay up to date in the relevant testGroupings (and to avoid version mismatch and general confusion)
the files inside the testGroups should only be xourses that load the test files from the dtxTests folder, not new
test files. To submit a new test file, see the section on ``Creating a New Test File``. -->


# Naming Schemes

## Each test xourse is named after a dtx file.
Since  development work is implemented via dtx file, we can test new code by
pulling up the relevant dtxTestXourse(s) and loading the test bed xourse(s) that correspond to your changed dtx file.
These in turn load all the relevant test files that correspond to the individual elements implemented by that dtx file.

## Each tested element has a file in the relevant (subfolder) of the dtxTests Folder
Each element that is implemented in a dtx should have its own test file in that dtxTests subfolder, 
named after the relevant element. This should test the most basic form of the element.

However, often there are a number of options, or other elements for whatever is being tested that also need a test.
We don't want to have a single test file that contains all the various complexities of these things,
as it becomes difficult to see what aspect ended up generating issues (if/when there are issues from testing).
Thus test files should have a basic use test file that is the minimal implementation of the tested item, 
(named for the element, e.g. ''problem.tex'' would be the name for the basic test for the problem environment).

For relevant options, combinations, or other necessary testing conditions, various other files should be included
in the subfolder that test these other relevant aspects, each named after whatever it tests (e.g. ''numbering'' or 
''nesting'' for testing the numbering scheme and nesting behavior inside the problem subfolder in the dtxTests folder
respectively).

## Use of Preambles
Some specific test files/xourses need to load specific options or alternative files as part of their
testing (e.g. the graphics testing file needs to input graphics, and set graphics paths in the preamble). When this is
necessary, **do note change the xmPreamble** of the test repo - instead you should make a preamble with the relevant test
file (or xourse as appropriate) name, appended with ''Preamble'' - e.g. ''imagePreamble.tex'' is the preamble file
for the image.tex test file.
Similarly, some specific elements have (intended) different behavior depending on server source (e.g. UF, OSU, KL, etc).
In this case, you should add another test file with the intended behavior specific to the server source, and append the
server name/code to the test file. For example, if OSU has intended behavior that differs from ximera base for hints,
then there should be a ''hintsOSU.tex'' with tests for these differences along with documentation of expected behavior.

## Example of Intended Naming Scheme
To demonstrate the intended naming scheme, consider the problem-like environments. The thing being tested is the ''problem''
environment, so all tests go into a ''problem'' folder inside the dtxTests folder. We need the base case that
tests the very bare implementation of the problem like environments - but it also requires a test for how problem
numbering is handled, and a test for how nesting problems is handled. Thus there should be (at least) three test files 
inside the problem subfolder of the dtxTests folder: ``problem.tex``, ``nesting.tex``, and ``numbering.tex``.
each is a ximera documentclass that is testing the basic implementation, nesting behavior, and numbering scheme respectively.
These are in turn loaded by the ``problemTest.tex`` file, which is the xourse documentclass file that loads the test files for
everything generated in the problem.dtx file.

So just the ``problem` related files would be in the structure as follows:
- dtxTests
    - problem
        - problem.tex file (basic usage implementation/info)
        - nesting.tex (test for nesting behavior)
        - numbering.tex (test for numbering scheme)
        - problemTest.tex (xourse file that loads the above files for testing)

# Creating a New Test File
[Wim had a good idea for this, but I don't remember the details well enough - will ask him to edit this part.]
<!--
If you have determined a meaningful test case that has no appropriate test file, you can do the following;
1) You should post the issue on the github issues tab of the example repo (**NOT** the ximeraLatex repo!) with
a detailed explanation of what you need to test - make sure to highlight exactly the things that need to be
tested that are not currently testable using the existing test files. In other words, make sure to include:
    - What is currently not able to be tested using existing test files.
    - What specifically you are trying to test overall (in the case that the part that is `untestable` is 
    only a piece of what you are trying to test overall).
    - Why you are trying to test and/or what you are trying to change about Ximera that needs testing.
2) Next - if you are able, you should make a branch of the main examples repo, and write your new test file. 
Once you have the new test file written (and tested) and think it is ready to be merged, submit a pull request 
with an explanation of what and how you are going about testing the thing you are submitting a new file for,
along with a reference to the github issue in the examples repo that you submitted from part 1. This will
allow another developer to quickly and easily review the file for submission and then merge it.
    - As a general rule, a different developer (than the author of the new file) should review/merge 
    a new test file for safety.
    - New test files should be verified to make sure they are necessary, suitably succinct in their testing,
    and conform to the various naming and design requirements listed in this readme.
    - Once the merge has been completed, whomever reviewed the test file and merged the new test file into
    the master test repo *must* be the one to close the github issue. This will help with quickly referencing
    who did what if there are any issues later on or if someone needs to verify something (helps minimize
    digging through the commit history).
-->

# Non-Testable dtx Files Explained

Each dtx file should have its own test xourse that loads the relevant test files. However, pending a reorganization
of dtx files and their content, there are currently many dtx files that do not contain any testable commands or environments
(for example, the banner.dtx file is just the ascii definition of the banner that displays in the console on page load).
Nonetheless it is important to know that a given dtx file has been parsed and any necessary content have relevant test files.
So we still have ''test files'' for non-testable dtx files (e.g. ``bannerTest.tex``) but place that file in a special subfolder
called ``Hardcoded`` which contains dtx files that do not contain anything that can/need be tested (like the banner.dtx).
Moreover, there are also depreciated dtx files - those dtx files whose contents will be removed in an upcoming ximera version 
and they do not require testing. These are separated into a ``Depreciated`` subfolder inside the dtxTests folder.


<!-- A more detailed description of how to use this repo for testing is in the [README_testing](README_testing.md) -->

