# G5 CMakeListsテンプレート

グループ5のプロジェクトでコンパイルのためにビルドツールの[CMake](https://cmake.org/)を使うときに必要な設定ファイルのテンプレートです。

## 使い方

まず、このリポジトリの中のCMakeLists.txtをコピーし、各プロジェクトに合わせて内容を変えます。

作ったソフトをコンパイルするときは、まずプロジェクト内に `build` というディレクトリを作り、そこに入ります。
```bash
# プロジェクトのルートディレクトリで
mkdir build
cd build
```

初めてコンパイルするときだけ以下を実行します。2回目以降はCMakeが自動で行ってくれるので不要です。

ライブラリが足りないときはここでエラー表示が出るので、足りないライブラリをインストールします。

```bash
cmake ..
```

以上で準備が終わり、Makefileが作られます。後はいつもどおり `make` でコンパイルします。

```
make
```

実行ファイルは `build` ディレクトリの中に作られます。

作ったものを削除する `make clean` も自動で定義されるので、実行できます。

## 参考文献

比較的短いCMakeの説明はこのあたり。

* januswel『[CMake 簡易まとめ](https://qiita.com/janus_wel/items/a673793d448c72cbc95e)』
* 寺村俊紀『[ごく簡単なcmakeの使い方](https://qiita.com/termoshtt/items/539541c180dfc40a1189)』

公式ドキュメント（英語）。

* [Documentation | CMake](https://cmake.org/documentation/)
