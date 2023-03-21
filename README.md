<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>QR Code Scanner</title>
    <script src="https://rawgit.com/schmich/instascan-builds/master/instascan.min.js"></script>
  </head>
  <body>
    <video id="camera" width="300" height="200"></video>
    <div id="result"></div>
    <script>
      let scanner = new Instascan.Scanner({ video: document.getElementById('camera') });
      scanner.addListener('scan', function (content) {
        document.getElementById('result').innerHTML = content;
      });
      Instascan.Camera.getCameras().then(function (cameras) {
        if (cameras.length > 0) {
          scanner.start(cameras[0]);
        } else {
          console.error('No cameras found.');
        }
      }).catch(function (e) {
        console.error(e);
      });
    </script>
  </body>
</html>
