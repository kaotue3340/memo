# .NET Framework がコンパイルされて動くまで
## 概要

## 昔今までの実行環境

## .NET Framweorkの利点

## .NET Frameworkの挙動

### ソースコードのマネージモジュールへのコンパイル
![image](https://user-images.githubusercontent.com/56548030/182310217-fd6bc395-0095-4740-a3e3-9ef91fd608a9.png)

* PE32/PE32+ヘッダ(Portable Executable)<br>
  このプログラムが動作可能なマシンの種類などが記載。<br>
  PE32かPE32+かは、ビルド時のターゲットによって変わる。<br>
  * PE32 : AnyCPU<br>
  * PE32+ : x64<br>
![image](https://user-images.githubusercontent.com/56548030/182280961-7e5011d3-b040-4cd4-aa2c-1383110bbeff.png)
* CLRヘッダ<br>
必要となるCLRバージョン、マネージモジュールのエントリポイントメソッド（Mainメソッド）の情報などが記載。<br>
* メタデータ<br>
  コード内で定義されたクラスや型、インタフェースなどコードに関する情報が記載。<br>
  VisualStudioのIntelliSense機能はメタデータを解析して、型が提供するメソッド、プロパティ、イベント、およびフィールドを（メソッドの場合はさらに、メソッドが必要とするパラメーターも）通知する。
* ILコード<br>
  コンパイラが生成したコード。実行時にCLRはILをネイティブのCPU命令にコンパイルする。<br>
  
### マネージモジュールの結合によるアセンブリの生成
![image](https://user-images.githubusercontent.com/73086030/182321173-668034ca-eaef-4e97-ad0a-fe346557cdce.png)

## 用語
* CLR (Common Language Runtime)<br>
マネージドコードの取得と機械語へのコンパイルと実行し<br>
それに加えて、メモリ管理、アセンブリのロード、例外処理、スレッドの同期などを処理する。<br>

* マネージドコードとアンマネージドコード<br>
  * マネージドコード：IL(中間言語)のみで構成され、特定の機種やOSなどに依存するコードを含まないプログラム。<br>
  * アンマネージコード：CLRが担当している、OSへの命令を直接記載したプログラム。<br>

* CLR対応のコンパイラ一覧<br>
  * Microsoft開発<br>
    * C#、VisualBasic、F#、ILアセンブラ<br>
    * C++<br>
      C++コンパイラは、開発者がマネージコードとアンマネージコードの両方を記述して、単一のモジュールとして出力できる唯一のコンパイラ。<br>
      開発者は既存のネイティブのC/C++コードをマネージコードから使用でき、既存のコードにマネージ型を組み入れていくことができる。<br
    * IronPython<br>
      .NET Framework上で動作するPythonの実装。2006年9月5日に初版がリリースされた。<br>
      長らくPythonの２系（※サポート終了）にしか対応していなかったが、
      最近になって３系対応のバージョンがリリースされたが、これもPython自体はサポート終了している。（※2022年8月時点で3.4.0-beta）<br>
      https://ironpython.net/
    * IronRuby<br>
      .NET Framework上で動作する、マイクロソフトによるRubyの実装。<br>
      2011年3月13日バージョン1.1.3リリースを最後に更新なし。<br>
      http://ironruby.net/
  * 他社開発<br>
　　Ada、APL、Caml、COBOL、Eiffel、Forth、Fortran、Haskell、Lexico、LISP、LOGO、Lua、Mercury、ML、Mondrian、Oberon、Pascal、Perl、PHP、Prolog、RPG、Scheme、Smalltalk、Tcl/Tk<br>

## 参考文献
* CLR 【Common Language Runtime】 共通言語ランタイムとは<br>
https://e-words.jp/w/CLR.html
