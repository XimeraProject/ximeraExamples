This Repo contains the master testbed for Ximera development. 
It also contains minimal examples and syntax for the Ximera commands, environments, etc. 
However, for a much in-depth treatment of Ximera commands, environments, etc you should
refer to the Ximera manual, which explains things in more detail and in a more user friendly way.

# General Structure and Intent of this Repo

* **This Repo (will eventually be) structured as follows...**

- depreciated (for content that is being removed in a future release, see README in folder)
    - (DTXFileName)Test.tex files (e.g. problemTest.tex)
- testFiles
    -compositeTestFiles (for tests of interactions between different dtx file contents, see README in folder.)
        -subfolder named to explain composite testing case.
    -dtxTestFiles (for individual dtx file testbeds, see README in folder.)
        - (Command/Env) folder; a folder for each testable command/enviroment/etc. (e.g. ''problem'' folder)
            - base.tex file (basic usage implementation/info)
            - (Additional Testing Feature).tex (e.g. nesting.tex or numbering.tex in the problem folder)
- testXourses (xourse files to lode relevant test files, see README in folder)
    - compositeTestXourses (xourses for testing interactions between different dtx files)
    - dtxTestXourses (xourses for testing individual dtx file contents)
        - (dtxFileName)Test.tex is the xourse that tests (dtxFileName) dtx file.
        - Includes hard coded non-tested content so it is easy to verify all non-depreciated dtx has been parsed.

* **testFiles Folder at a glance**
The testFiles folder is the folder that contains all the actual test ximera document class files
that are loaded and used for demo/testing. There are two subfolders in this folder.
1) The dtxTestFiles are the files that test individual dtx files to verify the integrity of all
the elements within that specific dtx file.
2) The compositeTestFiles subfolder is for files that test the integrity of elements that span
and/or interact between different dtx files.

* **testXourses Folder at a glance**
The testXourses is the location of all the xourse files. There are two subfolders;
1) The first subfolder is the dtxTestXourses subfolder. It is a subfolder for xourses that are
tests for each of the dtx files, these xourses should load all the relevant test files to verify
the functionality of all the elements that are touched by that dtx file.
2) The other subfolder is the compositeTestXourses folder, which are xourses that load all the relevant 
tests to verify the integrity of how elements in different dtx files interact with each other. These
should load each of the relevant test files in the corresponding compositeTestFiles subfolder
of the testFiles folder.

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
the files inside the testGroups should only be xourses that load the test files from the testFiles folder, not new
test files. To submit a new test file, see the section on ``Creating a New Test File``. -->


# Naming Schemes

* **Each test xourse in the testXourses/dtxTestXourses is named after a dtx file.**
Since all development work must be implemented via dtx file (as per CTAN standards) and most development work
tends to involve only a few dtx files (usually just one or two), it is often easiest to test the new code by testing
everything that is implemented by the newly changed dtx code. This testing bed makes that easy to accomplish by merely
pulling up the relevant dtxTestXourse(s) and loading thetest bed xourse(s) that correspond to your changed dtx file.
These in turn load all the relevant testFiles that correspond to the individual elements implemented by that dtx file
i.e. each command/environment (or reasonably obvious groupings, like all ``\newtheorem`` generated environments are
in the same place) has its own testing tile, making it relatively easy to investigate updated content, even inside a given dtx.
Thus **Each dtxTestXourse should be named  (dtxFileName)Test.tex** e.g. ''abstractTest.tex'' for the ''abstract.dtx'' file.

* **Each tested command/env/etc has a file in the relevant (subfolder) of the dtxTestFiles Folder**
Each command/environment/etc (referred to as ``element``) that is implemented in a dtx should have its own testFile 
in that dtxTestFiles subfolder, named after the relevant element. This should demo/test the most basic form of the 
element.
However, often there are a number of options, or other elements for whatever is being tested that also need a demo/test.
We don't want to have a single test file that contains all the various complexities of these things,
as it becomes difficult to see what aspect ended up generating issues (if there are issues from testing).
Thus test files should have the ''base.tex'' file that is the minimal implementation of the tested item, and then various
other files that demo/test the other relevant aspects, each named after whatever it tests (e.g. ''numbering'' or ''nesting''
for demo/testing the numbering scheme and nesting behavior inside the problem subfolder in the testFiles folder.).

