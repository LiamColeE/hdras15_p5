hdras15_p5
========

hdras15_p5ライブラリとは？
----
ProcessingからWi-fi経由でSony HDR-AS15のライブビュー画像を取得するライブラリ。640x360のライブビュー画像を取得することができます。

Processing
* http://processing.org/

Sony HDR-AS15
* http://www.sony.jp/actioncam/products/HDR-AS15/

How to use
----
1. あらかじめSony HDR-AS15を録画停止状態にしておく。
2. Sony HDR-AS15の自動スリープ機能を無効に設定する。
   * SETUP -> A.OFF -> OFF
3. Sony HDR-AS15のWi-fi機能を有効に設定する。
   * SETUP -> RMOTE -> ONに設定
4. PCからHDR-AS15のWi-fiに接続する。
   * SSIDが"DIRECT-????:HDR-AS15"のアクセスポイントへ接続。
5. ping 10.0.0.1を実行してHDR-AS15と接続できていることを確認する。
6. hdras15_p5ライブラリをlibrariesディレクトリへインストール。
   * ディレクトリ名はhdras15_p5でlibrariesディレクトリにコピーしてください。
7. サンプルスケッチを実行。

Tips?
----
PCからHDR-AS15のWi-fiに接続した際、たまにDHCPによるIPの取得に失敗することがあるので、10.0.1.5/16などのIPアドレスを手動で設定しておくといいかもしれないです。


Sample sketch for hdras15_p5 library
----
<pre>
import net.sabamiso.processing.hdras15.*;

HDRAS15 hdras15;

void setup() {
  size(640, 360);

  hdras15 = new HDRAS15();

  boolean rv;
  rv = hdras15.connect();
  if (rv == false) {
    println("error: connect() failed...");
    return;
  }
}
	
void draw() {
  PImage img = hdras15.getImage();
  if (img != null) {
    image(img, 0, 0);
  }
}
</pre>

How to create hdras15_p5.jar
----
* 1. hdras15_p5/libsディレクトリにProcessingのcore.jarを置く
* 2. hdras15_p5ディレクトリをEclipseで開く
* 3. net.sabamiso.processing.hdras15.TestMainを実行できるかどうか確認する
* 4. メニューのFile → Exportから"Runnable JAR File"を選択
* 5. Runnable JAR File Specificationとして次の内容を設定
  * "Launch Configuration" → 先ほど実行したTestMain
  * "Export destination" → "hdras15_p5\library\hdras15_p5.jar"
  * "Library Handling" → "Copy required libraries into a sub-folder..."
* 6. "Finish"ボタンを押すとhdras15_p5.jarが作成される

Copyright and license
----
Copyright (c) 2016 yoggy

Released under the [MIT license](LICENSE.txt)
