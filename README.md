<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Demonstração da Câmera</title>
</head>

<body>
  <h1>📷 Demonstração</h1>
  <p>Toque no botão e autorize o acesso à câmera.</p>

  <button onclick="abrirCamera()">Permitir câmera</button>

  <br><br>

  <video id="video" width="320" autoplay playsinline></video>

  <script>
    async function abrirCamera() {
      try {
        const stream = await navigator.mediaDevices.getUserMedia({
          video: true,
          audio: false
        });

        document.getElementById("video").srcObject = stream;
      } catch (erro) {
        alert("Câmera não autorizada.");
      }
    }
  </script>
</body>
</html># camera-demo
