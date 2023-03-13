---
layout: post
title: "Learning Notes: Font Tools and Typography Guide"
date: 2023-03-13 23:03:03 +0200
category: tutorial
tagline: ""
tags: [Font]
abstract : "Learning notes: font development tools, font families, and fonts for different languages."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [Tools](#tools)
  * [AFDKO](#afdko)
  * [fontTools](#fonttools)
* [Font Family](#font-family)
  * [Serif vs Sans Serif](#serif-vs-sans-serif)
* [Fonts for Different Languages](#fonts-for-different-languages)
  * [Chinese Fonts](#chinese-fonts)
* [References](#references)


# Introduction

This post provides an overview of font development tools, font family classifications, and resources for working with fonts across different languages. Whether you're converting font formats, understanding typography basics, or looking for fonts that support multiple languages, this guide covers essential tools and concepts for font development and typography.


# Tools

## AFDKO

Adobe Font Development Kit for OpenType (AFDKO): <https://github.com/adobe-type-tools/afdko/>

The AFDKO is a set of tools for building OpenType font files from PostScript and TrueType font data.

Provide a python script to convert OTF to TTF: <https://github.com/adobe-type-tools/afdko/blob/develop/python/afdko/otf2ttf.py>:

```python
# adobe_otf2ttf.py
import argparse
import glob
import logging
import os
import sys
from functools import partial, singledispatch
from itertools import chain
from multiprocessing import Pool

from fontTools import configLogger
from fontTools.misc.cliTools import makeOutputFileName
from fontTools.pens.cu2quPen import Cu2QuPen
from fontTools.pens.ttGlyphPen import TTGlyphPen
from fontTools.ttLib import TTCollection, TTFont, TTLibError, newTable

log = logging.getLogger()
configLogger(logger=log)

# default approximation error, measured in UPEM
MAX_ERR = 1.0

# default 'post' table format
POST_FORMAT = 2.0

# assuming the input contours' direction is correctly set (counter-clockwise),
# we just flip it to clockwise
REVERSE_DIRECTION = True


def glyphs_to_quadratic(
        glyphs, max_err=MAX_ERR, reverse_direction=REVERSE_DIRECTION):
    quadGlyphs = {}
    for gname in glyphs.keys():
        glyph = glyphs[gname]
        ttPen = TTGlyphPen(glyphs)
        cu2quPen = Cu2QuPen(ttPen, max_err,
                            reverse_direction=reverse_direction)
        glyph.draw(cu2quPen)
        quadGlyphs[gname] = ttPen.glyph()
    return quadGlyphs


def update_hmtx(ttFont, glyf):
    hmtx = ttFont["hmtx"]
    for glyphName, glyph in glyf.glyphs.items():
        if hasattr(glyph, 'xMin'):
            hmtx[glyphName] = (hmtx[glyphName][0], glyph.xMin)


@singledispatch
def otf_to_ttf(ttFont, post_format=POST_FORMAT, **kwargs):
    if ttFont.sfntVersion != "OTTO":
        raise TTLibError("Not a OpenType font (bad sfntVersion)")
    assert "CFF " in ttFont

    glyphOrder = ttFont.getGlyphOrder()

    ttFont["loca"] = newTable("loca")
    ttFont["glyf"] = glyf = newTable("glyf")
    glyf.glyphOrder = glyphOrder
    glyf.glyphs = glyphs_to_quadratic(ttFont.getGlyphSet(), **kwargs)
    del ttFont["CFF "]
    if "VORG" in ttFont:
        del ttFont["VORG"]
    glyf.compile(ttFont)
    update_hmtx(ttFont, glyf)

    ttFont["maxp"] = maxp = newTable("maxp")
    maxp.tableVersion = 0x00010000
    maxp.maxZones = 1
    maxp.maxTwilightPoints = 0
    maxp.maxStorage = 0
    maxp.maxFunctionDefs = 0
    maxp.maxInstructionDefs = 0
    maxp.maxStackElements = 0
    maxp.maxSizeOfInstructions = 0
    maxp.maxComponentElements = max(
        len(g.components if hasattr(g, 'components') else [])
        for g in glyf.glyphs.values())
    maxp.compile(ttFont)

    post = ttFont["post"]
    post.formatType = post_format
    post.extraNames = []
    post.mapping = {}
    post.glyphOrder = glyphOrder
    try:
        post.compile(ttFont)
    except OverflowError:
        post.formatType = 3
        log.warning("Dropping glyph names, they do not fit in 'post' table.")

    ttFont.sfntVersion = "\000\001\000\000"


@otf_to_ttf.register(TTCollection)
def _(fonts, **kwargs):
    skip = 0
    for font in fonts:
        try:
            otf_to_ttf(font, **kwargs)
        except TTLibError as warn:
            skip += 1
            log.warning(warn)

    if skip == len(fonts):
        raise TTLibError("a Font Collection that has Not a OpenType font")


def run(path, options):
    try:
        font = TTFont(path, fontNumber=options.face_index)
        extension = '.ttf'
    except TTLibError:
        font = TTCollection(path)
        extension = '.ttc'

    if options.output and not os.path.isdir(options.output):
        output = options.output
    else:
        output = makeOutputFileName(path, outputDir=options.output,
                                    extension=extension,
                                    overWrite=options.overwrite)

    try:
        otf_to_ttf(font,
                   post_format=options.post_format,
                   max_err=options.max_error,
                   reverse_direction=options.reverse_direction)
    except TTLibError as warn:
        log.warning(f'"{path}" cannot be converted since it is {warn}.')
    else:
        font.save(output)


def main(args=None):
    parser = argparse.ArgumentParser()
    parser.add_argument("input", nargs='+', metavar="INPUT")
    parser.add_argument("-o", "--output")
    parser.add_argument("-e", "--max-error", type=float, default=MAX_ERR)
    parser.add_argument("--post-format", type=float, default=POST_FORMAT)
    parser.add_argument(
        "--keep-direction", dest='reverse_direction', action='store_false')
    parser.add_argument("--face-index", type=int, default=-1)
    parser.add_argument("--overwrite", action='store_true')
    options = parser.parse_args(args)

    if options.output and len(options.input) > 1:
        if not os.path.isdir(options.output):
            parser.error("-o/--output option must be a directory when "
                         "processing multiple fonts")

    files = chain.from_iterable(map(glob.glob, options.input))

    # Do not use "with" statement, or code coverage will malfunction.
    pool = Pool()
    try:
        pool.map(partial(run, options=options), files)
    finally:
        pool.close()
        pool.join()


if __name__ == "__main__":
    sys.exit(main())
```

```python
# otf2ttf.py

#!/usr/bin/env python
from __future__ import print_function, division, absolute_import

import argparse
import logging
import os
import sys

from cu2qu.pens import Cu2QuPen
from fontTools import configLogger
from fontTools.misc.cliTools import makeOutputFileName
from fontTools.pens.ttGlyphPen import TTGlyphPen
from fontTools.ttLib import TTFont, newTable


log = logging.getLogger()

# default approximation error, measured in UPEM
MAX_ERR = 1.0

# default 'post' table format
POST_FORMAT = 2.0

# assuming the input contours' direction is correctly set (counter-clockwise),
# we just flip it to clockwise
REVERSE_DIRECTION = True


def glyphs_to_quadratic(
        glyphs, max_err=MAX_ERR, reverse_direction=REVERSE_DIRECTION):
    quadGlyphs = {}
    for gname in glyphs.keys():
        glyph = glyphs[gname]
        ttPen = TTGlyphPen(glyphs)
        cu2quPen = Cu2QuPen(ttPen, max_err,
                            reverse_direction=reverse_direction)
        glyph.draw(cu2quPen)
        quadGlyphs[gname] = ttPen.glyph()
    return quadGlyphs


def otf_to_ttf(ttFont, post_format=POST_FORMAT, **kwargs):
    assert ttFont.sfntVersion == "OTTO"
    assert "CFF " in ttFont

    glyphOrder = ttFont.getGlyphOrder()

    ttFont["loca"] = newTable("loca")
    ttFont["glyf"] = glyf = newTable("glyf")
    glyf.glyphOrder = glyphOrder
    glyf.glyphs = glyphs_to_quadratic(ttFont.getGlyphSet(), **kwargs)
    del ttFont["CFF "]
    glyf.compile(ttFont)

    ttFont["maxp"] = maxp = newTable("maxp")
    maxp.tableVersion = 0x00010000
    maxp.maxZones = 1
    maxp.maxTwilightPoints = 0
    maxp.maxStorage = 0
    maxp.maxFunctionDefs = 0
    maxp.maxInstructionDefs = 0
    maxp.maxStackElements = 0
    maxp.maxSizeOfInstructions = 0
    maxp.maxComponentElements = max(
        len(g.components if hasattr(g, 'components') else [])
        for g in glyf.glyphs.values())
    maxp.compile(ttFont)

    post = ttFont["post"]
    post.formatType = post_format
    post.extraNames = []
    post.mapping = {}
    post.glyphOrder = glyphOrder
    try:
        post.compile(ttFont)
    except OverflowError:
        post.formatType = 3
        log.warning("Dropping glyph names, they do not fit in 'post' table.")

    ttFont.sfntVersion = "\000\001\000\000"


def main(args=None):
    configLogger(logger=log)

    parser = argparse.ArgumentParser()
    parser.add_argument("input", nargs='+', metavar="INPUT")
    parser.add_argument("-o", "--output")
    parser.add_argument("-e", "--max-error", type=float, default=MAX_ERR)
    parser.add_argument("--post-format", type=float, default=POST_FORMAT)
    parser.add_argument(
        "--keep-direction", dest='reverse_direction', action='store_false')
    parser.add_argument("--face-index", type=int, default=0)
    parser.add_argument("--overwrite", action='store_true')
    options = parser.parse_args(args)

    if options.output and len(options.input) > 1:
        if not os.path.isdir(options.output):
            parser.error("-o/--output option must be a directory when "
                         "processing multiple fonts")

    for path in options.input:
        if options.output and not os.path.isdir(options.output):
            output = options.output
        else:
            output = makeOutputFileName(path, outputDir=options.output,
                                        extension='.ttf',
                                        overWrite=options.overwrite)

        font = TTFont(path, fontNumber=options.face_index)
        otf_to_ttf(font,
                   post_format=options.post_format,
                   max_err=options.max_error,
                   reverse_direction=options.reverse_direction)
        font.save(output)


if __name__ == "__main__":
    sys.exit(main())
```

## fontTools

Link: <https://github.com/fonttools/fonttools>

> fontTools is a library for manipulating fonts, written in Python. The project includes the TTX tool, that can convert TrueType and OpenType fonts to and from an XML text format, which is also called TTX.


# Font Family

Generic font families <https://www.w3schools.com/css/css_font.asp>:

- **Serif** – small strokes at edges, formal and elegant
- **Sans-serif** – clean lines, modern and minimal
- **Monospace** – fixed width letters
- **Cursive** – handwriting style
- **Fantasy** – decorative/playful

## Serif vs Sans Serif

Sans Serif is simpler without serif. More detailed explanation can be found in the links below:

- <https://en.wikipedia.org/wiki/Sans-serif>
- <https://www.fonts.com/content/learning/fontology/level-1/type-anatomy/serif-vs-sans-for-text-in-print>
- <https://www.impactplus.com/blog/sans-serif-vs-serif-font-which-should-you-use-when>


# Fonts for Different Languages

## Chinese Fonts

> Adobe and Google create: 思源黑体（Source Han Sans）. ("简体中文方面，它支持中国国家标准GB 18030以及教育部于2013年颁布的《通用规范汉字表》里规定的所有汉字。")
> Adobe → Source Han Sans (思源黑体), Google → Noto Sans CJK (in Noto pan-Unicode font family).

Open font resources and licenses discussed:

- [GNU通用公共许可证](http://www.gnu.org/licenses/old-licenses/){:target="_blank"} (GNU General Public License)是GNU运动为保证其软件在后续的发展中仍保持开源开放而为其软件设立的“使用条款”。
- [SIL开放字体许可证](https://scripts.sil.org/OFL){:target="_blank"} (SIL Open Font License) 由SIL国际制定，初版于2005年发布，如今已是诸多开源字体的首选授权条款，这种许可证比 GPL 要开明，不会扩散到使用 SIL 字体的作品上，而只要求对字体作出修改后的作品本身要以相同许可分发。
- IPA开放字型授权条款 (IPA Open Font License)是日本「IPA」以符合「开放原始码促进会（Open Source Initiative）」于2009年开源定义的使用条款。

Additional resources:

- Some Chinese fonts: <https://github.com/wordshub/free-font>
- Some Chinese fonts: <https://github.com/yetist/open-chinese-fonts>
- <https://source.typekit.com/source-han-serif/?scid=social71226596>


# References

1. [Adobe AFDKO](https://github.com/adobe-type-tools/afdko/){:target="_blank"}
2. [fontTools](https://github.com/fonttools/fonttools){:target="_blank"}
3. [Google Fonts](https://fonts.google.com/){:target="_blank"}
4. [https://github.com/googlefonts](https://github.com/googlefonts){:target="_blank"}
5. [https://en.wikipedia.org/wiki/Sans-serif](https://en.wikipedia.org/wiki/Sans-serif){:target="_blank"}
6. [https://www.fonts.com/content/learning/fontology/level-1/type-anatomy/serif-vs-sans-for-text-in-print](https://www.fonts.com/content/learning/fontology/level-1/type-anatomy/serif-vs-sans-for-text-in-print){:target="_blank"}
7. [https://www.impactplus.com/blog/sans-serif-vs-serif-font-which-should-you-use-when](https://www.impactplus.com/blog/sans-serif-vs-serif-font-which-should-you-use-when){:target="_blank"}
