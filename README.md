<!DOCTYPE html>
<html>
<head>
	<title>QRコードリーダー</title>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<script src="https://cdnjs.cloudflare.com/ajax/libs/qrcode-reader/1.0.0/qrcode.min.js"></script>
	<style>
		#video {
			width: 100%;
			height: auto;
		}
	</style>
</head>
<body>
	<video id="video"></video>
	<script>
		var video = document.querySelector("#video");
		var qr = new QCodeDecoder();

		qr.decodeFromCamera(video, function(result) {
			if (result) {
				window.location.href = result;
			}
		}, true);
	</script>
</body>
</html>
