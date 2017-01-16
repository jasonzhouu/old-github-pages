---
layout: post
title: "在网站后端将PPT文件转成PDF或图片"
---

## 转成PDF

#### [OpenOffice.org](https://www.openoffice.org/)

简称OOo，它提供了很多Java API，功能强大，但有点难学。

## [unocon](http://dag.wiee.rs/home-made/unoconv/)

unocon使用Python语言写的，用于将OpenOffice支持的文件格式互相转换。

> unoconv converts between any document format that OpenOffice understands. It uses OpenOffice's UNO bindings for non-interactive conversion of documents.
>
> Supported document formats include Open Document Format (.odt), MS Word (.doc), MS Office Open/MS OOXML (.xml), Portable Document Format (.pdf), HTML, XHTML, RTF, Docbook (.xml), and more.

使用前需要安装LibreOffice或OpenOffice

> It needs a recent LibreOffice or OpenOffice with UNO bindings.

支持Linux, Windows, MacOSX环境。

#### [Comtypes](https://pypi.python.org/pypi/comtypes)

Comtypes只能运行在windows环境：

> **comtypes** is a lightweight Python COM package, based on the [ctypes](http://docs.python.org/lib/module-ctypes.html) FFI library, in less than 10000 lines of code (not counting the tests).
>
> **comtypes** allows to define, call, and implement custom and dispatch-based COM interfaces in pure Python. It works on Windows, 64-bit Windows, and Windows CE.

下载地址：[comtypes-1.1.3-2.zip](https://pypi.python.org/packages/85/11/722b9ce6725bf8160bd8aca68b1e61bd9db422ab12dae28daa7defab2cdc/comtypes-1.1.3-2.zip#md5=4161cb8bc283a75af85e220ad662d5af)

将PPT转成PDF的代码：

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

#### [Ghostscript](https://www.ghostscript.com/)

- 使用Ghostscript能将PDF转成图片。

> use ghostscript to convert the pdf to png or other image format (something along the line of `gs -dSAFER -dBATCH -dNOPAUSE -sDEVICE=png16m -r100 -sOutputFile=out.png in.pdf`)

- 可以将每一页PDF各自转成一张图片

```shell
gs -dNOPAUSE -sDEVICE=jpeg -r144 -sOutputFile=p%03d.jpg file.pdf
```

source: [Quick one: converting a multi-page PDF to a JPG for each page on OSX](https://www.christianheilmann.com/2012/09/30/quick-one-converting-a-multi-page-pdf-to-a-jpg-for-each-page-on-osx/)

输出的文件名通过参数进行控制，具体可参考官网的[document](https://ghostscript.com/doc/9.20/Use.htm)。

> One page per file
>
> Specifying a single output file works fine for printing and rasterizing figures, but sometimes you want images of each page of a multi-page document. You can tell Ghostscript to put each page of output in a series of similarly named files. To do this place a template '%d' in the filename which Ghostscript will replace with the page number.

- 可以不把整个PDF转换成图片，而是选择特定一部分页，通过设置初始页面和结束页面就行了。比如只将第12张PDF转成图片:

```shell
gs \
 -sDEVICE=jpeg \
 -o %03d.jpeg \
 -dFirstPage=12 \
 -dLastPage=12 \
 -dJPEGQ=30 \
 -r72x72 \
  file.pdf
```

source: http://stackoverflow.com/questions/5527818/ghost-script-extract-a-single-page-from-a-pdf-and-convert-it-to-a-jpg

- 还可以用-sPageList=pagenumber参数指定转换的页面。

> -sPageList=pagenumber There are three possible values for this; even, odd or a list of pages to be processed. A list can include single pages or ranges of pages. Ranges of pages use the minus sign '-', individual pages and ranges of pages are separated by commas ','. A trailing minus '-' means process all remaining pages. For example;
>
> -sPageList=1,3,5 indicates that pages 1, 3 and 5 should be processed.
>
> -sPageList=5-10 indicates that pages 5, 6, 7, 8, 9 and 10 should be processed.
>
> -sPageList=1, 5-10, 12- indicates that pages 1, 5, 6, 7, 8, 9, 10 and 12 onwards should be processed.

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