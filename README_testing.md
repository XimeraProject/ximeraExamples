A possible testing session...

Note: if you just want to *test* or *try* something, and do not plan to make any changes, all forking and making-new-branches can be skipped.

* Fork, clone and checkout your copy of ximeraExamples
```
~/git/ximera/ximeraExamples$ git pull
Already up to date.
```
* Create a new branch for your new development/test (optional)
    * The new branch is only needed if you foresee to make new test, or adapt existing ones
```
~/git/ximera/ximeraExamples$ git checkout -b test-link
Switched to a new branch 'test-link'
```

* Setup the to be tested/changed ximeraLatex version:
  * if testing a dockerimage, update config.txt(local PC) or docker_compose.yml (in Codespace)
     * if you need to try a fix to the contents of the dockerimage, use can use 'xmlatex copySettingsLocal' to create a .ximera_local with the ximealatex contents from the current image.
  * if testing an existing ximeraLatex branch (perhaps on a clone somewhere) : check it out in .ximera_local
  * if making new changes to ximeraLatex: fork, clone, and checkout a new branch

```
~/git/ximera/ximeraExamples$ git clone https://github.com/bartsnapp/ximeraLatexFrameDev.git .ximera_local
Cloning into '.ximera_local'...
remote: Enumerating objects: 4273, done.
remote: Counting objects: 100% (284/284), done.
remote: Compressing objects: 100% (92/92), done.
remote: Total 4273 (delta 208), reused 193 (delta 192), pack-reused 3989 (from 3)
Receiving objects: 100% (4273/4273), 6.12 MiB | 4.84 MiB/s, done.
Resolving deltas: 100% (2753/2753), done.
```
* Use, update or create a relevant test 
   * you can use the VSCode 'PDF' or 'HTML' buttons, or the xmlatex script (see infra)
   * not the 'USING .ximera_local from local repo' line in the output when you made a .ximera_local
   * the .log file wiyll contain detailed info about which files where actually used/included
```
~/git/ximera/ximeraExamples$ xmlatex ghaction testXourses.TODO/linkTest.tex 
Restarting myself in docker (from image ghcr.io/ximeraproject/ximeralatex:v2.7.0)
Starting /usr/local/bin/xmlatex ghaction testXourses.TODO/linkTest.tex (on host docker-desktop, i.e. inside a docker container)
USING .ximera_local from local repo
Starting Github-action build (name; bake/frost/serve)
[INFO   ] main : Set compile_sequence=pdf,html (and output_formats=pdf,html)
[INFO   ] main : Processing argument 1: testXourses.TODO/linkTest.tex
[INFO   ] files: Marked source tex          NO_COMPILATION     for examples.TODO/links/links.tex
[INFO   ] files: Marked source tex          NEEDS_COMPILATIONS for testXourses.TODO/linkTest.tex
[STATUS ] main : 1 file needs compiling: testXourses.TODO/linkTest.tex
[STATUS ] main : Start bake
[INFO   ] bake : Added 2 compile commands for file   1/1: testXourses.TODO/linkTest.tex
[STATUS ] bake : There are 2 commands to run for 1 files
[STATUS ] bake : Command   1/2 (1) starting for  pdf of testXourses.TODO/linkTest.tex (pdf|testXourses.TODO/linkTest.tex)
[STATUS ] bake : Command   2/2 (2) starting for html of testXourses.TODO/linkTest.tex (html|testXourses.TODO/linkTest.tex)
[STATUS ] bake : Command   2/2 (2) returns OK after 7.5 seconds (0 failed) for html of testXourses.TODO/linkTest.tex
[INFO   ] bake : Command html|testXourses.TODO/linkTest.tex scheduled for RETRY (was job 2 (2))
[STATUS ] bake : Command  2r/2 (2) starting for html of testXourses.TODO/linkTest.tex (html|testXourses.TODO/linkTest.tex)
[INFO   ] bake : Moving /code/testXourses.TODO/linkTest.pdf to ximera-downloads/with-answers/testXourses.TODO/linkTest.pdf
[STATUS ] bake : Command   1/2 (1) returns OK after 10.0 seconds (0 failed) for pdf of testXourses.TODO/linkTest.tex
[INFO   ] html : No parts found, adding one, as this is needed in (some versions of) the ximeraServer
[INFO   ] html : Adapted html being saved as testXourses.TODO/linkTest.html (/code/testXourses.TODO/linkTest.html)
[STATUS ] bake : Command  2r/2 (2) returns OK after 5.0 seconds (0 failed) for html of testXourses.TODO/linkTest.tex
[STATUS ] bake : Finished compiling 1 files in 13.6 seconds
[STATUS ] main : Bake succeeded: Baked 1 files, no errors found
[INFO   ] main : Mmm, file testXourses.TODO/linkTest.tex still needs compilation.
[INFO   ] main : Still 1 files to be compiled after bake.
[STATUS ] main : Start frost
[WARNING] frost: There are 2 uncommitted files; should serve only to localhost
[WARNING] frost: There are 1 file to be compiled; should serve only to localhost
[INFO   ] frost: Adding XOURSE testXourses.TODO/linkTest.tex (Master link Test Xourse)
[INFO   ] frost: Found publications/0333286ab0e4c1ceb1046418afcc88032080ff59  (tree:e58298d99203d801017d707c551651ab53fdce1f tag:0333286ab0e4c1ceb1046418afcc88032080ff59) 
[STATUS ] frost: Creating tag publications/a40cd692e6e6af56fd0ce8fc37f7db318d567d35 for a40cd692e6e6af56fd0ce8fc37f7db318d567d35
[STATUS ] main : Frost succeeded: Created publications/a40cd692e6e6af56fd0ce8fc37f7db318d567d35
[STATUS ] main : Start serve
[INFO   ] frost: Publishing to localhost: http://localhost:2000/ximeraexamples.git
[STATUS ] frost: Forced serving (git push -f ximera publications/a40cd692e6e6af56fd0ce8fc37f7db318d567d35)
[STATUS ] frost: Forced serving (git push -f ximera a40cd692e6e6af56fd0ce8fc37f7db318d567d35:refs/heads/master)
[STATUS ] main : Serve succeeded: Published  publications/a40cd692e6e6af56fd0ce8fc37f7db318d567d35to  http://localhost:2000/ximeraexamples
```
   * Verify the output

* If yoy make useful changes in .ximera_local : commit and push, make a pull request for ximeraLatex
* If you make useful changes in ximeraExamples: commit and push, make a pull request for ximeraExamples
* when in doubt, or when this procedure does not work as advertized: contact ximera-project!






