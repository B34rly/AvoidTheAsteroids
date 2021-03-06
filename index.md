<html lang="en-us">

<head>
	<meta charset="utf-8">
	<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
	<title>Avoid The Asteroids</title>
	<style>
		html,
		body {
			background: #000;
			width: 100%;
			height: 100%;
			overflow: visible;
			padding: 0;
			margin: 0;
		}

		div#gameContainer {
			background: transparent !important;
			position: absolute;
		}

		div#gameContainer canvas {
			position: absolute;
		}
	</style>
</head>

<body>
	<div id="gameContainer">
		<canvas id="unity-canvas"></canvas>
		<script src="Build/AvoidTheAsteroidV1.3.loader.js"></script>
		<script>
			createUnityInstance(document.querySelector("#unity-canvas"), {
				dataUrl: "Build/AvoidTheAsteroidV1.3.data",
				frameworkUrl: "Build/AvoidTheAsteroidV1.3.framework.js",
				codeUrl: "Build/AvoidTheAsteroidV1.3.wasm",
				streamingAssetsUrl: "StreamingAssets",
				companyName: "Beribus",
				productName: "Avoid The Asteroids",
				productVersion: "1.3",
			}).then(function (instance) {
				var canvas = instance.Module.canvas;
				var container = canvas.parentElement;
				function onResize() {
					var w;
					var h;

					if (scaleToFit) {
						w = window.innerWidth;
						h = window.innerHeight;

						var r = 720 / 1280;

						if (w * r > window.innerHeight) {
							w = Math.min(w, Math.ceil(h / r));
						}
						h = Math.floor(w * r);
					} else {
						w = 1280;
						h = 720;
					}

					container.style.width = canvas.style.width = w + "px";
					container.style.height = canvas.style.height = h + "px";
					container.style.top = Math.floor((window.innerHeight - h) / 2) + "px";
					container.style.left = Math.floor((window.innerWidth - w) / 2) + "px";
				}

				var scaleToFit;
				try {
					scaleToFit = !!JSON.parse("");
				} catch (e) {
					scaleToFit = true;
				}
				window.addEventListener('resize', onResize);
				onResize();
			});
		</script>
	</div>
</body>

</html>
