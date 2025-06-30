# Intent/Summary of This Folder
This folder will contain test files for those structures that we need to
test, that involve expansive interactions between several different 
elements contained within different dtx structures. For example, we should
have a test file to test the interaction between the label/ref system
and theorems, problems, explanations, and other environments that might
need to be referenced/cited. These environments are all implemented
across several dtx files, so there isn't a nice way to test them using the
dtx-specific test files

# Organization Scheme
The testfiles that will be in this folder are not naturally separable, 
since - by their nature - they are compositions of many different dtx files.
However, these test files should arise naturally out of a more global concern
(e.g. ``how does label/referencing interact with environments?``), so the
author of test files for this area should try their best to create and name
a (sub)folder so that others can guess what kind of thing the files inside
are testing. Each composite test situation is again likely to have a number
of test files for different aspects of the testing of that situation
(e.g. a file to test label/ref with problem-like envs, another for
theorem-like envs, another for expository-like envs, etc), so each
composite test should have its own subfolder, containing the test files.
Ideally the xourse for composite test files should go into the testGroupings
folder.

