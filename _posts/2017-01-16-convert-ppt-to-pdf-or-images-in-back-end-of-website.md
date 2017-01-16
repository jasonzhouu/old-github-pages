---
layout: post
title: "在网站后端将PPT文件转成PDF或图片"
---

## 转成PDF

#### [OpenOffice.org](https://www.openoffice.org/)

使用OpenOffice.org，它提供了很多Java API，功能强大，当有点难学。

#### [Comtypes](https://pypi.python.org/pypi/comtypes)

```python
import comtypes.client

def PPTtoPDF(inputFileName, outputFileName, formatType = 32):
    powerpoint = comtypes.client.CreateObject("Powerpoint.Application")
    powerpoint.Visible = 1

    if outputFileName[-3:] != 'pdf':
        outputFileName = outputFileName + ".pdf"
    deck = powerpoint.Presentations.Open(inputFileName)
    deck.SaveAs(outputFileName, formatType) # formatType = 32 for ppt to pdf
    deck.Close()
    powerpoint.Quit()
#source: http://stackoverflow.com/questions/31487478/how-to-convert-a-pptx-to-pdf-using-python
```

## 转成图片

#### [ImageMagick](http://www.imagemagick.org/script/index.php)

然后还可以使用ImageMagick将PDF转成图片，ImageMagick是个用于创建、编辑图片的开源的软件，可以通过命令行控制。

> ImageMagick® is a free software suite to create, edit, and compose bitmap images. It can read, convert and write images in a large variety of formats. Images can be cropped, colors can be changed, various effects can be applied, images can be rotated and combined, and text, lines, polygons, ellipses and Bézier curves can be added to images and stretched and rotated.
>
> source: https://wiki.python.org/moin/ImageMagick

ImageMagick可以读取很多格式的图片：

> It can read and write images in a variety of [formats](http://www.imagemagick.org/script/formats.php) (over 200) including PNG, JPEG, JPEG-2000, GIF, TIFF, [DPX](http://www.imagemagick.org/script/motion-picture.php), [EXR](http://www.imagemagick.org/script/high-dynamic-range.php), WebP, Postscript, PDF, and SVG.
>
> source: http://www.imagemagick.org/script/index.php

它提供了很多语言的接口，其中包括Python语言的接口[PythonMagick](https://wiki.python.org/moin/PythonMagick)，PythonMagick的下载地址是[http://www.imagemagick.org/download/python/](http://www.imagemagick.org/download/python/)。

> The functionality of ImageMagick is typically utilized from the [command-line](http://www.imagemagick.org/script/command-line-processing.php) or you can use the features from programs written in your favorite language. Choose from these interfaces: [G2F](http://www.imagemagick.org/script/api.php#ada) (Ada), [MagickCore](http://www.imagemagick.org/script/api.php#c) (C), [MagickWand](http://www.imagemagick.org/script/api.php#c) (C), [ChMagick](http://www.imagemagick.org/script/api.php#ch) (Ch), [ImageMagickObject](http://www.imagemagick.org/script/api.php#com_) (COM+), [Magick++](http://www.imagemagick.org/script/api.php#c__) (C++), [JMagick](http://www.imagemagick.org/script/api.php#java) (Java), [JuliaIO](http://www.imagemagick.org/script/api.php#julia) (Julia), [L-Magick](http://www.imagemagick.org/script/api.php#lisp) (Lisp), [Lua](http://www.imagemagick.org/script/api.php#lua) (LuaJIT), [NMagick](http://www.imagemagick.org/script/api.php#neko) (Neko/haXe), [Magick.NET](http://www.imagemagick.org/script/api.php#dot-net) (.NET), [PascalMagick](http://www.imagemagick.org/script/api.php#pascal) (Pascal),[PerlMagick](http://www.imagemagick.org/script/api.php#perl) (Perl), [MagickWand for PHP](http://www.imagemagick.org/script/api.php#php) (PHP), [IMagick](http://www.imagemagick.org/script/api.php#php) (PHP), [PythonMagick](http://www.imagemagick.org/script/api.php#python) (Python), [RMagick](http://www.imagemagick.org/script/api.php#ruby) (Ruby), or [TclMagick](http://www.imagemagick.org/script/api.php#tcl) (Tcl/TK). With a language interface, use ImageMagick to modify or create images dynamically and automagically.
>
> source: http://www.imagemagick.org/script/index.php

ImageMagick在包括PythonMagick在内有4种Python语言的工具，Wand库、PythonMagick接口、PythonMagickWand接口、Scilab Image Processing工具箱。

> [Wand](http://wand-py.org/) is a ctypes-based ImagedMagick binding library for Python.
>
> [PythonMagick](https://www.imagemagick.org/download/python/) is an object-oriented Python interface to ImageMagick.
>
> [PythonMagickWand](http://www.assembla.com/wiki/show/pythonmagickwand) is an object-oriented Python interface to MagickWand based on ctypes.
>
> [Scilab Image Processing](http://siptoolbox.sourceforge.net/) toolbox utilizes ImageMagick to do imaging tasks such as filtering, blurring, edge detection, thresholding, histogram manipulation, segmentation, mathematical morphology, color image processing, etc..
>
> source: http://www.imagemagick.org/script/api.php#python

#### [Ghostscript](https://www.ghostscript.com/)

使用Ghostscript也能将PDF转成图片。

> use ghostscript to convert the pdf to png or other image format (something along the line of `gs -dSAFER -dBATCH -dNOPAUSE -sDEVICE=png16m -r100 -sOutputFile=out.png in.pdf`)