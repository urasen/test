<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>QR Code Reader</title>
  </head>
  <body>
    <h1>QR Code Reader</h1>
    <p>Scan a QR code to see the result:</p>
    <form>
      <input type="file" accept="image/*" capture="camera" id="qr-reader" onchange="readQRCode(this)">
    </form>
    <div id="result"></div>
    <script src="qr.js"></script>
    <script>
      function readQRCode(input) {
        if (input.files && input.files[0]) {
          var reader = new FileReader();
          reader.onload = function (e) {
            var img = new Image();
            img.onload = function () {
              var canvas = document.createElement('canvas');
              var ctx = canvas.getContext('2d');
              canvas.width = img.width;
              canvas.height = img.height;
              ctx.drawImage(img, 0, 0, canvas.width, canvas.height);
              var imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
              var qr = new QRCode();
              qr.callback = function (result) {
                document.getElementById('result').innerHTML = result;
              };
              qr.decode(imageData);
            };
            img.src = e.target.result;
          };
          reader.readAsDataURL(input.files[0]);
        }
      }
    </script>
  </body>
</html>
