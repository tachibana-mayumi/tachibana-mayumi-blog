---
title: "E:株式会社エナジー〇〇といった頭文字と対応させるプログラム"
date: 2022-12-24
categories: ["python"]
tags: ["python"]
menu: main
---

↓↓昔に作ったコードのメモ。
会社の研修でPythonを使うことになったので簡単な操作のメモ。
今回はTkinterを用いた入力、ウィンドウ表示について。
(簡単すぎるメモだけど、何も言わないでください)

立花真由美→a001、立花理香→a002、みたいな感じで社員番号を返すものもこれから作る。

## aloha→ハワイのように地域名に対応する挨拶を表示する
日本なら「こんにちは」、アメリカなら「Hello」と表示されるプログラム。
ハワイなら「aloha」とかも入れてみた。
(ハワイ、というか南国に行きたいから)

```python
from tkinter import *
from tkinter import ttk
from tkinter import messagebox

#関数
def get_text(ref_dict):
    text_input = text.get()
    print("地域:",text_input)
    print("挨拶:",ref_dict[text_input])
    messagebox.showinfo("確認", "地域:"+text_input+" 挨拶:"+ref_dict[text_input])
    

#挨拶(日本はこんにちは、アメリカはHello、ハワイはaloha)
hello_dict = {"日本":"こんにちは","ハワイ":"aloha", "アメリカ":"Hello", "中国":"ニーハオ"}

root = Tk()
root.title("世界の挨拶")

#オブジェクト
label = ttk.Label(root, text = "地域名を入れると挨拶を返します")
label.pack()

#テキストの入力
text = StringVar()
entry = ttk.Entry(root,textvariable=text)
entry.pack()

#OKを押すとテキストを取得
button = ttk.Button(root,text="OK",command=lambda:get_text(hello_dict))
button.pack()

#ウィンドウを表示し続ける
root.mainloop()
```
まだやっていないこと
・OKを押したらウインドウが閉じる
・辞書に入っていない単語を入れたときにエラーを返す

## E：株式会社エナジー〇〇といった頭文字から会社名を出す
似たような取り組みで、頭文字から会社名を表示するようにした。
一応仕事なのでちゃんと「株式会社」も入れた。
株式会社アンペア、株式会社エナジー、クーロン株式会社みたいに科学関係の単語を使った架空の会社名にしてみた。

```python
from tkinter import *
from tkinter import ttk
from tkinter import messagebox

#関数定義
def get_text(ref_dict):
    text_input = text.get()
    print("頭文字:",text_input)
    print("会社名:",ref_dict[text_input])
    messagebox.showinfo("確認", "頭文字:"+text_input+" 会社名:"+ref_dict[text_input])
    

#会社名(株式会社エナジー、クーロン、アンペア)
company_dict = {"A":"株式会社アンペア","C":"クーロン株式会社", "E":"株式会社エナジー"}

root = Tk()
root.title("各企業の頭文字")

#オブジェクト
label = ttk.Label(root, text = "頭文字から企業名を表示します")
label.pack()

#テキストの入力
text = StringVar()
entry = ttk.Entry(root,textvariable=text)
entry.pack()

#OKを押すとテキストを取得
button = ttk.Button(root,text="OK",command=lambda:get_text(company_dict))
button.pack()

#ウィンドウを表示し続ける
root.mainloop()
```

tkinterはインストールせずとも使えるし、動作も軽いので便利ではある。
ただ、ウィンドウのサイズの指定方法がわからなかったり、デザインが簡素すぎるのでちょっととっつきにくい。

もう少し手軽にウィンドウを表示させるライブラリとかあるのかな。
要調査。