* **When Preambles are Necessary**
Some specific test files/xourses need to load specific options or alternative files as part of their
testing (e.g. the graphics testing file needs to input graphics, and set graphics paths in the preamble). When this is
necessary, **do note use the xmpreamble** for the test repo - instead you should make a preamble with the relevant test
file (or xourse as appropriate) name, appended with ''preamble'' - e.g. ''imagePreamble.tex'' is the preamble file
for the image.tex test file.
Similarly, some specific elements have (intended) different behavior depending on server source (e.g. UF, OSU, KL, etc).
In this case, you should add another test file with the intended behavior specific to the server source, and append the
server name/code to the test file. For example, if OSU has intended behavior that differs from ximera base for hints,
then there should be a ''hintsOSU'' or possibly a ''hintsBaseOSU'' as appropriate.

* **Example of Intended Naming Scheme:** 
To demonstrate the intended naming scheme, consider the problem-like environments. The thing being tested is the ''problem''
environment, so all tests go into a ''problem'' folder inside the testFiles folder. We need the base case that
demo/tests the very bare implementation of the problem like environments - but it also requires a test for how problem
numbering is handled, and a test for how nesting problems is handled. Thus there should be three test files inside the problem
subfolder of the testFiles folder; problemBase.tex, problemNesting.tex, and problemNumbering.tex. 
each is a ximera documentclass that is demoing/testing the basic implementation, nesting behavior, 
and numbering scheme respectivvely. These are in turn loaded by the
''problemTest.tex'' file, which is the xourse documentclass that loads the content generated in the problem.dtx file.
So just the ''problem'' related files would be in the structure as follows:
- testXourses
    - problemTest.tex
- testFiles
    - problem
        - base.tex file (basic usage implementation/info)
        - nesting.tex (demo/test for nesting behavior)
        - numbering.tex (demo/test for numbering scheme)

# Creating a New Test File
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

# Non-Testable dtx Files Explained

Each dtx file should have its own test xourse that loads the relevant test files. However, pending a reorganization
of dtx files and their content, there are currently many dtx files that do not contain any testable commands or environments
(for example, the banner.dtx file is just the ascii definition of the banner that displays in the console on page load).
Nonetheless it is important to know that a given dtx file has been parsed and any necessary content have relevant test files.
So we still make test files for non-testable dtx files (e.g. BannerTest.tex) but place that file in a special top-level folder
called ''untestedDTX'' which contains two different types of non-tested files. There are depreciated dtx files - those dtx
files whose contents will be removed in an upcoming ximera version and so tests aren't needed (these are separated into
a 'depreciated' folder inside the untestedDTX folder) as well as the dtx files that do not contain anything that can/need
be tested (like the banner.dtx) - test files for these are put in the ''hardCoded'' subfolder of the untestedDTX folder.


# Public Publishing Locations

Content from this repo is published publically for others to see, and link to. This is mostly as a quick-ref demo resource
for authors, but can be used by anyone - it is publically available after all. You can find these servers here:

 * at [KU Leuven](https://set-p-dsb-zomercursus-latest.cloud-ext.icts.kuleuven.be/ximeraexamples/coreXimeraFeatures/environments/theoremEnvironments).
 * at [OSU](https://ximera.osu.edu/ximeraexamples).

Note you can always get the TeX-code by appending .tex to the URL of an activity.


<!-- A more detailed description of how to use this repo for testing is in the [README_testing](README_testing.md) -->

# Notes from talking with Wim

1) Make a ``global testing files`` type subfolder in the testFiles folder for test files that are designed
to test more global interactions - not things that are contianed within a single dtx file.
For example, the label/ref interactions with certain environments like theorems or problems; or 
complicated ToC implementation with nesting sections/subsections and chapterstyle/sectionstyle commands.




