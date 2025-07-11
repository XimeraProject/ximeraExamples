# Intent/Summary of This Folder
This folder is intended to have the test files that (completely) test the
individual dtx files in isolation. These are likely to be the most used/important
test files as development is *usually* isolated to individual dtx files,
rather than more sweeping composite changes that impact many different types
of files simultaneously. 

# Organization Scheme
This folder should mirror the dtx structure of the ximera package, so that
one can find the dtx file to test by tracing the same folder pathway as the
dtx file that they were editing. The only difference is that the dtx file
in the ximera package is now a folder, as individual dtx files can have
several different test files to account for several testing aspects within
that test file (e.g. the problem.dtx has base.tex, numbering.tex and
nesting.tex testing files).