# How can you convert an Adobe Illustrator (ai) file to an Encapsulated PostScript (eps) file?

One of my web applications is using [RML](https://www.reportlab.com/software/rml-reference/) to render PDFs.

For one PDF document template I received a new logo file which was produced with Adobe Illustrator (file extension .ai).

The **RML library** cannot handle ai-files, but eps-files.

In order to convert the file I used Ghostscript as following:

```
gs -dNOPAUSE -dBATCH -sDEVICE=eps2write -sOutputFile=out.eps input.ai
```

where
- `-dNOPAUSE` means "no pause after page"
- `-dBATCH` means "exit after last file"
- `-sDEVICE` selects the device
- `-sOutputFile` is the name of the - you can guess it - the output file

P.S.: I ❤️ open source and Linux!
