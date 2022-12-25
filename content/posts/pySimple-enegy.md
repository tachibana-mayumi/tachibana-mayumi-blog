---
title: "E:株式会社エナジーというプログラムをpySimpleGUIで書いてみる"
date: 2022-12-24
categories: ["python"]
tags: ["python"]
menu: main
---

前回に作成した記事に対して「PySimpleGUIというライブラリが使いやすい」というコメントを頂いた。
初心者なのでこういったライブラリの紹介は本当にありがたいです。
alohaをハワイの挨拶、といった前回作ったプログラムも合わせて改良してみた。

今回はPySimpleGUIを使って以下のプログラムを作ってみた。

立花真由美→a001、立花理香→a002、みたいな感じで社員番号を返すもの
日本→こんにちは、アメリカ→Hello、ハワイ→alohaみたいな感じで地域名を入れると挨拶を返すもの
A→株式会社アンペア、E→株式会社エナジーといった感じでアルファベットから取引先を返すもの

### ハワイ→alohaと返すようなプログラム(PySimpleGUI版)
日本→こんにちは、アメリカ→Hello、ハワイ→alohaと返すようなプログラム。
今回は合わせて社員番号から社員を返すプログラムも作ってみた。
確かにPySimpleGUIはコマンドがわかりやすかったり、コードがシンプルになってとてもいい感じ。

```python
import PySimpleGUI as sg

#　社員リスト
workers = {'a001':'立花真由美','a002':'立花理香','a003':'立花慎之介'}

#　社員番号を確認するウィンドウ
w_workers = [[sg.Text('社員番号を入れてください')],
             [sg.Input(key='-社員番号-')],
             [sg.Button('決定')]]

w_window = sg.Window('社員番号確認',w_workers)

while True:
    #　ウィンドウを読み込む
    w_event, w_values = w_window.read()
    w_input_value = w_values['-社員番号-']

    #　該当する社員番号がある場合は名前を表示、なければここでプログラムを終了
    if w_input_value in workers:
        sg.popup(f'ようこそ{workers.get(w_input_value)}さん')
        if (w_event == sg.WIN_CLOSED) or (w_event == sg.popup_ok):
            break
    else:
        sg.popup('該当する社員はいません')
        exit()

    break


#　挨拶(日本はこんにちは、アメリカはHello、ハワイはaloha)
hello_dict = {"日本":"こんにちは","ハワイ":"aloha", "アメリカ":"Hello", "中国":"ニーハオ"}

#　文字を表示する(三行目は結果を返す用の空欄)
w_text =[[sg.Text('地域名を入れると挨拶を返します(終了は右上の✕ボタンから)     ')],
         [sg.Text('地域'), sg.Input(key='-地域名-')],
         [sg.Text('', key = '-結果-')],
         [sg.Button('決定')]]

#　ウィンドウのインスタンスを作る
window = sg.Window('世界の挨拶',w_text)

while True:
    #　ウィンドウを読み込む(event:ボタン、values:入力したもの)
    event, values = window.read()
    input_value = values['-地域名-']

    if event == sg.WIN_CLOSED:
        break

    #　決定を押したら結果を返す(3行目の空き行に表示)
    if event == '決定':
        if (input_value in hello_dict):
            window['-結果-'].update(f'地域名：{input_value}, 挨拶：{hello_dict.get(input_value)}')
        else:
            window['-結果-'].update(f'{input_value}の挨拶はありません')
      
#　画面を閉じる
window.close()
```

### E→株式会社エナジーといった頭文字から会社名を出すプログラム(PySimpleGUI版)
前回と同様に頭文字から会社名を表示するプログラム。
仕事なのでちゃんと「株式会社」も入れた。
株式会社アンペア、株式会社エナジー、クーロン株式会社みたいに科学関係の単語を使った架空の会社名にしてみた。

```python
import PySimpleGUI as sg

#　会社名(株式会社エナジー、クーロン、アンペア)
company_dict = {"A":"株式会社アンペア","C":"株式会社クーロン", "E":"株式会社エナジー"}

#　文字を表示する(三行目は結果を返す用の空欄)
w_text =[[sg.Text('頭文字から企業名を表示します(終了は右上の✕ボタンから)     ')],
         [sg.Text('頭文字'), sg.Input(key='-頭文字-')],
         [sg.Text('', key = '-結果-')],
         [sg.Button('決定')]]

#　ウィンドウのインスタンスを作る
window = sg.Window('取引先の照合',w_text)

while True:
    #ウィンドウを読み込む(event:ボタン、values:入力したもの)
    event, values = window.read()
    input_value = values['-頭文字-']

    if event == sg.WIN_CLOSED:
        break

    #　決定を押したら結果を返す(3行目の空き行に表示)
    if event == '決定':
        if (input_value in company_dict):
            window['-結果-'].update(f'頭文字：{input_value}, 企業名：{company_dict.get(input_value)}')
        else:
            window['-結果-'].update(f'頭文字：{input_value}の企業はありません')
      
#　画面を閉じる
window.close()
```