# Intent/Summary of This Folder
This folder will a xourse file for each dtx file in the ximera package,
named after that dtx folder. This is for testing changes whose impact
is expected to be within a specific dtx file (e.g. changing how the
problem-like environments are rendered should only impact the problem.dtx
file). 

# Organization Scheme
Each file in this folder should have the name of a dtx file from the 
ximera package, appended with ``Test``, e.g. the ``hints.dtx`` file in
the ximera package is associated with the ``hintsTest.tex`` xourse file
in this folder. This allows developers to test changes that are only
expected to impact single dtx file contents.
For changes that are expected to impact how contents of *different*
dtx files interrelate (e.g. label/ref across various environments) devs
should use the xoure files found in the compositeTestXourses folder.
