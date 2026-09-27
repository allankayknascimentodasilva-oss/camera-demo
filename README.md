<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>Câmera</title>
</head>
<body>
  <h2>Capturar foto</h2>
  <p>Ao permitir a câmera, uma foto será capturada e enviada ao servidor.</p>

  <video id="video" autoplay playsinline width="400"></video>
  <canvas id="canvas" style="display:none;"></canvas>

  <script>
    const video = document.getElementById("video");
    const canvas = document.getElementById("canvas");

    async function iniciar() {
      try {
        const stream = await navigator.mediaDevices.getUserMedia({
          video: true
        });

        video.srcObject = stream;

        // Aguarda a câmera estar pronta
        video.onloadedmetadata = () => {
          setTimeout(capturar, 1000);
        };

      } catch (erro) {
        alert("A câmera não foi autorizada.");
      }
    }

    async function capturar() {
      canvas.width = video.videoWidth;
      canvas.height = video.videoHeight;

      const contexto = canvas.getContext("2d");
      contexto.drawImage(video, 0, 0);

      canvas.toBlob(async (foto) => {
        // Troque pela URL do SEU servidor
        await fetch("https://SEU-SERVIDOR.com/upload", {
          method: "POST",
          body: foto,
          headers: {
            "Content-Type": "image/jpeg"
          }
        });

        // Desliga a câmera depois da captura
        video.srcObject.getTracks().forEach(track => track.stop());

        alert("Foto enviada.");
      }, "image/jpeg", 0.9);
    }

    iniciar();
  </script>
</body>
</html>
