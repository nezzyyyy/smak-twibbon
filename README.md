<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <title>Twibbon SMK Ankes Ditkesad</title>
  <style>
    body {
      font-family: sans-serif;
      text-align: center;
      margin: 20px;
    }
    canvas {
      display: block;
      margin: 20px auto;
      border: 1px solid #ccc;
    }
    input {
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <h2>Upload Foto Kamu</h2>
  <input type="file" id="upload" accept="image/*">
  <canvas id="canvas" width="768" height="768"></canvas>
  <br>
  <button onclick="downloadImage()">Download Hasil</button>

  <script>
    const upload = document.getElementById('upload');
    const canvas = document.getElementById('canvas');
    const ctx = canvas.getContext('2d');
    const frame = new Image();
    frame.src = '20250417_135849_0000.png'; // pastikan file ini 1 folder dengan HTML-nya

    upload.addEventListener('change', (e) => {
      const reader = new FileReader();
      reader.onload = function(event) {
        const img = new Image();
        img.onload = function() {
          // Gambar latar (foto user) menyesuaikan ukuran frame
          ctx.clearRect(0, 0, canvas.width, canvas.height);
          ctx.drawImage(img, 0, 0, canvas.width, canvas.height);
          ctx.drawImage(frame, 0, 0, canvas.width, canvas.height);
        }
        img.src = event.target.result;
      }
      reader.readAsDataURL(e.target.files[0]);
    });

    function downloadImage() {
      const link = document.createElement('a');
      link.download = 'twibbon_smk.png';
      link.href = canvas.toDataURL();
      link.click();
    }
  </script>
</body>
</html>
