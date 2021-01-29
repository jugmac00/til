# How can you count the number of selected lines in VS Code?

Today I wrote a CSV export with many, many columns, where in my Python code each colum was calculated on a single line.

So, in order to get the number of columns, I selected all related lines and in the status bar I saw the number of all selected chars! wat?

## solutions

After some searching on Google and stackoverflow I came to the conclusion...

Either

a) you install an outdated plugin

b) or you
- open a terminal
- open your file in vim
- use visual mode and select the lines

c) or you copy paste the lines into an empty file and do a `wc -l`

d) or you copy paste the lines into a new buffer/file and have a look at the total lines

There are ~~several~~ many, many issues on the VS Code issue tracker about line count.

They were all closed and it was recommended to install a plugin :-/

Even without knowing anything about the security model of VS Code I won't ever install an outdated plugin from some random repository for doing such a basic task.

## sources

- https://github.com/microsoft/vscode/issues/932
- https://github.com/microsoft/vscode/issues/15344
- https://github.com/microsoft/vscode/issues/45726
- https://stackoverflow.com/questions/61339515/how-to-set-vscode-to-display-the-number-of-selected-lines

## money quote

> Considering this is "VS Code" and not "VS Word," I find it hard to believe that most users care about the number of characters selected.

[@ericlaspe](https://github.com/microsoft/vscode/pull/17955#issuecomment-454581543)
