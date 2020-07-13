# PyxelUnicode

Pyxel用のファミコン風フォントビルダー

\[[日本語](./README.jp.md) | [中文](./README.sc.md) | [English](./README.md)\]

## イントロ
**PyxelUnicode** は[Pyxel](https://github.com/kitao/pyxel)用のファミコン風フォント生成器です。

[Pyxel](https://github.com/kitao/pyxel)は本当に素晴らしいゲームエンジンで、python初心者やゲームクリエイターにとって十分簡単で使いやすいと思います。私はこのゲームエンジンが大好きです。

しかし、Pyxelには一つの弱点があります。ビルドインされた`pyxel.text()`は基本のASCII文字しかサポートしていません。私がASCII文字以外の文字(つまりユニコード文字)を出力しようとすると、それらの文字を逐次デザインし、ゲーム内にハードコーディングしないといけません。この作業に本当にうんざりしています。なので、私はこのユーティリティライブラリを作りました。

また、こういった簡単なゲームはいつも子供が作るか、子供のために作られるものです。英語にまだなれていない子もいると思うので、こういったローカル言語表示へのサポートも未だに需要があると思います。

## デモ
![some image](./resources/pyxelunicode_demo.png)
![some image](./resources/pyxelunicode_detact_font_size.png)
![some image](./resources/pyxelunicode_unicode_combining_characters.png)

## インストール方法
本パッケージはpypiに公開されていて、以下のコマンドでインストールできます。
```
pip install pyxelunicode
```

## 使い方
以下の例で簡単な使い方を示します。
### 一般的な使い方

```python
import pyxel
from pyxelunicode import PyxelUnicode

pyxel.init(256, 256, caption="PyxelUnicode General Usage")
pyxel.cls(0)

font_path = "PATH_TO_YOUR_FONT_FILE.ttf" # ttfファイルのパス
font_size = 12  # このフォントが設計された大きさ(px単位)を代入する

# PyxelUnicodeのインスタンスを作成
pyuni = PyxelUnicode(font_path, font_size)
y = 20

# x:15, y:20の座標で'あのイーハトーヴォのすきとおった風' を表示させる
# 文字のデフォルトの色は7(白)、背景色のデフォルトはなし(透過)
pyuni.text(15, y, 'あのイーハトーヴォのすきとおった風')

# 以下のように現在つかているフォントの高さを取得できる
y += pyuni.font_height + 10

# (x,y)=(15,20+font_height+10)の座標で'夏でも底に冷たさをもつ青いそら' を表示させる
# 文字の色は3で背景色は5に設定する
pyuni.text(15, y, '夏でも底に冷たさをもつ青いそら', 3, 5)

pyxel.show()
```

### このフォントの一番適切な大きさを探す
もし、このフォントの最適なサイズがわからなければ、以下のコードでサイズごとの見た目を確認することができます。

```python
import pyxel
from pyxelunicode import PyxelUnicode

pyxel.init(256, 256, caption="PyxelUnicode find font size")
pyxel.cls(0)

font_path = "PATH_TO_YOUR_FONT_FILE.ttf"

y = 0
# このフォントが [8,10,12,14,16.....] のサイズの時の見え方を確認する
for s in range(8,36, 2):
    pyuni = PyxelUnicode(font_path, original_size=s)
    pyxel.text(0, y, str(s), 7)
    pyuni.text(10, y, s='DUMMY TEXT, dummy text.')
    y += pyuni.font_height

pyxel.show()
```

### treat with [合成文字](https://ja.wikipedia.org/wiki/%E7%B5%90%E5%90%88%E6%96%87%E5%AD%97)
一部の言語では(例えば、タイ語や存在していない日本語(あ゜い゛)など)、一つの文字に見えるが、実は基底文字と複数の結合文字で組み合わされているかもしれません。こういう場合は、どれが一つの文字として扱えばいいかをプログラムに教えないといけません。

時々変な出力になるかもしれませんので、改善策が分かれば、教えていただきたいです。

```python
import pyxel
from pyxelunicode import PyxelUnicode

pyxel.init(256, 256, caption="PyxelUnicode General Usage")
pyxel.cls(0)

font_path = "PATH_TO_YOUR_FONT_FILE.ttf"
font_size = 12  # set the most suitable size of this font

pyuni = PyxelUnicode(font_path, font_size)
# 文の中に結合文字があれば、この文全体を文字ごとに分割されたリストに直す必要がある。
# 文字列をただlist(string)で直すことはできない、必ず手動で全部の文字を分割する
pyuni.text(10, 50, ['นั่', 'น', 'คื', 'ā', 'ć', 'ģ'])

pyxel.show()

```

## ファミコン風フォントのソース

**<font color='red' >必ずライセンスを一読した上で利用してください</font>**

**ライセンスは下の関連ページにあります**

|フォント名|主要サポート文字|サイズ(px)|ダウンロード|関連ページ|
|:---:|:---:|:---:|:---:|:---:|
|Pixel UniCode|Greek<br>Cyrillic<br>Arabic|16|<a href="https://dl.dafont.com/dl/?f=pixel_unicode" download="">download</a>|<a href="https://fontstruct.com/fontstructions/show/908795/pixel_unicode">release page</a>|
|Zpix|Traditional Chinese<br>Simplified Chinese<br>Japanese|12|<a href="https://raw.githubusercontent.com/SolidZORO/zpix-pixel-font/master/dist/Zpix.ttf" download="">download</a>|<a href='https://github.com/SolidZORO/zpix-pixel-font'>github</a><br><a href="https://solidzoro.com/zpix-pixel-font/">review</a>|
|美咲フォント(8x8)|Japanese|8|<a href="https://littlelimit.net/arc/misaki/misaki_ttf_2019-10-19.zip" download="">download</a>|<a href="https://littlelimit.net/misaki.htm">home page</a>|
|PixelMplus|Japanese|10<br>12|<a href="https://ja.osdn.net/frs/redir.php?m=ymu&f=mix-mplus-ipa%2F58930%2FPixelMplus-20130602.zip" download="">download</a>|<a href="http://itouhiro.hatenablog.com/entry/20130602/font">blog</a>|
|Neo둥근모 프로젝트|Korean|16<br>32|<a href="https://github.com/Dalgona/neodgm/releases/download/v1.50/neodgm.ttf" download="">download</a>|<a href="https://dalgona.github.io/neodgm/">home page</a><br><a href="https://github.com/Dalgona/neodgm">github</a>|
|DungGeunMo(둥근모꼴+ Fixedsys)|Korean|16|<a href="http://cactus.tistory.com/attachment/cfile4.uf@994754395C3A4DC30E1F26.zip" download="">download</a>|<a href="https://cactus.tistory.com/193" >home page</a>|
|ZoodHarit4Bit|Thai|21|<a href="https://www.f0nt.com/download/zood/ZoodHarit4Bit-thai.ttf.zip" download="" >download</a>|<a href="https://www.f0nt.com/release/zoodharit4bit/" >release page</a>|



