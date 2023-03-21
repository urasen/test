<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>QRコードリーダー</title>
    <script src="https://rawgit.com/LazarSoft/jsqrcode/master/src/qr_packed.js"></script>
    <style>
      #qr-canvas {
        width: 100%;
        height: 100%;
        margin: auto;
      }
    </style>
  </head>
  <body>
    <h1>QRコードリーダー</h1>
    <p>QRコードをカメラでスキャンしてください。</p>
    <video id="video"></video>
    <canvas id="qr-canvas"></canvas>
    <script type="text/javascript">
      var video = document.querySelector("#video");
      var canvas = document.querySelector("#qr-canvas");
      var context = canvas.getContext("2d");
      var qrResult = document.querySelector("#qr-result");
      var decodeButton = document.querySelector("#decode-button");
      var scanning = false;

      // QRコードを解析する関数
      function decode() {
        context.drawImage(video, 0, 0, canvas.width, canvas.height);
        scanning = true;
        qrcode.decode();
      }

      // カメラから映像をストリーミングする関数
      function startCamera() {
        navigator.mediaDevices.getUserMedia({video: { facingMode: "environment" }})
          .then(function(stream) {
            video.srcObject = stream;
            video.setAttribute("playsinline", true); //iOS用
            video.play();
            requestAnimationFrame(tick);
          });
      }

      // スキャン中のQRコードを解析する関数
      function tick() {
        if (scanning) {
          decode();
        }
        requestAnimationFrame(tick);
      }

      // QRコードが解析されたときに呼び出されるコールバック関数
      function onDecodeComplete(result) {
        scanning = false;
        alert(result);
        // ここで、解析された情報を表示するためのコードを記述する
      }

      // QRコード解析のためのオブジェクトを作成する
      var qrcode = new QRCodeDecoder();

      // QRコード解析のためのコールバック関数を登録する
      qrcode.callback = onDecodeComplete;

      // カメラから映像を取得する
      startCamera();
    </script>
  </body>
</html>
