# PyxelUnicode

a unicode pixel font builder for pyxel

\[[English](./README.md) | [日本語](./README.jp.md) | [中文](./README.sc.md)\]

## Introduction
**PyxelUnicode** is a pixel style unicode font builder for [Pyxel](https://github.com/kitao/pyxel).

[Pyxel](https://github.com/kitao/pyxel) is a really good game engine. It's simple and easy enough for a python beginner and game creator. I like it very much.

But there's a problem. The built-in function `pyxel.text()` only supports the basic ASCII characters. If I want to print some characters which are not in ASCII table(generally, Unicode character), I have to design and make a hard coding for these characters. This work really annoying me a lot. So I made this little utility library to do this work instead.

These kinds of simple games are always made by or for some who are young, they may not be familiar with English. The local language text display is needed.

## Demo
![some image](./resources/pyxelunicode_demo.png)
![some image](./resources/pyxelunicode_detact_font_size.png)
![some image](./resources/pyxelunicode_unicode_combining_characters.png)

## How To Install
Install PyxelUnicode with the following pip command
```
pip install pyxelunicode
```

## How To Use
The examples below show you how to use it.
### general usage

```python
import pyxel
from pyxelunicode import PyxelUnicode

pyxel.init(256, 256, caption="PyxelUnicode General Usage")
pyxel.cls(0)

font_path = "PATH_TO_YOUR_FONT_FILE.ttf"
font_size = 12  # set the most suitable size of this font

# make a pyxelunicode instance
pyuni = PyxelUnicode(font_path, font_size)
y = 20

# print the text 'HELLO PyxelUnicode' at (x,y)=(15,20), 
# default fg_color is 7 (white) and no background color
pyuni.text(15, y, 'HELLO PyxelUnicode!')

# you can get font height as below
y += pyuni.font_height + 10

# print the text 'BYE PyxelUnicode' at (x,y)=(15,20+font_height+10), 
# use foreground color 3, background color 5
pyuni.text(15, y, 'BYE PyxelUnicode!', 3, 5)

pyxel.show()
```

### find the most suitable font size
If you do not know the most suitable font size, try the code below. It shows the font size and how it looks.

```python
import pyxel
from pyxelunicode import PyxelUnicode

pyxel.init(256, 256, caption="PyxelUnicode find font size")
pyxel.cls(0)

font_path = "PATH_TO_YOUR_FONT_FILE.ttf"

y = 0
# check how it looks like when the size are [8,10,12,14,16.....]
for s in range(8,36, 2):
    pyuni = PyxelUnicode(font_path, original_size=s)
    pyxel.text(0, y, str(s), 7)
    pyuni.text(10, y, s='DUMMY TEXT, dummy text.')
    y += pyuni.font_height

pyxel.show()
```

### treat with [unicode-combining-characters](https://en.wikipedia.org/wiki/Combining_character)
In some languages(e.g. Cyrillic, Thai, invalid Japanese), the characters may be made by a main character (base character) and several diacritics. In this case, you have to tell the program which character is a unicode combining character.

It may not work perfectly, and I do not know why. I welcome any kinds of imporvement.

```python
import pyxel
from pyxelunicode import PyxelUnicode

pyxel.init(256, 256, caption="PyxelUnicode General Usage")
pyxel.cls(0)

font_path = "PATH_TO_YOUR_FONT_FILE.ttf"
font_size = 12  # set the most suitable size of this font

pyuni = PyxelUnicode(font_path, font_size)
# use a list of unicode-combining-characters as string
pyuni.text(10, 50, ['นั่', 'น', 'คื', 'ā', 'ć', 'ģ'])

pyxel.show()

```

## unicode pixel font sources

**<font color='red' >PLEASE READ THE LINCESES BEFORE USING</font>**

**You could find the licenses in their relative pages.**

|Font Name|Mainly Supported Characters|size(px)|Download|Relative Pages|
|:---:|:---:|:---:|:---:|:---:|
|Pixel UniCode|Greek<br>Cyrillic<br>Arabic|16|<a href="https://dl.dafont.com/dl/?f=pixel_unicode" download="">download</a>|<a href="https://fontstruct.com/fontstructions/show/908795/pixel_unicode">release page</a>|
|Zpix|Traditional Chinese<br>Simplified Chinese<br>Japanese|12|<a href="https://raw.githubusercontent.com/SolidZORO/zpix-pixel-font/master/dist/Zpix.ttf" download="">download</a>|<a href='https://github.com/SolidZORO/zpix-pixel-font'>github</a><br><a href="https://solidzoro.com/zpix-pixel-font/">review</a>|
|美咲フォント(8x8)|Japanese|8|<a href="https://littlelimit.net/arc/misaki/misaki_ttf_2019-10-19.zip" download="">download</a>|<a href="https://littlelimit.net/misaki.htm">home page</a>|
|PixelMplus|Japanese|10<br>12|<a href="https://ja.osdn.net/frs/redir.php?m=ymu&f=mix-mplus-ipa%2F58930%2FPixelMplus-20130602.zip" download="">download</a>|<a href="http://itouhiro.hatenablog.com/entry/20130602/font">blog</a>|
|Neo둥근모 프로젝트|Korean|16<br>32|<a href="https://github.com/Dalgona/neodgm/releases/download/v1.50/neodgm.ttf" download="">download</a>|<a href="https://dalgona.github.io/neodgm/">home page</a><br><a href="https://github.com/Dalgona/neodgm">github</a>|
|DungGeunMo(둥근모꼴+ Fixedsys)|Korean|16|<a href="http://cactus.tistory.com/attachment/cfile4.uf@994754395C3A4DC30E1F26.zip" download="">download</a>|<a href="https://cactus.tistory.com/193" >home page</a>|
|ZoodHarit4Bit|Thai|21|<a href="https://www.f0nt.com/download/zood/ZoodHarit4Bit-thai.ttf.zip" download="" >download</a>|<a href="https://www.f0nt.com/release/zoodharit4bit/" >release page</a>|



