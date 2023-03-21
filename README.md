<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8">
	<title>QRコード読み取り</title>
</head>
<body>
	<h1>QRコード読み取り</h1>
	<p>QRコードをカメラに向けてください。</p>
	<video id="qr-video" width="300" height="300"></video>
	<div id="qr-result"></div>

	<script src="https://rawgit.com/schmich/instascan-builds/master/instascan.min.js"></script>
	<script>
		// カメラの起動
		const scanner = new Instascan.Scanner({ video: document.getElementById('qr-video') });
		scanner.addListener('scan', function (content) {
			// QRコードからの情報を取得
			const qrResult = document.getElementById('qr-result');
			qrResult.innerHTML = content;
			// カメラを停止
			scanner.stop();
		});
		Instascan.Camera.getCameras().then(function (cameras) {
			if (cameras.length > 0) {
				scanner.start(cameras[0]);
			} else {
				console.error('カメラがありません。');
			}
		}).catch(function (e) {
			console.error(e);
		});
	</script>
</body>
</html>
