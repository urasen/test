<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>QRコードリーダー</title>
    <script src="https://rawgit.com/LazarSoft/jsqrcode/master/src/qr_packed.js"></script>
    <style>
      #qr-canvas {
        width: 100%;
        height: 100%;
      }
    </style>
  </head>
  <body>
    <div id="qr-reader">
      <div id="qr-canvas"></div>
    </div>
    <script>
      // カメラから読み取ったQRコードを解析して情報を表示する関数
      function onQRCodeScanned(result) {
        // 解析結果を表示する要素を取得する
        var qrOutput = document.getElementById('qr-output');
        // 解析結果を表示する
        qrOutput.innerHTML = result;
      }

      // QRコードリーダーを初期化する関数
      function initQRCodeReader() {
        // QRコードを解析するためのオブジェクトを作成する
        var qr = new QCodeDecoder();
        // QRコードを解析したときに呼ばれるコールバック関数を設定する
        qr.decodeFromCamera(document.getElementById('qr-canvas'), onQRCodeScanned);
      }

      // QRコードリーダーを初期化する
      initQRCodeReader();
    </script>
  </body>
</html>
