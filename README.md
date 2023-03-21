<!DOCTYPE html>
<html>
<head>
    <title>QR Code Reader</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <script src="https://cdn.jsdelivr.net/npm/jsqr/dist/jsQR.min.js"></script>
    <style>
        video {
            width: 100%;
            max-width: 500px;
            height: auto;
        }
    </style>
</head>
<body>
    <h1>QR Code Reader</h1>
    <video id="video" autoplay></video>
    <div id="output"></div>
    <script>
        const video = document.getElementById('video');
        const output = document.getElementById('output');
        const constraints = {
            video: {facingMode: "environment"}
        };
        
        navigator.mediaDevices.getUserMedia(constraints)
            .then(stream => {
                video.srcObject = stream;
                video.setAttribute("playsinline", true);
                video.play();
                requestAnimationFrame(tick);
            })
            .catch(error => {
                console.error(error);
            });
            
        function tick() {
            if (video.readyState === video.HAVE_ENOUGH_DATA) {
                const canvas = document.createElement("canvas");
                const canvasContext = canvas.getContext("2d");
                canvas.width = video.videoWidth;
                canvas.height = video.videoHeight;
                canvasContext.drawImage(video, 0, 0, canvas.width, canvas.height);
                const imageData = canvasContext.getImageData(0, 0, canvas.width, canvas.height);
                const code = jsQR(imageData.data, imageData.width, imageData.height, {
                    inversionAttempts: "dontInvert",
                });
                if (code) {
                    output.innerHTML = code.data;
                }
            }
            requestAnimationFrame(tick);
        }
    </script>
</body>
</html>
