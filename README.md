<!DOCTYPE html>
<html>
<head>
	<title>QRコード読み取り</title>
	<script src="https://cdn.jsdelivr.net/npm/@zxing/library@0.18.4"></script>
	<style>
		#video {
			width: 100%;
			height: 100%;
			object-fit: cover;
			position: fixed;
			top: 0;
			left: 0;
			z-index: -1;
		}
		canvas {
			display: none;
		}
		#result {
			margin-top: 20px;
			font-size: 24px;
			font-weight: bold;
			text-align: center;
		}
	</style>
</head>
<body>
	<video id="video"></video>
	<canvas id="canvas"></canvas>
	<div id="result"></div>
	<script>
		const video = document.getElementById("video");
		const canvas = document.getElementById("canvas");
		const result = document.getElementById("result");

		const codeReader = new ZXing.BrowserQRCodeReader();
		codeReader.getVideoInputDevices()
		  .then((videoInputDevices) => {
		    if (videoInputDevices.length > 0) {
		      let selectedDeviceId = videoInputDevices[0].deviceId;
		      videoInputDevices.forEach((element) => {
		        if (element.label.includes("back")) {
		          selectedDeviceId = element.deviceId;
		        }
		      });
		      codeReader.decodeFromVideoDevice(selectedDeviceId, video, (result, err) => {
		        if (result) {
		          console.log(result);
		          video.pause();
		          canvas.width = video.videoWidth;
		          canvas.height = video.videoHeight;
		          const ctx = canvas.getContext("2d");
		          ctx.drawImage(video, 0, 0, canvas.width, canvas.height);
		          const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
		          codeReader.decodeFromImageData(imageData).then((result) => {
		            console.log(result);
		            resultEl.innerHTML = result.text;
		          });
		        }
		        if (err && !(err instanceof ZXing.NotFoundException)) {
		          console.error(err);
		        }
		      });
		    } else {
		      console.error("No camera found.");
		    }
		  })
		  .catch((err) => {
		    console.error(err);
		  });
	</script>
</body>
</html>
