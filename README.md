This Repo contains the master testbed for Ximera development. 
It also contains minimal examples and syntax for the Ximera commands, environments, etc. 
However, for a much in-depth treatment of Ximera commands, environments, etc you should
refer to the Ximera manual, which explains things in more detail and in a more user friendly way.

# General Structure and Intent of this Repo

This Repo (will) be structured as follows...


- masterTestFolder
    - (DTXFileName)Test.tex files (e.g. problemTest.tex)
- testFiles
    - (command/Env)Base.tex files (e.g. problemBase.tex)
    - (command/Env)(Additional Testing Feature).tex (e.g. problemNesting.tex or problemNumbering.tex)
- testGroups
    - (Group By Type) folder. (e.g. ''environments'' or ''authorTools'' folders)
        - Each folder contains a group of test xourses relevant to that grouping. 
- untestedDTX
    - depreciated folder
        - (dtxFileName)Test.tex files for dtx files that contain only content that 
        will be removed in a future release of ximera (e.g. gradedTest.tex)
    - hardCoded folder
        - (dtxFileName)Test.tex files for the dtx files with no testable elements (e.g. banner.dtx)


**testFiles Folder at a glance**

The testFiles folder is the folder that contains all the actual test ximera document class files
that are loaded and used for demo/testing. Files in this folder should adhere to a specific naming
scheme, and by large should not need to be edited after they have been finalized as testing bed files.
(More on this below).

**masterTestFolder Folder at a glance**

The masterTestFolder is the location of all the xourse files that represent tests for each of the
possible (individual) areas for testing - e.g. ''problem'' type environments or ''maketitle'' command.
Again, these all adhere to a specific naming scheme and should not need to be edited once they have
been verified as valid testbed files until/unless more content is added to its category.
(Again, more on this below).

**testGroupings Folder at a glance**

Finally, the testGroupings folder is likely where most of the testing will actually take place. This
folder should contain a list of folders that represent ''types'' of content that may need to be verified
or tested - e.g. ''environments'', ''answerables'' or ''authorship tools''. More folders may be added here
as we determine elements that are commonly needed to test together/in tandem. Note that the intent here,
is that the same test file/xourse may appear in multiple (indeed many) of these subfolders... since something
like the ``\answer`` command is likely to show up under a lot of different categories of areas that might need
testing (e.g. ''student interactions'', ''page credit generating elements'', and ''javascript elements'' would
all have the ``\answer`` command as a relevant test).

**Important Note About Test Groupings**

To ensure all tests stay up to date in the relevant testGroupings (and to avoid version mismatch and general confusion)
the files inside the testGroups will be symlinks to the relevant test xourse in the masterTestFolder. So the only
real test xourses will be the files in the master test folder - meaning there is only one file to update and keep
track of, and any changes to that one file will automatically update all relevant tests in the test groupings.


# Naming Schemes

* Each test xourse is named after a dtx file, and every dtx file should have a test xourse named after it (with some exceptions, see below).
Since all development work must be implemented via dtx file (as per CTAN standards) and most development work
tends to involve only a few dtx files (usually just one or two), it is often easiest to test the new code by testing
everything that is implemented by the newly changed dtx code. This testing bed makes that easy to accomplish by merely
pulling up the master test folder and loading the one or two test bed xourses that correspond to your changed dtx file.
These in turn load all the relevant testFiles that correspond to the individual elements implemented by that dtx file
i.e. each command/environment (or reasonably obvious groupings, like all ``\newtheorem`` generated environments are
in the same place) has its own testing tile, making it relatively easy to investigate updated content, even inside a given dtx.
Thus **Each test xourse should be named  (dtxFileName)Test.tex** e.g. ''abstractTest.tex'' for the ''abstract.dtx'' file.

* Each test file in the testFiles folder is named after the relevant command, environment, etc that it is testing.
In most cases, this means it will be named the same as the dtx file (e.g. the ''abstract'' test file for the ''abstractTest''
xourse). However, often there are a number of options, or other elements that need to be demo'ed/testable for a given 
command/environment/etc. We don't want to have a single test file that contains all the various complexities of these
things, as it becomes difficult to see what aspect ended up generating issues (if there are issues from a new update).
Thus test files should have a ''Base'' version that is the minimal implementation of the tested item, and then various
other files that demo/test the other relevant aspects.

* As a special note, some specific test files/xourses need to load specific options or alternative files as part of their
testing (e.g. the graphics testing file needs to input graphics, and set graphics paths in the preamble). When this is
necessary, **do note use the xmpreamble** for the test repo - instead you should make a preamble with the relevant test
file (or xourse as appropriate) name, appended with ''preamble'' - e.g. ''imagePreamble.tex'' is the preamble file
for the image.tex test file.
Similarly, some specific elements have (intended) different behavior depending on server source (e.g. UF, OSU, KL, etc).
In this case, you should add another test file with the intended behavior specific to the server source, and append the
server name/code to the test file. For example, if OSU has intended behavior that differs from ximera base for hints,
then there should be a ''hintsOSU'' or possibly a ''hintsBaseOSU'' as appropriate.

* **Example of Intended Naming Scheme:** 
To demonstrate the intended naming scheme, consider the problem-like environments. The tests need to have a base case that
demo/tests the very bare implementation of the problem like environments - but it also requires a test for how problem
numbering is handled, and a test for how nesting problems is handled. Thus there should be three test files;
problemBase.tex, problemNesting.tex, and problemNumbering.tex - each is a ximera documentclass that is demoing/testing
the basic implementation, nesting behavior, and numbering scheme respectivvely. These are in turn loaded by the
''problemTest.tex'' file, which is the xourse documentclass that loads the content generated in the problem.dtx file.

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

