# OWASP Mutillidate Ⅱ

## OWASP 2017

### A1 Injection(SQL)

#### SQLi Extract Data

##### User Info(SQL)
  - Level0
    - ノーガード
    1. nameに「'」入れてみる
    1. エラーメッセージ表示される
    1. nameに「' or true ; -- 」入れる
    1. ユーザ一覧取得

  - level1
    - 画面側だけで防ごうとする
    1. name/passに任意の値入れる
    1. 通信を止めて、nameの値に「'」入れてみる
    1. エラーメッセージ表示される(level0と同じ)
    1. 通信を止めて、nameに「' or true ; -- 」入れる
    1. ユーザ一覧取得

  - level5
    - スキル不足で突破できない


  - 下記セクションは原理的に同じっぽいの割愛
    - SQLi Bypass Authentication
    - Insert Injection
    - Blind SQL via timing (sleepコマンドを使わせたい?)
