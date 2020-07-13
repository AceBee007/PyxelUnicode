# PyxelUnicode

为pyxel设计的点阵字生成器

\[[中文](./README.sc.md) | [日本語](./README.jp.md) | [English](./README.md)\]

## 简介
**PyxelUnicode** 是一个为[Pyxel](https://github.com/kitao/pyxel)设计的点阵字生成器。

[Pyxel](https://github.com/kitao/pyxel)这个游戏引擎真的很不错。对于python初学者和游戏制作人来说，非常简单易用。我也很喜欢这个游戏引擎。

但是这个引擎有个很大的缺点。内含的`pyxel.text()`只支持ASCII码表上的文字，如果我想表示一些ASCII码表上不存在的文字（也就是unicode文字），我必须逐个设计这些文字的点阵版字体并把设计好的文字数据写进程序中。我真的烦透了这个事，所以我写了这个小程序来解决这个问题。

另外，一般是小孩子来用这个引擎做游戏，或者用这个引擎做的游戏是给小孩子玩的。而没有习惯使用英语的小孩子也有很大一部分，所以表示这些地方语言文字的需求还是有的。

## 演示
![some image](./resources/pyxelunicode_demo.png)
![some image](./resources/pyxelunicode_detact_font_size.png)
![some image](./resources/pyxelunicode_unicode_combining_characters.png)

## 如何安装
可以通过以下的pip指令安装
```
pip install pyxelunicode
```

## 如何使用
以下的代码示范了如何使用此模组
### 通常的用法

```python
import pyxel
from pyxelunicode import PyxelUnicode

pyxel.init(256, 256, caption="PyxelUnicode General Usage")
pyxel.cls(0)

font_path = "PATH_TO_YOUR_FONT_FILE.ttf" # 填写本地ttf字体文件的路径
font_size = 12  # 点阵字体一般存在一个最适应的大小，请填写于此

# 生成一个pyxelunicode的实例
pyuni = PyxelUnicode(font_path, font_size)
y = 20

# 在(x,y)=(15,20)的位置表示这段文字
# 默认的字体颜色是7（白色），默认的背景色是无色（不填充）
pyuni.text(15, y, '星斗稀，鐘鼓歇，簾外曉鶯殘月。')

# 你可以通过以下方式获取这个字体的高度
y += pyuni.font_height + 10

# 在(x,y)=(15,20+font_height+10)的位置表示这段文字
# 使用3号颜色作为文字颜色，使用5号颜色作为背景填充色
pyuni.text(15, y, '兰露重，柳风斜，满庭堆落花。', 3, 5)

pyxel.show()
```

### 寻找最适应的字体大小
如果你不知道现在使用的字体的最适应大小是多少，可以尝试以下的代码。他会表示出各个大小设定时的文字看起来的样子。

```python
import pyxel
from pyxelunicode import PyxelUnicode

pyxel.init(256, 256, caption="PyxelUnicode find font size")
pyxel.cls(0)

font_path = "PATH_TO_YOUR_FONT_FILE.ttf"

y = 0
# 检查大小是[8,10,12,14,16.....]时字体看起来的样子
for s in range(8,36, 2):
    pyuni = PyxelUnicode(font_path, original_size=s)
    pyxel.text(0, y, str(s), 7)
    pyuni.text(10, y, s='DUMMY TEXT, dummy text.')
    y += pyuni.font_height

pyxel.show()
```

### 如何处理[组合字符](https://zh.wikipedia.org/wiki/%E7%B5%84%E5%90%88%E5%AD%97%E7%AC%A6)
在某些语言中(例如：中文异体字，泰语，不符合常规的日语)，看起来是一个文字但其实是由一个主要字符和多个附加字符组成的。在这个情况下，你必须告诉程序哪个字是该被看作一个字的。

在应对这些字符时可能不能完美地运行，原因不明，如果你知道任何改进方法请告诉我。

```python
import pyxel
from pyxelunicode import PyxelUnicode

pyxel.init(256, 256, caption="PyxelUnicode General Usage")
pyxel.cls(0)

font_path = "PATH_TO_YOUR_FONT_FILE.ttf"
font_size = 12  # 点阵字体一般存在一个最适应的大小，请填写于此

pyuni = PyxelUnicode(font_path, font_size)
# 不实用字符串，使用组合字符的列表来取而代之
# 组合字符不能用list(string)来简单的转换，请手动设定
pyuni.text(10, 50, ['นั่', 'น', 'คื', 'ā', 'ć', 'ģ'])

pyxel.show()

```

## Unicode点阵字体资源

**<font color='red' >使用前请仔细阅读使用许可</font>**

**你可以在以下的关联页面中找到使用许可**

|字体名称|主要支持语言|最适字号(px)|下载|相关页面|
|:---:|:---:|:---:|:---:|:---:|
|Pixel UniCode|Greek<br>Cyrillic<br>Arabic|16|<a href="https://dl.dafont.com/dl/?f=pixel_unicode" download="">download</a>|<a href="https://fontstruct.com/fontstructions/show/908795/pixel_unicode">release page</a>|
|Zpix|Traditional Chinese<br>Simplified Chinese<br>Japanese|12|<a href="https://raw.githubusercontent.com/SolidZORO/zpix-pixel-font/master/dist/Zpix.ttf" download="">download</a>|<a href='https://github.com/SolidZORO/zpix-pixel-font'>github</a><br><a href="https://solidzoro.com/zpix-pixel-font/">review</a>|
|美咲フォント(8x8)|Japanese|8|<a href="https://littlelimit.net/arc/misaki/misaki_ttf_2019-10-19.zip" download="">download</a>|<a href="https://littlelimit.net/misaki.htm">home page</a>|
|PixelMplus|Japanese|10<br>12|<a href="https://ja.osdn.net/frs/redir.php?m=ymu&f=mix-mplus-ipa%2F58930%2FPixelMplus-20130602.zip" download="">download</a>|<a href="http://itouhiro.hatenablog.com/entry/20130602/font">blog</a>|
|Neo둥근모 프로젝트|Korean|16<br>32|<a href="https://github.com/Dalgona/neodgm/releases/download/v1.50/neodgm.ttf" download="">download</a>|<a href="https://dalgona.github.io/neodgm/">home page</a><br><a href="https://github.com/Dalgona/neodgm">github</a>|
|DungGeunMo(둥근모꼴+ Fixedsys)|Korean|16|<a href="http://cactus.tistory.com/attachment/cfile4.uf@994754395C3A4DC30E1F26.zip" download="">download</a>|<a href="https://cactus.tistory.com/193" >home page</a>|
|ZoodHarit4Bit|Thai|21|<a href="https://www.f0nt.com/download/zood/ZoodHarit4Bit-thai.ttf.zip" download="" >download</a>|<a href="https://www.f0nt.com/release/zoodharit4bit/" >release page</a>|



