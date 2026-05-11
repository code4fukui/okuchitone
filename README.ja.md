# okuchitone


ウェブカメラとリアルタイムのフェイストラッキングを使用して、口の動きを音に変換するウェブベースのシンセサイザーです。

[**ライブデモ**](https://code4fukui.github.io/okuchitone/)

## 仕組み

このアプリケーションは、ウェブカメラを使用し、MediaPipe Face Meshを介して顔のランドマークを検出します。そして、特定の唇の動きを音声パラメーターにマッピングします。

-   **音量:** 音の大きさは口の開き具合によって制御されます。上下の内側の唇（ランドマーク13と14）の垂直距離が大きいほど、音は大きくなります。
-   **音程:** 音の高さは、画面上の口の垂直位置によって決まります。頭を上下に動かすと音程が変わります。

## 特徴

-   口の形と位置に基づくリアルタイムの音声合成。
-   高精度な顔のランドマークトラッキングにMediaPipe Face Meshを活用。
-   最大5つの顔を同時にサポートし、それぞれが独立したサウンドチャンネルを持ちます。
-   音程と音量を動的に制御するため、Web Audio APIを介して音声を生成します。
-   ノコギリ波（sawtooth）またはカスタムの周期波形を選択可能。

## 使い方

1.  [デモページ](https://code4fukui.github.io/okuchitone/)にアクセスします。
2.  ブラウザにカメラへのアクセスを許可します。
3.  **SOUND START**ボタンをクリックして音声を初期化します。
4.  口を開閉したり、頭を上下に動かしたりして音をコントロールします。

### コントロール

-   **show original image**: カメラの生の映像の表示/非表示を切り替えます。
-   **mirror mode**: 映像を左右反転させます（デフォルトで有効）。
-   **backcamera mode**: 利用可能な場合、デバイスの背面カメラに切り替えます。

## 技術的な詳細

-   **フェイストラッキング:** このアプリは[MediaPipe Face Mesh](https://developers.google.com/mediapipe/solutions/vision/face_landmarker)を使用して、顔ごとに478個のランドマークを検出します。各フレームで唇のランドマークの距離と位置を計算し、音声を調整します。
-   **音声合成:** コアとなるオーディオエンジンである `XTone.js` は、[Web Audio API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API)を使用して `OscillatorNode`（音色用）と `GainNode`（音量用）を作成します。これらはユーザーの顔の動きを反映するために継続的に更新されます。

## ローカルでの実行

1.  このリポジトリをクローンします。
2.  ローカルのウェブサーバー（例: `python -m http.server` や VS Code の Live Server 拡張機能など）を使用して、プロジェクトディレクトリを配信します。
3.  提供されたローカルURLをモダンなウェブブラウザで開きます。

## 参考資料

-   このプロジェクトは、[MediaPipe test](https://code4fukui.github.io/mediapipe-test/) と [smaphotone](https://code4fukui.github.io/smaphotone/) のコンセプトにインスパイアされ、それらを基に構築されています。
-   Face Mesh ライブラリ情報: [Face Mesh - mediapipe](https://chuoling.github.io/mediapipe/solutions/face_mesh.html)

## ライセンス

このプロジェクトは MIT License の下で利用可能です。
