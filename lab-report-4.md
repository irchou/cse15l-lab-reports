# Lab Report 4
## Step 4
![Image](/images/Step4.png) 
```
Keys Pressed:
ssh<space>irchou<shift+2>ieng6-201.ucsd.edu<enter>
```
To log in to my ieng account, I typed the `ssh` command and my username before pressing `<enter>`.

## Step 5
![Image](/images/Step5.png) 
```
Keys Pressed:
git<space>clone<space><ctrl+v><enter>
```
The `git clone` command was used to clone the forked repository. I copied the ssh clone URL of the fork and pasted it after the `git clone` command using `ctrl+v`. 

## Step 6
![Image](/images/Step6.png) 
```
Keys Pressed:
cd<space>l<tab><enter>
bash<space>t<tab><enter>
```
To run the tests, I first moved into the new directory containing the forked repo `/lab7` using `cd`. Since the only directory starting with 'l' was `lab7`, by tabbing after typing `cd l`, the terminal filled in the rest of the command with the `lab7` directory. Then, I ran the bash script `test.sh`. I again used `<tab>` to fill in `test.sh` after typing `bash t` because the only file starting with 't' in the working directory was `test.sh`.

## Step 7
![Image](/images/Step7a.png) 
![Image](/images/Step7b.png) 
```
Keys Pressed:
vim<space><shift+l><tab>.<tab><enter>
43j12li<backspace>2<escape><shift+;>wq<shift+1><enter>
```
To edit the code file, I used `vim` and gave it the name of the file I wanted to edit. By typing 'L' and hitting `<tab>`, bash filled in `ListExamples` since the only files starting with 'L' both start with "ListExamples". I typed '.' afterwards to differentiate `ListExamples.java` from `ListExamplesTests.java`, and hit `<tab>` again to fill in the rest of the file name `ListExamples.java`.
After opening vim, my cursor was at the top of the file, so I moved it down to the line with the error using `43j` and moved it to the right to where the error is on that line using `12l`. By pressing `i`, I entered insert mode and edited `index1` to be `index2` before exiting insert mode using `escape`. Then, I saved and exited the file by entering `:wq!`.

## Step 8
![Image](/images/Step8.png) 
```
Keys Pressed:
<up><up><enter>
```
Since `bash test.sh` was the second to last command that was ran, I used the up arrow twice to access it again. Then, it was ran by pressing `<enter>`.

## Step 9
![Image](/images/Step9.png) 
```
Keys Pressed:
git<space>add<space><shift+l><tab>.<tab><enter>
git<space>commit<space>-m<space><shift+'>fix<space>bug<shift+'><enter>
git<space>push<enter>
```
First, I added the changes from the `ListExamples.java` file by using the `git add` command. I typed 'L' before pressing `<tab>` for it to autofill in the 'ListExamples' and then typed '.' before pressing `<tab>` again to fill in the rest of the `ListExamples.java`. Then, I used the `git commit` command to commit the added changes. I used the `-m` option to include the commit message where I wrote `"fix bug"` in. Lastly, I used the `git push` command to push the commit.
