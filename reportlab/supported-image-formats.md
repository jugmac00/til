# Which image formats are supported by ReportLab's pdf library?

[ReportLab](https://pypi.org/project/reportlab/) is an open source library for generating PDFs, written in Python.

While ReportLab is absolutely battle tested, even [Wikipedia](https://www.reportlab.com/casestudies/wikipedia/) uses it for PDF generation, documentation lacks a bit.

I could not find a reliable source for supported image formats.

Also, there is both an open source and a commercial license for ReportLab, with different feature sets.
The latter one is supposed to be able to treat PDFs as image files, which then can be embedded.

In Mike Driscoll's book [ReportLab - PDF Processing with Python](https://leanpub.com/reportlab), I finally found a good hint:

> By default, ReportLab only supports the jpeg format. However if you have the Pillow (or PIL) package installed, then most other image types are also supported.

Still, I'd like to have a list of supported formats.

Finally, as a last resort, [pdb++](https://pypi.org/project/pdbpp/), my debugger of choice, helped me to find the supported image formats:

```
['BLP', 'BMP', 'BUFR', 'CUR', 'DCX', 'DDS', 'DIB', 'EPS', 'FITS', 'FLI', 'FTEX', 'GBR', 'GIF', 'GRIB', 'HDF5', 'ICNS', 'ICO', 'IM', 'IMT', 'IPTC', 'JPEG', 'JPEG2000', 'MCIDAS', 'MPEG', 'MSP', 'PCD', 'PCX', 'PIXAR', 'PNG', 'PPM', 'PSD', 'SGI', 'SPIDER', 'SUN', 'TGA', 'TIFF', 'WEBP', 'WMF', 'XBM', 'XPM', 'XVTHUMB']
```
