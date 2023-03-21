<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>QRコードリーダー</title>
  </head>
  <body>
    <h1>QRコードリーダー</h1>
    <p>QRコードを読み取るには、以下のボタンをクリックしてください。</p>
    <button onclick="scanQR()">QRコードをスキャン</button>
    <p id="qrResult"></p>
    <script src="https://rawgit.com/LazarSoft/jsqrcode/master/src/qr_packed.js"></script>
    <script>
      function scanQR() {
        if (typeof window.FileReader === 'undefined') {
          alert('このブラウザはQRコードのスキャンに対応していません。');
          return;
        }
        var fileInput = document.createElement('input');
        fileInput.setAttribute('type', 'file');
        fileInput.setAttribute('accept', 'image/*');
        fileInput.onchange = function () {
          var reader = new FileReader();
          reader.onload = function (event) {
            var image = new Image();
            image.onload = function () {
              var canvas = document.createElement('canvas');
              canvas.width = image.width;
              canvas.height = image.height;
              canvas.getContext('2d').drawImage(image, 0, 0, image.width, image.height);
              var imageData = canvas.getContext('2d').getImageData(0, 0, canvas.width, canvas.height);
              var code = jsQR(imageData.data, imageData.width, imageData.height);
              if (code) {
                document.getElementById('qrResult').innerHTML = 'QRコードの内容: ' + code.data;
              } else {
                alert('QRコードが見つかりませんでした。');
              }
            };
            image.src = event.target.result;
          };
          reader.readAsDataURL(fileInput.files[0]);
        };
        fileInput.click();
      }
    </script>
  </body>
</html>
