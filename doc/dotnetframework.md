# .NET Framework がコンパイルされて動くまで
## 概要

## 用語
* CLR (Common Language Runtime)<br>
マネージドコードの取得と機械語へのコンパイルと実行し<br>
それに加えて、メモリ管理、アセンブリのロード、例外処理、スレッドの同期などを処理する<br>

* マネージドコードとアンマネージドコード<br>
マネージドコード：IL(中間言語)のみで構成され、特定の機種やOSなどに依存するコードを含まないプログラム<br>
アンマネージコード：CLRが担当している、OSへの命令を直接記載したプログラム<br>

* CLR対応のコンパイラ一覧<br>
  * Microsoft開発<br>
    * C++、C#、VisualBasic、F#、ILアセンブラ<br>
    * IronPython<br>
      .NET Framework上で動作するPythonの実装。2006年9月5日に初版がリリースされた。<br>
      長らくPythonの２系（※サポート終了）にしか対応していなかったが、
      最近になって３系対応のバージョンがリリースされたが、これもPython自体はサポート終了している（※2022年8月時点で3.4.0-beta）<br>
      https://ironpython.net/
    * IronRuby<br>
      .NET Framework上で動作する、マイクロソフトによるRubyの実装。<br>
      2011年3月13日バージョン1.1.3リリースを最後に更新なし<br>
      http://ironruby.net/
  * 他社開発<br>
　　Ada、APL、Caml、COBOL、Eiffel、Forth、Fortran、Haskell、Lexico、LISP、LOGO、Lua、Mercury、ML、Mondrian、Oberon、Pascal、Perl、PHP、Prolog、RPG、Scheme、Smalltalk、Tcl/Tk<br>

## 参考文献
* CLR 【Common Language Runtime】 共通言語ランタイムとは<br>
https://e-words.jp/w/CLR.html
